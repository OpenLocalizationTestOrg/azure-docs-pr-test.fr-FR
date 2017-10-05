---
title: "Architectures de base de données à multiples maîtres avec Azure Cosmos DB | Microsoft Docs"
description: "En savoir plus sur la conception des architectures d’application avec les lectures et écritures locales dans plusieurs régions géographiques avec Azure Cosmos DB."
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
ms.openlocfilehash: cf1482ae7b1070023703f5dbe861d151f5d64fd8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="multi-master-globally-replicated-database-architectures-with-azure-cosmos-db"></a><span data-ttu-id="3223f-103">Architectures de base de données à multiples maîtres répliquées de façon globale avec Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="3223f-103">Multi-master globally replicated database architectures with Azure Cosmos DB</span></span>
<span data-ttu-id="3223f-104">Azure Cosmos DB prend en charge la [réplication globale](distribute-data-globally.md) clé en main, qui vous permet de distribuer les données dans plusieurs régions avec accès à faible latence n’importe où dans la charge de travail.</span><span class="sxs-lookup"><span data-stu-id="3223f-104">Azure Cosmos DB supports turnkey [global replication](distribute-data-globally.md), which allows you to distribute data to multiple regions with low latency access anywhere in the workload.</span></span> <span data-ttu-id="3223f-105">Ce modèle est généralement utilisé pour les charges de travail éditeur/consommateur, où un enregistreur existe dans une région géographique unique et des lecteurs sont distribués mondialement dans d’autres régions (lecture).</span><span class="sxs-lookup"><span data-stu-id="3223f-105">This model is commonly used for publisher/consumer workloads where there is a writer in a single geographic region and globally distributed readers in other (read) regions.</span></span> 

<span data-ttu-id="3223f-106">Vous pouvez également utiliser la prise en charge de la réplication globale d’Azure Cosmos DB pour créer des applications dans lesquelles des enregistreurs et des lecteurs sont distribués mondialement.</span><span class="sxs-lookup"><span data-stu-id="3223f-106">You can also use Azure Cosmos DB's global replication support to build applications in which writers and readers are globally distributed.</span></span> <span data-ttu-id="3223f-107">Ce document décrit un modèle qui permet d’obtenir un accès en écriture locale et en lecture locale pour les enregistreurs utilisant Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3223f-107">This document outlines a pattern that enables achieving local write and local read access for distributed writers using Azure Cosmos DB.</span></span>

## <span data-ttu-id="3223f-108"><a id="ExampleScenario"></a>Publication de contenu : un exemple de scénario</span><span class="sxs-lookup"><span data-stu-id="3223f-108"><a id="ExampleScenario"></a>Content Publishing - an example scenario</span></span>
<span data-ttu-id="3223f-109">Examinons un scénario réel pour décrire la manière dont vous pouvez utiliser des modèles de lecture/écriture mondialement distribués multirégions/multimaîtres avec Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3223f-109">Let's look at a real world scenario to describe how you can use globally distributed multi-region/multi-master read write patterns with Azure Cosmos DB.</span></span> <span data-ttu-id="3223f-110">Prenons l’exemple d’une plateforme de contenu reposant sur Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3223f-110">Consider a content publishing platform built on Azure Cosmos DB.</span></span> <span data-ttu-id="3223f-111">Voici certaines exigences que cette plateforme doit respecter pour une expérience utilisateur exceptionnelle pour les éditeurs et les consommateurs.</span><span class="sxs-lookup"><span data-stu-id="3223f-111">Here are some requirements that this platform must meet for a great user experience for both publishers and consumers.</span></span>

