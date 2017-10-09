---
title: "conseils d’aaaPerformance - Azure Cosmos DB NoSQL | Documents Microsoft"
description: "En savoir plus les performances de la base de données client configuration options tooimprove base de données Azure Cosmos"
keywords: tooimprove base de performances
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 94ff155e-f9bc-488f-8c7a-5e7037091bb9
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: mimig
ms.openlocfilehash: 4f3e82ae5048e3dbc20b0fd891a2d3aa22adf3fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tips-for-azure-cosmos-db"></a>Conseils sur les performances pour Azure Cosmos DB
Azure Cosmos DB est une base de données distribuée rapide et flexible qui peut être mise à l’échelle en toute transparence avec une latence et un débit garantis. Ne pas avoir les modifications de l’architecture principale toomake ou écrire un code complexe tooscale votre base de données avec la base de données Cosmos. Il suffit d’un simple appel d’API ou de méthode de [kit de développement logiciel (SDK)](set-throughput.md#set-throughput-sdk)pour effectuer une mise à l’échelle. Toutefois, Cosmos de base de données est accessible via les appels réseau il sont optimisations côté client vous pouvez apporter tooachieve maximiser les performances.

Si vous vous demandez comment améliorer les performances de votre base de données, Tenez compte des hello options suivantes :

## <a name="networking"></a>Mise en réseau
<a id="direct-connection"></a>

1. **Stratégie de connexion : utilisation du mode de connexion direct**

    Comment un client connecte tooCosmos DB a des implications importantes sur les performances, tout particulièrement en termes de latence observée sur le côté client. Il existe deux paramètres de configuration de la clé de configuration client stratégie de connexion : connexion de hello *mode* et hello [connexion *protocole*](#connection-protocol).  Hello de deux modes disponibles est :

   1. Mode passerelle (par défaut)
   2. Mode direct

      Mode de passerelle est pris en charge sur toutes les plateformes de kit de développement logiciel et est par défaut de hello configuré.  Si votre application s’exécute dans un réseau d’entreprise avec des restrictions de pare-feu strict, Mode de passerelle est hello meilleur choix, car elle utilise le port HTTPS standard hello et un seul point de terminaison. Hello compromis de performances, toutefois, est que passerelle Mode implique un saut réseau supplémentaire chaque fois les données sont lues ou écrites tooCosmos DB. Pour cette raison, le Mode Direct offre de meilleures performances en raison de tronçons toofewer.
<a id="use-tcp"></a>
2. **Stratégie de connexion : utiliser le protocole TCP hello**

    Lorsque vous utilisez le mode direct, deux options de protocole sont disponibles :

   * TCP
   * HTTPS

     Cosmos DB fournit un modèle de programmation RESTful simple et ouvert sur HTTPS. En outre, il offre un protocole TCP efficace, également RESTful dans son modèle de communication et est disponible via le SDK de client .NET hello. Direct TCP et HTTPS SSL utilisent tous deux SSL pour l’authentification initiale et le chiffrement du trafic. Pour de meilleures performances, utilisez le protocole TCP hello lorsque cela est possible.

     Lorsque vous utilisez TCP en Mode de passerelle, le Port TCP 443 est hello Cosmos DB port et 10255 est le port de MongoDB API hello. Lors de l’utilisation de TCP en Mode Direct, dans les ports de passerelle toohello addition, vous avez besoin de port de hello tooensure compris entre 10000 et 20000 est ouvert, car Cosmos DB utilise des ports TCP dynamiques. Si ces ports ne sont pas ouverts et que vous essayez de toouse TCP, vous recevez une erreur de 503 Service non disponible.

     Mode de connectivité de Hello est configuré pendant la construction de hello d’instance de DocumentClient hello avec le paramètre ConnectionPolicy hello. Si le Mode Direct est utilisé, hello protocole peut également être définie dans paramètres de ConnectionPolicy hello.

    ```C#
    var serviceEndpoint = new Uri("https://contoso.documents.net");
    var authKey = new "your authKey from hello Azure portal";
    DocumentClient client = new DocumentClient(serviceEndpoint, authKey,
    new ConnectionPolicy
    {
        ConnectionMode = ConnectionMode.Direct,
        ConnectionProtocol = Protocol.Tcp
    });
    ```

    TCP est uniquement pris en charge en Mode Direct, si le Mode de passerelle est utilisé, puis hello le protocole HTTPS est toujours utilisé toocommunicate avec hello passerelle et hello valeur du protocole Bonjour que connectionpolicy est ignoré.

    ![Illustration de la stratégie de connexion de base de données Azure Cosmos de hello](./media/performance-tips/connection-policy.png)

3. **Latence de démarrage de tooavoid OpenAsync des appels à la première demande**

    Par défaut, la première demande de hello a une latence plus élevée, car elle contient la table de routage d’adresse toofetch hello. tooavoid cette latence de démarrage sur hello demande tout d’abord, vous devez appeler OpenAsync() qu’une seule fois lors de l’initialisation, comme suit.

        await client.OpenAsync();
   <a id="same-region"></a>
4. **Colocalisation des clients dans la même région Azure pour les performances**

    Lorsque possible, place toutes les applications de l’appel de base de données Cosmos dans hello même région que hello de base de données de base de données de Cosmos. Pour une comparaison approximative, appelle tooCosmos DB dans hello même région se termine dans 1 à 2 ms, mais la latence hello entre hello ouest et la côte est de hello US est > à 50 ms. Cette latence peut varier probablement de toorequest demande en fonction de l’itinéraire hello pris par la demande de hello lorsqu’il passe à partir de la limite de centre de données Azure hello client toohello. Hello la latence la plus basse possible est obtenue en garantissant l’appel hello se trouve dans hello même région Azure que hello configuré de point de terminaison de base de données Cosmos. Pour obtenir la liste des régions disponibles, voir [Régions Azure](https://azure.microsoft.com/regions/#services).

    ![Illustration de la stratégie de connexion de base de données Azure Cosmos de hello](./media/performance-tips/same-region.png)
   <a id="increase-threads"></a>
5. **Augmentation du nombre de threads/tâches**

    Étant donné que les appels tooAzure Cosmos DB sont effectuées via le réseau de hello, vous devrez peut-être degré de hello toovary de parallélisme de vos demandes afin que l’application cliente de hello consacre à très peu de temps d’attente entre les demandes. Par exemple, si vous utilisez. De NET [bibliothèque parallèle de tâches](https://msdn.microsoft.com//library/dd460717.aspx), créer dans l’ordre de hello de 100 s de lecture ou écriture tooCosmos base de données de tâches.

## <a name="sdk-usage"></a>Utilisation du kit de développement logiciel (SDK)
1. **Installer hello du Kit de développement logiciel plus récent**

    Hello Cosmos DB SDK sont constamment hello tooprovide amélioration des performances optimales. Consultez hello [Cosmos DB SDK](documentdb-sdk-dotnet.md) pages toodetermine hello du Kit de développement logiciel plus récent et passez en revue les améliorations.
2. **Utiliser un client de base de données Cosmos singleton pour la durée de vie hello de votre application**

    Notez que chaque instance de DocumentClient est thread-safe et effectue une gestion des connexions efficace et une mise en cache d’adresses lorsque le mode direct est sélectionné. gestion des connexions efficace de tooallow et de meilleures performances par DocumentClient, il est recommandé d’une seule instance de DocumentClient par AppDomain toouse pour la durée de vie de hello d’application hello.

   <a id="max-connection"></a>
3. **Augmentation de System.Net MaxConnections par hôte lors de l’utilisation du mode passerelle**

    COSMOS DB demandes sont effectuées via le protocole HTTPS/REST lorsque le mode de passerelle et sont soumis toohello limite de connexion par défaut par le nom d’hôte ou adresse IP. Vous devrez peut-être tooset hello MaxConnections tooa valeur plus élevée (100-1000) afin que hello bibliothèque cliente peut utiliser plusieurs connexions simultanées tooCosmos DB. Hello .NET SDK 1.8.0 et ci-dessus, hello la valeur par défaut de [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx) est 50 et toochange hello valeur, vous pouvez définir des hello [Documents.Client.ConnectionPolicy.MaxConnectionLimit ](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.connectionpolicy.maxconnectionlimit.aspx) tooa plus élevée.   
4. **Paramétrage des requêtes parallèles pour les collections partitionnées**

     DocumentDB .NET SDK version à 1.9.0 et versions ultérieures de la prise en charge des requêtes parallèles, ce qui vous permettent de tooquery une collection partitionnée en parallèle (voir [utilisation de kits de développement logiciel de hello](documentdb-partition-data.md#working-with-the-azure-cosmos-db-sdks) et hello liées [exemples de code](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Queries/Program.cs) pour plus d’informations). Requêtes parallèles sont débit et la latence requête tooimprove conçue sur leur équivalent en série. Requêtes parallèles fournissent deux paramètres que les utilisateurs peuvent paramétrer toocustom ajuster leurs exigences, (a) MaxDegreeOfParallelism : nombre maximal de toocontrol hello de partitions puis peut être interrogée en parallèle et (b) MaxBufferedItemCount : nombre de hello toocontrol de résultats préalablement extraites.

    (a) La requête parallèle ***Tuning MaxDegreeOfParallelism\:*** interroge plusieurs partitions en parallèle. Toutefois, les données à partir d’une collecte partitionnée individuel sont extraites en série avec respect toohello requête. Par conséquent, la définition hello MaxDegreeOfParallelism toohello du nombre de partitions est hello maximale susceptible d’aboutir atteindre hello la plupart des requêtes de performant, fourni toutes les autres conditions système restent hello même. Si vous ne connaissez pas nombre hello de partitions, vous pouvez définir le nombre élevé de hello MaxDegreeOfParallelism tooa et système de hello choisit le minimum de hello (nombre de partitions, l’entrée d’utilisateur fourni) comme hello MaxDegreeOfParallelism.

    Il est important toonote parallèles requêtes produisent hello avantages si les données de salutation sont répartie équitablement entre toutes les partitions avec respect toohello requête. Si hello partitionnée collection est partitionnée de telle façon que tout ou une majorité des données hello retournées par une requête est concentrée dans plusieurs partitions (une partition dans le pire des cas), puis performances hello de requête de hello serait être encombré par ces partitions.

    (b) ***MaxBufferedItemCount de réglage\: *** requête parallèle est résultats de l’extraction toopre conçue pendant le traitement de lot en cours de hello des résultats par le client de hello. Hello prérécupération permet à l’amélioration de la latence globale d’une requête. MaxBufferedItemCount est hello paramètre toolimit hello différents résultats préalablement extraites. Paramètre MaxBufferedItemCount toohello attendu hello requête tooreceive maximum de profit de prérécupération permet de nombre de résultats retournés (ou un nombre plus élevé).

    Notez qu’avant l’extraction works hello même façon indépendamment de hello MaxDegreeOfParallelism, et une seule mémoire tampon pour les données de salutation de toutes les partitions.  
5. **Activation de GC côté serveur**

    Réduction de fréquence hello du garbage collection peut aider dans certains cas. Dans .NET, définissez [gcServer](https://msdn.microsoft.com/library/ms229357.aspx) tootrue.
6. **Implémentation d’interruption à des intervalles de RetryAfter**

    Lors du test de performances, vous devez augmenter la charge jusqu’à une limite d’un petit nombre de requêtes. Si la limitation, hello application cliente doit interruption en cas de limitation pour hello spécifiée par le serveur intervalle avant nouvelle tentative. En respectant hello interruption garantit que vous passez des minimiser le temps d’attente entre deux tentatives. Prise en charge de stratégie de nouvelle tentative est inclus dans la Version 1.8.0 et versions ultérieures de hello DocumentDB [.NET](documentdb-sdk-dotnet.md) et [Java](documentdb-sdk-java.md), version à 1.9.0 et versions ultérieures de hello [Node.js](documentdb-sdk-node.md) et [ Python](documentdb-sdk-python.md), et toutes les versions de hello [.NET Core](documentdb-sdk-dotnet-core.md) kits de développement logiciel. Pour plus d’informations, consultez la section [Dépassement des limites de débit réservé](request-units.md#RequestRateTooLarge) et [Propriété RetryAfter](https://msdn.microsoft.com/library/microsoft.azure.documents.documentclientexception.retryafter.aspx).
7. **Augmentation de la taille des instances de votre charge de travail cliente**

    Si vous testez à des niveaux de débit élevé (> 50 000 ur/s), application de client hello peut devenir le goulot d’étranglement hello en raison de la limitation des machine toohello out sur l’utilisation du processeur ou le réseau. Si vous atteignez ce point, vous pouvez continuer compte plus de toopush hello Cosmos DB par montée en puissance parallèle de vos applications clientes sur plusieurs serveurs.
8. **Mise en cache d’URI de document pour une latence de lecture plus faible**

    Document du cache URI autant que possible pour de meilleures performances de lecture hello.
   <a id="tune-page-size"></a>
9. **Régler la taille de la page hello pour les flux de requêtes/lecture pour de meilleures performances**

    Lors de l’exécution d’un bloc de lecture de documents à l’aide de la lecture de flux de fonctionnalités (par exemple, ReadDocumentFeedAsync) ou lors de l’émission d’une requête SQL DocumentDB, les résultats de hello sont retournés sous forme de segmenté si le jeu de résultats hello est trop grande. Par défaut, les résultats sont retournés dans des segments de 100 éléments ou de 1 Mo, selon la limite atteinte en premier.

    nombre de hello tooreduce de réseau tooretrieve d’allers-retours requis tous les résultats applicables, vous pouvez augmenter la taille de page hello too1000 de tooup d’en-tête x-ms-max-item-count demande. Dans le cas où vous devez toodisplay que quelques résultats, par exemple, si votre API d’application ou d’interface utilisateur retourne uniquement les 10 entraîne un temps, vous pouvez également réduire hello page taille too10 tooreduce hello débit consommé pour les lectures et les requêtes.

    Vous pouvez également définir la taille de la page hello à l’aide de hello disponible Cosmos DB kits de développement logiciel.  Par exemple :

        IQueryable<dynamic> authorResults = client.CreateDocumentQuery(documentCollection.SelfLink, "SELECT p.Author FROM Pages p WHERE p.Title = 'About Seattle'", new FeedOptions { MaxItemCount = 1000 });
10. **Augmentation du nombre de threads/tâches**

    Consultez [augmenter le nombre de threads/tâches](#increase-threads) Bonjour section de mise en réseau.

11. **Utilisation du processus hôte 64 bits**

    Hello DocumentDB SDK fonctionne dans un processus hôte 32 bits lorsque vous utilisez le Kit de développement logiciel .NET DocumentDB version 1.11.4 et versions ultérieures. Toutefois, que si vous utilisez des requêtes entre les partitions, le processus hôte 64 bits est recommandé pour améliorer les performances. Hello, les types d’applications suivants ont hôte 32 bits traiter comme valeur par défaut de hello, par conséquent, dans l’ordre toochange too64 bits autrement, procédez comme suit selon le type hello de votre application :

    - Pour les applications exécutables, cela est possible en décochant les cases hello **préférer 32 bits** option Bonjour **propriétés du projet** fenêtre hello **générer** onglet.

    - Pour VSTest basés sur des projets de test, cela peut être effectuée en sélectionnant **Test**->**des paramètres de Test**->**Architecture du processeur par défaut en tant que X64**, à partir de hello **Visual Studio Test** option de menu.

    - Pour les applications Web ASP.NET déployées localement, cela est possible en vérifiant hello **utilisez hello 64 bits d’IIS Express pour les projets et sites web**, sous **outils** ->  **Options**->**projets et Solutions**->**projets Web**.

    - Pour les applications Web ASP.NET déployées sur Azure, cela est possible en choisissant hello **plate-forme 64 bits** Bonjour **paramètres de l’Application** sur hello portail Azure.

## <a name="indexing-policy"></a>Stratégie d'indexation
1. **Utilisation de l’indexation différée pour des taux d’ingestion plus rapides en période de pointe**

    COSMOS DB permet toospecify – au niveau de collection hello : une stratégie d’indexation, qui vous permet de toochoose si vous souhaitez que les documents hello dans un toobe collection automatiquement indexé ou non.  En outre, vous avez le choix entre des mises à jour d’index synchrones (cohérentes) et asynchrones (différées). Par défaut, les index hello est mis à jour synchrone chaque insertion, remplacer ou supprimer d’une collection de toohello document. Mode synchrone en mode Active hello requêtes toohonor hello même [au niveau de cohérence](consistency-levels.md) que celui de hello document lit sans délai pour les index hello trop « rattraper ».

    Indexation différée peut être considéré comme pour les scénarios dans lesquels les données sont écrites en rafales, et que vous souhaitez tooamortize hello travail requis tooindex contenu sur une longue période de temps. Indexation différée vous permet également de toouse votre approvisionné efficacement de débit et de servir des requêtes d’écriture aux heures de pointe avec une latence minimale. Il est important toonote, toutefois, que lors de l’indexation différée est activée, les résultats de requête sont cohérentes quel que soit le niveau de cohérence hello configuré pour le compte de base de données Cosmos hello.

    Par conséquent, mode d’indexation cohérent (IndexingPolicy.IndexingMode a la valeur tooConsistent) entraîne hello plus élevé demande unité coût pour chaque écriture, tout en Lazy indexation mode (IndexingPolicy.IndexingMode a la valeur tooLazy) et l’indexation (IndexingPolicy.Automatic a la valeur tooFalse) ont coût nul indexation au moment de hello d’écriture.
2. **Exclusion des chemins d’accès inutilisés de l’indexation pour des écritures plus rapides**

    Stratégie d’indexation COSMOS de base de données vous permet également de toospecify tooinclude de chemins d’accès de document ou à exclure de l’indexation en tirant parti de l’indexation des chemins d’accès (IndexingPolicy.IncludedPaths et IndexingPolicy.ExcludedPaths). utilisation de Hello de l’indexation de chemins d’accès peut offrir des performances d’écriture amélioré et le stockage d’index inférieure pour les scénarios qui Bonjour modèles de requête sont appelés au préalable, les coûts d’indexation sont directement en corrélation nombre toohello de chemins d’accès uniques indexés.  Par exemple, hello suivant de code montre comment tooexclude une section complète de hello documents (aussi appelé) une sous-arborescence) de l’indexation à l’aide de hello « * » générique.

    ```C#
    var collection = new DocumentCollection { Id = "excludedPathCollection" };
    collection.IndexingPolicy.IncludedPaths.Add(new IncludedPath { Path = "/*" });
    collection.IndexingPolicy.ExcludedPaths.Add(new ExcludedPath { Path = "/nonIndexedContent/*");
    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), excluded);
    ```

    Pour plus d’informations, consultez [Stratégies d’indexation d’Azure Cosmos DB](indexing-policies.md).

## <a name="throughput"></a>Débit
<a id="measure-rus"></a>

1. **Mesure et réglage pour réduire l’utilisation d’unités de requête par seconde**

    COSMOS DB offre un ensemble complet d’opérations de base de données, y compris des requêtes relationnelles et hiérarchiques avec UDF, procédures stockées et déclencheurs – fonctionnement sur des documents hello dans une collection de base de données. coût Hello associée à chacune de ces opérations varie en fonction de hello UC, e/s et mémoire requise toocomplete hello opération. Au lieu de penser et la gestion des ressources matérielles, vous pouvez considérer d’une unité de demande (RU) en tant qu’une seule mesure pour tooperform requis de ressources hello diverses opérations de base de données et le service demande d’une application.

    [Unités de requête](request-units.md) sont configurés pour chaque compte de base de données en fonction du nombre de hello d’unités de capacité que vous achetez. La consommation d'unités de demande est évaluée en fonction d'un taux par seconde. Les applications qui dépassent les unités de demande configuré hello du taux de leur compte est limité jusqu'à ce que le taux de hello inférieure hello niveau réservé pour le compte de hello. Si votre application a besoin d'un niveau de débit plus élevé, vous pouvez acheter des unités de capacité supplémentaires.

    complexité Hello d’une requête a un impact sur le nombre d’unités demande sont consommé pour une opération. nombre Hello de prédicats, nature de prédicats de hello, nombre des UDF et la taille de hello du jeu de données source hello tous influencent coût hello d’opérations de requête.

    surcharge de hello toomeasure de n’importe quelle opération (créer, mettre à jour ou supprimer), inspecter l’en-tête x-ms-demande-frais de hello (ou hello propriété RequestCharge équivalente dans ResourceResponse<T> ou FeedResponse<T> Bonjour .NET SDK) toomeasure nombre de Hello d’unités de demande utilisés par ces opérations.

    ```C#
    // Measure hello performance (request units) of writes
    ResourceResponse<Document> response = await client.CreateDocumentAsync(collectionSelfLink, myDocument);
    Console.WriteLine("Insert of document consumed {0} request units", response.RequestCharge);
    // Measure hello performance (request units) of queries
    IDocumentQuery<dynamic> queryable = client.CreateDocumentQuery(collectionSelfLink, queryString).AsDocumentQuery();
    while (queryable.HasMoreResults)
         {
              FeedResponse<dynamic> queryResponse = await queryable.ExecuteNextAsync<dynamic>();
              Console.WriteLine("Query batch consumed {0} request units", queryResponse.RequestCharge);
         }
    ```             

    frais de demande renvoyé dans cet en-tête Hello désigne une fraction de votre débit approvisionné (c'est-à-dire 2000 RUs / seconde). Par exemple, si hello requête précédente retourne 1000 1 Ko-documents, coût hello d’opération de hello est 1000. Par conséquent, au sein d’une seconde, serveur de hello ne honore que deux de ces demandes avant la limitation des demandes suivantes. Pour plus d’informations, consultez [unités de requête](request-units.md) et hello [calculatrice des unités de demande](https://www.documentdb.com/capacityplanner).
<a id="429"></a>
2. **Gestion de la limite de taux/du taux de requête trop importants**

    Lorsqu’un client essaie de débit réservés de tooexceed hello pour un compte, il n’existe aucune dégradation des performances sur le serveur de hello et aucune utilisation de la capacité de débit au-delà du niveau de hello réservé. serveur de Hello va se terminer manière préemptive demande hello avec RequestRateTooLarge (code d’état HTTP 429) et retour hello x-ms-nouvelle tentative-après-ms en-tête indiquant hello durée, en millisecondes, pendant lequel hello utilisateur doit attendre avant de retenter la demande de hello.

        HTTP Status 429,
        Status Line: RequestRateTooLarge
        x-ms-retry-after-ms :100

    Kits de développement logiciel Hello toutes implicitement intercepter cette réponse respectent en-tête hello spécifiée par le serveur retry-after et nouvelle tentative de demande de hello. À moins que votre compte est accessible simultanément par plusieurs clients, hello suivant sera réalisée.

    Si vous avez plusieurs clients cumulative d’exploitation cohérente du taux de demande hello, hello par défaut de nouvelles tentatives actuellement too9 ensemble en interne par le client de hello ne suffisent pas ; Dans ce cas, les clients hello lève une DocumentClientException avec l’application en état code 429 toohello. nombre de tentatives Hello par défaut peut être modifié par hello paramètre RetryOptions sur l’instance de ConnectionPolicy hello. Par défaut, hello DocumentClientException avec le code d’état 429 est retourné après un délai d’attente cumulé de 30 secondes si la demande de hello continue toooperate du taux de demande hello. Cela produit même lorsque nombre de tentatives hello est inférieur au nombre de tentatives maximum de hello, qu’il s’agisse de la valeur par défaut hello 9 ou une valeur définie par l’utilisateur.

    Tandis que hello automatisée comportement des nouvelles tentatives permet aux tooimprove résilience et la facilité d’utilisation pour hello la plupart des applications, il peut provenir opposés lors de l’exécution des tests de performances, en particulier quand mesurer la latence.  latence de client observée Hello atteindra si expérience de hello atteint la limitation du serveur hello et provoque le client hello réessayer toosilently de kit de développement logiciel. latence de tooavoid des pics se produisent au cours des expériences de performances, mesure hello frais retournés par chaque opération et s’assurer que les demandes fonctionnent sous les taux réservé hello. Pour plus d’informations, consultez [Unités de requête](request-units.md).
3. **Conception de documents plus petits pour un débit plus élevé**

    Bonjour demande frais (autrement dit, le coût de traitement de la demande) d’une opération donnée sont directement mis en corrélation de taille toohello du document de hello. Des opérations sur des documents volumineux coûtent plus cher que des opérations sur de petits documents.

## <a name="next-steps"></a>Étapes suivantes
Pour un tooevaluate d’application utilisée exemple Cosmos DB pour les scénarios de haute performance sur quelques ordinateurs clients, consultez [performances et évolutivité de test avec la base de données Cosmos](performance-testing.md).

En outre, toolearn savoir plus sur la conception de votre application pour la mise à l’échelle et de hautes performances, consultez [de partitionnement et de mise à l’échelle dans la base de données Azure Cosmos](partition-data.md).
