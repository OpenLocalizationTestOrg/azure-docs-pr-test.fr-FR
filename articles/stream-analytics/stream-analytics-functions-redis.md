---
title: "aaaStream le traitement Analytique en temps réel pour les fonctions de Azure | Documents Microsoft"
description: "Découvrez comment toouse une fonction Azure connectées à une file d’attente Service Bus, toopopulate un cache Azure Redis Cache de sortie hello d’une tâche de flux de données Analytique."
keywords: "flux de données, cache redis, file d’attente Service Bus"
services: stream-analytics
author: ryancrawcour
manager: jhubbard
documentationcenter: 
ms.assetid: d428bb33-4244-4001-b93d-c77bed816527
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/28/2017
ms.author: ryancraw
ms.openlocfilehash: 5ef4fe76c2cadf896a80eeaf421f010c315918af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toostore-data-from-azure-stream-analytics-in-an-azure-redis-cache-using-azure-functions"></a>Comment toostore des données à partir de l’Analytique des flux de données Azure dans un Cache Redis Azure à l’aide des fonctions d’Azure
Analytique de flux de données Azure vous permet de développer et déployer des informations en temps réel de solutions de faible coût toogain à partir d’appareils, capteurs, infrastructure et les applications ou n’importe quel flux de données rapidement. Il permet de déployer différents cas d’utilisation, notamment la gestion en temps réel, la commande et le contrôle, la détection des fraudes, les voitures connectées et bien plus encore. Dans de tels scénarios, vous pouvez vouloir toostore les données générées par Analytique de flux de données Azure dans un magasin de données distribuées comme un cache Redis Azure.

Supposons que vous faites partie d’une société de télécommunications. La tentative de fraude de carte SIM toodetect où plusieurs appels en provenance de hello même identité, à hello même temps, mais dans différents géographiquement emplacements. Vous devez stocker toutes les hello potentiels frauduleux appels dans un cache Redis Azure. Dans ce blog, nous donnons des conseils sur la manière dont vous pouvez facilement réaliser cette tâche. 

## <a name="prerequisites"></a>Composants requis
Hello complète [en temps réel la détection des fraudes] [ fraud-detection] étape par étape pour ASA

## <a name="architecture-overview"></a>Présentation de l'architecture
![Capture d’écran de l’architecture](./media/stream-analytics-functions-redis/architecture-overview.png)

Comme indiqué dans hello précédant figure, Analytique de flux de données permet de diffusion en continu des données d’entrée toobe interrogées et envoyé tooan sortie. En fonction de la sortie de hello, fonctions de Azure peut déclencher ensuite un type d’événement. 

Dans ce blog, nous concentrer sur hello Azure des fonctions dans ce pipeline ou hello plus spécifiquement le déclenchement d’un événement qui stocke les données frauduleuses dans le cache de hello.
Après avoir effectué hello [en temps réel la détection des fraudes] [ fraud-detection] didacticiel, vous avez une entrée (un concentrateur d’événements), une requête et une sortie (stockage d’objets blob) déjà configuré et en cours d’exécution. Dans ce blog, nous modifier hello sortie toouse une file d’attente du Bus de Service à la place. Après cela, nous vous connecter à une file d’attente de Azure fonction toothis. 

## <a name="create-and-connect-a-service-bus-queue-output"></a>Création et connexion d’une sortie de la file d’attente Service Bus
toocreate une file d’attente du Bus de Service, suivez les étapes 1 et 2 de la section de .NET hello dans [prise en main les files d’attente de Service Bus][servicebus-getstarted].
Maintenant nous allons connecter hello file d’attente toohello flux Analytique travail qui a été créé dans hello antérieur procédure de détection de fraude.

1. Bonjour portail Azure, accédez à toohello **sorties** Panneau de votre travail, puis sélectionnez **ajouter** en hello haut hello.
   
    ![Ajout de sorties](./media/stream-analytics-functions-redis/adding-outputs.png)
