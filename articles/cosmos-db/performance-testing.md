---
title: "aaaAzure Cosmos DB échelle et les tests de performances | Documents Microsoft"
description: "Découvrez comment tooperform l’échelle et test des performances avec la base de données Azure Cosmos"
keywords: Tester les performances
services: cosmos-db
author: arramac
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: f4c96ebd-f53c-427d-a500-3f28fe7b11d0
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: arramac
ms.openlocfilehash: 46d1217e11a39ee970a868de9a5c5dfcf52cedf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-and-scale-testing-with-azure-cosmos-db"></a><span data-ttu-id="12138-104">Test des performances et de la mise à l’échelle avec Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="12138-104">Performance and scale testing with Azure Cosmos DB</span></span>
<span data-ttu-id="12138-105">Le test des performances et de la mise à l’échelle est une étape essentielle du développement d’applications.</span><span class="sxs-lookup"><span data-stu-id="12138-105">Performance and scale testing is a key step in application development.</span></span> <span data-ttu-id="12138-106">Pour de nombreuses applications, couche de base de données hello a un impact significatif hello les performances globales et l’évolutivité, et est par conséquent, un composant essentiel de performances de test.</span><span class="sxs-lookup"><span data-stu-id="12138-106">For many applications, hello database tier has a significant impact on hello overall performance and scalability, and is therefore a critical component of performance testing.</span></span> <span data-ttu-id="12138-107">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) a été spécialement conçu pour une mise à l’échelle élastique et des performances prévisibles et, par conséquent, convient parfaitement aux applications nécessitant un niveau de base de données hautes performances.</span><span class="sxs-lookup"><span data-stu-id="12138-107">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is purpose-built for elastic scale and predictable performance, and therefore a great fit for applications that need a high-performance database tier.</span></span> 

<span data-ttu-id="12138-108">Cet article est une référence pour les développeurs implémentant des suites de tests de performances pour leurs charges de travail Cosmos DB ou évaluant Cosmos DB pour des scénarios d’applications hautes performances.</span><span class="sxs-lookup"><span data-stu-id="12138-108">This article is a reference for developers implementing performance test suites for their Cosmos DB workloads, or evaluating Cosmos DB for high-performance application scenarios.</span></span> <span data-ttu-id="12138-109">Il se concentre essentiellement sur les tests de performances isolé de base de données hello, mais il inclut également les meilleures pratiques pour les applications de production.</span><span class="sxs-lookup"><span data-stu-id="12138-109">It focuses primarily on isolated performance testing of hello database, but also includes best practices for production applications.</span></span>

<span data-ttu-id="12138-110">Après avoir lu cet article, vous serez hello en mesure de tooanswer suivant questions :</span><span class="sxs-lookup"><span data-stu-id="12138-110">After reading this article, you will be able tooanswer hello following questions:</span></span>   

* <span data-ttu-id="12138-111">Où puis-je trouver un exemple d’application cliente .NET pour le test des performances de Cosmos DB ?</span><span class="sxs-lookup"><span data-stu-id="12138-111">Where can I find a sample .NET client application for performance testing of Cosmos DB?</span></span> 
* <span data-ttu-id="12138-112">Comment atteindre des niveaux de débit élevés avec Cosmos DB à partir de mon application cliente ?</span><span class="sxs-lookup"><span data-stu-id="12138-112">How do I achieve high throughput levels with Cosmos DB from my client application?</span></span>

<span data-ttu-id="12138-113">tooget a démarré avec le code, téléchargez projet à partir de hello [exemple de test de Performance Azure Cosmos DB](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark).</span><span class="sxs-lookup"><span data-stu-id="12138-113">tooget started with code, please download hello project from [Azure Cosmos DB Performance Testing Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark).</span></span> 

> [!NOTE]
> <span data-ttu-id="12138-114">Hello cette application vise toodemonstrate meilleures pratiques pour l’extraction de meilleures performances en dehors de la base de données Cosmos avec un petit nombre d’ordinateurs clients.</span><span class="sxs-lookup"><span data-stu-id="12138-114">hello goal of this application is toodemonstrate best practices for extracting better performance out of Cosmos DB with a small number of client machines.</span></span> <span data-ttu-id="12138-115">Cela a été pas de capacité de pointe hello toodemonstrate du service de hello, qui peut mettre à l’échelle limitlessly.</span><span class="sxs-lookup"><span data-stu-id="12138-115">This was not made toodemonstrate hello peak capacity of hello service, which can scale limitlessly.</span></span>
> 
> 

<span data-ttu-id="12138-116">Si vous recherchez des options de configuration côté client tooimprove Cosmos DB performances, consultez [conseils relatifs aux performances de base de données Azure Cosmos](performance-tips.md).</span><span class="sxs-lookup"><span data-stu-id="12138-116">If you're looking for client-side configuration options tooimprove Cosmos DB performance, see [Azure Cosmos DB performance tips](performance-tips.md).</span></span>

