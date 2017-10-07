---
title: "aaaGetting en main de Visual Studio et de stockage de la file d’attente des services connectés (projets de la tâche Web) | Documents Microsoft"
description: "Comment tooget démarrer l’utilisation du stockage de file d’attente Azure dans un projet de la tâche Web une fois la connexion de compte de stockage tooa à l’aide de Visual Studio services connectés."
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5c3ef267-2a67-44e9-ab4a-1edd7015034f
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 47a446aa5c6bbf25526339823db4952ac1a8802f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-webjob-projects"></a>Prise en main du stockage de files d'attente Azure et des services connectés Visual Studio (projets WebJob)
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Vue d'ensemble
Cet article décrit comment obtenir démarré à l’aide de la file d’attente Azure storage dans un projet de la tâche Web de Visual Studio Azure une fois que vous avez créé ou référencé d’un compte de stockage Azure à l’aide de hello Visual Studio **ajouter des Services connectés** boîte de dialogue. Lorsque vous ajoutez un projet de tâche Web tooa compte stockage à l’aide de Visual Studio de hello **ajouter des Services connectés** boîte de dialogue, les packages NuGet de stockage Azure appropriés hello sont installées, les références .NET appropriées hello sont toohello ajouté projet et les chaînes de connexion pour le compte de stockage hello sont mis à jour dans le fichier App.config hello.  

Cet article fournit des exemples de code c# qui montrent comment toouse hello Azure WebJobs SDK version 1.x avec hello service de stockage de file d’attente Azure.