2. Choisissez **file d’attente du Bus de Service** comme hello **récepteur** et suivez les instructions de hello sur l’écran hello. Être vraiment espace de noms de hello toochoose Hello file d’attente du Bus de Service que vous avez créé dans [prise en main les files d’attente de Service Bus][servicebus-getstarted]. Lorsque vous avez terminé, cliquez sur le bouton « droit » hello.
3. Spécifiez hello valeurs suivantes :
   
   * **Format du sérialiseur d'événement**: JSON
   * **Encodage**: UTF8
   * **FORMAT**: séparé par une ligne
4. Cliquez sur hello **créer** bouton tooadd cette source et tooverify qu’Analytique de flux de connexion compte de stockage toohello.
5. Bonjour **requête** onglet, remplacez la requête active hello par qui suit hello. Remplacer * [votre SERVICE BUS nom] * avec le nom de sortie hello créé à l’étape 3. 
   
    ```    
   
        SELECT 
            System.Timestamp as Time, CS1.CallingIMSI, CS1.CallingNum as CallingNum1, 
            CS2.CallingNum as CallingNum2, CS1.SwitchNum as Switch1, CS2.SwitchNum as Switch2
   
        INTO [YOUR SERVICE BUS NAME]
   
        FROM CallStream CS1 TIMESTAMP BY CallRecTime
        JOIN CallStream CS2 TIMESTAMP BY CallRecTime
            ON CS1.CallingIMSI = CS2.CallingIMSI AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5
   
        WHERE CS1.SwitchNum != CS2.SwitchNum
   
    ```

## <a name="create-an-azure-redis-cache"></a>Création d'un cache Redis Azure
Créer un cache Redis Azure en suivant la section .NET hello [comment tooUse le Cache Redis Azure] [ use-rediscache] jusqu'à ce que la section de hello appelé ***configurer les clients de cache hello***.
Une fois que vous avez terminé, vous disposez d’un nouveau cache Redis. Sous **tous les paramètres**, sélectionnez **clés d’accès** et notez les hello ***chaîne de connexion principale***.

![Capture d’écran de l’architecture](./media/stream-analytics-functions-redis/redis-cache-keys.png)