## <a name="run-hello-performance-testing-application"></a><span data-ttu-id="12138-117">Exécuter l’application de test de performance de hello</span><span class="sxs-lookup"><span data-stu-id="12138-117">Run hello performance testing application</span></span>
<span data-ttu-id="12138-118">Hello tooget de manière plus rapide démarré est toocompile et exécution hello, exemple .NET ci-dessous, comme décrit dans les étapes de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="12138-118">hello quickest way tooget started is toocompile and run hello .NET sample below, as described in hello steps below.</span></span> <span data-ttu-id="12138-119">Vous pouvez également consulter le code source de hello et implémenter des applications client propre tooyour configurations similaires.</span><span class="sxs-lookup"><span data-stu-id="12138-119">You can also review hello source code and implement similar configurations tooyour own client applications.</span></span>

<span data-ttu-id="12138-120">**Étape 1 :** projet hello de téléchargement à partir de [exemple de test de Performance Azure Cosmos DB](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark), ou le référentiel GitHub branchement hello.</span><span class="sxs-lookup"><span data-stu-id="12138-120">**Step 1:** Download hello project from [Azure Cosmos DB Performance Testing Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark), or fork hello GitHub repository.</span></span>

<span data-ttu-id="12138-121">**Étape 2 :** modifier les paramètres de hello pour EndpointUrl, AuthorizationKey, CollectionThroughput et DocumentTemplate (facultatif) dans le fichier App.config.</span><span class="sxs-lookup"><span data-stu-id="12138-121">**Step 2:** Modify hello settings for EndpointUrl, AuthorizationKey, CollectionThroughput and DocumentTemplate (optional) in App.config.</span></span>