* <span data-ttu-id="3223f-112">Les auteurs et les abonnés sont répartis dans le monde entier</span><span class="sxs-lookup"><span data-stu-id="3223f-112">Both authors and subscribers are spread over the world</span></span> 
* <span data-ttu-id="3223f-113">Les auteurs doivent publier (écriture) les articles dans leur région (la plus proche)</span><span class="sxs-lookup"><span data-stu-id="3223f-113">Authors must publish (write) articles to their local (closest) region</span></span>
* <span data-ttu-id="3223f-114">Les auteurs ont des lecteurs/abonnés de leurs articles répartis dans le monde entier.</span><span class="sxs-lookup"><span data-stu-id="3223f-114">Authors have readers/subscribers of their articles who are distributed across the globe.</span></span> 
* <span data-ttu-id="3223f-115">Les abonnés doivent recevoir une notification lorsque de nouveaux articles sont publiés.</span><span class="sxs-lookup"><span data-stu-id="3223f-115">Subscribers should get a notification when new articles are published.</span></span>
* <span data-ttu-id="3223f-116">Les abonnés doivent être en mesure de lire les articles de leur région.</span><span class="sxs-lookup"><span data-stu-id="3223f-116">Subscribers must be able to read articles from their local region.</span></span> <span data-ttu-id="3223f-117">Ils doivent également être en mesure d’ajouter des avis concernant ces articles.</span><span class="sxs-lookup"><span data-stu-id="3223f-117">They should also be able to add reviews to these articles.</span></span> 
* <span data-ttu-id="3223f-118">Tout le monde, y compris l’auteur des articles, doit être en mesure de visualiser tous les avis liés aux articles à partir d’une région.</span><span class="sxs-lookup"><span data-stu-id="3223f-118">Anyone including the author of the articles should be able view all the reviews attached to articles from a local region.</span></span> 

<span data-ttu-id="3223f-119">En supposant qu’il y a des millions de consommateurs et d’éditeurs avec des milliards d’articles, nous devrons bientôt faire face à des problèmes de mise à l’échelle et de garantie de localité d’accès.</span><span class="sxs-lookup"><span data-stu-id="3223f-119">Assuming millions of consumers and publishers with billions of articles, soon we have to confront the problems of scale along with guaranteeing locality of access.</span></span> <span data-ttu-id="3223f-120">Comme avec la plupart des problèmes d’évolutivité, la solution réside dans une bonne stratégie de partitionnement.</span><span class="sxs-lookup"><span data-stu-id="3223f-120">As with most scalability problems, the solution lies in a good partitioning strategy.</span></span> <span data-ttu-id="3223f-121">Ensuite, nous verrons comment modéliser des articles, des avis et des notifications sous forme de documents, configurer des comptes Azure Cosmos DB et implémenter une couche d’accès aux données.</span><span class="sxs-lookup"><span data-stu-id="3223f-121">Next, let's look at how to model articles, review, and notifications as documents, configure Azure Cosmos DB accounts, and implement a data access layer.</span></span> 