## <a name="create-an-azure-function"></a>Création d’une fonction Azure
Suivez [créer votre première fonction Azure] [ functions-getstarted] tooget didacticiel route avec les fonctions de Azure. Si vous disposez déjà d’une fonction d’Azure, vous devez comme toouse, puis passez trop[écriture tooRedis du Cache](#Writing-to-Redis-Cache)

1. Dans le portail hello, sélectionnez les Services d’application de navigation de gauche hello, puis cliquez sur le site Web de de votre fonction Azure application tooget toohello fonction nom application.
    ![Capture d’écran de la liste des applications App Services](./media/stream-analytics-functions-redis/app-services-function-list.png)
2. Cliquez sur **Nouvelle fonction > ServiceBusQueueTrigger – C#**. Pourquoi les champs suivants, suivez ces instructions :
   
   * **Nom de la file d’attente**: hello même nom en tant que nom hello vous avez entré lorsque vous avez créé la file d’attente hello dans [prise en main les files d’attente de Service Bus] [ servicebus-getstarted] (pas le nom d’hello du bus de service hello). Vérifiez que vous utilisez une file d’attente hello qui est connecté toohello Analytique de flux de sortie.
   * **Connexion Service Bus** : sélectionnez **Ajouter une chaîne de connexion**. chaîne de connexion toofind hello, accédez toohello de portail classique, sélectionnez **Service Bus**, hello bus de service que vous avez créé, et **les informations de connexion** bas hello écran hello. Vérifiez que vous êtes sur l’écran principal de hello sur cette page. Copiez et collez la chaîne de connexion hello. Vous pouvez tooenter libre n’importe quel nom de connexion.
     
       ![Capture d’écran de la connexion Service Bus](./media/stream-analytics-functions-redis/servicebus-connection.png)
   * **AccessRights** : choisissez **Gérer**
3. Cliquez sur **Créer**

## <a name="writing-tooredis-cache"></a>TooRedis de l’écriture du Cache
Nous avons maintenant créé une fonction Azure qui lit à partir d’une file d’attente Service Bus. Tout ce qui reste toodo est utiliser notre toowrite fonction cette toohello de données du Cache Redis. 

1. Sélectionnez votre nouvellement créé **ServiceBusQueueTrigger**, puis cliquez sur **paramètres de l’application de la fonction** sur hello coin supérieur droit. Sélectionnez **aller tooApp Service Paramètres > Paramètres > Paramètres de l’Application**
2. Dans la section de chaînes de connexion de hello, créez un nom Bonjour **nom** section. Collez la chaîne de connexion principale hello trouvé à hello **créer un Cache Redis** pas à pas détaillé hello **valeur** section. Sélectionnez **Personnalisé** pour la **Base de données SQL**.
3. Cliquez sur **enregistrer** haut hello.
   
    ![Capture d’écran de la connexion Service Bus](./media/stream-analytics-functions-redis/function-connection-string.png)
4. Revenez toohello paramètres de Service de l’application et sélectionnez **Outils > Éditeur de Service d’applications (version préliminaire) > sur > accédez**.
   
    ![Capture d’écran de la connexion Service Bus](./media/stream-analytics-functions-redis/app-service-editor.png)
5. Dans un éditeur de votre choix, créez un fichier JSON nommé **project.json** avec hello suivant et enregistrez-le disque tooyour.
   
        {
            "frameworks": {
                "net46": {
                    "dependencies": {
                        "StackExchange.Redis":"1.1.603",
                        "Newtonsoft.Json": "9.0.1"
                    }
                }
            }
        }
6. Télécharger ce fichier dans le répertoire racine de hello de votre fonction (pas WWWROOT). Vous devez voir un fichier nommé **project.lock.json** s’affichent automatiquement, en confirmant que hello Nuget packages « StackExchange.Redis » et « Newtonsoft.Json » ont été importés.
7. Bonjour **run.csx** de fichiers, remplacez les code prégénérés hello hello suivant de code. Dans la fonction de lazyConnection hello, remplacez « CONN NAME » par nom de hello créé à l’étape 2 de **stocker les données dans le cache Redis hello**.

````

    using System;
    using System.Threading.Tasks;
    using StackExchange.Redis;
    using Newtonsoft.Json;
    using System.Configuration;

    public static void Run(string myQueueItem, TraceWriter log)
    {
        log.Info($"Function processed message: {myQueueItem}");

        // Connection refers tooa property that returns a ConnectionMultiplexer
        IDatabase db = Connection.GetDatabase();
        log.Info($"Created database {db}");

        // Parse JSON and extract hello time
        var message = JsonConvert.DeserializeObject<dynamic>(myQueueItem);
        string time = message.time;
        string callingnum1 = message.callingnum1;

        // Perform cache operations using hello cache object...
        // Simple put of integral data types into hello cache
        string key = time + " - " + callingnum1;
        db.StringSet(key, myQueueItem);
        log.Info($"Object put in database. Key is {key} and value is {myQueueItem}");

        // Simple get of data types from hello cache
        string value = db.StringGet(key);
        log.Info($"Database got: {value}"); 
    }

    // Connect toohello Service Bus
    private static Lazy<ConnectionMultiplexer> lazyConnection = 
        new Lazy<ConnectionMultiplexer>(() =>
            {
                var cnn = ConfigurationManager.ConnectionStrings["CONN NAME"].ConnectionString
                return ConnectionMultiplexer.Connect();
            });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }

````