> [!NOTE]
> <span data-ttu-id="12138-122">Avant de configurer des regroupements avec un débit élevé, reportez-vous à toohello [Page de tarification](https://azure.microsoft.com/pricing/details/cosmos-db/) tooestimate les coûts de hello par collection.</span><span class="sxs-lookup"><span data-stu-id="12138-122">Before provisioning collections with high throughput, please refer toohello [Pricing Page](https://azure.microsoft.com/pricing/details/cosmos-db/) tooestimate hello costs per collection.</span></span> <span data-ttu-id="12138-123">Base de données Azure Cosmos facture débit indépendamment de toutes les heures et de stockage afin de conserver les coûts en supprimant ou en diminuant le débit de vos collections de base de données Azure Cosmos hello après le test.</span><span class="sxs-lookup"><span data-stu-id="12138-123">Azure Cosmos DB bills storage and throughput independently on an hourly basis, so you can save costs by deleting or lowering hello throughput of your Azure Cosmos DB collections after testing.</span></span>
> 
> 

<span data-ttu-id="12138-124">**Étape 3 :** compiler et exécuter l’application de console hello à partir de la ligne de commande hello.</span><span class="sxs-lookup"><span data-stu-id="12138-124">**Step 3:** Compile and run hello console app from hello command line.</span></span> <span data-ttu-id="12138-125">Sortie hello suivante doit s’afficher :</span><span class="sxs-lookup"><span data-stu-id="12138-125">You should see output like hello following:</span></span>

    Summary:
    ---------------------------------------------------------------------
    Endpoint: https://docdb-scale-demo.documents.azure.com:443/
    Collection : db.testdata at 50000 request units per second
    Document Template*: Player.json
    Degree of parallelism*: 500
    ---------------------------------------------------------------------

    DocumentDBBenchmark starting...
    Creating database db
    Creating collection testdata
    Creating metric collection metrics
    Retrying after sleeping for 00:03:34.1720000
    Starting Inserts with 500 tasks
    Inserted 661 docs @ 656 writes/s, 6860 RU/s (18B max monthly 1KB reads)
    Inserted 6505 docs @ 2668 writes/s, 27962 RU/s (72B max monthly 1KB reads)
    Inserted 11756 docs @ 3240 writes/s, 33957 RU/s (88B max monthly 1KB reads)
    Inserted 17076 docs @ 3590 writes/s, 37627 RU/s (98B max monthly 1KB reads)
    Inserted 22106 docs @ 3748 writes/s, 39281 RU/s (102B max monthly 1KB reads)
    Inserted 28430 docs @ 3902 writes/s, 40897 RU/s (106B max monthly 1KB reads)
    Inserted 33492 docs @ 3928 writes/s, 41168 RU/s (107B max monthly 1KB reads)
    Inserted 38392 docs @ 3963 writes/s, 41528 RU/s (108B max monthly 1KB reads)
    Inserted 43371 docs @ 4012 writes/s, 42051 RU/s (109B max monthly 1KB reads)
    Inserted 48477 docs @ 4035 writes/s, 42282 RU/s (110B max monthly 1KB reads)
    Inserted 53845 docs @ 4088 writes/s, 42845 RU/s (111B max monthly 1KB reads)
    Inserted 59267 docs @ 4138 writes/s, 43364 RU/s (112B max monthly 1KB reads)
    Inserted 64703 docs @ 4197 writes/s, 43981 RU/s (114B max monthly 1KB reads)
    Inserted 70428 docs @ 4216 writes/s, 44181 RU/s (115B max monthly 1KB reads)
    Inserted 75868 docs @ 4247 writes/s, 44505 RU/s (115B max monthly 1KB reads)
    Inserted 81571 docs @ 4280 writes/s, 44852 RU/s (116B max monthly 1KB reads)
    Inserted 86271 docs @ 4273 writes/s, 44783 RU/s (116B max monthly 1KB reads)
    Inserted 91993 docs @ 4299 writes/s, 45056 RU/s (117B max monthly 1KB reads)
    Inserted 97469 docs @ 4292 writes/s, 44984 RU/s (117B max monthly 1KB reads)
    Inserted 99736 docs @ 4192 writes/s, 43930 RU/s (114B max monthly 1KB reads)
    Inserted 99997 docs @ 4013 writes/s, 42051 RU/s (109B max monthly 1KB reads)
    Inserted 100000 docs @ 3846 writes/s, 40304 RU/s (104B max monthly 1KB reads)

    Summary:
    ---------------------------------------------------------------------
    Inserted 100000 docs @ 3834 writes/s, 40180 RU/s (104B max monthly 1KB reads)
    ---------------------------------------------------------------------
    DocumentDBBenchmark completed successfully.


<span data-ttu-id="12138-126">**Étape 4 (si nécessaire) :** hello débit signalé (ur/s) à partir de l’outil de hello doit être hello identique ou supérieur à débit approvisionné de hello de collection de hello.</span><span class="sxs-lookup"><span data-stu-id="12138-126">**Step 4 (if necessary):** hello throughput reported (RU/s) from hello tool should be hello same or higher than hello provisioned throughput of hello collection.</span></span> <span data-ttu-id="12138-127">Si ce n’est pas le cas, croissant hello DegreeOfParallelism par petits incréments peut-être vous aider à atteindre la limite de hello.</span><span class="sxs-lookup"><span data-stu-id="12138-127">If not, increasing hello DegreeOfParallelism in small increments may help you reach hello limit.</span></span> <span data-ttu-id="12138-128">Si des plateaux débit hello à partir de votre application cliente, lancer plusieurs instances de l’application hello sur hello identiques ou différents ordinateurs vous aideront à atteindre la limite de hello configuré sur hello différentes instances.</span><span class="sxs-lookup"><span data-stu-id="12138-128">If hello throughput from your client app plateaus, launching multiple instances of hello app on hello same or different machines will help you reach hello provisioned limit across hello different instances.</span></span> <span data-ttu-id="12138-129">Si vous avez besoin d’aide pour cette étape, veuillez écrire un message électronique tooaskcosmosdb@microsoft.com ou le fichier d’un ticket de support à partir de hello [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="12138-129">If you need help with this step, please, write an email tooaskcosmosdb@microsoft.com or file a support ticket from hello [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="12138-130">Une fois que vous avez application hello en cours d’exécution, vous pouvez essayer différents [stratégies d’indexation](indexing-policies.md) et [niveaux de cohérence](consistency-levels.md) toounderstand leur impact sur le débit et la latence.</span><span class="sxs-lookup"><span data-stu-id="12138-130">Once you have hello app running, you can try different [Indexing policies](indexing-policies.md) and [Consistency levels](consistency-levels.md) toounderstand their impact on throughput and latency.</span></span> <span data-ttu-id="12138-131">Vous pouvez également consulter le code source de hello et implémenter similaire configurations tooyour propre des suites de tests ou les applications de production.</span><span class="sxs-lookup"><span data-stu-id="12138-131">You can also review hello source code and implement similar configurations tooyour own test suites or production applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="12138-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="12138-132">Next steps</span></span>
<span data-ttu-id="12138-133">Dans cet article, nous avons vu comment effectuer des tests de performances et d’évolutivité avec Cosmos DB à l’aide d’une application console .NET.</span><span class="sxs-lookup"><span data-stu-id="12138-133">In this article, we looked at how you can perform performance and scale testing with Cosmos DB using a .NET console app.</span></span> <span data-ttu-id="12138-134">Consultez les liens toohello ci-dessous pour plus d’informations sur l’utilisation de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="12138-134">Please refer toohello links below for additional information on working with Azure Cosmos DB.</span></span>

* [<span data-ttu-id="12138-135">Exemple de test des performances Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="12138-135">Azure Cosmos DB performance testing sample</span></span>](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark)
* [<span data-ttu-id="12138-136">Client configuration options tooimprove les performances de base de données Azure Cosmos</span><span class="sxs-lookup"><span data-stu-id="12138-136">Client configuration options tooimprove Azure Cosmos DB performance</span></span>](performance-tips.md)
* [<span data-ttu-id="12138-137">Guide de partitionnement et de mise à l’échelle dans Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="12138-137">Server-side partitioning in Azure Cosmos DB</span></span>](partition-data.md)


