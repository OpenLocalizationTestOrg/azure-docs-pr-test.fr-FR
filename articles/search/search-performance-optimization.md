---
title: "Considérations de performances et l’optimisation de la recherche aaaAzure | Documents Microsoft"
description: "Réglage des performances d’Azure Search et configuration d’une mise à l’échelle optimale"
services: search
documentationcenter: 
author: LiamCavanagh
manager: pablocas
editor: 
ms.assetid: 4d3cd864-29d2-4921-be0d-a3f1a819de46
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: liamca
ms.openlocfilehash: 725149ba32773ab6b4c9d4b441424aba78db7c42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-search-performance-and-optimization-considerations"></a><span data-ttu-id="fed93-103">Considérations sur les performances et l’optimisation d’Azure Search</span><span class="sxs-lookup"><span data-stu-id="fed93-103">Azure Search performance and optimization considerations</span></span>
<span data-ttu-id="fed93-104">Une expérience de recherche est une clé toosuccess nombreux mobile et des applications web.</span><span class="sxs-lookup"><span data-stu-id="fed93-104">A great search experience is a key toosuccess for many mobile and web applications.</span></span> <span data-ttu-id="fed93-105">Immobilier, à partir de catalogues de tooonline tooused voiture places de marché, une recherche rapide et résultats pertinents affectera expérience hello.</span><span class="sxs-lookup"><span data-stu-id="fed93-105">From real estate, tooused car marketplaces tooonline catalogs, fast search and relevant results will affect hello customer experience.</span></span> <span data-ttu-id="fed93-106">Ce document est prévue toohelp découvrir les meilleures pratiques pour comment hello tooget parti d’Azure Search, en particulier pour des scénarios avancés avec sophistiqué configuration requise pour l’évolutivité, de prise en charge multilingue ou de classement personnalisé.</span><span class="sxs-lookup"><span data-stu-id="fed93-106">This document is intended toohelp you discover best practices for how tooget hello most out of Azure Search, especially for advanced scenarios with sophisticated requirements for scalability, multi-language support, or custom ranking.</span></span>  <span data-ttu-id="fed93-107">En outre, ce document détaille les mécanismes internes et décrit les approches qui fonctionnent efficacement dans les applications clientes réelles.</span><span class="sxs-lookup"><span data-stu-id="fed93-107">In addition, this document outlines internals and covers approaches that work effectively in real-world customer apps.</span></span>

## <a name="performance-and-scale-tuning-for-search-services"></a><span data-ttu-id="fed93-108">Réglage des performances et de la mise à l’échelle pour les services de recherche</span><span class="sxs-lookup"><span data-stu-id="fed93-108">Performance and scale tuning for Search services</span></span>
<span data-ttu-id="fed93-109">Nous sommes tous les moteurs toosearch utilisés tels que Bing et Google et hello hautes performances qu’elles proposent.</span><span class="sxs-lookup"><span data-stu-id="fed93-109">We are all used toosearch engines such as Bing and Google and hello high performance they offer.</span></span>  <span data-ttu-id="fed93-110">Par conséquent, lorsque les clients utilisent la fonction de recherche de votre application mobile ou web, ils s’attendent à bénéficier des mêmes performances.</span><span class="sxs-lookup"><span data-stu-id="fed93-110">As a result, when customers use your search-enabled web or mobile application, they will expect similar performance characteristics.</span></span>  <span data-ttu-id="fed93-111">Lors de l’optimisation des performances de la recherche, une des approches de meilleures hello est toofocus sur la latence, ce qui est le temps hello toocomplete et retourner les résultats d’une requête est.</span><span class="sxs-lookup"><span data-stu-id="fed93-111">When optimizing for search performance, one of hello best approaches is toofocus on latency, which is hello time a query takes toocomplete and return results.</span></span>  <span data-ttu-id="fed93-112">Lors de l’optimisation de la latence de recherche, il est important de noter les points suivants :</span><span class="sxs-lookup"><span data-stu-id="fed93-112">When optimizing for search latency it is important to:</span></span>

