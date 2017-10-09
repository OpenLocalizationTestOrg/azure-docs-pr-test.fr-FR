---
title: "architectures de base de données master d’aaaMulti avec la base de données Azure Cosmos | Documents Microsoft"
description: "Découvrez comment les architectures d’application toodesign avec local lit et écrit dans plusieurs régions géographiques avec la base de données Azure Cosmos."
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: 
ms.assetid: 706ced74-ea67-45dd-a7de-666c3c893687
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3269c8405afe16f75db69b42e576fe76e00a8e16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="multi-master-globally-replicated-database-architectures-with-azure-cosmos-db"></a>Architectures de base de données à multiples maîtres répliquées de façon globale avec Azure Cosmos DB
Base de données Azure Cosmos prend en charge les clés en main [réplication globale](distribute-data-globally.md), qui vous permet de toodistribute données toomultiple régions à faible latence n’importe où dans la charge de travail hello. Ce modèle est généralement utilisé pour les charges de travail éditeur/consommateur, où un enregistreur existe dans une région géographique unique et des lecteurs sont distribués mondialement dans d’autres régions (lecture). 

Vous pouvez également utiliser Azure Cosmos DB global de réplication prennent toobuild des applications dans lesquelles les enregistreurs et lecteurs sont globalement distribuées. Ce document décrit un modèle qui permet d’obtenir un accès en écriture locale et en lecture locale pour les enregistreurs utilisant Azure Cosmos DB.

## <a id="ExampleScenario"></a>Publication de contenu : un exemple de scénario
Examinons un toodescribe de scénario réel comment vous pouvez utiliser les modèles distribués internationalement multiples region/multi-cluster master lecture/écriture avec la base de données Azure Cosmos. Prenons l’exemple d’une plateforme de contenu reposant sur Azure Cosmos DB. Voici certaines exigences que cette plateforme doit respecter pour une expérience utilisateur exceptionnelle pour les éditeurs et les consommateurs.

* Les auteurs et les abonnés sont répartis sur Bonjour 
* Les auteurs doivent publier région (le plus proche) locale articles tootheir (écriture)
* Les auteurs des lecteurs/abonnés de leurs articles qui sont distribuées monde hello. 
* Les abonnés doivent recevoir une notification lorsque de nouveaux articles sont publiés.
* Les abonnés doivent être en mesure de tooread des articles à partir de leur région. Ils doivent aussi être en mesure de tooadd révisions toothese articles. 
* Toute personne notamment auteur hello d’articles de hello doit être en mesure de visualiser que toutes les hello révisions de tooarticles attaché à partir d’une région. 

En supposant que des millions d’utilisateurs et les éditeurs avec des milliards d’articles, dès que nous avons des problèmes de hello tooconfront de mise à l’échelle en même temps que ce qui garantit la localité d’accès. Comme avec la plupart des problèmes d’évolutivité, la solution de hello se trouve dans une stratégie de partitionnement efficace. Ensuite, nous allons examiner comment toomodel articles, révision et des notifications sous forme de documents, configurent des comptes de la base de données Azure Cosmos et implémenter une couche d’accès aux données. 

Si vous souhaitez que toolearn plus d’informations sur les clés de partition et de partitionnement, consultez [le partitionnement et la mise à l’échelle dans la base de données Azure Cosmos](partition-data.md).

## <a id="ModelingNotifications"></a>Modélisation des notifications
Les notifications sont utilisateur tooa spécifique du flux de données. Par conséquent, les modèles d’accès hello pour les documents de notifications sont toujours dans le contexte de hello d’utilisateur unique. Par exemple, vous serez « post utilisateur tooa notification » ou « extraire toutes les notifications pour un utilisateur donné ». Par conséquent, hello meilleur choix de clé de partitionnement pour ce type n’est `UserId`.

    class Notification 
    { 
        // Unique ID for Notification. 
        public string Id { get; set; }

        // hello user Id for which notification is addressed to. 
        public string UserId { get; set; }

        // hello partition Key for hello resource. 
        public string PartitionKey 
        { 
            get 
            { 
                return this.UserId; 
            }
        }

        // Subscription for which this notification is raised. 
        public string SubscriptionFilter { get; set; }

        // Subject of hello notification. 
        public string ArticleId { get; set; } 
    }

## <a id="ModelingSubscriptions"></a>Modélisation des abonnements
Les abonnements peuvent être créés selon différents critères comme une catégorie spécifique d’articles d’intérêt ou un éditeur spécifique. Par conséquent, hello `SubscriptionFilter` est un bon choix pour la clé de partition.

    class Subscriptions 
    { 
        // Unique ID for Subscription 
        public string Id { get; set; }

        // Subscription source. Could be Author | Category etc. 
        public string SubscriptionFilter { get; set; }

        // subscribing User. 
        public string UserId { get; set; }

        public string PartitionKey 
        { 
            get 
            { 
                return this.SubscriptionFilter; 
            } 
        } 
    }

