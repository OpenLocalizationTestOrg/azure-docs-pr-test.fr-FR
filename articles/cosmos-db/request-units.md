---
title: "aaaRequest unités et estimer le débit - base de données Azure Cosmos | Documents Microsoft"
description: "Découvrez comment toounderstand, spécifiez et estimer les besoins d’unité de demande dans la base de données Azure Cosmos."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: d0a3c310-eb63-4e45-8122-b7724095c32f
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 13c4e7aeb6222fa14ef982e238716e15a0159fd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="request-units-in-azure-cosmos-db"></a><span data-ttu-id="4ab20-103">Unités de requête dans Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="4ab20-103">Request Units in Azure Cosmos DB</span></span>
<span data-ttu-id="4ab20-104">Désormais disponible : [calculatrice d’unités de requête](https://www.documentdb.com/capacityplanner) Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="4ab20-104">Now available: Azure Cosmos DB [request unit calculator](https://www.documentdb.com/capacityplanner).</span></span> <span data-ttu-id="4ab20-105">Pour en savoir plus, consultez [Estimation des besoins de débit](request-units.md#estimating-throughput-needs).</span><span class="sxs-lookup"><span data-stu-id="4ab20-105">Learn more in [Estimating your throughput needs](request-units.md#estimating-throughput-needs).</span></span>

![Calculatrice de débit][5]

## <a name="introduction"></a><span data-ttu-id="4ab20-107">Introduction</span><span class="sxs-lookup"><span data-stu-id="4ab20-107">Introduction</span></span>
<span data-ttu-id="4ab20-108">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) est un service de base de données multimodèle mondialement distribué de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4ab20-108">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is Microsoft's globally distributed multi-model database.</span></span> <span data-ttu-id="4ab20-109">Avec la base de données Azure Cosmos, vous n’avez toorent des machines virtuelles, déployer des logiciels ou surveiller les bases de données.</span><span class="sxs-lookup"><span data-stu-id="4ab20-109">With Azure Cosmos DB, you don't have toorent virtual machines, deploy software, or monitor databases.</span></span> <span data-ttu-id="4ab20-110">Azure Cosmos DB est traitée et en permanence contrôlé par Microsoft ingénieurs supérieur toodeliver world classe disponibilité, performances et protection des données.</span><span class="sxs-lookup"><span data-stu-id="4ab20-110">Azure Cosmos DB is operated and continuously monitored by Microsoft top engineers toodeliver world class availability, performance, and data protection.</span></span> <span data-ttu-id="4ab20-111">Vous pouvez accéder à vos données à l’aide des API de votre choix, sachant que les API [SQL DocumentDB](documentdb-sql-query.md) (document), MongoDB (document), [Stockage Table Azure](https://azure.microsoft.com/services/storage/tables/) (clé-valeur) et [Gremlin](https://tinkerpop.apache.org/gremlin.html) (graphique) sont toutes prises en charge de manière native.</span><span class="sxs-lookup"><span data-stu-id="4ab20-111">You can access your data using APIs of your choice, as [DocumentDB SQL](documentdb-sql-query.md) (document), MongoDB (document), [Azure Table Storage](https://azure.microsoft.com/services/storage/tables/) (key-value), and [Gremlin](https://tinkerpop.apache.org/gremlin.html) (graph) are all natively supported.</span></span> <span data-ttu-id="4ab20-112">Hello la devise de base de données Azure Cosmos est hello unité demande (RU).</span><span class="sxs-lookup"><span data-stu-id="4ab20-112">hello currency of Azure Cosmos DB is hello Request Unit (RU).</span></span> <span data-ttu-id="4ab20-113">Avec RUs, vous n’avez pas besoin de capacités de lecture/écriture tooreserve ou de disposition du processeur, mémoire et e/s.</span><span class="sxs-lookup"><span data-stu-id="4ab20-113">With RUs, you do not need tooreserve read/write capacities or provision CPU, Memory and IOPS.</span></span>

<span data-ttu-id="4ab20-114">Azure Cosmos DB prend en charge un certain nombre d’API avec différentes opérations allant de simples lit et écrit toocomplex les requêtes de graphique.</span><span class="sxs-lookup"><span data-stu-id="4ab20-114">Azure Cosmos DB supports a number of APIs with different operations ranging from simple reads and writes toocomplex graph queries.</span></span> <span data-ttu-id="4ab20-115">Pas toutes les demandes étant égales, ils sont attribués à une quantité normalisée de **unités de requête** selon la quantité hello de demande de calcul requis tooserve hello.</span><span class="sxs-lookup"><span data-stu-id="4ab20-115">Since not all requests are equal, they are assigned a normalized quantity of **request units** based on hello amount of computation required tooserve hello request.</span></span> <span data-ttu-id="4ab20-116">nombre de Hello d’unités de demande pour une opération est déterministe, et vous pouvez suivre le nombre de hello d’unités de demande consommé par aucune opération dans la base de données Azure Cosmos via un en-tête de réponse.</span><span class="sxs-lookup"><span data-stu-id="4ab20-116">hello number of request units for an operation is deterministic, and you can track hello number of request units consumed by any operation in Azure Cosmos DB via a response header.</span></span> 

<span data-ttu-id="4ab20-117">tooprovide des performances prévisibles, vous devez débit tooreserve en unités de 100 ur/seconde.</span><span class="sxs-lookup"><span data-stu-id="4ab20-117">tooprovide predictable performance, you need tooreserve throughput in units of 100 RU/second.</span></span> 

<span data-ttu-id="4ab20-118">Après avoir lu cet article, vous serez hello en mesure de tooanswer suivant questions :</span><span class="sxs-lookup"><span data-stu-id="4ab20-118">After reading this article, you'll be able tooanswer hello following questions:</span></span>  

* <span data-ttu-id="4ab20-119">Que sont les unités de requête et les frais de requête ?</span><span class="sxs-lookup"><span data-stu-id="4ab20-119">What are request units and request charges?</span></span>
* <span data-ttu-id="4ab20-120">Comment spécifier la capacité d’unités de requête pour une collection ?</span><span class="sxs-lookup"><span data-stu-id="4ab20-120">How do I specify request unit capacity for a collection?</span></span>
* <span data-ttu-id="4ab20-121">Comment estimer les besoins en unités de requête de mon application ?</span><span class="sxs-lookup"><span data-stu-id="4ab20-121">How do I estimate my application's request unit needs?</span></span>
* <span data-ttu-id="4ab20-122">Que se passe-t-il si je dépasse la capacité d’unités de requête pour une collection ?</span><span class="sxs-lookup"><span data-stu-id="4ab20-122">What happens if I exceed request unit capacity for a collection?</span></span>

<span data-ttu-id="4ab20-123">Azure Cosmos DB est une base de données comportant plusieurs modèle, il est important toonote que nous appelons tooa collection ou de document pour un document API, un nœud/graphique pour une API graph et/une entité de table pour l’API de table.</span><span class="sxs-lookup"><span data-stu-id="4ab20-123">As Azure Cosmos DB is a multi-model database, it is important toonote that we will refer tooa collection/document for a document API, a graph/node for a graph API and a table/entity for table API.</span></span> <span data-ttu-id="4ab20-124">Débit de ce document, nous allons généraliser toohello les concepts de conteneur ou cet élément.</span><span class="sxs-lookup"><span data-stu-id="4ab20-124">Throughput this document we will generalize toohello concepts of container/item.</span></span>