1. <span data-ttu-id="fed93-113">Choisir une latence sur la cible (ou la durée maximale) qu’une demande de recherche par défaut doit prendre toocomplete.</span><span class="sxs-lookup"><span data-stu-id="fed93-113">Pick a target latency (or maximum amount of time) that a typical search request should take toocomplete.</span></span>
2. <span data-ttu-id="fed93-114">Créer et tester une charge de travail réelle par rapport à votre service de recherche avec un jeu de données réaliste de toomeasure ces taux de latence.</span><span class="sxs-lookup"><span data-stu-id="fed93-114">Create and test a real workload against your search service with a realistic dataset toomeasure these latency rates.</span></span>
3. <span data-ttu-id="fed93-115">Démarrer avec un petit nombre de requêtes par seconde (QPS) et continuer le nombre de hello tooincrease exécutée dans un test de hello tant que requête hello latence inférieure hello défini par la latence sur la cible.</span><span class="sxs-lookup"><span data-stu-id="fed93-115">Start with a low number of queries per second (QPS) and continue tooincrease hello number executed in hello test until hello query latency drops below hello defined target latency.</span></span>  <span data-ttu-id="fed93-116">Il s’agit d’un toohelp banc d’essai important que prévoir l’échelle à mesure que votre application augmente l’utilisation.</span><span class="sxs-lookup"><span data-stu-id="fed93-116">This is an important benchmark toohelp you plan for scale as your application grows in usage.</span></span>
4. <span data-ttu-id="fed93-117">Dans la mesure du possible, réutilisez les connexions HTTP.</span><span class="sxs-lookup"><span data-stu-id="fed93-117">Wherever possible, reuse HTTP connections.</span></span>  <span data-ttu-id="fed93-118">Si vous utilisez hello Azure Search .NET SDK, cela signifie que vous devez réutiliser une instance ou [SearchIndexClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.searchindexclient) d’instance et si vous utilisez hello API REST, vous devez le réutiliser un client HTTP unique.</span><span class="sxs-lookup"><span data-stu-id="fed93-118">If you are using hello Azure Search .NET SDK, this means you should reuse an instance or [SearchIndexClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.searchindexclient) instance, and if you are using hello REST API, you should reuse a single HttpClient.</span></span>

<span data-ttu-id="fed93-119">Lors de la création de ces charges de travail de test, il existe certaines caractéristiques de tookeep Azure Search à l’esprit :</span><span class="sxs-lookup"><span data-stu-id="fed93-119">While creating these test workloads, there are some characteristics of Azure Search tookeep in mind:</span></span>

1. <span data-ttu-id="fed93-120">Il est possible toopush autant les requêtes de recherche à la fois, que les ressources de hello disponibles dans votre service Azure Search seront saturé au point.</span><span class="sxs-lookup"><span data-stu-id="fed93-120">It is possible toopush so many search queries at one time, that hello resources available in your Azure Search service will be overwhelmed.</span></span>  <span data-ttu-id="fed93-121">Dans ce cas, vous verrez les codes de réponse HTTP 503.</span><span class="sxs-lookup"><span data-stu-id="fed93-121">When this happens, you will see HTTP 503 response codes.</span></span>  <span data-ttu-id="fed93-122">Pour cette raison, il est meilleure toostart avec différentes plages de recherche les demandes toosee hello différences dans le taux de latence que vous ajoutez plus de requêtes de recherche.</span><span class="sxs-lookup"><span data-stu-id="fed93-122">For this reason, it is best toostart with various ranges of search requests toosee hello differences in latency rates as you add more search requests.</span></span>
2. <span data-ttu-id="fed93-123">Le téléchargement de contenu tooAzure recherche aura un impact sur hello les performances globales et la latence de hello service Azure Search.</span><span class="sxs-lookup"><span data-stu-id="fed93-123">Uploading of content tooAzure Search will impact hello overall performance and latency of hello Azure Search service.</span></span>  <span data-ttu-id="fed93-124">Si vous pensez que les données toosend tandis que les utilisateurs effectuant des recherches, il est important tootake cette charge de travail en compte dans vos tests.</span><span class="sxs-lookup"><span data-stu-id="fed93-124">If you expect toosend data while users are performing searches, it is important tootake this workload into account in your tests.</span></span>
3. <span data-ttu-id="fed93-125">Pas de chaque requête de recherche effectuera à hello même les niveaux de performance.</span><span class="sxs-lookup"><span data-stu-id="fed93-125">Not every search query will perform at hello same performance levels.</span></span>  <span data-ttu-id="fed93-126">Par exemple, une recherche de document ou une suggestion de recherche s’exécutera plus rapidement qu’une requête comportant un nombre important de facettes et les filtres.</span><span class="sxs-lookup"><span data-stu-id="fed93-126">For example, a document lookup or search suggestion will typically perform faster than a query with a significant number of facets and filters.</span></span>  <span data-ttu-id="fed93-127">Il s’agit des meilleures tootake hello différentes requêtes souhaitées toosee en compte lors de la génération de vos tests.</span><span class="sxs-lookup"><span data-stu-id="fed93-127">It is best tootake hello various queries you expect toosee into account when building your tests.</span></span>  
4. <span data-ttu-id="fed93-128">Variation de demandes de recherche est importante, car si vous exécutez en permanence hello les mêmes requêtes de recherche, mise en cache des données de performances toomake de début recherche mieux qu’il peut avec une requête plus disparates défini.</span><span class="sxs-lookup"><span data-stu-id="fed93-128">Variation of search requests is important because if you continually execute hello same search requests, caching of data will start toomake performance look better than it might with a more disparate query set.</span></span>