Stockage de file d’attente Azure est un service pour stocker un grand nombre de messages qui sont accessibles à partir de n’importe où dans le monde hello via des appels authentifiés à l’aide de HTTP ou HTTPS. Un message de la file d’attente unique peut être de taille too64 Ko, et une file d’attente peut contenir des millions de messages, des limites de capacité totale de toohello d’un compte de stockage. Pour plus d’informations, consultez la section [Prise en main d’Azure Queue Storage à l’aide de .NET](../storage/queues/storage-dotnet-how-to-use-queues.md) . Pour plus d’informations sur ASP.NET, voir le site [ASP.NET](http://www.asp.net)(en anglais).

## <a name="how-tootrigger-a-function-when-a-queue-message-is-received"></a>Comment tootrigger une fonction lors de la réception d’un message de la file d’attente
toowrite une fonction qui hello WebJobs SDK appelle lors de la réception d’un message de la file d’attente, utilisez hello **QueueTrigger** attribut. constructeur d’attribut Hello prend un paramètre de chaîne qui spécifie le nom hello de toopoll de file d’attente hello. toosee comment tooset hello le nom de la file d’attente dynamique, consultez [comment tooset les Options de Configuration](#how-to-set-configuration-options).

### <a name="string-queue-messages"></a>Messages de file d’attente de chaîne
Dans l’exemple suivant de hello, file d’attente hello contient un message de type chaîne, donc **QueueTrigger** est le paramètre de chaîne tooa appliqué nommé **logMessage** qui contient le contenu du message de file d’attente hello hello. Hello fonction [écrit un toohello de message du journal du tableau de bord](#how-to-write-logs).

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

En outre **chaîne**, paramètre hello peut être un tableau d’octets, un **CloudQueueMessage** objet ou un POCO que vous définissez.

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a>Messages en file d’attente POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))
Dans l’exemple suivant de hello, message de file d’attente hello contient des données JSON pour un **BlobInformation** objet qui inclut un **BlobName** propriété. Hello SDK désérialise automatiquement l’objet de hello.

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

Hello SDK utilise hello [package Newtonsoft.Json NuGet](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize et désérialiser les messages. Si vous créez des messages de la file d’attente dans un programme qui n’utilise pas hello WebJobs SDK, vous pouvez écrire du code comme hello suivant exemple toocreate un message de la file d’attente POCO qui hello que SDK peut analyser.

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a>Fonctions asynchrones
Hello suivant fonction async [écrit un tableau de bord de toohello journal](#how-to-write-logs).

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

Fonctions Async peuvent prendre un [jeton d’annulation](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), comme indiqué dans hello qui copie un objet blob de l’exemple suivant. (Pour obtenir une explication de hello **queueTrigger** espace réservé, consultez hello [BLOB](#how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message) section.)

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

## <a name="types-hello-queuetrigger-attribute-works-with"></a>Attribut de types hello QueueTrigger fonctionne avec
Vous pouvez utiliser **QueueTrigger** avec hello les types suivants :

* **string**
* Type d’objet POCO sérialisé au format JSON
* **byte[]**
* **CloudQueueMessage**

## <a name="polling-algorithm"></a>Algorithme d’interrogation
Hello SDK implémente un effet de hello tooreduce aléatoire exponentielle algorithme de temporisation d’inactivité-file d’attente sur les coûts de stockage.  Lorsqu’un message est détecté, hello SDK attend deux secondes, puis vérifie un autre message ; Lorsque aucun message n’est trouvé, il attend environ quatre secondes avant de réessayer. Après les tentatives ayant échoué tooget un message de la file d’attente, temps d’attente hello continue tooincrease jusqu'à ce qu’il atteigne le délai d’attente maximal hello, les minutes tooone de valeurs par défaut. [Hello délai d’attente maximal est configurable](#how-to-set-configuration-options).

## <a name="multiple-instances"></a>Instances multiples
Si votre application web s’exécute sur plusieurs instances, une tâche Web continue s’exécute sur chaque ordinateur, et chaque ordinateur va attendre que les déclencheurs et essayer de fonctions de toorun. Dans certains scénarios, que cela peut entraîner toosome les fonctions de traitement hello à deux reprises, les mêmes données fonctions ne doivent donc être idempotentes (écrite afin que les appeler à plusieurs reprises avec les mêmes données d’entrée ne génère pas de hello dupliquer les résultats).  

## <a name="parallel-execution"></a>Exécution en parallèle
Si vous avez plusieurs fonctions à l’écoute sur différentes files d’attente, hello SDK appellera les en parallèle lorsque les messages sont reçus simultanément.

Hello est de même lorsque plusieurs messages sont reçus d’une file d’attente unique. Par défaut, hello SDK Obtient un lot de messages de file d’attente 16 à la fois et exécute la fonction hello qui les traite en parallèle. [taille de lot Hello est configurable](#how-to-set-configuration-options). Lorsqu’il obtient nombre hello en cours de traitement vers le bas toohalf hello taille de lot, hello SDK Obtient un autre lot et commence à traiter les messages. Par conséquent nombre maximal de hello de messages simultanés en cours de traitement par la fonction est la taille du lot une fois et demie hello. Cette limite s’applique séparément les fonction tooeach qui a un **QueueTrigger** attribut. Si vous ne souhaitez pas l’exécution en parallèle pour les messages reçus sur une file d’attente, définissez too1 de taille de lot hello.

## <a name="get-queue-or-queue-message-metadata"></a>Obtention des métadonnées de file d'attente ou de message de file d'attente
Vous pouvez obtenir hello suivant des propriétés de message en ajoutant la signature de méthode toohello paramètres :

* **DateTimeOffset** expirationTime
* **DateTimeOffset** insertionTime
* **DateTimeOffset** nextVisibleTime
* **string** queueTrigger (contient le texte du message)
* **string** id
* **string** popReceipt
* **int** dequeueCount

Si vous souhaitez toowork directement avec hello API de stockage Azure, vous pouvez également ajouter un **CloudStorageAccount** paramètre.

Hello exemple suivant écrit tous ce métadonnées tooan informations journal d’application. Dans l’exemple de hello, logMessage et queueTrigger contiennent le contenu du message de file d’attente hello hello.

        public static void WriteLog([QueueTrigger("logqueue")] string logMessage,
            DateTimeOffset expirationTime,
            DateTimeOffset insertionTime,
            DateTimeOffset nextVisibleTime,
            string id,
            string popReceipt,
            int dequeueCount,
            string queueTrigger,
            CloudStorageAccount cloudStorageAccount,
            TextWriter logger)
        {
            logger.WriteLine(
                "logMessage={0}\n" +
            "expirationTime={1}\ninsertionTime={2}\n" +
                "nextVisibleTime={3}\n" +
                "id={4}\npopReceipt={5}\ndequeueCount={6}\n" +
                "queue endpoint={7} queueTrigger={8}",
                logMessage, expirationTime,
                insertionTime,
                nextVisibleTime, id,
                popReceipt, dequeueCount,
                cloudStorageAccount.QueueEndpoint,
                queueTrigger);
        }

Voici un exemple de journal écrit par l’exemple de code hello :

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

## <a name="graceful-shutdown"></a>Arrêt approprié
Une fonction qui s’exécute dans une tâche Web continue peut accepter un **CancellationToken** paramètre qui permet la fonction hello toonotify hello de système d’exploitation lorsque hello la tâche Web est sur toobe terminée. Vous pouvez utiliser cette toomake de notification que la fonction hello n’arrêt inattendu d’une manière qui laisse les données dans un état incohérent.

Hello suivant montre l’exemple de comment toocheck à l’arrêt de la tâche Web imminente dans une fonction.

    public static void GracefulShutdownDemo(
                [QueueTrigger("inputqueue")] string inputText,
                TextWriter logger,
                CancellationToken token)
    {
        for (int i = 0; i < 100; i++)
        {
            if (token.IsCancellationRequested)
            {
                logger.WriteLine("Function was cancelled at iteration {0}", i);
                break;
            }
            Thread.Sleep(1000);
            logger.WriteLine("Normal processing for queue message={0}", inputText);
        }
    }

**Remarque :** hello du tableau de bord ne peut pas afficher correctement état de hello et la sortie de fonctions qui ont été arrêtés.

Pour plus d’informations, consultez [Arrêt correct de WebJobs](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).   

## <a name="how-toocreate-a-queue-message-while-processing-a-queue-message"></a>Comment toocreate une file d’attente de message lors du traitement d’un message de la file d’attente
toowrite une fonction qui crée un nouveau message de file d’attente, utilisez hello **file d’attente** attribut. Comme **QueueTrigger**, vous passez dans un nom de file d’attente hello sous forme de chaîne, ou vous pouvez [définir le nom de file d’attente hello dynamiquement](#how-to-set-configuration-options).

### <a name="string-queue-messages"></a>Messages de file d’attente de chaîne
Hello suivant l’exemple de code non-async crée un nouveau message de file d’attente dans la file d’attente hello nommé « outputqueue » avec hello même contenu en tant que message de file d’attente de salutation reçu dans la file d’attente hello nommé « inputqueue ». (Dans le cas de fonctions asynchrones, utilisez l'élément **IAsyncCollector<T>** , comme indiqué plus loin dans la présente section.)

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a>Messages en file d’attente POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))
type d’un message de la file d’attente qui contient un POCO plutôt que d’une chaîne, passez hello POCO toocreate comme un toohello de paramètre de sortie **file d’attente** constructeur d’attribut.

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

Kit de développement logiciel de Hello sérialise automatiquement hello objet tooJSON. Un message de la file d’attente est toujours créé, même si l’objet hello est null.

### <a name="create-multiple-messages-or-in-async-functions"></a>Création de plusieurs messages de file d’attente dans des fonctions asynchrones
toocreate plusieurs messages, vérifiez le type de paramètre hello pour la file d’attente de sortie hello **ICollector<T>**  ou **IAsyncCollector<T>**, comme indiqué dans hello l’exemple suivant.

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

Chaque message de la file d’attente est créée immédiatement lorsque hello **ajouter** méthode est appelée.

### <a name="types-that-hello-queue-attribute-works-with"></a>Types de cet attribut de la file d’attente hello fonctionne avec
Vous pouvez utiliser hello **file d’attente** attribut sur hello les types de paramètres suivants :

* **chaîne** (crée le message de la file d’attente si la valeur du paramètre est non null lors de la fin de la fonction hello)
* **out byte[]** (fonctionne comme **string**)
* **out CloudQueueMessage** (fonctionne comme **string**)
* **out POCO** (un type sérialisable, crée un message avec un objet null si hello paramètre est null lors de la fin de la fonction hello)
* **ICollector**
* **IAsyncCollector**
* **CloudQueue** (pour la création de messages manuellement à l’aide de hello API de stockage Azure directement)

### <a name="use-webjobs-sdk-attributes-in-hello-body-of-a-function"></a>Utiliser les attributs de WebJobs SDK dans le corps d’une fonction de hello
Si vous avez besoin de toodo certains fonctionnent dans votre fonction avant d’utiliser un attribut WebJobs SDK comme **file d’attente**, **Blob**, ou **Table**, vous pouvez utiliser hello **IBinder** interface.

Hello, l’exemple suivant prend un message de la file d’attente d’entrée et crée un nouveau message avec hello même contenu dans une file d’attente de sortie. nom de file d’attente de sortie Hello est définie par le code dans le corps de hello de fonction hello.

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

Hello **IBinder** interface peut également être utilisée avec hello **Table** et **Blob** attributs.

## <a name="how-tooread-and-write-blobs-and-tables-while-processing-a-queue-message"></a>Comment tooread et l’écriture d’objets BLOB et les tables lors du traitement d’un message de la file d’attente
Hello **Blob** et **Table** attributs vous tooread et écrire des objets BLOB et tables. exemples de Hello dans cette section s’appliquent tooblobs. Pour obtenir des exemples de code qui montrent comment tootrigger traite lorsque les objets BLOB est créés ou mis à jour, consultez [comment toouse Azure stockage d’objets blob par hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)et pour obtenir des exemples de code qui lisent et écrivent des tables, consultez [comment toouse table Azure stockage avec hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-tables-how-to.md).

### <a name="string-queue-messages-triggering-blob-operations"></a>Messages en file d’attente de chaîne déclenchant des opérations d’objet blob
Pour un message de la file d’attente qui contient une chaîne, **queueTrigger** est un espace réservé que vous pouvez utiliser Bonjour **Blob** l’attribut **blobPath** paramètre qui contient le contenu de hello de message de type Hello.

Hello exemple suivant utilise **flux** objets blobs tooread et d’écriture. message de file d’attente Hello est nom hello d’un objet blob situé dans le conteneur de textblobs hello. Une copie de l’objet blob de hello avec «-nouveau » ajouté toohello nom est créé dans hello même conteneur.

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

Hello **Blob** attribut constructeur prend un **blobPath** paramètre qui spécifie le conteneur de hello et nom d’objet blob. Pour plus d’informations sur cet espace réservé, consultez [comment toouse Azure stockage d’objets blob par hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md).

Lorsque les attributs hello décore un **flux** de l’objet, un autre paramètre de constructeur spécifie hello **FileAccess** mode en lecture, écriture ou en lecture/écriture.

Hello exemple suivant utilise un **CloudBlockBlob** toodelete un objet blob de l’objet. message de file d’attente Hello est nom hello d’objet blob de hello.

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a>Messages en file d’attente POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))
Pour un POCO stockée en tant que JSON dans le message de file d’attente d’appel, vous pouvez utiliser des espaces réservés qui nommer les propriétés d’objet de hello en hello **file d’attente** l’attribut **blobPath** paramètre. Vous pouvez également utiliser des noms de propriété de métadonnées de file d'attente comme espaces réservés. Consultez la section [Obtention des métadonnées de file d’attente ou de message de file d’attente](#get-queue-or-queue-message-metadata).

Hello exemple suivant copie un objet blob tooa nouvel objet blob avec une autre extension. message de file d’attente Hello est un **BlobInformation** objet inclut **BlobName** et **BlobNameWithoutExtension** propriétés. les noms de propriété Hello sont utilisés comme espaces réservés dans le chemin d’accès des blob hello pour hello **Blob** attributs.

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

Hello SDK utilise hello [package Newtonsoft.Json NuGet](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize et désérialiser les messages. Si vous créez des messages de la file d’attente dans un programme qui n’utilise pas hello WebJobs SDK, vous pouvez écrire du code comme hello suivant exemple toocreate un message de la file d’attente POCO qui hello que SDK peut analyser.

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

Si vous devez toodo certains fonctionnent dans votre fonction avant de lier un objet tooan d’objets blob, vous pouvez utiliser attribut hello dans les corps de hello de fonction hello, comme indiqué dans [attributs utiliser le SDK WebJobs dans le corps d’une fonction de hello](#use-webjobs-sdk-attributes-in-the-body-of-a-function).

### <a name="types-you-can-use-hello-blob-attribute-with"></a>Vous pouvez utiliser hello des types d’objets Blob attribut avec
Hello **Blob** attribut peut être utilisé avec les types suivants de hello :

* **Flux** (lecture ou écriture, spécifiée à l’aide du paramètre de constructeur FileAccess hello)
* **TextReader**
* **TextWriter**
* **string** (lecture)
* **chaîne** (écriture ; crée un objet blob uniquement si le paramètre de chaîne hello est non null lors de la fonction hello retourne)
* POCO (lecture)
* out POCO (écrire ; toujours crée un objet blob, crée en tant qu’objet null si POCO paramètre est null lors de la fonction hello retourne)
* **CloudBlobStream** (écriture)
* **ICloudBlob** (lecture ou écriture)
* **CloudBlockBlob** (lecture ou écriture)
* **CloudPageBlob** (lecture ou écriture)

## <a name="how-toohandle-poison-messages"></a>Comment toohandle des messages incohérents
Les messages dont le contenu provoque une toofail de fonction sont appelées *messages incohérents*. En cas d’échec de la fonction hello, message de file d’attente hello n’est pas supprimé et finalement est de nouveau récupéré, entraînant toobe de cycle de hello répétée. Hello SDK peut interrompre automatiquement hello cycle après un nombre limité d’itérations, ou vous pouvez le faire manuellement.

### <a name="automatic-poison-message-handling"></a>Gestion automatique des messages incohérents
Kit de développement logiciel de Hello appelle une fonction des too5 tooprocess de fois où un message de la file d’attente. Si vous essayez de cinquième hello échoue, le message de type hello est file d’attente de messages incohérents tooa déplacé. Vous pouvez voir comment tooconfigure hello nombre maximal de tentatives dans [comment les options de configuration tooset](#how-to-set-configuration-options).

file d’attente de messages incohérents Hello est nommé *{originalqueuename}*-incohérents. Vous pouvez écrire une fonction tooprocess messages de file d’attente de messages incohérents hello par les enregistrer ou de l’envoi d’une notification qu’attention manuelle est nécessaire.

Bonjour suivant hello d’exemple **CopyBlob** ne fonctionnera pas si un message de la file d’attente contient nom hello d’un objet blob qui n’existe pas. Lorsque cela se produit, message de type hello est déplacé à partir de la file d’attente de file d’attente toohello copyblobqueue-incohérents hello copyblobqueue. Hello **ProcessPoisonMessage** puis journaux hello message incohérent.

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

        public static void ProcessPoisonMessage(
            [QueueTrigger("copyblobqueue-poison")] string blobName, TextWriter logger)
        {
            logger.WriteLine("Failed toocopy blob, name=" + blobName);
        }

Hello suivant montre l’illustration sortie de console à partir de ces fonctions lorsqu’un message incohérent est traité.

![Sortie de la console pour la gestion des messages incohérents](./media/vs-storage-webjobs-getting-started-queues/poison.png)

### <a name="manual-poison-message-handling"></a>Gestion manuelle des messages incohérents
Vous pouvez obtenir le nombre de hello de fois où un message n’a été sélectionné pour le traitement en ajoutant une **int** paramètre nommé **dequeueCount** tooyour (fonction). Vous pouvez ensuite cocher hello dequeue nombre dans le code de fonction et effectuer votre propre gestion de message incohérent lorsque le nombre de hello dépasse un seuil, comme indiqué dans hello l’exemple suivant.

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName, int dequeueCount,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput,
            TextWriter logger)
        {
            if (dequeueCount > 3)
            {
                logger.WriteLine("Failed toocopy blob, name=" + blobName);
            }
            else
            {
            blobInput.CopyTo(blobOutput, 4096);
            }
        }

## <a name="how-tooset-configuration-options"></a>Comment les options de configuration tooset
Vous pouvez utiliser hello **JobHostConfiguration** hello tooset de type des options de configuration suivantes :

* Définir des chaînes de connexion du Kit de développement logiciel hello dans le code.
* Configuration des paramètres **QueueTrigger** tels que le nombre de retraits maximal.
* Obtention des noms de file d’attente de la configuration.

### <a name="set-sdk-connection-strings-in-code"></a>Définition des chaînes de connexion du Kit de développement logiciel (SDK) dans le code
Définition des chaînes de connexion du Kit de développement logiciel hello dans le code permet vous toouse vos propres noms de chaîne de connexion dans les fichiers de configuration ou des variables d’environnement, comme indiqué dans hello l’exemple suivant.

        static void Main(string[] args)
        {
            var _storageConn = ConfigurationManager
                .ConnectionStrings["MyStorageConnection"].ConnectionString;

            var _dashboardConn = ConfigurationManager
                .ConnectionStrings["MyDashboardConnection"].ConnectionString;

            var _serviceBusConn = ConfigurationManager
                .ConnectionStrings["MyServiceBusConnection"].ConnectionString;

            JobHostConfiguration config = new JobHostConfiguration();
            config.StorageConnectionString = _storageConn;
            config.DashboardConnectionString = _dashboardConn;
            config.ServiceBusConnectionString = _serviceBusConn;
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <a name="configure-queuetrigger--settings"></a>Configuration des paramètres QueueTrigger
Vous pouvez configurer hello suivant les paramètres qui s’appliquent le traitement des messages toohello file d’attente :

* Hello nombre maximal de messages de file d’attente sont appliquées simultanément les toobe exécuté en parallèle (valeur par défaut est 16).
* Hello nombre maximal de tentatives avant que la file d’attente de messages incohérents tooa envoi d’un message de la file d’attente (valeur par défaut est 5).
* délai d’attente maximal Hello avant d’interroger à nouveau lorsqu’une file d’attente est vide (valeur par défaut est 1 minute).

Hello suivant montre l’exemple de comment tooconfigure ces paramètres :

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <a name="set-values-for-webjobs-sdk-constructor-parameters-in-code"></a>Définition des valeurs des paramètres de constructeur du Kit de développement logiciel (SDK) WebJobs dans le code
Parfois vous toospecify un nom de file d’attente, un nom d’objet blob ou un conteneur ou nom de la table dans le code au lieu de coder en dur il. Par exemple, vous pourriez le nom de file d’attente toospecify hello pour **QueueTrigger** dans une variable d’environnement ou le fichier de configuration.

C’est également en passant un **NameResolver** objet toohello **JobHostConfiguration** type. Vous incluez des espaces réservés spéciales, délimitées par des signes de pourcentage (%) dans les paramètres de constructeur d’attribut WebJobs SDK et votre **NameResolver** code spécifie hello toobe de valeurs réelles utilisée à la place de ces espaces réservés.

Par exemple, supposons que vous vouliez toouse une file d’attente nommée logqueuetest dans l’environnement de test hello et un logqueueprod nommée en production. Au lieu d’un nom codé en dur la file d’attente, vous souhaitez nom hello de toospecify d’une entrée dans hello **appSettings** collection qui aurait le nom de file d’attente réel hello. Si hello **appSettings** la clé est logqueue, votre fonction pourrait ressembler à hello l’exemple suivant.

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

Votre **NameResolver** classe pu obtenir ensuite le nom de file d’attente de hello de **appSettings** comme indiqué dans hello l’exemple suivant :

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

Vous passez hello **NameResolver** classe dans toohello **JobHost** de l’objet comme indiqué dans hello l’exemple suivant.

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

**Remarque :** file d’attente, de table et noms d’objets blob ne sont pas résolus chaque fois une fonction est appelée, mais les noms de conteneur d’objets blob sont résolues uniquement au démarrage d’application hello. Vous ne pouvez pas modifier le nom de conteneur pendant l’exécution du travail de hello.

## <a name="how-tootrigger-a-function-manually"></a>Comment tootrigger une fonction manuellement
une fonction de tootrigger utiliser manuellement, hello **appeler** ou **CallAsync** méthode sur hello **JobHost** objet et hello **NoAutomaticTrigger** attribut sur la fonction hello, comme indiqué dans hello l’exemple suivant.

        public class Program
        {
            static void Main(string[] args)
            {
                JobHost host = new JobHost();
                host.Call(typeof(Program).GetMethod("CreateQueueMessage"), new { value = "Hello world!" });
            }

            [NoAutomaticTrigger]
            public static void CreateQueueMessage(
                TextWriter logger,
                string value,
                [Queue("outputqueue")] out string message)
            {
                message = value;
                logger.WriteLine("Creating queue message: ", message);
            }
        }

## <a name="how-toowrite-logs"></a>Mode de journalisation des toowrite
Hello du tableau de bord affiche les journaux à deux emplacements : page hello pourquoi la tâche Web et page hello pour un appel de la tâche Web particulier.

![Journaux affichés dans la page relative aux tâches web](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

![Journaux affichés dans la page d’appel de fonctions](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

Sortie des méthodes de Console que vous appelez une fonction ou Bonjour **Main()** méthode s’affiche dans la page de tableau de bord hello pourquoi la tâche Web, et non dans la page hello pour un appel de méthode particulier. Sortie à partir de l’objet TextWriter hello que vous obtenez à partir d’un paramètre dans la signature de méthode s’affiche dans la page de tableau de bord hello pour un appel de méthode.

La sortie de console ne peut pas être appel de méthode particulière tooa lié étant hello Console monothread, tandis que de nombreuses fonctions de travail peuvent s’exécuter à hello même temps. C’est pourquoi hello SDK fournit à chaque appel de fonction avec son propre objet d’enregistreur de journal unique.

toowrite [journaux de suivi d’application](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), utilisez **Console.Out** (crée des journaux marquées comme INFO) et **Console.Error** (crée des journaux marquées comme erreur). Une autre solution consiste à toouse [Trace ou TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), qui fournit des commentaires, avertissement, et des niveaux critique dans tooInfo d’ajout et d’erreur. Journaux de suivi d’application s’affichent dans les fichiers de journaux hello web app, les tables Azure, ou les objets BLOB Azure en fonction de la façon dont vous configurez votre application web Azure. Qu’est remplie de toutes les sorties de la Console, derniers journaux d’application 100 hello apparaissent également dans la page de tableau de bord hello pourquoi la tâche Web, page de hello pas pour un appel de fonction.

La sortie de console s’affiche dans hello du tableau de bord uniquement si le programme de hello est en cours d’exécution dans une tâche Web Azure, pas si le programme de hello s’exécute localement ou dans tout autre environnement.

Vous pouvez désactiver la journalisation en définissant toonull de chaîne de connexion de tableau de bord hello. Pour plus d’informations, consultez [comment tooset les Options de Configuration](#how-to-set-configuration-options).

Hello suivant montre plusieurs façons toowrite journaux :

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

Bonjour le tableau de bord WebJobs SDK, hello sortie de hello **TextWriter** de l’objet s’affiche lorsque vous ouvrez la page toohello pour un particulier appel de fonction et sélectionnez **bascule sortie**:

![Lien d’appel](./media/vs-storage-webjobs-getting-started-queues/dashboardinvocations.png)

![Journaux affichés dans la page d’appel de fonctions](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

Bonjour le tableau de bord WebJobs SDK, lignes hello 100 la plus récente de la Console de sortie afficher des lorsque vous accédez page toohello pourquoi la tâche Web (et non de l’appel de la fonction hello) et sélectionnez **bascule sortie**.

![Activer/désactiver la sortie](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

Dans une tâche Web continue, journaux des applications s’affichent dans/données/tâches/continu/*{webjobname}*/job_log.txt hello web application système de fichiers.

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

Dans une application de hello d’objets blob Azure des journaux ressembler à ceci : 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world !, 2014-09-26T21:01:13, erreur, contosoadsnew, 491e54, 635473620738373502,0,17404,19,console.Error - Hello world !, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world !,

Et un Bonjour Azure table **Console.Out** et **Console.Error** journaux ressembler à ceci :

![Journal d’informations dans la table](./media/vs-storage-webjobs-getting-started-queues/tableinfo.png)

![Journal d’erreurs dans la table](./media/vs-storage-webjobs-getting-started-queues/tableerror.png)

## <a name="next-steps"></a>Étapes suivantes
Cet article a fourni le code des exemples qui montrent comment toohandle des scénarios courants pour l’utilisation des files d’attente Azure. Pour plus d’informations sur la façon dont toouse tâches Web Azure et hello WebJobs SDK, consultez [les ressources de documentation Azure WebJobs](http://go.microsoft.com/fwlink/?linkid=390226).

