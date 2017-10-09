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
# <a name="multi-master-globally-replicated-database-architectures-with-azure-cosmos-db"></a><span data-ttu-id="83359-103">Architectures de base de données à multiples maîtres répliquées de façon globale avec Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="83359-103">Multi-master globally replicated database architectures with Azure Cosmos DB</span></span>
<span data-ttu-id="83359-104">Base de données Azure Cosmos prend en charge les clés en main [réplication globale](distribute-data-globally.md), qui vous permet de toodistribute données toomultiple régions à faible latence n’importe où dans la charge de travail hello.</span><span class="sxs-lookup"><span data-stu-id="83359-104">Azure Cosmos DB supports turnkey [global replication](distribute-data-globally.md), which allows you toodistribute data toomultiple regions with low latency access anywhere in hello workload.</span></span> <span data-ttu-id="83359-105">Ce modèle est généralement utilisé pour les charges de travail éditeur/consommateur, où un enregistreur existe dans une région géographique unique et des lecteurs sont distribués mondialement dans d’autres régions (lecture).</span><span class="sxs-lookup"><span data-stu-id="83359-105">This model is commonly used for publisher/consumer workloads where there is a writer in a single geographic region and globally distributed readers in other (read) regions.</span></span> 

<span data-ttu-id="83359-106">Vous pouvez également utiliser Azure Cosmos DB global de réplication prennent toobuild des applications dans lesquelles les enregistreurs et lecteurs sont globalement distribuées.</span><span class="sxs-lookup"><span data-stu-id="83359-106">You can also use Azure Cosmos DB's global replication support toobuild applications in which writers and readers are globally distributed.</span></span> <span data-ttu-id="83359-107">Ce document décrit un modèle qui permet d’obtenir un accès en écriture locale et en lecture locale pour les enregistreurs utilisant Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="83359-107">This document outlines a pattern that enables achieving local write and local read access for distributed writers using Azure Cosmos DB.</span></span>

## <span data-ttu-id="83359-108"><a id="ExampleScenario"></a>Publication de contenu : un exemple de scénario</span><span class="sxs-lookup"><span data-stu-id="83359-108"><a id="ExampleScenario"></a>Content Publishing - an example scenario</span></span>
<span data-ttu-id="83359-109">Examinons un toodescribe de scénario réel comment vous pouvez utiliser les modèles distribués internationalement multiples region/multi-cluster master lecture/écriture avec la base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="83359-109">Let's look at a real world scenario toodescribe how you can use globally distributed multi-region/multi-master read write patterns with Azure Cosmos DB.</span></span> <span data-ttu-id="83359-110">Prenons l’exemple d’une plateforme de contenu reposant sur Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="83359-110">Consider a content publishing platform built on Azure Cosmos DB.</span></span> <span data-ttu-id="83359-111">Voici certaines exigences que cette plateforme doit respecter pour une expérience utilisateur exceptionnelle pour les éditeurs et les consommateurs.</span><span class="sxs-lookup"><span data-stu-id="83359-111">Here are some requirements that this platform must meet for a great user experience for both publishers and consumers.</span></span>

* <span data-ttu-id="83359-112">Les auteurs et les abonnés sont répartis sur Bonjour</span><span class="sxs-lookup"><span data-stu-id="83359-112">Both authors and subscribers are spread over hello world</span></span> 
* <span data-ttu-id="83359-113">Les auteurs doivent publier région (le plus proche) locale articles tootheir (écriture)</span><span class="sxs-lookup"><span data-stu-id="83359-113">Authors must publish (write) articles tootheir local (closest) region</span></span>
* <span data-ttu-id="83359-114">Les auteurs des lecteurs/abonnés de leurs articles qui sont distribuées monde hello.</span><span class="sxs-lookup"><span data-stu-id="83359-114">Authors have readers/subscribers of their articles who are distributed across hello globe.</span></span> 
* <span data-ttu-id="83359-115">Les abonnés doivent recevoir une notification lorsque de nouveaux articles sont publiés.</span><span class="sxs-lookup"><span data-stu-id="83359-115">Subscribers should get a notification when new articles are published.</span></span>
* <span data-ttu-id="83359-116">Les abonnés doivent être en mesure de tooread des articles à partir de leur région.</span><span class="sxs-lookup"><span data-stu-id="83359-116">Subscribers must be able tooread articles from their local region.</span></span> <span data-ttu-id="83359-117">Ils doivent aussi être en mesure de tooadd révisions toothese articles.</span><span class="sxs-lookup"><span data-stu-id="83359-117">They should also be able tooadd reviews toothese articles.</span></span> 
* <span data-ttu-id="83359-118">Toute personne notamment auteur hello d’articles de hello doit être en mesure de visualiser que toutes les hello révisions de tooarticles attaché à partir d’une région.</span><span class="sxs-lookup"><span data-stu-id="83359-118">Anyone including hello author of hello articles should be able view all hello reviews attached tooarticles from a local region.</span></span> 