## <a name="start-hello-stream-analytics-job"></a>Démarrer la tâche de flux de données Analytique hello
1. Démarrez l’application de telcodatagen.exe hello. l’utilisation de Hello est comme suit :````telcodatagen.exe [#NumCDRsPerHour] [SIM Card Fraud Probability] [#DurationHours]````
2. Dans le panneau de tâche Analytique de Stream hello dans le portail de hello, cliquez sur **Démarrer** en hello haut hello.
   
    ![Capture d’écran de la tâche de démarrage](./media/stream-analytics-functions-redis/starting-job.png)
3. Bonjour **Start job** panneau qui s’affiche, sélectionnez **maintenant** puis cliquez sur hello **Démarrer** bouton bas hello écran hello. état de la tâche Hello modifie tooStarting et tard tooRunning de modifications.
   
    ![Capture d’écran de la sélection de l’heure de la tâche de démarrage](./media/stream-analytics-functions-redis/start-job-time.png)

## <a name="run-solution-and-check-results"></a>Exécution de la solution et vérification des résultats
Si vous revenez en tooyour **ServiceBusQueueTrigger** page, vous devez maintenant voir consigner les instructions. Ces journaux indiquent que vous avez obtenu un élément hello file d’attente du Bus de Service, placer dans la base de données hello et il extraites à l’aide de la durée de hello en tant que clé de hello !

tooverify vos données sont dans le cache Redis, accédez à tooyour Redis cache page hello nouveau portail (comme indiqué dans hello précédent [créer un cache Azure Redis Cache](#Create-an-Azure-Redis-Cache) étape), puis sélectionnez Console.

Vous pouvez maintenant écrire Redis commandes tooconfirm que les données sont en fait dans le cache de hello.

![Capture d’écran de la console Redis](./media/stream-analytics-functions-redis/redis-console.png)

## <a name="next-steps"></a>Étapes suivantes
Nous sommes heureux de choses hello nouvelles fonctions d’Azure et analytique de flux peut faire ensemble, et nous espérons que cette opération déverrouille nouvelles possibilités pour vous. Si vous avez des commentaires sur ce que vous souhaitez ensuite, vous pouvez toouse libre hello [site Azure UserVoice](https://feedback.azure.com/forums/270577-stream-analytics).

Si vous êtes de nouveau Microsoft Azure, nous vous invitons tootry il expire en vous connectant à un [libérer le compte d’évaluation Azure](https://azure.microsoft.com/pricing/free-trial/). Si vous êtes de nouveau tooStream Analytique, nous vous invitons trop[créer votre première tâche de flux de données Analytique](stream-analytics-create-a-job.md).

Si vous avez besoin d’aide ou avez des questions, postez-les sur les forums [MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) ou [Stackoverflow](http://stackoverflow.com/questions/tagged/azure-stream-analytics). 

Vous pouvez également voir hello suivant des ressources :

* [Référence du développeur Azure Functions](../azure-functions/functions-reference.md)
* [Informations de référence pour les développeurs C# sur Azure Functions](../azure-functions/functions-reference-csharp.md)
* [Informations de référence pour les développeurs F# sur Azure Functions](../azure-functions/functions-reference-fsharp.md)
* [Azure Functions NodeJS developer reference (Référence pour les développeurs NodeJS Azure Functions)](../azure-functions/functions-reference.md)
* [Déclencheurs et liaisons Azure Functions](../azure-functions/functions-triggers-bindings.md)
* [Comment toomonitor Cache Redis Azure](../redis-cache/cache-how-to-monitor.md)

toostay à jour sur toutes les informations les plus récentes hello et fonctionnalités, procédez comme [ @AzureStreaming ](https://twitter.com/AzureStreaming) sur Twitter.

[fraud-detection]: stream-analytics-real-time-fraud-detection.md
[servicebus-getstarted]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[use-rediscache]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md
[functions-getstarted]: ../azure-functions/functions-create-first-azure-function.md