## <a name="request-units-and-request-charges"></a><span data-ttu-id="4ab20-125">Unités de requête et frais de requête</span><span class="sxs-lookup"><span data-stu-id="4ab20-125">Request units and request charges</span></span>
<span data-ttu-id="4ab20-126">Base de données Cosmos Azure offre des performances rapides et prévisibles par *réservation* ressources toosatisfy a besoin d’un débit de votre application.</span><span class="sxs-lookup"><span data-stu-id="4ab20-126">Azure Cosmos DB delivers fast, predictable performance by *reserving* resources toosatisfy your application's throughput needs.</span></span>  <span data-ttu-id="4ab20-127">Étant donné que l’application charge et schémas d’accès changent au fil du temps, base de données Azure Cosmos vous permet d’augmenter de tooeasily ou diminuer hello application tooyour disponible de débit réservés.</span><span class="sxs-lookup"><span data-stu-id="4ab20-127">Because application load and access patterns change over time, Azure Cosmos DB allows you tooeasily increase or decrease hello amount of reserved throughput available tooyour application.</span></span>

<span data-ttu-id="4ab20-128">Avec Azure Cosmos DB, un débit réservé est spécifié en termes de traitement d’unités de requête par seconde.</span><span class="sxs-lookup"><span data-stu-id="4ab20-128">With Azure Cosmos DB, reserved throughput is specified in terms of request units processing per second.</span></span> <span data-ttu-id="4ab20-129">Vous pouvez considérer d’unités de demande comme devise de débit, dans laquelle vous *réserver* garantie de la quantité d’unités de demande application tooyour disponible sur par seconde.</span><span class="sxs-lookup"><span data-stu-id="4ab20-129">You can think of request units as throughput currency, whereby you *reserve* an amount of guaranteed request units available tooyour application on per second basis.</span></span>  <span data-ttu-id="4ab20-130">Chaque opération dans Azure Cosmos DB (écriture d’un document, exécution d’une requête, mise à jour d’un document) consomme des ressources de processeur, de mémoire et d’E/S par seconde.</span><span class="sxs-lookup"><span data-stu-id="4ab20-130">Each operation in Azure Cosmos DB - writing a document, performing a query, updating a document - consumes CPU, memory, and IOPS.</span></span>  <span data-ttu-id="4ab20-131">Autrement dit, chaque opération entraîne des *frais de requête*, exprimés en *unités de requête*.</span><span class="sxs-lookup"><span data-stu-id="4ab20-131">That is, each operation incurs a *request charge*, which is expressed in *request units*.</span></span>  <span data-ttu-id="4ab20-132">Comprendre les facteurs hello qui a un impact sur les coûts d’unité de demande, ainsi que les exigences de débit de votre application, permet de vous toorun votre application en tant que coût efficacement que possible.</span><span class="sxs-lookup"><span data-stu-id="4ab20-132">Understanding hello factors which impact request unit charges, along with your application's throughput requirements, enables you toorun your application as cost effectively as possible.</span></span> <span data-ttu-id="4ab20-133">l’Explorateur de requête Hello est également un outil merveilleux tootest hello core d’une requête.</span><span class="sxs-lookup"><span data-stu-id="4ab20-133">hello query explorer is also a wonderful tool tootest hello core of a query.</span></span>

<span data-ttu-id="4ab20-134">Nous vous recommandons de mise en route en regardant hello suivant vidéo, où Aravind Ramachandran explique les unités de demande et de la prévisibilité des performances avec la base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="4ab20-134">We recommend getting started by watching hello following video, where Aravind Ramachandran explains request units and predictable performance with Azure Cosmos DB.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Predictable-Performance-with-DocumentDB/player]
> 
> 

## <a name="specifying-request-unit-capacity-in-azure-cosmos-db"></a><span data-ttu-id="4ab20-135">Spécification de la capacité d’unités de requête dans Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="4ab20-135">Specifying request unit capacity in Azure Cosmos DB</span></span>
<span data-ttu-id="4ab20-136">Lorsque vous démarrez une nouvelle collection, un tableau ou un graphique, vous spécifiez le nombre de hello d’unités de demande par seconde (RU par seconde) à réserver.</span><span class="sxs-lookup"><span data-stu-id="4ab20-136">When starting a new collection, table or graph, you specify hello number of request units per second (RU per second) you want reserved.</span></span> <span data-ttu-id="4ab20-137">Selon le débit approvisionné de hello, base de données Azure Cosmos alloue toohost de partitions physiques votre collection et fractionnements/rebalances données sur plusieurs partitions qu’elle se développe.</span><span class="sxs-lookup"><span data-stu-id="4ab20-137">Based on hello provisioned throughput, Azure Cosmos DB allocates physical partitions toohost your collection and splits/rebalances data across partitions as it grows.</span></span>

<span data-ttu-id="4ab20-138">Base de données Azure Cosmos requiert qu'un toobe de clé de partition spécifié lorsqu’une collection est configurée avec 2 500 unités de demande ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="4ab20-138">Azure Cosmos DB requires a partition key toobe specified when a collection is provisioned with 2,500 request units or higher.</span></span> <span data-ttu-id="4ab20-139">Une clé de partition est également requis tooscale débit de votre collection au-delà de 2 500 unités de demande Bonjour futures.</span><span class="sxs-lookup"><span data-stu-id="4ab20-139">A partition key is also required tooscale your collection's throughput beyond 2,500 request units in hello future.</span></span> <span data-ttu-id="4ab20-140">Par conséquent, il est vivement recommandé tooconfigure un [clé de partition](partition-data.md) lors de la création d’un conteneur, quelle que soit votre débit initial.</span><span class="sxs-lookup"><span data-stu-id="4ab20-140">Therefore, it is highly recommended tooconfigure a [partition key](partition-data.md) when creating a container regardless of your initial throughput.</span></span> <span data-ttu-id="4ab20-141">Étant donné que vos données peuvent avoir toobe divisée en plusieurs partitions, il est nécessaire toopick une clé de partition qui a une cardinalité élevée (100 toomillions de valeurs distinctes) afin que votre collection/table/graphique et les demandes peuvent être monté en uniformément par base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="4ab20-141">Since your data might have toobe split across multiple partitions, it is necessary toopick a partition key that has a high cardinality (100 toomillions of distinct values) so that your collection/table/graph and requests can be scaled uniformly by Azure Cosmos DB.</span></span> 

> [!NOTE]
> <span data-ttu-id="4ab20-142">Une clé de partition est une limite logique et non physique.</span><span class="sxs-lookup"><span data-stu-id="4ab20-142">A partition key is a logical boundary, and not a physical one.</span></span> <span data-ttu-id="4ab20-143">Par conséquent, vous n’avez pas besoin de nombre de hello toolimit partition distinctes des valeurs de clé.</span><span class="sxs-lookup"><span data-stu-id="4ab20-143">Therefore, you do not need toolimit hello number of distinct partition key values.</span></span> <span data-ttu-id="4ab20-144">Il s’agit en fait une meilleure toohave plus distincte inférieure, des valeurs de clé de partition comme base de données Azure Cosmos a plus d’options d’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="4ab20-144">It is in fact better toohave more distinct partition key values than less, as Azure Cosmos DB has more load balancing options.</span></span>

<span data-ttu-id="4ab20-145">Voici un extrait de code pour la création d’une collection de 3 000 demande unités par seconde en utilisant hello .NET SDK :</span><span class="sxs-lookup"><span data-stu-id="4ab20-145">Here is a code snippet for creating a collection with 3,000 request units per second using hello .NET SDK:</span></span>

```csharp
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000 });
```