<span data-ttu-id="83359-119">En supposant que des millions d’utilisateurs et les éditeurs avec des milliards d’articles, dès que nous avons des problèmes de hello tooconfront de mise à l’échelle en même temps que ce qui garantit la localité d’accès.</span><span class="sxs-lookup"><span data-stu-id="83359-119">Assuming millions of consumers and publishers with billions of articles, soon we have tooconfront hello problems of scale along with guaranteeing locality of access.</span></span> <span data-ttu-id="83359-120">Comme avec la plupart des problèmes d’évolutivité, la solution de hello se trouve dans une stratégie de partitionnement efficace.</span><span class="sxs-lookup"><span data-stu-id="83359-120">As with most scalability problems, hello solution lies in a good partitioning strategy.</span></span> <span data-ttu-id="83359-121">Ensuite, nous allons examiner comment toomodel articles, révision et des notifications sous forme de documents, configurent des comptes de la base de données Azure Cosmos et implémenter une couche d’accès aux données.</span><span class="sxs-lookup"><span data-stu-id="83359-121">Next, let's look at how toomodel articles, review, and notifications as documents, configure Azure Cosmos DB accounts, and implement a data access layer.</span></span> 

<span data-ttu-id="83359-122">Si vous souhaitez que toolearn plus d’informations sur les clés de partition et de partitionnement, consultez [le partitionnement et la mise à l’échelle dans la base de données Azure Cosmos](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="83359-122">If you would like toolearn more about partitioning and partition keys, see [Partitioning and Scaling in Azure Cosmos DB](partition-data.md).</span></span>

## <span data-ttu-id="83359-123"><a id="ModelingNotifications"></a>Modélisation des notifications</span><span class="sxs-lookup"><span data-stu-id="83359-123"><a id="ModelingNotifications"></a>Modeling notifications</span></span>
<span data-ttu-id="83359-124">Les notifications sont utilisateur tooa spécifique du flux de données.</span><span class="sxs-lookup"><span data-stu-id="83359-124">Notifications are data feeds specific tooa user.</span></span> <span data-ttu-id="83359-125">Par conséquent, les modèles d’accès hello pour les documents de notifications sont toujours dans le contexte de hello d’utilisateur unique.</span><span class="sxs-lookup"><span data-stu-id="83359-125">Therefore, hello access patterns for notifications documents are always in hello context of single user.</span></span> <span data-ttu-id="83359-126">Par exemple, vous serez « post utilisateur tooa notification » ou « extraire toutes les notifications pour un utilisateur donné ».</span><span class="sxs-lookup"><span data-stu-id="83359-126">For example, you would "post a notification tooa user" or "fetch all notifications for a given user".</span></span> <span data-ttu-id="83359-127">Par conséquent, hello meilleur choix de clé de partitionnement pour ce type n’est `UserId`.</span><span class="sxs-lookup"><span data-stu-id="83359-127">So, hello optimal choice of partitioning key for this type would be `UserId`.</span></span>

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

## <span data-ttu-id="83359-128"><a id="ModelingSubscriptions"></a>Modélisation des abonnements</span><span class="sxs-lookup"><span data-stu-id="83359-128"><a id="ModelingSubscriptions"></a>Modeling subscriptions</span></span>
<span data-ttu-id="83359-129">Les abonnements peuvent être créés selon différents critères comme une catégorie spécifique d’articles d’intérêt ou un éditeur spécifique.</span><span class="sxs-lookup"><span data-stu-id="83359-129">Subscriptions can be created for various criteria like a specific category of articles of interest, or a specific publisher.</span></span> <span data-ttu-id="83359-130">Par conséquent, hello `SubscriptionFilter` est un bon choix pour la clé de partition.</span><span class="sxs-lookup"><span data-stu-id="83359-130">Hence hello `SubscriptionFilter` is a good choice for partition key.</span></span>

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

## <span data-ttu-id="83359-131"><a id="ModelingArticles"></a>Modélisation des articles</span><span class="sxs-lookup"><span data-stu-id="83359-131"><a id="ModelingArticles"></a>Modeling articles</span></span>
<span data-ttu-id="83359-132">Une fois qu’un article est identifié par le biais des notifications, les requêtes suivantes sont généralement basés sur hello `Article.Id`.</span><span class="sxs-lookup"><span data-stu-id="83359-132">Once an article is identified through notifications, subsequent queries are typically based on hello `Article.Id`.</span></span> <span data-ttu-id="83359-133">En choisissant `Article.Id` en tant que partition clé de hello fournit ainsi la distribution de meilleures hello pour le stockage des articles à l’intérieur d’une collection de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="83359-133">Choosing `Article.Id` as partition hello key thus provides hello best distribution for storing articles inside an Azure Cosmos DB collection.</span></span> 

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

## <span data-ttu-id="83359-134"><a id="ModelingReviews"></a>Modélisation des avis</span><span class="sxs-lookup"><span data-stu-id="83359-134"><a id="ModelingReviews"></a>Modeling reviews</span></span>
<span data-ttu-id="83359-135">Comme des articles, révisions sont principalement écrites et lues dans le contexte de hello d’article.</span><span class="sxs-lookup"><span data-stu-id="83359-135">Like articles, reviews are mostly written and read in hello context of article.</span></span> <span data-ttu-id="83359-136">Choisir `ArticleId` en tant que clé de partition fournit une meilleure distribution et un accès efficace aux avis associés à l’article.</span><span class="sxs-lookup"><span data-stu-id="83359-136">Choosing `ArticleId` as a partition key provides best distribution and efficient access of reviews associated with article.</span></span> 

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

## <span data-ttu-id="83359-137"><a id="DataAccessMethods"></a>Méthodes de couche d’accès aux données</span><span class="sxs-lookup"><span data-stu-id="83359-137"><a id="DataAccessMethods"></a>Data access layer methods</span></span>
<span data-ttu-id="83359-138">Maintenant examinons les données principales hello nous devons tooimplement méthodes d’accès.</span><span class="sxs-lookup"><span data-stu-id="83359-138">Now let's look at hello main data access methods we need tooimplement.</span></span> <span data-ttu-id="83359-139">Voici la liste hello des méthodes hello `ContentPublishDatabase` doit :</span><span class="sxs-lookup"><span data-stu-id="83359-139">Here's hello list of methods that hello `ContentPublishDatabase` needs:</span></span>

    class ContentPublishDatabase 
    { 
        public async Task CreateSubscriptionAsync(string userId, string category);
    
        public async Task<IEnumerable<Notification>> ReadNotificationFeedAsync(string userId);
    
        public async Task<Article> ReadArticleAsync(string articleId);
    
        public async Task WriteReviewAsync(string articleId, string userId, string reviewText, int rating);
    
        public async Task<IEnumerable<Review>> ReadReviewsAsync(string articleId); 
    }

## <span data-ttu-id="83359-140"><a id="Architecture"></a>Configuration du compte Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="83359-140"><a id="Architecture"></a>Azure Cosmos DB account configuration</span></span>
<span data-ttu-id="83359-141">tooguarantee local lit et écrit, nous devez partitionner les données non seulement sur la clé de partition, mais également basé sur le modèle d’accès géographiques hello en régions.</span><span class="sxs-lookup"><span data-stu-id="83359-141">tooguarantee local reads and writes, we must partition data not just on partition key, but also based on hello geographical access pattern into regions.</span></span> <span data-ttu-id="83359-142">modèle de Hello s’appuie sur la présence d’un compte de base de données de base de données Azure Cosmos de géo-répliquées pour chaque région.</span><span class="sxs-lookup"><span data-stu-id="83359-142">hello model relies on having a geo-replicated Azure Cosmos DB database account for each region.</span></span> <span data-ttu-id="83359-143">Voici, par exemple, une configuration pour les écritures multirégions avec deux régions :</span><span class="sxs-lookup"><span data-stu-id="83359-143">For example, with two regions, here's a setup for multi-region writes:</span></span>

| <span data-ttu-id="83359-144">Nom du compte</span><span class="sxs-lookup"><span data-stu-id="83359-144">Account Name</span></span> | <span data-ttu-id="83359-145">Région d’écriture</span><span class="sxs-lookup"><span data-stu-id="83359-145">Write Region</span></span> | <span data-ttu-id="83359-146">Région de lecture</span><span class="sxs-lookup"><span data-stu-id="83359-146">Read Region</span></span> |
| --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |

<span data-ttu-id="83359-147">Hello diagramme suivant montre comment les lectures et écritures sont effectuées dans une application classique avec ce programme d’installation :</span><span class="sxs-lookup"><span data-stu-id="83359-147">hello following diagram shows how reads and writes are performed in a typical application with this setup:</span></span>

![Architecture à multiples maîtres Azure Cosmos DB](./media/multi-region-writers/multi-master.png)

<span data-ttu-id="83359-149">Voici un extrait de code montrant comment tooinitialize hello clients dans la couche DAL en cours d’exécution dans hello `West US` région.</span><span class="sxs-lookup"><span data-stu-id="83359-149">Here is a code snippet showing how tooinitialize hello clients in a DAL running in hello `West US` region.</span></span>
    
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

<span data-ttu-id="83359-150">Avec hello précédant le programme d’installation, couche d’accès aux données hello peut transférer toutes les écritures toohello compte local basé sur lesquels il est déployé.</span><span class="sxs-lookup"><span data-stu-id="83359-150">With hello preceding setup, hello data access layer can forward all writes toohello local account based on where it is deployed.</span></span> <span data-ttu-id="83359-151">Les lectures sont effectuées par la lecture à partir de ces deux vue comptes tooget hello globale de données.</span><span class="sxs-lookup"><span data-stu-id="83359-151">Reads are performed by reading from both accounts tooget hello global view of data.</span></span> <span data-ttu-id="83359-152">Cette approche peut être étendu tooas plusieurs régions, en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="83359-152">This approach can be extended tooas many regions as required.</span></span> <span data-ttu-id="83359-153">Voici, par exemple, une configuration avec trois régions :</span><span class="sxs-lookup"><span data-stu-id="83359-153">For example, here's a setup with three geographic regions:</span></span>

| <span data-ttu-id="83359-154">Nom du compte</span><span class="sxs-lookup"><span data-stu-id="83359-154">Account Name</span></span> | <span data-ttu-id="83359-155">Région d’écriture</span><span class="sxs-lookup"><span data-stu-id="83359-155">Write Region</span></span> | <span data-ttu-id="83359-156">Région de lecture 1</span><span class="sxs-lookup"><span data-stu-id="83359-156">Read Region 1</span></span> | <span data-ttu-id="83359-157">Région de lecture 2</span><span class="sxs-lookup"><span data-stu-id="83359-157">Read Region 2</span></span> |
| --- | --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |`Southeast Asia` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |`Southeast Asia` |
| `contentpubdatabase-asia.documents.azure.com` | `Southeast Asia` |`North Europe` |`West US` |

## <span data-ttu-id="83359-158"><a id="DataAccessImplementation"></a>Mise en œuvre de la couche d’accès aux données</span><span class="sxs-lookup"><span data-stu-id="83359-158"><a id="DataAccessImplementation"></a>Data access layer implementation</span></span>
<span data-ttu-id="83359-159">Maintenant examinons implémentation hello de hello couche d’accès aux données (DAL) pour une application avec les deux régions accessible en écriture.</span><span class="sxs-lookup"><span data-stu-id="83359-159">Now let's look at hello implementation of hello data access layer (DAL) for an application with two writable regions.</span></span> <span data-ttu-id="83359-160">Hello DAL doit implémenter hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="83359-160">hello DAL must implement hello following steps:</span></span>

* <span data-ttu-id="83359-161">Créer plusieurs instances de `DocumentClient` pour chaque compte.</span><span class="sxs-lookup"><span data-stu-id="83359-161">Create multiple instances of `DocumentClient` for each account.</span></span> <span data-ttu-id="83359-162">Avec deux régions, chaque instance de la couche d’accès aux données possède un `writeClient` et `readClient`.</span><span class="sxs-lookup"><span data-stu-id="83359-162">With two regions, each DAL instance has one `writeClient` and one `readClient`.</span></span> 
* <span data-ttu-id="83359-163">En fonction de la région de hello déployée de l’application hello, configurer des points de terminaison hello pour `writeclient` et `readClient`.</span><span class="sxs-lookup"><span data-stu-id="83359-163">Based on hello deployed region of hello application, configure hello endpoints for `writeclient` and `readClient`.</span></span> <span data-ttu-id="83359-164">Par exemple, hello DAL déployée dans `West US` utilise `contentpubdatabase-usa.documents.azure.com` pour effectuer des écritures.</span><span class="sxs-lookup"><span data-stu-id="83359-164">For example, hello DAL deployed in `West US` uses `contentpubdatabase-usa.documents.azure.com` for performing writes.</span></span> <span data-ttu-id="83359-165">Hello DAL déployé dans `NorthEurope` utilise `contentpubdatabase-europ.documents.azure.com` pour les écritures.</span><span class="sxs-lookup"><span data-stu-id="83359-165">hello DAL deployed in `NorthEurope` uses `contentpubdatabase-europ.documents.azure.com` for writes.</span></span>

<span data-ttu-id="83359-166">Avec hello précédant le programme d’installation, les méthodes d’accès données hello peuvent être implémentés.</span><span class="sxs-lookup"><span data-stu-id="83359-166">With hello preceding setup, hello data access methods can be implemented.</span></span> <span data-ttu-id="83359-167">Écrire des opérations transférer hello écriture toohello correspondant `writeClient`.</span><span class="sxs-lookup"><span data-stu-id="83359-167">Write operations forward hello write toohello corresponding `writeClient`.</span></span>

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

<span data-ttu-id="83359-168">Pour lire les notifications et les analyses, vous devez lire les régions et les résultats de l’union hello comme indiqué dans hello suivant extrait :</span><span class="sxs-lookup"><span data-stu-id="83359-168">For reading notifications and reviews, you must read from both regions and union hello results as shown in hello following snippet:</span></span>

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

<span data-ttu-id="83359-169">Par conséquent, en choisissant une bonne clé de partitionnement et le partitionnement statique basé sur les comptes, vous pouvez effectuer des lectures et écritures locales multirégions à l’aide d’Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="83359-169">Thus, by choosing a good partitioning key and static account-based partitioning, you can achieve multi-region local writes and reads using Azure Cosmos DB.</span></span>

## <span data-ttu-id="83359-170"><a id="NextSteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="83359-170"><a id="NextSteps"></a>Next steps</span></span>
<span data-ttu-id="83359-171">Dans cet article, nous avons décrit comment vous pouvez utiliser des modèles lecture/écriture multirégions mondialement distribués avec Azure Cosmos DB à l’aide de la publication de contenu comme exemple de scénario.</span><span class="sxs-lookup"><span data-stu-id="83359-171">In this article, we described how you can use globally distributed multi-region read write patterns with Azure Cosmos DB using content publishing as a sample scenario.</span></span>

* <span data-ttu-id="83359-172">Découvrez-en plus sur la manière dont Azure Cosmos DB prend en charge la [distribution mondiale](distribute-data-globally.md)</span><span class="sxs-lookup"><span data-stu-id="83359-172">Learn about how Azure Cosmos DB supports [global distribution](distribute-data-globally.md)</span></span>
* <span data-ttu-id="83359-173">En savoir plus sur les [basculements manuels et automatiques dans Azure Cosmos DB](regional-failover.md)</span><span class="sxs-lookup"><span data-stu-id="83359-173">Learn about [automatic and manual failovers in Azure Cosmos DB](regional-failover.md)</span></span>
* <span data-ttu-id="83359-174">Découvrez-en plus sur [la cohérence globale avec Azure Cosmos DB](consistency-levels.md)</span><span class="sxs-lookup"><span data-stu-id="83359-174">Learn about [global consistency with Azure Cosmos DB](consistency-levels.md)</span></span>
* <span data-ttu-id="83359-175">Développer avec plusieurs régions à l’aide de hello [Azure Cosmos DB - API DocumentDB](tutorial-global-distribution-documentdb.md)</span><span class="sxs-lookup"><span data-stu-id="83359-175">Develop with multiple regions using hello [Azure Cosmos DB - DocumentDB API](tutorial-global-distribution-documentdb.md)</span></span>
* <span data-ttu-id="83359-176">Développer avec plusieurs régions à l’aide de hello [Azure Cosmos DB - MongoDB API](tutorial-global-distribution-MongoDB.md)</span><span class="sxs-lookup"><span data-stu-id="83359-176">Develop with multiple regions using hello [Azure Cosmos DB - MongoDB API](tutorial-global-distribution-MongoDB.md)</span></span>
* <span data-ttu-id="83359-177">Développer avec plusieurs régions à l’aide de hello [Azure Cosmos DB - API de Table](tutorial-global-distribution-table.md)</span><span class="sxs-lookup"><span data-stu-id="83359-177">Develop with multiple regions using hello [Azure Cosmos DB - Table API](tutorial-global-distribution-table.md)</span></span>