## <a id="ModelingArticles"></a>Modélisation des articles
Une fois qu’un article est identifié par le biais des notifications, les requêtes suivantes sont généralement basés sur hello `Article.Id`. En choisissant `Article.Id` en tant que partition clé de hello fournit ainsi la distribution de meilleures hello pour le stockage des articles à l’intérieur d’une collection de base de données Azure Cosmos. 

    class Article 
    { 
        // Unique ID for Article 
        public string Id { get; set; }
        
        public string PartitionKey 
        { 
            get 
            { 
                return this.Id; 
            } 
        }
        
        // Author of hello article
        public string Author { get; set; }

        // Category/genre of hello article
        public string Category { get; set; }

        // Tags associated with hello article
        public string[] Tags { get; set; }

        // Title of hello article
        public string Title { get; set; }
        
        //... 
    }

## <a id="ModelingReviews"></a>Modélisation des avis
Comme des articles, révisions sont principalement écrites et lues dans le contexte de hello d’article. Choisir `ArticleId` en tant que clé de partition fournit une meilleure distribution et un accès efficace aux avis associés à l’article. 

    class Review 
    { 
        // Unique ID for Review 
        public string Id { get; set; }

        // Article Id of hello review 
        public string ArticleId { get; set; }

        public string PartitionKey 
        { 
            get 
            { 
                return this.ArticleId; 
            } 
        }
        
        //Reviewer Id 
        public string UserId { get; set; }
        public string ReviewText { get; set; }
        
        public int Rating { get; set; } }
    }

## <a id="DataAccessMethods"></a>Méthodes de couche d’accès aux données
Maintenant examinons les données principales hello nous devons tooimplement méthodes d’accès. Voici la liste hello des méthodes hello `ContentPublishDatabase` doit :

    class ContentPublishDatabase 
    { 
        public async Task CreateSubscriptionAsync(string userId, string category);
    
        public async Task<IEnumerable<Notification>> ReadNotificationFeedAsync(string userId);
    
        public async Task<Article> ReadArticleAsync(string articleId);
    
        public async Task WriteReviewAsync(string articleId, string userId, string reviewText, int rating);
    
        public async Task<IEnumerable<Review>> ReadReviewsAsync(string articleId); 
    }

## <a id="Architecture"></a>Configuration du compte Azure Cosmos DB
tooguarantee local lit et écrit, nous devez partitionner les données non seulement sur la clé de partition, mais également basé sur le modèle d’accès géographiques hello en régions. modèle de Hello s’appuie sur la présence d’un compte de base de données de base de données Azure Cosmos de géo-répliquées pour chaque région. Voici, par exemple, une configuration pour les écritures multirégions avec deux régions :

| Nom du compte | Région d’écriture | Région de lecture |
| --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |

Hello diagramme suivant montre comment les lectures et écritures sont effectuées dans une application classique avec ce programme d’installation :

![Architecture à multiples maîtres Azure Cosmos DB](./media/multi-region-writers/multi-master.png)

Voici un extrait de code montrant comment tooinitialize hello clients dans la couche DAL en cours d’exécution dans hello `West US` région.
    
    ConnectionPolicy writeClientPolicy = new ConnectionPolicy { ConnectionMode = ConnectionMode.Direct, ConnectionProtocol = Protocol.Tcp };
    writeClientPolicy.PreferredLocations.Add(LocationNames.WestUS);
    writeClientPolicy.PreferredLocations.Add(LocationNames.NorthEurope);

    DocumentClient writeClient = new DocumentClient(
        new Uri("https://contentpubdatabase-usa.documents.azure.com"), 
        writeRegionAuthKey,
        writeClientPolicy);

    ConnectionPolicy readClientPolicy = new ConnectionPolicy { ConnectionMode = ConnectionMode.Direct, ConnectionProtocol = Protocol.Tcp };
    readClientPolicy.PreferredLocations.Add(LocationNames.NorthEurope);
    readClientPolicy.PreferredLocations.Add(LocationNames.WestUS);

    DocumentClient readClient = new DocumentClient(
        new Uri("https://contentpubdatabase-europe.documents.azure.com"),
        readRegionAuthKey,
        readClientPolicy);

Avec hello précédant le programme d’installation, couche d’accès aux données hello peut transférer toutes les écritures toohello compte local basé sur lesquels il est déployé. Les lectures sont effectuées par la lecture à partir de ces deux vue comptes tooget hello globale de données. Cette approche peut être étendu tooas plusieurs régions, en fonction des besoins. Voici, par exemple, une configuration avec trois régions :

| Nom du compte | Région d’écriture | Région de lecture 1 | Région de lecture 2 |
| --- | --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |`Southeast Asia` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |`Southeast Asia` |
| `contentpubdatabase-asia.documents.azure.com` | `Southeast Asia` |`North Europe` |`West US` |

## <a id="DataAccessImplementation"></a>Mise en œuvre de la couche d’accès aux données
Maintenant examinons implémentation hello de hello couche d’accès aux données (DAL) pour une application avec les deux régions accessible en écriture. Hello DAL doit implémenter hello comme suit :