<span data-ttu-id="4ab20-146">Azure Cosmos DB fonctionne sur un modèle de réservation du débit.</span><span class="sxs-lookup"><span data-stu-id="4ab20-146">Azure Cosmos DB operates on a reservation model on throughput.</span></span> <span data-ttu-id="4ab20-147">Autrement dit, vous êtes facturé pour la quantité de hello de débit *réservé*, quelle que soit la quantité que le débit est activement *utilisé*.</span><span class="sxs-lookup"><span data-stu-id="4ab20-147">That is, you are billed for hello amount of throughput *reserved*, regardless of how much of that throughput is actively *used*.</span></span> <span data-ttu-id="4ab20-148">Comme charge, les données et l’utilisation de modèles modification de votre application vous pouvez facilement évoluer hello quantité réservées RUs via les kits de développement logiciel ou à l’aide de hello [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4ab20-148">As your application's load, data, and usage patterns change you can easily scale up and down hello amount of reserved RUs through SDKs or using hello [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="4ab20-149">Chaque collection/table/graphique sont mappés tooan `Offer` ressource dans Cosmos base de données Azure, qui contient les métadonnées sur le débit approvisionné de hello.</span><span class="sxs-lookup"><span data-stu-id="4ab20-149">Each collection/table/graph are mapped tooan `Offer` resource in Azure Cosmos DB, which has metadata about hello provisioned throughput.</span></span> <span data-ttu-id="4ab20-150">Vous pouvez modifier le débit de hello allouée en recherchant la ressource offre correspondante de hello pour un conteneur, puis mettre à jour avec la nouvelle valeur de débit hello.</span><span class="sxs-lookup"><span data-stu-id="4ab20-150">You can change hello allocated throughput by looking up hello corresponding offer resource for a container, then updating it with hello new throughput value.</span></span> <span data-ttu-id="4ab20-151">Voici un extrait de code pour modifier le débit de hello d’une collection de too5, 000 unités de demande par seconde en utilisant hello .NET SDK :</span><span class="sxs-lookup"><span data-stu-id="4ab20-151">Here is a code snippet for changing hello throughput of a collection too5,000 request units per second using hello .NET SDK:</span></span>

```csharp
// Fetch hello resource toobe updated
Offer offer = client.CreateOfferQuery()
                .Where(r => r.ResourceLink == collection.SelfLink)    
                .AsEnumerable()
                .SingleOrDefault();

// Set hello throughput too5000 request units per second
offer = new OfferV2(offer, 5000);

// Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offer);
```

<span data-ttu-id="4ab20-152">Il n’est pas votre conteneur de disponibilité toohello impact lorsque vous modifiez un débit hello.</span><span class="sxs-lookup"><span data-stu-id="4ab20-152">There is no impact toohello availability of your container when you change hello throughput.</span></span> <span data-ttu-id="4ab20-153">Débit de nouveau réservés hello est généralement efficace en quelques secondes dans l’application du débit de nouveau hello.</span><span class="sxs-lookup"><span data-stu-id="4ab20-153">Typically hello new reserved throughput is effective within seconds on application of hello new throughput.</span></span>

## <a name="request-unit-considerations"></a><span data-ttu-id="4ab20-154">Considérations relatives aux unités de requête</span><span class="sxs-lookup"><span data-stu-id="4ab20-154">Request unit considerations</span></span>
<span data-ttu-id="4ab20-155">Lorsque vous estimez le nombre de hello de tooreserve d’unités de demande pour votre conteneur de base de données Azure Cosmos, il est hello tootake important suivant des variables en considération :</span><span class="sxs-lookup"><span data-stu-id="4ab20-155">When estimating hello number of request units tooreserve for your Azure Cosmos DB container, it is important tootake hello following variables into consideration:</span></span>

* <span data-ttu-id="4ab20-156">**Taille de l’élément**.</span><span class="sxs-lookup"><span data-stu-id="4ab20-156">**Item size**.</span></span> <span data-ttu-id="4ab20-157">Comme la taille augmente hello unités consommées tooread ou écrire des données hello augmente également.</span><span class="sxs-lookup"><span data-stu-id="4ab20-157">As size increases hello units consumed tooread or write hello data will also increase.</span></span>
* <span data-ttu-id="4ab20-158">**Nombre de propriétés de l’élément**.</span><span class="sxs-lookup"><span data-stu-id="4ab20-158">**Item property count**.</span></span> <span data-ttu-id="4ab20-159">En supposant que la valeur par défaut de l’indexation de toutes les propriétés, toowrite d’unités consommées hello un document/nœud/ntity augmente à mesure que de l’augmentation du nombre de propriété hello.</span><span class="sxs-lookup"><span data-stu-id="4ab20-159">Assuming default indexing of all properties, hello units consumed toowrite a document/node/ntity will increase as hello property count increases.</span></span>
* <span data-ttu-id="4ab20-160">**Cohérence des données**.</span><span class="sxs-lookup"><span data-stu-id="4ab20-160">**Data consistency**.</span></span> <span data-ttu-id="4ab20-161">Lorsque vous utilisez des niveaux de cohérence des données de Strong ou Bounded Staleness, des unités supplémentaires seront consommées tooread éléments.</span><span class="sxs-lookup"><span data-stu-id="4ab20-161">When using data consistency levels of Strong or Bounded Staleness, additional units will be consumed tooread items.</span></span>
* <span data-ttu-id="4ab20-162">**Propriétés indexées**.</span><span class="sxs-lookup"><span data-stu-id="4ab20-162">**Indexed properties**.</span></span> <span data-ttu-id="4ab20-163">Une stratégie d’indexation sur chaque conteneur détermine quelles propriétés sont indexées par défaut.</span><span class="sxs-lookup"><span data-stu-id="4ab20-163">An index policy on each container determines which properties are indexed by default.</span></span> <span data-ttu-id="4ab20-164">Vous pouvez réduire la consommation de votre unité de demande en limitant le nombre de hello des propriétés indexées ou en activant l’indexation différée.</span><span class="sxs-lookup"><span data-stu-id="4ab20-164">You can reduce your request unit consumption by limiting hello number of indexed properties or by enabling lazy indexing.</span></span>
* <span data-ttu-id="4ab20-165">**Indexation des documents**.</span><span class="sxs-lookup"><span data-stu-id="4ab20-165">**Document indexing**.</span></span> <span data-ttu-id="4ab20-166">Par défaut de que chaque élément est automatiquement indexé, vous allez consommer moins d’unités de demande si vous choisissez tooindex pas certains de vos éléments.</span><span class="sxs-lookup"><span data-stu-id="4ab20-166">By default each item is automatically indexed, you will consume fewer request units if you choose not tooindex some of your items.</span></span>
* <span data-ttu-id="4ab20-167">**Modèles de requête**.</span><span class="sxs-lookup"><span data-stu-id="4ab20-167">**Query patterns**.</span></span> <span data-ttu-id="4ab20-168">complexité Hello d’une requête a un impact sur le nombre d’unités demande sont consommé pour une opération.</span><span class="sxs-lookup"><span data-stu-id="4ab20-168">hello complexity of a query impacts how many Request Units are consumed for an operation.</span></span> <span data-ttu-id="4ab20-169">nombre Hello de prédicats, de la nature de hello prédicats, projections, nombre des UDF et la taille de hello du jeu de données source hello tous influencent coût hello d’opérations de requête.</span><span class="sxs-lookup"><span data-stu-id="4ab20-169">hello number of predicates, nature of hello predicates, projections, number of UDFs, and hello size of hello source data set all influence hello cost of query operations.</span></span>
* <span data-ttu-id="4ab20-170">**Utilisation des scripts**.</span><span class="sxs-lookup"><span data-stu-id="4ab20-170">**Script usage**.</span></span>  <span data-ttu-id="4ab20-171">Comme avec les requêtes, des procédures stockées et les déclencheurs consomment des unités de demande en fonction de la complexité de hello d’opérations hello en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="4ab20-171">As with queries, stored procedures and triggers consume request units based on hello complexity of hello operations being performed.</span></span> <span data-ttu-id="4ab20-172">Lorsque vous développez votre application, inspecter des frais de demande hello en-tête toobetter comprendre comment chaque opération consomme la capacité des unités de demande.</span><span class="sxs-lookup"><span data-stu-id="4ab20-172">As you develop your application, inspect hello request charge header toobetter understand how each operation is consuming request unit capacity.</span></span>

## <a name="estimating-throughput-needs"></a><span data-ttu-id="4ab20-173">Estimation des besoins de débit</span><span class="sxs-lookup"><span data-stu-id="4ab20-173">Estimating throughput needs</span></span>
<span data-ttu-id="4ab20-174">Une unité de requête est une mesure normalisée du coût de traitement de la requête.</span><span class="sxs-lookup"><span data-stu-id="4ab20-174">A request unit is a normalized measure of request processing cost.</span></span> <span data-ttu-id="4ab20-175">Une unité de demande unique représente hello traitement capacité requise tooread (via l’élément self link ou id) un 1 Ko unique élément composé de 10 valeurs de propriété unique (à l’exception des propriétés système).</span><span class="sxs-lookup"><span data-stu-id="4ab20-175">A single request unit represents hello processing capacity required tooread (via self link or id) a single 1KB item consisting of 10 unique property values (excluding system properties).</span></span> <span data-ttu-id="4ab20-176">Une demande de toocreate (insert), remplacer ou supprimer des hello même élément consommera plus de traitement du service de hello et donc plusieurs unités de requête.</span><span class="sxs-lookup"><span data-stu-id="4ab20-176">A request toocreate (insert), replace or delete hello same item will consume more processing from hello service and thereby more request units.</span></span>   

> [!NOTE]
> <span data-ttu-id="4ab20-177">ligne de base Hello d’unité de 1 demande pour une base de connaissances 1 correspond élément tooa simple obtenir par id d’élément de hello ou un élément self link.</span><span class="sxs-lookup"><span data-stu-id="4ab20-177">hello baseline of 1 request unit for a 1KB item corresponds tooa simple GET by self link or id of hello item.</span></span>
> 
> 

<span data-ttu-id="4ab20-178">Par exemple, Voici un tableau qui indique le nombre de demandes tooprovision unités à trois tailles d’élément différent (1 Ko, 4 Ko et 64 Ko) et à deux niveaux de performance différents (lectures par seconde de 500 écritures par seconde de 100 et 500 lectures par seconde + 500 écritures par seconde).</span><span class="sxs-lookup"><span data-stu-id="4ab20-178">For example, here's a table that shows how many request units tooprovision at three different item sizes (1KB, 4KB, and 64KB) and at two different performance levels (500 reads/second + 100 writes/second and 500 reads/second + 500 writes/second).</span></span> <span data-ttu-id="4ab20-179">la cohérence des données Hello a été configurée au niveau de la Session et hello stratégie d’indexation a été défini tooNone.</span><span class="sxs-lookup"><span data-stu-id="4ab20-179">hello data consistency was configured at Session, and hello indexing policy was set tooNone.</span></span>

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><span data-ttu-id="4ab20-180"><strong>Taille de l’élément</strong></span><span class="sxs-lookup"><span data-stu-id="4ab20-180"><strong>Item size</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="4ab20-181"><strong>Lectures par seconde</strong></span><span class="sxs-lookup"><span data-stu-id="4ab20-181"><strong>Reads/second</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="4ab20-182"><strong>Écritures par seconde</strong></span><span class="sxs-lookup"><span data-stu-id="4ab20-182"><strong>Writes/second</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="4ab20-183"><strong>Unités de demande</strong></span><span class="sxs-lookup"><span data-stu-id="4ab20-183"><strong>Request units</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="4ab20-184">1 Ko</span><span class="sxs-lookup"><span data-stu-id="4ab20-184">1 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="4ab20-185">500</span><span class="sxs-lookup"><span data-stu-id="4ab20-185">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="4ab20-186">100</span><span class="sxs-lookup"><span data-stu-id="4ab20-186">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="4ab20-187">(500 * 1) + (100 * 5) = 1 000 UR/s</span><span class="sxs-lookup"><span data-stu-id="4ab20-187">(500 * 1) + (100 * 5) = 1,000 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="4ab20-188">1 Ko</span><span class="sxs-lookup"><span data-stu-id="4ab20-188">1 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="4ab20-189">500</span><span class="sxs-lookup"><span data-stu-id="4ab20-189">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="4ab20-190">500</span><span class="sxs-lookup"><span data-stu-id="4ab20-190">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="4ab20-191">(500 * 1) + (500 * 5) = 3 000 UR/s</span><span class="sxs-lookup"><span data-stu-id="4ab20-191">(500 * 1) + (500 * 5) = 3,000 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="4ab20-192">4 Ko</span><span class="sxs-lookup"><span data-stu-id="4ab20-192">4 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="4ab20-193">500</span><span class="sxs-lookup"><span data-stu-id="4ab20-193">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="4ab20-194">100</span><span class="sxs-lookup"><span data-stu-id="4ab20-194">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="4ab20-195">(500 * 1.3) + (100 * 7) = 1 350 UR/s</span><span class="sxs-lookup"><span data-stu-id="4ab20-195">(500 * 1.3) + (100 * 7) = 1,350 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="4ab20-196">4 Ko</span><span class="sxs-lookup"><span data-stu-id="4ab20-196">4 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="4ab20-197">500</span><span class="sxs-lookup"><span data-stu-id="4ab20-197">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="4ab20-198">500</span><span class="sxs-lookup"><span data-stu-id="4ab20-198">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="4ab20-199">(500 * 1.3) + (500 * 7) = 4 150 UR/s</span><span class="sxs-lookup"><span data-stu-id="4ab20-199">(500 * 1.3) + (500 * 7) = 4,150 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="4ab20-200">64 Ko</span><span class="sxs-lookup"><span data-stu-id="4ab20-200">64 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="4ab20-201">500</span><span class="sxs-lookup"><span data-stu-id="4ab20-201">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="4ab20-202">100</span><span class="sxs-lookup"><span data-stu-id="4ab20-202">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="4ab20-203">(500 * 10) + (100 * 48) = 9 800 UR/s</span><span class="sxs-lookup"><span data-stu-id="4ab20-203">(500 * 10) + (100 * 48) = 9,800 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="4ab20-204">64 Ko</span><span class="sxs-lookup"><span data-stu-id="4ab20-204">64 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="4ab20-205">500</span><span class="sxs-lookup"><span data-stu-id="4ab20-205">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="4ab20-206">500</span><span class="sxs-lookup"><span data-stu-id="4ab20-206">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="4ab20-207">(500 * 10) + (500 * 48) = 29 000 UR/s</span><span class="sxs-lookup"><span data-stu-id="4ab20-207">(500 * 10) + (500 * 48) = 29,000 RU/s</span></span></p></td>
        </tr>
    </tbody>
</table>

### <a name="use-hello-request-unit-calculator"></a><span data-ttu-id="4ab20-208">Utiliser la calculatrice des unités hello demande</span><span class="sxs-lookup"><span data-stu-id="4ab20-208">Use hello request unit calculator</span></span>
<span data-ttu-id="4ab20-209">clients toohelp fines paramétrer les estimations de débit, il est basé sur le web [calculatrice des unités de demande](https://www.documentdb.com/capacityplanner) toohelp estimation hello demande unité configuration requise pour les opérations courantes, notamment :</span><span class="sxs-lookup"><span data-stu-id="4ab20-209">toohelp customers fine tune their throughput estimations, there is a web based [request unit calculator](https://www.documentdb.com/capacityplanner) toohelp estimate hello request unit requirements for typical operations, including:</span></span>

* <span data-ttu-id="4ab20-210">Créations (écritures) d’éléments</span><span class="sxs-lookup"><span data-stu-id="4ab20-210">Item creates (writes)</span></span>
* <span data-ttu-id="4ab20-211">Lectures d’éléments</span><span class="sxs-lookup"><span data-stu-id="4ab20-211">Item reads</span></span>
* <span data-ttu-id="4ab20-212">Suppressions d’éléments</span><span class="sxs-lookup"><span data-stu-id="4ab20-212">Item deletes</span></span>
* <span data-ttu-id="4ab20-213">Mises à jour d’éléments</span><span class="sxs-lookup"><span data-stu-id="4ab20-213">Item updates</span></span>

<span data-ttu-id="4ab20-214">outil de Hello inclut également la prise en charge pour l’estimation des besoins de stockage de données en fonction de vous fournissez des exemples d’éléments de hello.</span><span class="sxs-lookup"><span data-stu-id="4ab20-214">hello tool also includes support for estimating data storage needs based on hello sample items you provide.</span></span>

<span data-ttu-id="4ab20-215">À l’aide d’outil de hello est simple :</span><span class="sxs-lookup"><span data-stu-id="4ab20-215">Using hello tool is simple:</span></span>

1. <span data-ttu-id="4ab20-216">Chargez un ou plusieurs éléments représentatifs.</span><span class="sxs-lookup"><span data-stu-id="4ab20-216">Upload one or more representative items.</span></span>
   
    ![Télécharger la calculatrice des unités de demande toohello éléments][2]
2. <span data-ttu-id="4ab20-218">exigences de stockage de données tooestimate, entrez le nombre total de hello d’éléments toostore prévu.</span><span class="sxs-lookup"><span data-stu-id="4ab20-218">tooestimate data storage requirements, enter hello total number of items you expect toostore.</span></span>
3. <span data-ttu-id="4ab20-219">Entrez nombre hello d’éléments à créer, lire, mettre à jour et supprimer les opérations que vous avez besoin (sur une base par seconde).</span><span class="sxs-lookup"><span data-stu-id="4ab20-219">Enter hello number of items create, read, update, and delete operations you require (on a per-second basis).</span></span> <span data-ttu-id="4ab20-220">coûts d’unité de demande hello tooestimate d’opérations de mise à jour d’élément, téléchargez une copie de l’exemple d’élément hello à l’étape 1 ci-dessus qui inclut les mises à jour de champ par défaut.</span><span class="sxs-lookup"><span data-stu-id="4ab20-220">tooestimate hello request unit charges of item update operations, upload a copy of hello sample item from step 1 above that includes typical field updates.</span></span>  <span data-ttu-id="4ab20-221">Par exemple, si les mises à jour de l’élément généralement modifient deux propriétés nommées lastLogin et userVisits, puis copiez simplement exemple d’élément hello, mettre à jour les valeurs hello pour ces deux propriétés et télécharger hello copié des éléments.</span><span class="sxs-lookup"><span data-stu-id="4ab20-221">For example, if item updates typically modify two properties named lastLogin and userVisits, then simply copy hello sample item, update hello values for those two properties, and upload hello copied item.</span></span>
   
    ![Entrez des exigences de débit de la calculatrice d’unité hello demande][3]
4. <span data-ttu-id="4ab20-223">Cliquez sur Calculer et examiner les résultats de hello.</span><span class="sxs-lookup"><span data-stu-id="4ab20-223">Click calculate and examine hello results.</span></span>
   
    ![Résultats de la calculatrice d’unités de demande][4]

> [!NOTE]
> <span data-ttu-id="4ab20-225">Si vous avez des types d’éléments qui varient considérablement en termes de taille et hello nombre de propriétés indexées, puis télécharger un exemple de chaque *type* de l’élément toohello outil, puis calcule les résultats hello.</span><span class="sxs-lookup"><span data-stu-id="4ab20-225">If you have item types which will differ dramatically in terms of size and hello number of indexed properties, then upload a sample of each *type* of typical item toohello tool and then calculate hello results.</span></span>
> 
> 

### <a name="use-hello-azure-cosmos-db-request-charge-response-header"></a><span data-ttu-id="4ab20-226">Utiliser l’en-tête de réponse des frais hello Azure Cosmos DB demande</span><span class="sxs-lookup"><span data-stu-id="4ab20-226">Use hello Azure Cosmos DB request charge response header</span></span>
<span data-ttu-id="4ab20-227">Chaque réponse de hello service de base de données Azure Cosmos inclut un en-tête personnalisé (`x-ms-request-charge`) qui contient les unités de demande hello consommées pour la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="4ab20-227">Every response from hello Azure Cosmos DB service includes a custom header (`x-ms-request-charge`) that contains hello request units consumed for hello request.</span></span> <span data-ttu-id="4ab20-228">Cet en-tête est également accessible via hello kits de développement de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="4ab20-228">This header is also accessible through hello Azure Cosmos DB SDKs.</span></span> <span data-ttu-id="4ab20-229">Bonjour .NET SDK, RequestCharge est une propriété d’objet de ResourceResponse hello.</span><span class="sxs-lookup"><span data-stu-id="4ab20-229">In hello .NET SDK, RequestCharge is a property of hello ResourceResponse object.</span></span>  <span data-ttu-id="4ab20-230">Pour les requêtes, hello Azure Cosmos DB requête Explorer Bonjour portail Azure fournit des informations de frais de demande pour les requêtes exécutées.</span><span class="sxs-lookup"><span data-stu-id="4ab20-230">For queries, hello Azure Cosmos DB Query Explorer in hello Azure portal provides request charge information for executed queries.</span></span>

![Examen des frais RU Bonjour Explorer de requête][1]

<span data-ttu-id="4ab20-232">Dans cet esprit, une méthode d’estimation de la quantité de hello de débit réservés requise par votre application est toorecord hello demande unité des frais associés avec les opérations en cours d’exécution par rapport à un élément représentatif utilisé par votre application, puis estimation du nombre de hello d’opérations vous comptez effectuer chaque seconde.</span><span class="sxs-lookup"><span data-stu-id="4ab20-232">With this in mind, one method for estimating hello amount of reserved throughput required by your application is toorecord hello request unit charge associated with running typical operations against a representative item used by your application and then estimating hello number of operations you anticipate performing each second.</span></span>  <span data-ttu-id="4ab20-233">Être vraiment toomeasure et inclure des requêtes et utilisation des scripts de base de données Azure Cosmos ainsi.</span><span class="sxs-lookup"><span data-stu-id="4ab20-233">Be sure toomeasure and include typical queries and Azure Cosmos DB script usage as well.</span></span>

> [!NOTE]
> <span data-ttu-id="4ab20-234">Si vous avez des types d’éléments qui varient considérablement en termes de taille et hello nombre de propriétés indexées, puis enregistrer des frais d’unité hello opération applicable demande associées à chaque *type* d’élément.</span><span class="sxs-lookup"><span data-stu-id="4ab20-234">If you have item types which will differ dramatically in terms of size and hello number of indexed properties, then record hello applicable operation request unit charge associated with each *type* of typical item.</span></span>
> 
> 

<span data-ttu-id="4ab20-235">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="4ab20-235">For example:</span></span>

1. <span data-ttu-id="4ab20-236">Enregistrer des frais d’unitaires hello demande de création (insertion) un élément.</span><span class="sxs-lookup"><span data-stu-id="4ab20-236">Record hello request unit charge of creating (inserting) a typical item.</span></span> 
2. <span data-ttu-id="4ab20-237">Enregistrement hello demande unité des frais de la lecture d’un élément.</span><span class="sxs-lookup"><span data-stu-id="4ab20-237">Record hello request unit charge of reading a typical item.</span></span>
3. <span data-ttu-id="4ab20-238">Enregistrement hello demande unité des frais de mise à jour d’un élément.</span><span class="sxs-lookup"><span data-stu-id="4ab20-238">Record hello request unit charge of updating a typical item.</span></span>
4. <span data-ttu-id="4ab20-239">Enregistrement hello demande unité des frais de requêtes d’élément classiques, courantes.</span><span class="sxs-lookup"><span data-stu-id="4ab20-239">Record hello request unit charge of typical, common item queries.</span></span>
5. <span data-ttu-id="4ab20-240">Enregistrement hello demande frais unitaires des scripts personnalisés (procédures stockées, déclencheurs, fonctions définies par l’utilisateur) exploité par l’application hello</span><span class="sxs-lookup"><span data-stu-id="4ab20-240">Record hello request unit charge of any custom scripts (stored procedures, triggers, user-defined functions) leveraged by hello application</span></span>
6. <span data-ttu-id="4ab20-241">Calculer les demande requis hello qu'unités indiqué le nombre estimé de hello d’opérations vous anticipez toorun chaque seconde.</span><span class="sxs-lookup"><span data-stu-id="4ab20-241">Calculate hello required request units given hello estimated number of operations you anticipate toorun each second.</span></span>

### <span data-ttu-id="4ab20-242"><a id="GetLastRequestStatistics"></a>Utiliser la commande GetLastRequestStatistics de l’API pour MongoDB</span><span class="sxs-lookup"><span data-stu-id="4ab20-242"><a id="GetLastRequestStatistics"></a>Use API for MongoDB's GetLastRequestStatistics command</span></span>
<span data-ttu-id="4ab20-243">API pour MongoDB prend en charge une commande personnalisée, *getLastRequestStatistics*, pour récupérer des frais de demande hello pour les opérations spécifiées.</span><span class="sxs-lookup"><span data-stu-id="4ab20-243">API for MongoDB supports a custom command, *getLastRequestStatistics*, for retrieving hello request charge for specified operations.</span></span>

<span data-ttu-id="4ab20-244">Par exemple, Bonjour Mongo Shell, exécutez opération hello tooverify hello demande frais pour.</span><span class="sxs-lookup"><span data-stu-id="4ab20-244">For example, in hello Mongo Shell, execute hello operation you want tooverify hello request charge for.</span></span>
```
> db.sample.find()
```

<span data-ttu-id="4ab20-245">Ensuite, exécutez la commande hello *getLastRequestStatistics*.</span><span class="sxs-lookup"><span data-stu-id="4ab20-245">Next, execute hello command *getLastRequestStatistics*.</span></span>
```
> db.runCommand({getLastRequestStatistics: 1})
{
    "_t": "GetRequestStatisticsResponse",
    "ok": 1,
    "CommandName": "OP_QUERY",
    "RequestCharge": 2.48,
    "RequestDurationInMilliSeconds" : 4.0048
}
```

<span data-ttu-id="4ab20-246">Dans cet esprit, une méthode d’estimation de la quantité de hello de débit réservés requise par votre application est toorecord hello demande unité des frais associés avec les opérations en cours d’exécution par rapport à un élément représentatif utilisé par votre application, puis estimation du nombre de hello d’opérations vous comptez effectuer chaque seconde.</span><span class="sxs-lookup"><span data-stu-id="4ab20-246">With this in mind, one method for estimating hello amount of reserved throughput required by your application is toorecord hello request unit charge associated with running typical operations against a representative item used by your application and then estimating hello number of operations you anticipate performing each second.</span></span>

> [!NOTE]
> <span data-ttu-id="4ab20-247">Si vous avez des types d’éléments qui varient considérablement en termes de taille et hello nombre de propriétés indexées, puis enregistrer des frais d’unité hello opération applicable demande associées à chaque *type* d’élément.</span><span class="sxs-lookup"><span data-stu-id="4ab20-247">If you have item types which will differ dramatically in terms of size and hello number of indexed properties, then record hello applicable operation request unit charge associated with each *type* of typical item.</span></span>
> 
> 

## <a name="use-api-for-mongodbs-portal-metrics"></a><span data-ttu-id="4ab20-248">Utiliser les mesures du portail de l’API pour MongoDB</span><span class="sxs-lookup"><span data-stu-id="4ab20-248">Use API for MongoDB's portal metrics</span></span>
<span data-ttu-id="4ab20-249">Hello tooget de façon la plus simple de frais une bonne estimation de l’unité de demande correspondant à votre API pour la base de données MongoDB est toouse hello [portail Azure](https://portal.azure.com) métriques.</span><span class="sxs-lookup"><span data-stu-id="4ab20-249">hello simplest way tooget a good estimation of request unit charges for your API for MongoDB database is toouse hello [Azure portal](https://portal.azure.com) metrics.</span></span> <span data-ttu-id="4ab20-250">Avec hello *nombre de demandes* et *demande frais* graphiques, vous pouvez obtenir une estimation du nombre d’unités de demande chaque opération est le nombre d’unités de demande et de consommation tomberont relatif tooone un autre.</span><span class="sxs-lookup"><span data-stu-id="4ab20-250">With hello *Number of requests* and *Request Charge* charts, you can get an estimation of how many request units each operation is consuming and how many request units they consume relative tooone another.</span></span>

![Mesures du portail de l’API pour MongoDB][6]

## <a name="a-request-unit-estimation-example"></a><span data-ttu-id="4ab20-252">Exemple d’estimation d’unités de requête</span><span class="sxs-lookup"><span data-stu-id="4ab20-252">A request unit estimation example</span></span>
<span data-ttu-id="4ab20-253">Tenez compte des hello suivant le document de ~ 1 Ko :</span><span class="sxs-lookup"><span data-stu-id="4ab20-253">Consider hello following ~1KB document:</span></span>

```json
{
 "id": "08259",
  "description": "Cereals ready-to-eat, KELLOGG, KELLOGG'S CRISPIX",
  "tags": [
    {
      "name": "cereals ready-to-eat"
    },
    {
      "name": "kellogg"
    },
    {
      "name": "kellogg's crispix"
    }
  ],
  "version": 1,
  "commonName": "Includes USDA Commodity B855",
  "manufacturerName": "Kellogg, Co.",
  "isFromSurvey": false,
  "foodGroup": "Breakfast Cereals",
  "nutrients": [
    {
      "id": "262",
      "description": "Caffeine",
      "nutritionValue": 0,
      "units": "mg"
    },
    {
      "id": "307",
      "description": "Sodium, Na",
      "nutritionValue": 611,
      "units": "mg"
    },
    {
      "id": "309",
      "description": "Zinc, Zn",
      "nutritionValue": 5.2,
      "units": "mg"
    }
  ],
  "servings": [
    {
      "amount": 1,
      "description": "cup (1 NLEA serving)",
      "weightInGrams": 29
    }
  ]
}
```

> [!NOTE]
> <span data-ttu-id="4ab20-254">Les documents sont réduites dans la base de données Azure Cosmos, donc calculé par le système de hello taille du document hello ci-dessus est légèrement inférieure à 1 Ko.</span><span class="sxs-lookup"><span data-stu-id="4ab20-254">Documents are minified in Azure Cosmos DB, so hello system calculated size of hello document above is slightly less than 1KB.</span></span>
> 
> 

<span data-ttu-id="4ab20-255">Hello tableau suivant illustre approximative demande coûts d’unité pour les opérations courantes sur cet élément (hello demande approximative unité frais part du principe que le niveau de cohérence de compte de hello est défini trop « Session » et que tous les éléments sont indexés automatiquement) :</span><span class="sxs-lookup"><span data-stu-id="4ab20-255">hello following table shows approximate request unit charges for typical operations on this item (hello approximate request unit charge assumes that hello account consistency level is set too“Session” and that all items are automatically indexed):</span></span>

| <span data-ttu-id="4ab20-256">Opération</span><span class="sxs-lookup"><span data-stu-id="4ab20-256">Operation</span></span> | <span data-ttu-id="4ab20-257">Frais d’unités de requête</span><span class="sxs-lookup"><span data-stu-id="4ab20-257">Request Unit Charge</span></span> |
| --- | --- |
| <span data-ttu-id="4ab20-258">Créer un élément</span><span class="sxs-lookup"><span data-stu-id="4ab20-258">Create item</span></span> |<span data-ttu-id="4ab20-259">~15 unités de requête</span><span class="sxs-lookup"><span data-stu-id="4ab20-259">~15 RU</span></span> |
| <span data-ttu-id="4ab20-260">Lire un élément</span><span class="sxs-lookup"><span data-stu-id="4ab20-260">Read item</span></span> |<span data-ttu-id="4ab20-261">~1 unité de requête</span><span class="sxs-lookup"><span data-stu-id="4ab20-261">~1 RU</span></span> |
| <span data-ttu-id="4ab20-262">Interroger un élément par id</span><span class="sxs-lookup"><span data-stu-id="4ab20-262">Query item by id</span></span> |<span data-ttu-id="4ab20-263">~2,5 unités de requête</span><span class="sxs-lookup"><span data-stu-id="4ab20-263">~2.5 RU</span></span> |

<span data-ttu-id="4ab20-264">En outre, ce tableau montre demande approximative de coûts d’unité pour les requêtes par défaut utilisés dans une application hello :</span><span class="sxs-lookup"><span data-stu-id="4ab20-264">Additionally, this table shows approximate request unit charges for typical queries used in hello application:</span></span>

| <span data-ttu-id="4ab20-265">Interroger</span><span class="sxs-lookup"><span data-stu-id="4ab20-265">Query</span></span> | <span data-ttu-id="4ab20-266">Frais d’unités de requête</span><span class="sxs-lookup"><span data-stu-id="4ab20-266">Request Unit Charge</span></span> | <span data-ttu-id="4ab20-267">Nombre d’éléments renvoyés</span><span class="sxs-lookup"><span data-stu-id="4ab20-267"># of Returned Items</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4ab20-268">Sélectionner un aliment par id</span><span class="sxs-lookup"><span data-stu-id="4ab20-268">Select food by id</span></span> |<span data-ttu-id="4ab20-269">~2,5 unités de requête</span><span class="sxs-lookup"><span data-stu-id="4ab20-269">~2.5 RU</span></span> |<span data-ttu-id="4ab20-270">1</span><span class="sxs-lookup"><span data-stu-id="4ab20-270">1</span></span> |
| <span data-ttu-id="4ab20-271">Sélectionner un aliment par fabricant</span><span class="sxs-lookup"><span data-stu-id="4ab20-271">Select foods by manufacturer</span></span> |<span data-ttu-id="4ab20-272">~7 unités de requête</span><span class="sxs-lookup"><span data-stu-id="4ab20-272">~7 RU</span></span> |<span data-ttu-id="4ab20-273">7</span><span class="sxs-lookup"><span data-stu-id="4ab20-273">7</span></span> |
| <span data-ttu-id="4ab20-274">Sélectionner par groupe d’aliments et trier par poids</span><span class="sxs-lookup"><span data-stu-id="4ab20-274">Select by food group and order by weight</span></span> |<span data-ttu-id="4ab20-275">~70 unités de requête</span><span class="sxs-lookup"><span data-stu-id="4ab20-275">~70 RU</span></span> |<span data-ttu-id="4ab20-276">100</span><span class="sxs-lookup"><span data-stu-id="4ab20-276">100</span></span> |
| <span data-ttu-id="4ab20-277">Sélectionner les 10 premiers aliments dans un groupe d’aliments</span><span class="sxs-lookup"><span data-stu-id="4ab20-277">Select top 10 foods in a food group</span></span> |<span data-ttu-id="4ab20-278">~10 unités de requête</span><span class="sxs-lookup"><span data-stu-id="4ab20-278">~10 RU</span></span> |<span data-ttu-id="4ab20-279">10</span><span class="sxs-lookup"><span data-stu-id="4ab20-279">10</span></span> |

> [!NOTE]
> <span data-ttu-id="4ab20-280">Frais de RU varient en fonction nombre hello d’éléments renvoyés.</span><span class="sxs-lookup"><span data-stu-id="4ab20-280">RU charges vary based on hello number of items returned.</span></span>
> 
> 

<span data-ttu-id="4ab20-281">Avec ces informations, nous pouvons estimer les besoins en RU hello pour ce numéro hello d’application en raison d’opérations et nous pensons que par seconde de requêtes :</span><span class="sxs-lookup"><span data-stu-id="4ab20-281">With this information, we can estimate hello RU requirements for this application given hello number of operations and queries we expect per second:</span></span>

| <span data-ttu-id="4ab20-282">Opération/Requête</span><span class="sxs-lookup"><span data-stu-id="4ab20-282">Operation/Query</span></span> | <span data-ttu-id="4ab20-283">Nombre estimé par seconde</span><span class="sxs-lookup"><span data-stu-id="4ab20-283">Estimated number per second</span></span> | <span data-ttu-id="4ab20-284">Unités de requête nécessaires</span><span class="sxs-lookup"><span data-stu-id="4ab20-284">Required RUs</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4ab20-285">Créer un élément</span><span class="sxs-lookup"><span data-stu-id="4ab20-285">Create item</span></span> |<span data-ttu-id="4ab20-286">10</span><span class="sxs-lookup"><span data-stu-id="4ab20-286">10</span></span> |<span data-ttu-id="4ab20-287">150</span><span class="sxs-lookup"><span data-stu-id="4ab20-287">150</span></span> |
| <span data-ttu-id="4ab20-288">Lire un élément</span><span class="sxs-lookup"><span data-stu-id="4ab20-288">Read item</span></span> |<span data-ttu-id="4ab20-289">100</span><span class="sxs-lookup"><span data-stu-id="4ab20-289">100</span></span> |<span data-ttu-id="4ab20-290">100</span><span class="sxs-lookup"><span data-stu-id="4ab20-290">100</span></span> |
| <span data-ttu-id="4ab20-291">Sélectionner un aliment par fabricant</span><span class="sxs-lookup"><span data-stu-id="4ab20-291">Select foods by manufacturer</span></span> |<span data-ttu-id="4ab20-292">25</span><span class="sxs-lookup"><span data-stu-id="4ab20-292">25</span></span> |<span data-ttu-id="4ab20-293">175</span><span class="sxs-lookup"><span data-stu-id="4ab20-293">175</span></span> |
| <span data-ttu-id="4ab20-294">Sélectionner par groupe d’aliments</span><span class="sxs-lookup"><span data-stu-id="4ab20-294">Select by food group</span></span> |<span data-ttu-id="4ab20-295">10</span><span class="sxs-lookup"><span data-stu-id="4ab20-295">10</span></span> |<span data-ttu-id="4ab20-296">700</span><span class="sxs-lookup"><span data-stu-id="4ab20-296">700</span></span> |
| <span data-ttu-id="4ab20-297">Sélectionner les 10 premiers</span><span class="sxs-lookup"><span data-stu-id="4ab20-297">Select top 10</span></span> |<span data-ttu-id="4ab20-298">15</span><span class="sxs-lookup"><span data-stu-id="4ab20-298">15</span></span> |<span data-ttu-id="4ab20-299">150 Total</span><span class="sxs-lookup"><span data-stu-id="4ab20-299">150 Total</span></span> |

<span data-ttu-id="4ab20-300">Dans ce cas, nous estimons l’exigence de débit moyen à 1275 unités de requête par seconde.</span><span class="sxs-lookup"><span data-stu-id="4ab20-300">In this case, we expect an average throughput requirement of 1,275 RU/s.</span></span>  <span data-ttu-id="4ab20-301">Arrondi toohello le plus proche de 100, nous serait approvisionner 1 300 ur/s pour la collecte de cette application.</span><span class="sxs-lookup"><span data-stu-id="4ab20-301">Rounding up toohello nearest 100, we would provision 1,300 RU/s for this application's collection.</span></span>

## <span data-ttu-id="4ab20-302"><a id="RequestRateTooLarge"></a> Dépassement des limites de débit réservé dans Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="4ab20-302"><a id="RequestRateTooLarge"></a> Exceeding reserved throughput limits in Azure Cosmos DB</span></span>
<span data-ttu-id="4ab20-303">Rappelez-vous que la consommation d’unités de demande est évaluée comme un taux par seconde si l’allocation de réserve hello est vide.</span><span class="sxs-lookup"><span data-stu-id="4ab20-303">Recall that request unit consumption is evaluated as a rate per second if hello budget is empty.</span></span> <span data-ttu-id="4ab20-304">Pour les applications qui dépassent hello demande approvisionné unité pour un conteneur, demandes toothat collection vont être activée jusqu'à ce que le débit de hello devient inférieur au niveau de hello réservé.</span><span class="sxs-lookup"><span data-stu-id="4ab20-304">For applications that exceed hello provisioned request unit rate for a container, requests toothat collection will be throttled until hello rate drops below hello reserved level.</span></span> <span data-ttu-id="4ab20-305">Lorsqu’une limitation se produit, le serveur de hello va se terminer manière préemptive demande hello avec RequestRateTooLargeException (code d’état HTTP 429) et en retour hello x-ms-nouvelle tentative-après-ms en-tête indiquant hello durée, en millisecondes, pendant lequel hello utilisateur doit attendre avant nouvelle tentative de demande de hello.</span><span class="sxs-lookup"><span data-stu-id="4ab20-305">When a throttle occurs, hello server will preemptively end hello request with RequestRateTooLargeException (HTTP status code 429) and return hello x-ms-retry-after-ms header indicating hello amount of time, in milliseconds, that hello user must wait before reattempting hello request.</span></span>

    HTTP Status 429
    Status Line: RequestRateTooLarge
    x-ms-retry-after-ms :100

<span data-ttu-id="4ab20-306">Si vous utilisez des requêtes de Client .NET SDK et LINQ hello, puis la plupart du temps hello jamais avoir toodeal avec cette exception, comme la version actuelle de hello Hello Client .NET SDK intercepte implicitement cette réponse, égards hello spécifiée par le serveur en-tête retry-after, et demande de hello de nouvelles tentatives.</span><span class="sxs-lookup"><span data-stu-id="4ab20-306">If you are using hello .NET Client SDK and LINQ queries, then most of hello time you never have toodeal with this exception, as hello current version of hello .NET Client SDK implicitly catches this response, respects hello server-specified retry-after header, and retries hello request.</span></span> <span data-ttu-id="4ab20-307">À moins que votre compte est accessible simultanément par plusieurs clients, hello suivant sera réalisée.</span><span class="sxs-lookup"><span data-stu-id="4ab20-307">Unless your account is being accessed concurrently by multiple clients, hello next retry will succeed.</span></span>

<span data-ttu-id="4ab20-308">Si vous avez plusieurs clients cumulative fonctionne au-delà des taux de demandes hello, hello nouvelle tentative par défaut ne peut-être pas suffire, et client de hello lèvera une DocumentClientException avec application de toohello 429 état code.</span><span class="sxs-lookup"><span data-stu-id="4ab20-308">If you have more than one client cumulatively operating above hello request rate, hello default retry behavior may not suffice, and hello client will throw a DocumentClientException with status code 429 toohello application.</span></span> <span data-ttu-id="4ab20-309">Dans ce cas, vous pouvez envisager de la gestion des nouvelles tentatives et logique de l’erreur de votre application des routines de gestion ou augmente le débit réservé de hello pour le conteneur de hello.</span><span class="sxs-lookup"><span data-stu-id="4ab20-309">In cases such as this, you may consider handling retry behavior and logic in your application's error handling routines or increasing hello reserved throughput for hello container.</span></span>

## <span data-ttu-id="4ab20-310"><a id="RequestRateTooLargeAPIforMongoDB"></a> Dépassement des limites de débit réservé dans l’API pour MongoDB</span><span class="sxs-lookup"><span data-stu-id="4ab20-310"><a id="RequestRateTooLargeAPIforMongoDB"></a> Exceeding reserved throughput limits in API for MongoDB</span></span>
<span data-ttu-id="4ab20-311">Les applications qui dépassent les unités de demande hello configuré pour une collection vont être activées jusqu'à ce que le débit de hello devient inférieur au niveau de hello réservé.</span><span class="sxs-lookup"><span data-stu-id="4ab20-311">Applications that exceed hello provisioned request units for a collection will be throttled until hello rate drops below hello reserved level.</span></span> <span data-ttu-id="4ab20-312">En cas d’une limitation de bande passante, hello principal se termine manière préemptive demande hello avec un *16500* code d’erreur - *trop grand nombre de demandes*.</span><span class="sxs-lookup"><span data-stu-id="4ab20-312">When a throttle occurs, hello backend will preemptively end hello request with a *16500* error code - *Too Many Requests*.</span></span> <span data-ttu-id="4ab20-313">Par défaut, les API pour MongoDB va retenter automatiquement des heures de too10 avant de retourner un *trop grand nombre de demandes* code d’erreur.</span><span class="sxs-lookup"><span data-stu-id="4ab20-313">By default, API for MongoDB will automatically retry up too10 times before returning a *Too Many Requests* error code.</span></span> <span data-ttu-id="4ab20-314">Si vous recevez plusieurs *trop grand nombre de demandes* codes d’erreur, vous pouvez envisager l’ajout comportement des nouvelles tentatives dans Gestion d’erreur de votre application routines ou [augmente le débit réservé de hello pour collection de hello](set-throughput.md).</span><span class="sxs-lookup"><span data-stu-id="4ab20-314">If you are receiving many *Too Many Requests* error codes, you may consider either adding retry behavior in your application's error handling routines or [increasing hello reserved throughput for hello collection](set-throughput.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ab20-315">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4ab20-315">Next steps</span></span>
<span data-ttu-id="4ab20-316">toolearn en savoir plus sur le débit réservé avec les bases de données de base de données Azure Cosmos, Explorez ces ressources :</span><span class="sxs-lookup"><span data-stu-id="4ab20-316">toolearn more about reserved throughput with Azure Cosmos DB databases, explore these resources:</span></span>

* [<span data-ttu-id="4ab20-317">Tarification de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="4ab20-317">Azure Cosmos DB pricing</span></span>](https://azure.microsoft.com/pricing/details/cosmos-db/)
* [<span data-ttu-id="4ab20-318">Partitionnement, clés de partition et mise à l’échelle dans Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="4ab20-318">Partitioning data in Azure Cosmos DB</span></span>](partition-data.md)

<span data-ttu-id="4ab20-319">toolearn savoir plus sur la base de données Azure Cosmos, consultez hello Azure Cosmos DB [documentation](https://azure.microsoft.com/documentation/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="4ab20-319">toolearn more about Azure Cosmos DB, see hello Azure Cosmos DB [documentation](https://azure.microsoft.com/documentation/services/cosmos-db/).</span></span> 

<span data-ttu-id="4ab20-320">tooget en main de l’échelle et des tests de performances avec la base de données Azure Cosmos, consultez [test de performances et montée en puissance avec la base de données Azure Cosmos](performance-testing.md).</span><span class="sxs-lookup"><span data-stu-id="4ab20-320">tooget started with scale and performance testing with Azure Cosmos DB, see [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md).</span></span>

[1]: ./media/request-units/queryexplorer.png 
[2]: ./media/request-units/RUEstimatorUpload.png
[3]: ./media/request-units/RUEstimatorDocuments.png
[4]: ./media/request-units/RUEstimatorResults.png
[5]: ./media/request-units/RUCalculator2.png
[6]: ./media/request-units/api-for-mongodb-metrics.png