<span data-ttu-id="3223f-122">Si vous souhaitez en savoir plus sur le partitionnement et les clés de partition, consultez [Partitionnement et mise à l’échelle dans Azure Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="3223f-122">If you would like to learn more about partitioning and partition keys, see [Partitioning and Scaling in Azure Cosmos DB](partition-data.md).</span></span>

## <span data-ttu-id="3223f-123"><a id="ModelingNotifications"></a>Modélisation des notifications</span><span class="sxs-lookup"><span data-stu-id="3223f-123"><a id="ModelingNotifications"></a>Modeling notifications</span></span>
<span data-ttu-id="3223f-124">Les notifications sont des flux de données spécifiques à un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="3223f-124">Notifications are data feeds specific to a user.</span></span> <span data-ttu-id="3223f-125">Par conséquent, les modèles d’accès pour les documents de notifications sont toujours destinés à un utilisateur unique.</span><span class="sxs-lookup"><span data-stu-id="3223f-125">Therefore, the access patterns for notifications documents are always in the context of single user.</span></span> <span data-ttu-id="3223f-126">Ainsi, vous pouvez « publier une notification à un utilisateur » ou « extraire toutes les notifications pour un utilisateur donné ».</span><span class="sxs-lookup"><span data-stu-id="3223f-126">For example, you would "post a notification to a user" or "fetch all notifications for a given user".</span></span> <span data-ttu-id="3223f-127">Ainsi, le choix optimal de clé de partitionnement pour ce type est `UserId`.</span><span class="sxs-lookup"><span data-stu-id="3223f-127">So, the optimal choice of partitioning key for this type would be `UserId`.</span></span>

    class Notification 
    { 
        // Unique ID for Notification. 
        public string Id { get; set; }

        // The user Id for which notification is addressed to. 
        public string UserId { get; set; }

        // The partition Key for the resource. 
        public string PartitionKey 
        { 
            get 
            { 
                return this.UserId; 
            }
        }

        // Subscription for which this notification is raised. 
        public string SubscriptionFilter { get; set; }

        // Subject of the notification. 
        public string ArticleId { get; set; } 
    }

## <span data-ttu-id="3223f-128"><a id="ModelingSubscriptions"></a>Modélisation des abonnements</span><span class="sxs-lookup"><span data-stu-id="3223f-128"><a id="ModelingSubscriptions"></a>Modeling subscriptions</span></span>
<span data-ttu-id="3223f-129">Les abonnements peuvent être créés selon différents critères comme une catégorie spécifique d’articles d’intérêt ou un éditeur spécifique.</span><span class="sxs-lookup"><span data-stu-id="3223f-129">Subscriptions can be created for various criteria like a specific category of articles of interest, or a specific publisher.</span></span> <span data-ttu-id="3223f-130">Par conséquent, `SubscriptionFilter` constitue un bon choix pour la clé de partition.</span><span class="sxs-lookup"><span data-stu-id="3223f-130">Hence the `SubscriptionFilter` is a good choice for partition key.</span></span>

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

## <span data-ttu-id="3223f-131"><a id="ModelingArticles"></a>Modélisation des articles</span><span class="sxs-lookup"><span data-stu-id="3223f-131"><a id="ModelingArticles"></a>Modeling articles</span></span>
<span data-ttu-id="3223f-132">Une fois qu’un article est identifié par le biais des notifications, les requêtes suivantes sont généralement basés sur `Article.Id`.</span><span class="sxs-lookup"><span data-stu-id="3223f-132">Once an article is identified through notifications, subsequent queries are typically based on the `Article.Id`.</span></span> <span data-ttu-id="3223f-133">En choisissant `Article.Id` en tant que partition, la clé fournit la meilleure distribution pour le stockage des articles à l’intérieur d’une collection Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3223f-133">Choosing `Article.Id` as partition the key thus provides the best distribution for storing articles inside an Azure Cosmos DB collection.</span></span> 

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
        
        // Author of the article
        public string Author { get; set; }

        // Category/genre of the article
        public string Category { get; set; }

        // Tags associated with the article
        public string[] Tags { get; set; }

        // Title of the article
        public string Title { get; set; }
        
        //... 
    }