* Créer plusieurs instances de `DocumentClient` pour chaque compte. Avec deux régions, chaque instance de la couche d’accès aux données possède un `writeClient` et `readClient`. 
* En fonction de la région de hello déployée de l’application hello, configurer des points de terminaison hello pour `writeclient` et `readClient`. Par exemple, hello DAL déployée dans `West US` utilise `contentpubdatabase-usa.documents.azure.com` pour effectuer des écritures. Hello DAL déployé dans `NorthEurope` utilise `contentpubdatabase-europ.documents.azure.com` pour les écritures.

Avec hello précédant le programme d’installation, les méthodes d’accès données hello peuvent être implémentés. Écrire des opérations transférer hello écriture toohello correspondant `writeClient`.

    public async Task CreateSubscriptionAsync(string userId, string category)
    {
        await this.writeClient.CreateDocumentAsync(this.contentCollection, new Subscriptions
        {
            UserId = userId,
            SubscriptionFilter = category
        });
    }

    public async Task WriteReviewAsync(string articleId, string userId, string reviewText, int rating)
    {
        await this.writeClient.CreateDocumentAsync(this.contentCollection, new Review
        {
            UserId = userId,
            ArticleId = articleId,
            ReviewText = reviewText,
            Rating = rating
        });
    }

Pour lire les notifications et les analyses, vous devez lire les régions et les résultats de l’union hello comme indiqué dans hello suivant extrait :

    public async Task<IEnumerable<Notification>> ReadNotificationFeedAsync(string userId)
    {
        IDocumentQuery<Notification> writeAccountNotification = (
            from notification in this.writeClient.CreateDocumentQuery<Notification>(this.contentCollection) 
            where notification.UserId == userId 
            select notification).AsDocumentQuery();
        
        IDocumentQuery<Notification> readAccountNotification = (
            from notification in this.readClient.CreateDocumentQuery<Notification>(this.contentCollection) 
            where notification.UserId == userId 
            select notification).AsDocumentQuery();

        List<Notification> notifications = new List<Notification>();

        while (writeAccountNotification.HasMoreResults || readAccountNotification.HasMoreResults)
        {
            IList<Task<FeedResponse<Notification>>> results = new List<Task<FeedResponse<Notification>>>();

            if (writeAccountNotification.HasMoreResults)
            {
                results.Add(writeAccountNotification.ExecuteNextAsync<Notification>());
            }

            if (readAccountNotification.HasMoreResults)
            {
                results.Add(readAccountNotification.ExecuteNextAsync<Notification>());
            }

            IList<FeedResponse<Notification>> notificationFeedResult = await Task.WhenAll(results);

            foreach (FeedResponse<Notification> feed in notificationFeedResult)
            {
                notifications.AddRange(feed);
            }
        }
        return notifications;
    }

    public async Task<IEnumerable<Review>> ReadReviewsAsync(string articleId)
    {
        IDocumentQuery<Review> writeAccountReviews = (
            from review in this.writeClient.CreateDocumentQuery<Review>(this.contentCollection) 
            where review.ArticleId == articleId 
            select review).AsDocumentQuery();
        
        IDocumentQuery<Review> readAccountReviews = (
            from review in this.readClient.CreateDocumentQuery<Review>(this.contentCollection) 
            where review.ArticleId == articleId 
            select review).AsDocumentQuery();

        List<Review> reviews = new List<Review>();
        
        while (writeAccountReviews.HasMoreResults || readAccountReviews.HasMoreResults)
        {
            IList<Task<FeedResponse<Review>>> results = new List<Task<FeedResponse<Review>>>();

            if (writeAccountReviews.HasMoreResults)
            {
                results.Add(writeAccountReviews.ExecuteNextAsync<Review>());
            }

            if (readAccountReviews.HasMoreResults)
            {
                results.Add(readAccountReviews.ExecuteNextAsync<Review>());
            }

            IList<FeedResponse<Review>> notificationFeedResult = await Task.WhenAll(results);

            foreach (FeedResponse<Review> feed in notificationFeedResult)
            {
                reviews.AddRange(feed);
            }
        }

        return reviews;
    }

Par conséquent, en choisissant une bonne clé de partitionnement et le partitionnement statique basé sur les comptes, vous pouvez effectuer des lectures et écritures locales multirégions à l’aide d’Azure Cosmos DB.

## <a id="NextSteps"></a>Étapes suivantes
Dans cet article, nous avons décrit comment vous pouvez utiliser des modèles lecture/écriture multirégions mondialement distribués avec Azure Cosmos DB à l’aide de la publication de contenu comme exemple de scénario.

* Découvrez-en plus sur la manière dont Azure Cosmos DB prend en charge la [distribution mondiale](distribute-data-globally.md)
* En savoir plus sur les [basculements manuels et automatiques dans Azure Cosmos DB](regional-failover.md)
* Découvrez-en plus sur [la cohérence globale avec Azure Cosmos DB](consistency-levels.md)
* Développer avec plusieurs régions à l’aide de hello [Azure Cosmos DB - API DocumentDB](tutorial-global-distribution-documentdb.md)
* Développer avec plusieurs régions à l’aide de hello [Azure Cosmos DB - MongoDB API](tutorial-global-distribution-MongoDB.md)
* Développer avec plusieurs régions à l’aide de hello [Azure Cosmos DB - API de Table](tutorial-global-distribution-table.md)