> [!NOTE]
> <span data-ttu-id="fed93-129">[Test de charge Visual Studio](https://www.visualstudio.com/docs/test/performance-testing/run-performance-tests-app-before-release) est un tooperform très bonne façon votre test d’évaluation teste car elle vous permet les demandes tooexecute HTTP que vous avez besoin pour l’exécution de requêtes sur Azure Search et Active la parallélisation des requêtes.</span><span class="sxs-lookup"><span data-stu-id="fed93-129">[Visual Studio Load Testing](https://www.visualstudio.com/docs/test/performance-testing/run-performance-tests-app-before-release) is a really good way tooperform your benchmark tests as it allows you tooexecute HTTP requests as you would need for executing queries against Azure Search and enables parallelization of requests.</span></span>
> 
> 

## <a name="scaling-azure-search-for-high-query-rates-and-throttled-requests"></a><span data-ttu-id="fed93-130">Mise à l’échelle d’Azure Search pour obtenir des taux de requêtes élevés et des requêtes limitées</span><span class="sxs-lookup"><span data-stu-id="fed93-130">Scaling Azure Search for high query rates and throttled requests</span></span>
<span data-ttu-id="fed93-131">Lorsque vous recevez trop de demandes d’accélérée ou dépassez votre taux de latence cible à partir d’une charge accrue de requête, vous pouvez consulter le taux de latence toodecrease de deux manières :</span><span class="sxs-lookup"><span data-stu-id="fed93-131">When you are receiving too many throttled requests or exceed your target latency rates from an increased query load, you can look toodecrease latency rates in one of two ways:</span></span>

1. <span data-ttu-id="fed93-132">**Augmentation des réplicas :** un réplica est comme une copie de vos données, ce qui permet à Azure Search tooload équilibrer les demandes sur hello plusieurs copies.</span><span class="sxs-lookup"><span data-stu-id="fed93-132">**Increase Replicas:**  A replica is like a copy of your data allowing Azure Search tooload balance requests against hello multiple copies.</span></span>  <span data-ttu-id="fed93-133">Tous les équilibrage de charge et la réplication des données entre des réplicas est gérée par Azure Search, et vous pouvez modifier le nombre de hello de réplicas allouée pour votre service à tout moment.</span><span class="sxs-lookup"><span data-stu-id="fed93-133">All load balancing and replication of data across replicas is managed by Azure Search and you can alter hello number of replicas allocated for your service at any time.</span></span>  <span data-ttu-id="fed93-134">Vous pouvez allouer des réplicas too12 dans un service de recherche Standard et 3 dans un service de recherche de base.</span><span class="sxs-lookup"><span data-stu-id="fed93-134">You can allocate up too12 replicas in a Standard search service and 3 replicas in a Basic search service.</span></span> <span data-ttu-id="fed93-135">Les réplicas peuvent être ajusté à partir de hello [portail Azure](search-create-service-portal.md) ou [PowerShell](search-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="fed93-135">Replicas can be adjusted either from hello [Azure portal](search-create-service-portal.md) or [PowerShell](search-manage-powershell.md).</span></span>
2. <span data-ttu-id="fed93-136">**Augmenter le niveau de recherche :** la Recherche Azure est fournie avec un certain [nombre de niveaux](https://azure.microsoft.com/pricing/details/search/) et chacun de ces niveaux offre différents niveaux de performances.</span><span class="sxs-lookup"><span data-stu-id="fed93-136">**Increase Search Tier:**  Azure Search comes in a [number of tiers](https://azure.microsoft.com/pricing/details/search/) and each of these tiers offers different levels of performance.</span></span>  <span data-ttu-id="fed93-137">Dans certains cas, vous avez peut-être nombreuses requêtes ce niveau hello que vous êtes sur ne peut pas fournir les vitesses de transmission suffisamment faible latence, même lorsque les réplicas sont surexploités.  Dans ce cas, vous souhaiterez tooconsider tirant parti de niveaux de recherche supérieure hello comme niveau d’Azure Search S3 hello qui convient pour les scénarios avec un grand nombre de documents et les charges de travail très élevé de requête.</span><span class="sxs-lookup"><span data-stu-id="fed93-137">In some cases, you may have so many queries that hello tier you are on cannot provide sufficiently low latency rates, even when replicas are maxed out.  In this case, you may want tooconsider leveraging one of hello higher search tiers such as hello Azure Search S3 tier that is well suited for scenarios with large numbers of documents and extremely high query workloads.</span></span>

## <a name="scaling-azure-search-for-slow-individual-queries"></a><span data-ttu-id="fed93-138">Mise à l’échelle d’Azure Search pour des requêtes individuelles lentes</span><span class="sxs-lookup"><span data-stu-id="fed93-138">Scaling Azure Search for slow individual queries</span></span>
<span data-ttu-id="fed93-139">Une autre raison pourquoi les taux de latence peuvent être lents est à partir d’une seule requête prend trop de temps toocomplete.</span><span class="sxs-lookup"><span data-stu-id="fed93-139">Another reason why latency rates can be slow is from a single query taking too long toocomplete.</span></span>  <span data-ttu-id="fed93-140">Dans ce cas, l’ajout de réplicas n’améliorera pas les taux de latence.</span><span class="sxs-lookup"><span data-stu-id="fed93-140">In this case, adding replicas will not improve latency rates.</span></span>  <span data-ttu-id="fed93-141">Il existe alors deux options possibles :</span><span class="sxs-lookup"><span data-stu-id="fed93-141">For this case there are two options available:</span></span>

1. <span data-ttu-id="fed93-142">**Augmenter les partitions** Une partition est un mécanisme permettant de répartir vos données sur des ressources supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="fed93-142">**Increase Partitions** A partition is a mechanism for splitting your data across extra resources.</span></span>  <span data-ttu-id="fed93-143">Pour cette raison, lorsque vous ajoutez une deuxième partition, vos données sont divisées en deux.</span><span class="sxs-lookup"><span data-stu-id="fed93-143">For this reason, when you add a second partition, your data gets split into two.</span></span>  <span data-ttu-id="fed93-144">Une troisième partition divise votre index en trois, etc.  Cela a également effet hello que dans certains cas, les requêtes lentes seront exécutera plus rapidement en raison de la parallélisation toohello de calcul.</span><span class="sxs-lookup"><span data-stu-id="fed93-144">A third partition splits your index into three, etc.  This also has hello effect that in some cases, slow queries will perform faster due toohello parallelization of computation.</span></span>  <span data-ttu-id="fed93-145">Il existe quelques exemples dans lesquels cette parallélisation fonctionne très bien avec des requêtes affichant une faible sélectivité.</span><span class="sxs-lookup"><span data-stu-id="fed93-145">There are a few examples of where we have seen this parallelization work extremely well with queries that have low selectivity queries.</span></span>  <span data-ttu-id="fed93-146">Il s’agit de requêtes qui correspondent au nombre de documents ou lorsque des facettes doit tooprovide compte sur un grand nombre de documents.</span><span class="sxs-lookup"><span data-stu-id="fed93-146">This consists of queries that match many documents or when faceting needs tooprovide counts over large numbers of documents.</span></span>  <span data-ttu-id="fed93-147">Dans la mesure où il existe qu'un grand nombre de calculs nécessaires pertinence de hello tooscore de documents de hello toocount hello numéros ou des documents, l’ajout de partitions supplémentaires peuvent aider à tooprovide des calculs supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="fed93-147">Since there is a lot of computation needed tooscore hello relevancy of hello documents or toocount hello numbers of documents, adding extra partitions can help tooprovide additional computation.</span></span>  
   
   <span data-ttu-id="fed93-148">Il peut y avoir un maximum de 12 partitions dans le service de recherche Standard et 1 partition dans le service de recherche de base hello.</span><span class="sxs-lookup"><span data-stu-id="fed93-148">There can be a maximum of 12 partitions in Standard search service and 1 partition in hello basic search service.</span></span>  <span data-ttu-id="fed93-149">Les partitions peuvent être ajustés à partir de hello [portail Azure](search-create-service-portal.md) ou [PowerShell](search-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="fed93-149">Partitions can be adjusted either from hello [Azure portal](search-create-service-portal.md) or [PowerShell](search-manage-powershell.md).</span></span>
2. <span data-ttu-id="fed93-150">**Champs de cardinalité élevée de limitation :** un champ de cardinalité élevée consiste en un facetable filtrable champ qui a un nombre important de valeurs uniques et par conséquent, adopte un grand nombre de ressources toocompute résultats.</span><span class="sxs-lookup"><span data-stu-id="fed93-150">**Limit High Cardinality Fields:** A high cardinality field consists of a facetable or filterable field that has a significant number of unique values, and as a result, takes a lot of resources toocompute results over.</span></span>   <span data-ttu-id="fed93-151">Par exemple, la définition d’un champ de Description ou un ID de produit comme filterable/facetable créerait une cardinalité élevée, car la plupart des valeurs hello à partir du document toodocument est unique.</span><span class="sxs-lookup"><span data-stu-id="fed93-151">For example, setting a Product ID or Description field as facetable/filterable would make for high cardinality because most of hello values from document toodocument are unique.</span></span> <span data-ttu-id="fed93-152">Dans la mesure du possible, limiter le nombre de hello de champs de cardinalité élevée.</span><span class="sxs-lookup"><span data-stu-id="fed93-152">Wherever possible, limit hello number of high cardinality fields.</span></span>
3. <span data-ttu-id="fed93-153">**Niveau de recherche d’augmentation :** remontant tooa plus élevé de niveau d’Azure Search peut être des performances de tooimprove un autre moyen de requêtes lentes.</span><span class="sxs-lookup"><span data-stu-id="fed93-153">**Increase Search Tier:**  Moving up tooa higher Azure Search tier can be another way tooimprove performance of slow queries.</span></span>  <span data-ttu-id="fed93-154">Chaque niveau supérieur propose également un processeur plus rapide et plus de mémoire, ce qui peut avoir un impact positif sur les performances des requêtes.</span><span class="sxs-lookup"><span data-stu-id="fed93-154">Each higher tier also provides faster CPU’s and more memory which can have a positive impact on query performance.</span></span>

## <a name="scaling-for-availability"></a><span data-ttu-id="fed93-155">Mise à l’échelle pour la disponibilité</span><span class="sxs-lookup"><span data-stu-id="fed93-155">Scaling for availability</span></span>
<span data-ttu-id="fed93-156">Les réplicas permettent non seulement de réduire la latence des requêtes mais ils peuvent également offrir une plus grande disponibilité.</span><span class="sxs-lookup"><span data-stu-id="fed93-156">Replicas not only help reduce query latency but can also allow for high availability.</span></span>  <span data-ttu-id="fed93-157">Avec un seul réplica, attendez-vous à des temps morts périodiques d’échéance tooserver redémarrages après les mises à jour logicielles ou d’autres événements de maintenance qui seront produit.</span><span class="sxs-lookup"><span data-stu-id="fed93-157">With a single replica, you should expect periodic downtime due tooserver reboots after software updates or for other maintenance events that will occur.</span></span>  <span data-ttu-id="fed93-158">Par conséquent, il est important tooconsider si votre application requiert une haute disponibilité des recherches (requêtes) ainsi que les écritures (événements d’indexation).</span><span class="sxs-lookup"><span data-stu-id="fed93-158">As a result, it is important tooconsider if your application requires high availability of searches (queries) as well as writes (indexing events).</span></span>  <span data-ttu-id="fed93-159">Azure Search offre des options de contrat SLA sur tous les hello services de recherche avec hello suivant d’attributs :</span><span class="sxs-lookup"><span data-stu-id="fed93-159">Azure Search offers SLA options on all hello paid search offerings with hello following attributes:</span></span>

* <span data-ttu-id="fed93-160">2 réplicas pour la haute disponibilité des charges de travail en lecture seule (requêtes)</span><span class="sxs-lookup"><span data-stu-id="fed93-160">2 replicas for high availability of read-only workloads (queries)</span></span>
* <span data-ttu-id="fed93-161">3 réplicas (ou plus) pour la haute disponibilité des charges de travail en lecture-écriture (requêtes et indexation)</span><span class="sxs-lookup"><span data-stu-id="fed93-161">3 or more replicas for high availability of read-write workloads (queries and indexing)</span></span>

<span data-ttu-id="fed93-162">Pour plus d’informations, visitez hello [contrat de niveau de Service de recherche Azure](https://azure.microsoft.com/support/legal/sla/search/v1_0/).</span><span class="sxs-lookup"><span data-stu-id="fed93-162">For more details on this, please visit hello [Azure Search Service Level Agreement](https://azure.microsoft.com/support/legal/sla/search/v1_0/).</span></span>

<span data-ttu-id="fed93-163">Étant donné que les réplicas sont des copies de vos données, ayant plusieurs réplicas permet de redémarrages d’ordinateur Azure Search toodo et toobe toocontinue exécutée sur des requêtes de maintenance par rapport à un réplica à un moment tout en autorisant hello autres réplicas.</span><span class="sxs-lookup"><span data-stu-id="fed93-163">Since replicas are copies of your data, having multiple replicas allows Azure Search toodo machine reboots and maintenance against one replica at a time while allowing queries toocontinue toobe executed against hello other replicas.</span></span>  <span data-ttu-id="fed93-164">Pour cette raison, vous devez également tooconsider comment ce temps mort peut affecter les requêtes hello qui maintenant ont toobe exécutée sur une seule copie de moins de données de hello.</span><span class="sxs-lookup"><span data-stu-id="fed93-164">For that reason, you will also need tooconsider how this downtime may impact hello queries that now have toobe executed against one less copy of hello data.</span></span>

## <a name="scaling-geo-distributed-workloads-and-provide-geo-redundancy"></a><span data-ttu-id="fed93-165">Mise à l’échelle de charges de travail géo-distribuées et géo-redondance</span><span class="sxs-lookup"><span data-stu-id="fed93-165">Scaling geo-distributed workloads and provide geo-redundancy</span></span>
<span data-ttu-id="fed93-166">Pour les charges de travail géo-distribué, vous constaterez que les utilisateurs trouve loin d’être de centre de données hello héberge votre service Azure Search ont des taux de latence plus élevées.</span><span class="sxs-lookup"><span data-stu-id="fed93-166">For geo-distributed workloads, you will find that users located far from hello data center where your Azure Search service is hosted will have higher latency rates.</span></span>  <span data-ttu-id="fed93-167">Pour cette raison, il est souvent important toohave recherche plusieurs services dans des régions qui se trouvent dans les utilisateurs de toothese proximité plus proche.</span><span class="sxs-lookup"><span data-stu-id="fed93-167">For this reason, it is often important toohave multiple search services in regions that are in closer proximity toothese users.</span></span>  <span data-ttu-id="fed93-168">Azure Search ne fournit pas actuellement une méthode automatisée des index de recherche de Azure géo-réplication entre les régions, mais il existe quelques techniques qui peuvent être utilisés que peuvent rendre cette tooimplement simple de processus et à gérer.</span><span class="sxs-lookup"><span data-stu-id="fed93-168">Azure Search does not currently provide an automated method of geo-replicating Azure Search indexes across regions, but there are some techniques that can be used that can make this process simple tooimplement and manage.</span></span> <span data-ttu-id="fed93-169">Ils sont présentés dans hello sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="fed93-169">These are outlined in hello next few sections.</span></span>

<span data-ttu-id="fed93-170">l’objectif d’un ensemble de géo-distribué de services de recherche Hello est toohave deux ou plusieurs index disponibles dans deux ou plusieurs régions où un utilisateur sera routé service Azure Search toohello qui fournit la latence la plus faible de hello comme dans cet exemple :</span><span class="sxs-lookup"><span data-stu-id="fed93-170">hello goal of a geo-distributed set of search services is toohave two or more indexes available in two or more regions where a user will be routed toohello Azure Search service that provides hello lowest latency as seen in this example:</span></span>

   ![Tableau croisé des services par région][1]

### <a name="keeping-data-in-sync-across-multiple-azure-search-services"></a><span data-ttu-id="fed93-172">Synchronisation des données entre plusieurs services Azure Search</span><span class="sxs-lookup"><span data-stu-id="fed93-172">Keeping data in sync across multiple Azure Search services</span></span>
<span data-ttu-id="fed93-173">Il existe deux options pour conserver vos services de recherche distribuée synchronisés qui consistent à l’aide de hello [Azure Search Indexer](search-indexer-overview.md) ou hello API de Push (également appelée tooas hello [API REST Azure Search](https://docs.microsoft.com/rest/api/searchservice/)).</span><span class="sxs-lookup"><span data-stu-id="fed93-173">There are two options for keeping your distributed search services in sync which consist of either using hello [Azure Search Indexer](search-indexer-overview.md) or hello Push API (also referred tooas hello [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/)).</span></span>  

### <a name="azure-search-indexers"></a><span data-ttu-id="fed93-174">Indexeurs Azure Search</span><span class="sxs-lookup"><span data-stu-id="fed93-174">Azure Search Indexers</span></span>
<span data-ttu-id="fed93-175">Si vous utilisez hello indexeur de recherche Azure, vous importez déjà des modifications de données à partir d’une banque de données centrale telles que la base de données SQL Azure ou base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="fed93-175">If you are using hello Azure Search Indexer, you are already importing data changes from a central datastore such as Azure SQL DB or Azure Cosmos DB.</span></span> <span data-ttu-id="fed93-176">Lorsque vous créez une nouvelle recherche le Service, vous simplement également créer un nouvel indexeur de recherche Azure pour ce service qui toothis points même magasin de données.</span><span class="sxs-lookup"><span data-stu-id="fed93-176">When you create a new search Service, you simply also create a new Azure Search Indexer for that service that points toothis same datastore.</span></span> <span data-ttu-id="fed93-177">De cette façon, chaque fois que les nouvelles modifications entrent en magasin de données hello, elles seront indexés par hello plusieurs indexeurs.</span><span class="sxs-lookup"><span data-stu-id="fed93-177">That way, whenever new changes come into hello data store, they will then be indexed by hello various Indexers.</span></span>  

<span data-ttu-id="fed93-178">Voici à quoi ressemblerait une telle architecture.</span><span class="sxs-lookup"><span data-stu-id="fed93-178">Here is an example of what that architecture would look like.</span></span>

   ![Source de données unique avec indexeur distribué et combinaisons de service][2]

### <a name="push-api"></a><span data-ttu-id="fed93-180">API push</span><span class="sxs-lookup"><span data-stu-id="fed93-180">Push API</span></span>
<span data-ttu-id="fed93-181">Si vous utilisez l’API de Push Azure Search hello trop[mettre à jour le contenu de votre index Azure Search](https://docs.microsoft.com/rest/api/searchservice/update-index), vous pouvez synchroniser vos différents services de recherche en envoyant des services de recherche de modifications tooall chaque fois qu’une mise à jour est requise.</span><span class="sxs-lookup"><span data-stu-id="fed93-181">If you are using hello Azure Search Push API too[update content in your Azure Search index](https://docs.microsoft.com/rest/api/searchservice/update-index), you can keep your various search services in sync by pushing changes tooall search services whenever an update is required.</span></span>  <span data-ttu-id="fed93-182">Ce faisant, il est important toomake que toohandle cas où un service de recherche de tooone de mise à jour échoue et un ou plusieurs des mises à jour réussissent.</span><span class="sxs-lookup"><span data-stu-id="fed93-182">When doing this it is important toomake sure toohandle cases where an update tooone search service fails and one or more updates succeed.</span></span>

## <a name="leveraging-azure-traffic-manager"></a><span data-ttu-id="fed93-183">Utilisation d’Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="fed93-183">Leveraging Azure Traffic Manager</span></span>
<span data-ttu-id="fed93-184">[Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md) vous permet de tooroute demandes toomultiple géo-localisés des sites Web qui sont sauvegardés puis par plusieurs Services de recherche Azure.</span><span class="sxs-lookup"><span data-stu-id="fed93-184">[Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md) allows you tooroute requests toomultiple geo-located websites that are then backed by multiple Azure Search Services.</span></span>  <span data-ttu-id="fed93-185">Un avantage de hello Traffic Manager est qu’il peut détecter tooensure Azure Search qu’il est disponible et acheminer des services de recherche tooalternate les utilisateurs dans l’événement hello du temps d’arrêt.</span><span class="sxs-lookup"><span data-stu-id="fed93-185">One advantage of hello Traffic Manager is that it can probe Azure Search tooensure that it is available and route users tooalternate search services in hello event of downtime.</span></span>  <span data-ttu-id="fed93-186">En outre, si vous routez les demandes de recherche via les Sites Web Azure, Azure Traffic Manager vous permet de cas de solde tooload où le site Web de hello est haut, mais pas Azure Search.</span><span class="sxs-lookup"><span data-stu-id="fed93-186">In addition, if you are routing search requests through Azure Web Sites, Azure Traffic Manager allows you tooload balance cases where hello Website is up but not Azure Search.</span></span>  <span data-ttu-id="fed93-187">Voici un exemple d’architecture hello qui tire parti de Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="fed93-187">Here is an example of what hello architecture that leverages Traffic Manager.</span></span>

   ![Tableau croisé des services par région, avec Traffic Manager central][3]

## <a name="monitoring-performance"></a><span data-ttu-id="fed93-189">Analyse des performances</span><span class="sxs-lookup"><span data-stu-id="fed93-189">Monitoring performance</span></span>
<span data-ttu-id="fed93-190">Azure Search offre hello capacité tooanalyze et analysent hello les performances de votre service via [recherche le trafic Analytique (STA)](search-traffic-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="fed93-190">Azure Search offers hello ability tooanalyze and monitor hello performance of your service through [Search Traffic Analytics (STA)](search-traffic-analytics.md).</span></span> <span data-ttu-id="fed93-191">Via STA, vous pouvez éventuellement enregistrer les opérations de recherche individuelles hello ainsi que compte de stockage Azure tooan des mesures agrégées qui peut être traitée pour l’analyse ou de visualisation dans Power BI.</span><span class="sxs-lookup"><span data-stu-id="fed93-191">Through STA, you can optionally log hello individual search operations as well as aggregated metrics tooan Azure Storage account that can then be processed for analysis or visualized in Power BI.</span></span>  <span data-ttu-id="fed93-192">À l’aide de mesures STA, vous pouvez afficher les statistiques de performances comme le nombre moyen de requêtes ou les temps de réponse.</span><span class="sxs-lookup"><span data-stu-id="fed93-192">Using STA metrics, you can review performance statistics such as average number of queries or query response times.</span></span>  <span data-ttu-id="fed93-193">Enregistrement de l’opération hello permet en outre, toodrill dans les détails des opérations de recherche spécifique.</span><span class="sxs-lookup"><span data-stu-id="fed93-193">In addition, hello operation logging allows you toodrill into details of specific search operations.</span></span>

<span data-ttu-id="fed93-194">STA est un outil précieux toounderstand latence des taux à partir de ce point de vue Azure Search.</span><span class="sxs-lookup"><span data-stu-id="fed93-194">STA is a valuable tool toounderstand latency rates from that Azure Search perspective.</span></span>  <span data-ttu-id="fed93-195">Étant donné que les métriques de performances de requête hello connectés sont basés sur le temps de hello toobe entièrement traité dans Azure Search (à partir de hello temps toowhen demandé, il est diffusée) d’une requête est, vous êtes en mesure de toouse ce toodetermine si les problèmes de latence sont de hello service Azure Search côté ou en dehors de hello service, par exemple une latence du réseau.</span><span class="sxs-lookup"><span data-stu-id="fed93-195">Since hello query performance metrics logged are based on hello time a query takes toobe fully processed in Azure Search (from hello time it is requested toowhen it is sent out), you are able toouse this toodetermine if latency issues are from hello Azure Search service side or outside of hello service, such as from network latency.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="fed93-196">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fed93-196">Next steps</span></span>
<span data-ttu-id="fed93-197">toolearn en savoir plus sur hello tarification niveaux et les limites de services pour chacune d’elles, consultez [Service limites dans Azure Search](search-limits-quotas-capacity.md).</span><span class="sxs-lookup"><span data-stu-id="fed93-197">toolearn more about hello pricing tiers and services limits for each one, see [Service limits in Azure Search](search-limits-quotas-capacity.md).</span></span>

<span data-ttu-id="fed93-198">Visitez [planification de la capacité](search-capacity-planning.md) toolearn plus d’informations sur les combinaisons de partition et le réplica.</span><span class="sxs-lookup"><span data-stu-id="fed93-198">Visit [Capacity planning](search-capacity-planning.md) toolearn more about partition and replica combinations.</span></span>

<span data-ttu-id="fed93-199">Pour plus d’extraction sur les performances et toosee des démonstrations de comment tooimplement hello optimisations présentées dans cet article, regardez hello suivant vidéo :</span><span class="sxs-lookup"><span data-stu-id="fed93-199">For more drilldown on performance and toosee some demonstrations of how tooimplement hello optimizations discussed in this article, watch hello following video:</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON319/player]
> 
> 

<!--Image references-->
[1]: ./media/search-performance-optimization/geo-redundancy.png
[2]: ./media/search-performance-optimization/scale-indexers.png
[3]: ./media/search-performance-optimization/geo-search-traffic-mgr.png