## <span data-ttu-id="3223f-134"><a id="ModelingReviews"></a>Modélisation des avis</span><span class="sxs-lookup"><span data-stu-id="3223f-134"><a id="ModelingReviews"></a>Modeling reviews</span></span>
<span data-ttu-id="3223f-135">Les avis sont principalement écrits et lus dans le contexte de l’article.</span><span class="sxs-lookup"><span data-stu-id="3223f-135">Like articles, reviews are mostly written and read in the context of article.</span></span> <span data-ttu-id="3223f-136">Choisir `ArticleId` en tant que clé de partition fournit une meilleure distribution et un accès efficace aux avis associés à l’article.</span><span class="sxs-lookup"><span data-stu-id="3223f-136">Choosing `ArticleId` as a partition key provides best distribution and efficient access of reviews associated with article.</span></span> 

    class Review 
    { 
        // Unique ID for Review 
        public string Id { get; set; }

        // Article Id of the review 
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

## <span data-ttu-id="3223f-137"><a id="DataAccessMethods"></a>Méthodes de couche d’accès aux données</span><span class="sxs-lookup"><span data-stu-id="3223f-137"><a id="DataAccessMethods"></a>Data access layer methods</span></span>
<span data-ttu-id="3223f-138">Maintenant, examinons les méthodes d’accès aux données principales que nous devons mettre en œuvre.</span><span class="sxs-lookup"><span data-stu-id="3223f-138">Now let's look at the main data access methods we need to implement.</span></span> <span data-ttu-id="3223f-139">Voici une liste des méthodes dont `ContentPublishDatabase` a besoin :</span><span class="sxs-lookup"><span data-stu-id="3223f-139">Here's the list of methods that the `ContentPublishDatabase` needs:</span></span>

    class ContentPublishDatabase 
    { 
        public async Task CreateSubscriptionAsync(string userId, string category);
    
        public async Task<IEnumerable<Notification>> ReadNotificationFeedAsync(string userId);
    
        public async Task<Article> ReadArticleAsync(string articleId);
    
        public async Task WriteReviewAsync(string articleId, string userId, string reviewText, int rating);
    
        public async Task<IEnumerable<Review>> ReadReviewsAsync(string articleId); 
    }

## <span data-ttu-id="3223f-140"><a id="Architecture"></a>Configuration du compte Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="3223f-140"><a id="Architecture"></a>Azure Cosmos DB account configuration</span></span>
<span data-ttu-id="3223f-141">Pour garantir les lectures et écritures locales, nous devons partitionner les données, non seulement sur la clé de partition de clé, mais également selon le modèle d’accès géographique dans les régions.</span><span class="sxs-lookup"><span data-stu-id="3223f-141">To guarantee local reads and writes, we must partition data not just on partition key, but also based on the geographical access pattern into regions.</span></span> <span data-ttu-id="3223f-142">Le modèle repose sur l’existence d’un compte de base de données Azure Cosmos DB géorépliqué pour chaque région.</span><span class="sxs-lookup"><span data-stu-id="3223f-142">The model relies on having a geo-replicated Azure Cosmos DB database account for each region.</span></span> <span data-ttu-id="3223f-143">Voici, par exemple, une configuration pour les écritures multirégions avec deux régions :</span><span class="sxs-lookup"><span data-stu-id="3223f-143">For example, with two regions, here's a setup for multi-region writes:</span></span>

| <span data-ttu-id="3223f-144">Nom du compte</span><span class="sxs-lookup"><span data-stu-id="3223f-144">Account Name</span></span> | <span data-ttu-id="3223f-145">Région d’écriture</span><span class="sxs-lookup"><span data-stu-id="3223f-145">Write Region</span></span> | <span data-ttu-id="3223f-146">Région de lecture</span><span class="sxs-lookup"><span data-stu-id="3223f-146">Read Region</span></span> |
| --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |

<span data-ttu-id="3223f-147">Le diagramme suivant montre comment les lectures et écritures sont effectuées dans une application standard avec cette configuration :</span><span class="sxs-lookup"><span data-stu-id="3223f-147">The following diagram shows how reads and writes are performed in a typical application with this setup:</span></span>

![Architecture à multiples maîtres Azure Cosmos DB](./media/multi-region-writers/multi-master.png)

<span data-ttu-id="3223f-149">Voici un extrait de code montrant comment initialiser les clients dans une couche d’accès aux données en cours d’exécution dans la région `West US`.</span><span class="sxs-lookup"><span data-stu-id="3223f-149">Here is a code snippet showing how to initialize the clients in a DAL running in the `West US` region.</span></span>
    
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

<span data-ttu-id="3223f-150">Avec la configuration précédente, la couche d’accès aux données peut transférer toutes les écritures vers le compte local basé selon l’emplacement où il est déployé.</span><span class="sxs-lookup"><span data-stu-id="3223f-150">With the preceding setup, the data access layer can forward all writes to the local account based on where it is deployed.</span></span> <span data-ttu-id="3223f-151">Les lectures sont effectuées depuis les deux comptes pour une vue globale des données.</span><span class="sxs-lookup"><span data-stu-id="3223f-151">Reads are performed by reading from both accounts to get the global view of data.</span></span> <span data-ttu-id="3223f-152">Cette approche peut être étendue à autant de régions que nécessaire.</span><span class="sxs-lookup"><span data-stu-id="3223f-152">This approach can be extended to as many regions as required.</span></span> <span data-ttu-id="3223f-153">Voici, par exemple, une configuration avec trois régions :</span><span class="sxs-lookup"><span data-stu-id="3223f-153">For example, here's a setup with three geographic regions:</span></span>

| <span data-ttu-id="3223f-154">Nom du compte</span><span class="sxs-lookup"><span data-stu-id="3223f-154">Account Name</span></span> | <span data-ttu-id="3223f-155">Région d’écriture</span><span class="sxs-lookup"><span data-stu-id="3223f-155">Write Region</span></span> | <span data-ttu-id="3223f-156">Région de lecture 1</span><span class="sxs-lookup"><span data-stu-id="3223f-156">Read Region 1</span></span> | <span data-ttu-id="3223f-157">Région de lecture 2</span><span class="sxs-lookup"><span data-stu-id="3223f-157">Read Region 2</span></span> |
| --- | --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |`Southeast Asia` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |`Southeast Asia` |
| `contentpubdatabase-asia.documents.azure.com` | `Southeast Asia` |`North Europe` |`West US` |

## <span data-ttu-id="3223f-158"><a id="DataAccessImplementation"></a>Mise en œuvre de la couche d’accès aux données</span><span class="sxs-lookup"><span data-stu-id="3223f-158"><a id="DataAccessImplementation"></a>Data access layer implementation</span></span>
<span data-ttu-id="3223f-159">Maintenant, examinons la mise en œuvre de la couche d’accès aux données pour une application avec deux régions en écriture.</span><span class="sxs-lookup"><span data-stu-id="3223f-159">Now let's look at the implementation of the data access layer (DAL) for an application with two writable regions.</span></span> <span data-ttu-id="3223f-160">La couche d’accès aux données doit mettre en œuvre les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="3223f-160">The DAL must implement the following steps:</span></span>

* <span data-ttu-id="3223f-161">Créer plusieurs instances de `DocumentClient` pour chaque compte.</span><span class="sxs-lookup"><span data-stu-id="3223f-161">Create multiple instances of `DocumentClient` for each account.</span></span> <span data-ttu-id="3223f-162">Avec deux régions, chaque instance de la couche d’accès aux données possède un `writeClient` et `readClient`.</span><span class="sxs-lookup"><span data-stu-id="3223f-162">With two regions, each DAL instance has one `writeClient` and one `readClient`.</span></span> 
* <span data-ttu-id="3223f-163">En fonction de la région déployée de l’application, configurez des points de terminaison pour `writeclient` et `readClient`.</span><span class="sxs-lookup"><span data-stu-id="3223f-163">Based on the deployed region of the application, configure the endpoints for `writeclient` and `readClient`.</span></span> <span data-ttu-id="3223f-164">Par exemple, la couche d’accès aux données déployée dans `West US` utilise `contentpubdatabase-usa.documents.azure.com` pour effectuer des écritures.</span><span class="sxs-lookup"><span data-stu-id="3223f-164">For example, the DAL deployed in `West US` uses `contentpubdatabase-usa.documents.azure.com` for performing writes.</span></span> <span data-ttu-id="3223f-165">La couche DAL déployée dans `NorthEurope` utilise `contentpubdatabase-europ.documents.azure.com` pour les écritures.</span><span class="sxs-lookup"><span data-stu-id="3223f-165">The DAL deployed in `NorthEurope` uses `contentpubdatabase-europ.documents.azure.com` for writes.</span></span>

<span data-ttu-id="3223f-166">Avec la configuration précédente, les méthodes d’accès aux données peuvent être mises en œuvre.</span><span class="sxs-lookup"><span data-stu-id="3223f-166">With the preceding setup, the data access methods can be implemented.</span></span> <span data-ttu-id="3223f-167">Les opérations d’écriture transfèrent l’écriture au `writeClient` correspondant.</span><span class="sxs-lookup"><span data-stu-id="3223f-167">Write operations forward the write to the corresponding `writeClient`.</span></span>

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

<span data-ttu-id="3223f-168">Pour lire les notifications et les avis, vous devez lire à partir des régions et associer les résultats comme indiqué dans l’extrait suivant :</span><span class="sxs-lookup"><span data-stu-id="3223f-168">For reading notifications and reviews, you must read from both regions and union the results as shown in the following snippet:</span></span>

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

<span data-ttu-id="3223f-169">Par conséquent, en choisissant une bonne clé de partitionnement et le partitionnement statique basé sur les comptes, vous pouvez effectuer des lectures et écritures locales multirégions à l’aide d’Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3223f-169">Thus, by choosing a good partitioning key and static account-based partitioning, you can achieve multi-region local writes and reads using Azure Cosmos DB.</span></span>

## <span data-ttu-id="3223f-170"><a id="NextSteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3223f-170"><a id="NextSteps"></a>Next steps</span></span>
<span data-ttu-id="3223f-171">Dans cet article, nous avons décrit comment vous pouvez utiliser des modèles lecture/écriture multirégions mondialement distribués avec Azure Cosmos DB à l’aide de la publication de contenu comme exemple de scénario.</span><span class="sxs-lookup"><span data-stu-id="3223f-171">In this article, we described how you can use globally distributed multi-region read write patterns with Azure Cosmos DB using content publishing as a sample scenario.</span></span>

* <span data-ttu-id="3223f-172">Découvrez-en plus sur la manière dont Azure Cosmos DB prend en charge la [distribution mondiale](distribute-data-globally.md)</span><span class="sxs-lookup"><span data-stu-id="3223f-172">Learn about how Azure Cosmos DB supports [global distribution](distribute-data-globally.md)</span></span>
* <span data-ttu-id="3223f-173">En savoir plus sur les [basculements manuels et automatiques dans Azure Cosmos DB](regional-failover.md)</span><span class="sxs-lookup"><span data-stu-id="3223f-173">Learn about [automatic and manual failovers in Azure Cosmos DB](regional-failover.md)</span></span>
* <span data-ttu-id="3223f-174">Découvrez-en plus sur [la cohérence globale avec Azure Cosmos DB](consistency-levels.md)</span><span class="sxs-lookup"><span data-stu-id="3223f-174">Learn about [global consistency with Azure Cosmos DB](consistency-levels.md)</span></span>
* <span data-ttu-id="3223f-175">Développer en mode multirégions à l’aide de l’[API DocumentDB - Azure Cosmos DB](tutorial-global-distribution-documentdb.md)</span><span class="sxs-lookup"><span data-stu-id="3223f-175">Develop with multiple regions using the [Azure Cosmos DB - DocumentDB API](tutorial-global-distribution-documentdb.md)</span></span>
* <span data-ttu-id="3223f-176">Développer en mode multirégions à l’aide de l’[API MongoDB - Azure Cosmos DB](tutorial-global-distribution-MongoDB.md)</span><span class="sxs-lookup"><span data-stu-id="3223f-176">Develop with multiple regions using the [Azure Cosmos DB - MongoDB API](tutorial-global-distribution-MongoDB.md)</span></span>
* <span data-ttu-id="3223f-177">Développer en mode multirégions à l’aide de l’[API Table - Azure Cosmos DB](tutorial-global-distribution-table.md)</span><span class="sxs-lookup"><span data-stu-id="3223f-177">Develop with multiple regions using the [Azure Cosmos DB - Table API](tutorial-global-distribution-table.md)</span></span>
