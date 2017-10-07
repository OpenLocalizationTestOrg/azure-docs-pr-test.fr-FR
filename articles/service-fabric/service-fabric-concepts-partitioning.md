---
title: services de Service Fabric aaaPartitioning | Documents Microsoft
description: "Décrit comment les services avec état toopartition Service Fabric. Partitions Active le stockage des données sur les ordinateurs locaux hello données et calcul peuvent être mis à l’ensemble."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 3b7248c8-ea92-4964-85e7-6f1291b5cc7b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: msfussell
ms.openlocfilehash: 6ead48716c08f4212535202ee69d169067d5c6d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="partition-service-fabric-reliable-services"></a><span data-ttu-id="18872-104">Partitionnement des services fiables Service Fabric</span><span class="sxs-lookup"><span data-stu-id="18872-104">Partition Service Fabric reliable services</span></span>
<span data-ttu-id="18872-105">Cet article fournit une toohello présentation des concepts de base du partitionnement des services fiables Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="18872-105">This article provides an introduction toohello basic concepts of partitioning Azure Service Fabric reliable services.</span></span> <span data-ttu-id="18872-106">Hello code source utilisé dans l’article de hello est également disponible sur [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span><span class="sxs-lookup"><span data-stu-id="18872-106">hello source code used in hello article is also available on [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span></span>

## <a name="partitioning"></a><span data-ttu-id="18872-107">Partitionnement</span><span class="sxs-lookup"><span data-stu-id="18872-107">Partitioning</span></span>
<span data-ttu-id="18872-108">Le partitionnement n’est pas unique tooService l’ensemble fibre optique.</span><span class="sxs-lookup"><span data-stu-id="18872-108">Partitioning is not unique tooService Fabric.</span></span> <span data-ttu-id="18872-109">En réalité, il s’agit d’un modèle de base de création de services évolutifs.</span><span class="sxs-lookup"><span data-stu-id="18872-109">In fact, it is a core pattern of building scalable services.</span></span> <span data-ttu-id="18872-110">Dans un sens large, nous pouvons considérer comme un concept de la division de l’état (données) de partitionnement et de calcul dans les performances et l’évolutivité de plus petite unités accessible tooimprove.</span><span class="sxs-lookup"><span data-stu-id="18872-110">In a broader sense, we can think about partitioning as a concept of dividing state (data) and compute into smaller accessible units tooimprove scalability and performance.</span></span> <span data-ttu-id="18872-111">Le [partitionnement des données][wikipartition] constitue une forme bien connue de partitionnement.</span><span class="sxs-lookup"><span data-stu-id="18872-111">A well-known form of partitioning is [data partitioning][wikipartition], also known as sharding.</span></span>

### <a name="partition-service-fabric-stateless-services"></a><span data-ttu-id="18872-112">Partitionnement des services sans état Service Fabric</span><span class="sxs-lookup"><span data-stu-id="18872-112">Partition Service Fabric stateless services</span></span>
<span data-ttu-id="18872-113">Pour les services sans état, vous pouvez considérer une partition comme une unité logique contenant une ou plusieurs instances d’un service.</span><span class="sxs-lookup"><span data-stu-id="18872-113">For stateless services, you can think about a partition being a logical unit that contains one or more instances of a service.</span></span> <span data-ttu-id="18872-114">La figure 1 illustre un service sans état avec cinq instances distribuées sur un cluster à l’aide d’une seule partition.</span><span class="sxs-lookup"><span data-stu-id="18872-114">Figure 1 shows a stateless service with five instances distributed across a cluster using one partition.</span></span>

![Service sans état](./media/service-fabric-concepts-partitioning/statelessinstances.png)

<span data-ttu-id="18872-116">Il existe en réalité deux types de solutions de service sans état.</span><span class="sxs-lookup"><span data-stu-id="18872-116">There are really two types of stateless service solutions.</span></span> <span data-ttu-id="18872-117">Hello tout d’abord un est un service qui rend son état persistant en externe, par exemple dans une base de données SQL Azure (par exemple, un site Web qui stocke les données et les informations de session hello).</span><span class="sxs-lookup"><span data-stu-id="18872-117">hello first one is a service that persists its state externally, for example in an Azure SQL database (like a website that stores hello session information and data).</span></span> <span data-ttu-id="18872-118">Hello seconde est services calcul uniquement (comme un réduire en vignettes calculatrice ou image) qui ne gèrent pas tout état persistant.</span><span class="sxs-lookup"><span data-stu-id="18872-118">hello second one is computation-only services (like a calculator or image thumbnailing) that do not manage any persistent state.</span></span>

<span data-ttu-id="18872-119">Dans les deux cas, le partitionnement d’un service sans état constitue un scénario extrêmement rare. L’évolutivité et la disponibilité passent normalement par une augmentation du nombre d’instances.</span><span class="sxs-lookup"><span data-stu-id="18872-119">In either case, partitioning a stateless service is a very rare scenario--scalability and availability are normally achieved by adding more instances.</span></span> <span data-ttu-id="18872-120">Hello uniquement heure tooconsider plusieurs partitions pour les instances de service sans état est lorsque vous devez toomeet spécial routage des demandes.</span><span class="sxs-lookup"><span data-stu-id="18872-120">hello only time you want tooconsider multiple partitions for stateless service instances is when you need toomeet special routing requests.</span></span>

<span data-ttu-id="18872-121">Par exemple, imaginez un cas de figure où des utilisateurs dont les identifiants sont compris dans une certaine plage doivent être uniquement pris en charge par une instance de service particulière.</span><span class="sxs-lookup"><span data-stu-id="18872-121">As an example, consider a case where users with IDs in a certain range should only be served by a particular service instance.</span></span> <span data-ttu-id="18872-122">Un autre exemple de lorsque vous pouvez partitionner un service sans état est lorsque vous avez un backend réellement partitionné (par exemple, un partitionnée SQL de base de données) et que vous souhaitez toocontrol quelle instance de service doit écrire des partitions de base de données toohello--ou effectuer d’autres tâches de préparation dans Hello service sans état nécessitant hello même informations de partitionnement est utilisé dans le service principal hello.</span><span class="sxs-lookup"><span data-stu-id="18872-122">Another example of when you could partition a stateless service is when you have a truly partitioned backend (e.g. a sharded SQL database) and you want toocontrol which service instance should write toohello database shard--or perform other preparation work within hello stateless service that requires hello same partitioning information as is used in hello backend.</span></span> <span data-ttu-id="18872-123">Ces types de scénarios peuvent également être résolus de différentes façons et n’impliquent pas nécessairement un partitionnement du service.</span><span class="sxs-lookup"><span data-stu-id="18872-123">Those types of scenarios can also be solved in different ways and do not necessarily require service partitioning.</span></span>

<span data-ttu-id="18872-124">reste Hello de cette procédure pas à pas se concentre sur les services avec état.</span><span class="sxs-lookup"><span data-stu-id="18872-124">hello remainder of this walkthrough focuses on stateful services.</span></span>

### <a name="partition-service-fabric-stateful-services"></a><span data-ttu-id="18872-125">Partitionnement des services avec état Service Fabric</span><span class="sxs-lookup"><span data-stu-id="18872-125">Partition Service Fabric stateful services</span></span>
<span data-ttu-id="18872-126">Service Fabric rend toodevelop facilement des services évolutifs avec état en offrant un moyen de première classe toopartition état (données).</span><span class="sxs-lookup"><span data-stu-id="18872-126">Service Fabric makes it easy toodevelop scalable stateful services by offering a first-class way toopartition state (data).</span></span> <span data-ttu-id="18872-127">Point de vue conceptuel, vous pouvez considérer une partition d’un service avec état comme une unité d’échelle hautement fiable via [réplicas](service-fabric-availability-services.md) qui sont distribuées et équilibrée entre les nœuds hello dans un cluster.</span><span class="sxs-lookup"><span data-stu-id="18872-127">Conceptually, you can think about a partition of a stateful service as a scale unit that is highly reliable through [replicas](service-fabric-availability-services.md) that are distributed and balanced across hello nodes in a cluster.</span></span>

<span data-ttu-id="18872-128">Partitionnement dans le contexte de hello des services avec état de l’infrastructure de Service, toohello les processus permettant de déterminer qu’une partition de service particulier est chargée pour une partie de l’état du service de hello hello fait référence.</span><span class="sxs-lookup"><span data-stu-id="18872-128">Partitioning in hello context of Service Fabric stateful services refers toohello process of determining that a particular service partition is responsible for a portion of hello complete state of hello service.</span></span> <span data-ttu-id="18872-129">(Comme indiqué précédemment, une partition est un ensemble de [réplicas](service-fabric-availability-services.md)).</span><span class="sxs-lookup"><span data-stu-id="18872-129">(As mentioned before, a partition is a set of [replicas](service-fabric-availability-services.md)).</span></span> <span data-ttu-id="18872-130">Une bonne chose sur le Service Fabric est qu’il place les partitions hello sur différents nœuds.</span><span class="sxs-lookup"><span data-stu-id="18872-130">A great thing about Service Fabric is that it places hello partitions on different nodes.</span></span> <span data-ttu-id="18872-131">Cela leur permet de limite de ressource du nœud toogrow tooa.</span><span class="sxs-lookup"><span data-stu-id="18872-131">This allows them toogrow tooa node's resource limit.</span></span> <span data-ttu-id="18872-132">Comme les données de salutation besoins augmentent, la croissance des partitions et Service Fabric rééquilibrage des partitions sur les nœuds.</span><span class="sxs-lookup"><span data-stu-id="18872-132">As hello data needs grow, partitions grow, and Service Fabric rebalances partitions across nodes.</span></span> <span data-ttu-id="18872-133">Cela garantit hello suite à une utilisation efficace des ressources matérielles.</span><span class="sxs-lookup"><span data-stu-id="18872-133">This ensures hello continued efficient use of hardware resources.</span></span>

<span data-ttu-id="18872-134">toogive vous obtenir un exemple, vous dites commencent par un cluster à 5 nœuds et un service qui est configuré toohave 10 partitions et une cible de trois réplicas.</span><span class="sxs-lookup"><span data-stu-id="18872-134">toogive you an example, say you start with a 5-node cluster and a service that is configured toohave 10 partitions and a target of three replicas.</span></span> <span data-ttu-id="18872-135">Dans ce cas, l’infrastructure de Service serait équilibrer et distribuer des réplicas de hello sur le cluster de hello--et vous obtenez des deux principaux [réplicas](service-fabric-availability-services.md) par nœud.</span><span class="sxs-lookup"><span data-stu-id="18872-135">In this case, Service Fabric would balance and distribute hello replicas across hello cluster--and you would end up with two primary [replicas](service-fabric-availability-services.md) per node.</span></span>
<span data-ttu-id="18872-136">Si vous devez maintenant tooscale des nœuds de cluster de too10 hello, Service Fabric serait rééquilibrer hello principal [réplicas](service-fabric-availability-services.md) sur tous les nœuds de 10.</span><span class="sxs-lookup"><span data-stu-id="18872-136">If you now need tooscale out hello cluster too10 nodes, Service Fabric would rebalance hello primary [replicas](service-fabric-availability-services.md) across all 10 nodes.</span></span> <span data-ttu-id="18872-137">De même, si vous à l’échelle les nœuds too5 arrière, Service Fabric serait rééquilibrer tous les réplicas hello entre les nœuds hello 5.</span><span class="sxs-lookup"><span data-stu-id="18872-137">Likewise, if you scaled back too5 nodes, Service Fabric would rebalance all hello replicas across hello 5 nodes.</span></span>  

<span data-ttu-id="18872-138">Figure 2 montre la distribution hello de 10 partitions avant et après la mise à l’échelle de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="18872-138">Figure 2 shows hello distribution of 10 partitions before and after scaling hello cluster.</span></span>

![Service avec état](./media/service-fabric-concepts-partitioning/partitions.png)

<span data-ttu-id="18872-140">Par conséquent, hello montée en puissance parallèle est possible dans la mesure où les demandes des clients sont réparties sur plusieurs ordinateurs, les performances globales de l’application hello sont améliorée et la contention sur toochunks d’accès de données est réduite.</span><span class="sxs-lookup"><span data-stu-id="18872-140">As a result, hello scale-out is achieved since requests from clients are distributed across computers, overall performance of hello application is improved, and contention on access toochunks of data is reduced.</span></span>

## <a name="plan-for-partitioning"></a><span data-ttu-id="18872-141">Planification du partitionnement</span><span class="sxs-lookup"><span data-stu-id="18872-141">Plan for partitioning</span></span>
<span data-ttu-id="18872-142">Avant d’implémenter un service, vous devez toujours envisager hello stratégie est requise tooscale out de partitionnement. Il existe différentes manières, mais tous les se concentrent sur l’application hello doit tooachieve.</span><span class="sxs-lookup"><span data-stu-id="18872-142">Before implementing a service, you should always consider hello partitioning strategy that is required tooscale out. There are different ways, but all of them focus on what hello application needs tooachieve.</span></span> <span data-ttu-id="18872-143">Pour le contexte de hello de cet article, prenons l’exemple hello certains aspects les plus importants.</span><span class="sxs-lookup"><span data-stu-id="18872-143">For hello context of this article, let's consider some of hello more important aspects.</span></span>

<span data-ttu-id="18872-144">Une bonne approche est toothink sur la structure hello d’état hello toobe partitionnée, en tant que première étape de hello.</span><span class="sxs-lookup"><span data-stu-id="18872-144">A good approach is toothink about hello structure of hello state that needs toobe partitioned, as hello first step.</span></span>

<span data-ttu-id="18872-145">Prenons un exemple simple :</span><span class="sxs-lookup"><span data-stu-id="18872-145">Let's take a simple example.</span></span> <span data-ttu-id="18872-146">Si vous étiez toobuild un service pour un sondage countywide, vous pouvez créer une partition pour chaque ville dans la région de hello.</span><span class="sxs-lookup"><span data-stu-id="18872-146">If you were toobuild a service for a countywide poll, you could create a partition for each city in hello county.</span></span> <span data-ttu-id="18872-147">Ensuite, vous pouvez stocker des votes hello pour chaque personne dans Ville hello dans partition hello correspondant toothat ville.</span><span class="sxs-lookup"><span data-stu-id="18872-147">Then, you could store hello votes for every person in hello city in hello partition that corresponds toothat city.</span></span> <span data-ttu-id="18872-148">La figure 3 illustre un ensemble de personnes et hello ville dans lesquels ils résident.</span><span class="sxs-lookup"><span data-stu-id="18872-148">Figure 3 illustrates a set of people and hello city in which they reside.</span></span>

![Partition simple](./media/service-fabric-concepts-partitioning/cities.png)

<span data-ttu-id="18872-150">Comme la population hello des villes varie largement, vous risquez avec certaines partitions qui contiennent un grand nombre de données (par exemple, Seattle) et des autres partitions avec très peu état (par exemple, Kirkland).</span><span class="sxs-lookup"><span data-stu-id="18872-150">As hello population of cities varies widely, you may end up with some partitions that contain a lot of data (e.g. Seattle) and other partitions with very little state (e.g. Kirkland).</span></span> <span data-ttu-id="18872-151">Qu’est impact hello d’avoir des partitions avec des volumes irréguliers d’état ?</span><span class="sxs-lookup"><span data-stu-id="18872-151">So what is hello impact of having partitions with uneven amounts of state?</span></span>

<span data-ttu-id="18872-152">Si vous pensez à nouveau sur hello exemple, vous pouvez facilement voir que partition hello contient hello des votes pour Seattle obtenez davantage de trafic que Kirkland hello une.</span><span class="sxs-lookup"><span data-stu-id="18872-152">If you think about hello example again, you can easily see that hello partition that holds hello votes for Seattle will get more traffic than hello Kirkland one.</span></span> <span data-ttu-id="18872-153">Par défaut, l’infrastructure de Service permet de s’assurer qu’il existe sur hello même nombre de réplicas principaux et secondaires sur chaque nœud.</span><span class="sxs-lookup"><span data-stu-id="18872-153">By default, Service Fabric makes sure that there is about hello same number of primary and secondary replicas on each node.</span></span> <span data-ttu-id="18872-154">Par conséquent, vous pouvez obtenir des nœuds qui contiennent des réplicas qui servent plus de trafic et d’autres qui en servent moins.</span><span class="sxs-lookup"><span data-stu-id="18872-154">So you may end up with nodes that hold replicas that serve more traffic and others that serve less traffic.</span></span> <span data-ttu-id="18872-155">Vous pourriez préférence tooavoid à chaud et à froid taches comme suit dans un cluster.</span><span class="sxs-lookup"><span data-stu-id="18872-155">You would preferably want tooavoid hot and cold spots like this in a cluster.</span></span>

<span data-ttu-id="18872-156">Dans commande tooavoid cela, vous devez faire deux choses, d’un point de vue de partitionnement :</span><span class="sxs-lookup"><span data-stu-id="18872-156">In order tooavoid this, you should do two things, from a partitioning point of view:</span></span>

* <span data-ttu-id="18872-157">Essayez d’état de hello toopartition afin qu’elle est répartie équitablement entre toutes les partitions.</span><span class="sxs-lookup"><span data-stu-id="18872-157">Try toopartition hello state so that it is evenly distributed across all partitions.</span></span>
* <span data-ttu-id="18872-158">Charge de rapports à partir de chacun des réplicas hello pour le service de hello.</span><span class="sxs-lookup"><span data-stu-id="18872-158">Report load from each of hello replicas for hello service.</span></span> <span data-ttu-id="18872-159">(Pour plus d'informations sur la procédure à suivre, consultez cet article sur [Métriques et charge](service-fabric-cluster-resource-manager-metrics.md)).</span><span class="sxs-lookup"><span data-stu-id="18872-159">(For information on how, check out this article on [Metrics and Load](service-fabric-cluster-resource-manager-metrics.md)).</span></span> <span data-ttu-id="18872-160">Service Fabric fournit la charge de tooreport hello capacité consommée par les services, tels que la quantité de mémoire ou le nombre d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="18872-160">Service Fabric provides hello capability tooreport load consumed by services, such as amount of memory or number of records.</span></span> <span data-ttu-id="18872-161">En fonction de mesures hello signalées, Service Fabric détecte que certaines partitions servent des charges plus élevées que d’autres rééquilibre cluster hello par déplacement réplicas toomore approprié nœuds, afin que globalement aucun nœud n’est surchargé.</span><span class="sxs-lookup"><span data-stu-id="18872-161">Based on hello metrics reported, Service Fabric detects that some partitions are serving higher loads than others and rebalances hello cluster by moving replicas toomore suitable nodes, so that overall no node is overloaded.</span></span>

<span data-ttu-id="18872-162">Il arrive que la quantité de données dans une partition donnée ne soit pas connue.</span><span class="sxs-lookup"><span data-stu-id="18872-162">Sometimes, you cannot know how much data will be in a given partition.</span></span> <span data-ttu-id="18872-163">Par conséquent, une recommandation générale est toodo à la fois--tout d’abord, en adoptant une stratégie de partitionnement qui répartit hello données uniformément sur les partitions hello et, ensuite, par charge de création de rapports.</span><span class="sxs-lookup"><span data-stu-id="18872-163">So a general recommendation is toodo both--first, by adopting a partitioning strategy that spreads hello data evenly across hello partitions and second, by reporting load.</span></span>  <span data-ttu-id="18872-164">méthode première Hello empêche les situations décrites dans hello vote exemple, alors que hello ensuite permet de lisser les différences temporaires de l’accès ou de la charge au fil du temps.</span><span class="sxs-lookup"><span data-stu-id="18872-164">hello first method prevents situations described in hello voting example, while hello second helps smooth out temporary differences in access or load over time.</span></span>

<span data-ttu-id="18872-165">Un autre aspect de la planification de la partition est le nombre correct de hello toochoose de toobegin de partitions avec.</span><span class="sxs-lookup"><span data-stu-id="18872-165">Another aspect of partition planning is toochoose hello correct number of partitions toobegin with.</span></span>
<span data-ttu-id="18872-166">Du point de vue de Service Fabric, rien ne vous empêche de commencer par un nombre de partitions plus élevé que prévu pour votre scénario.</span><span class="sxs-lookup"><span data-stu-id="18872-166">From a Service Fabric perspective, there is nothing that prevents you from starting out with a higher number of partitions than anticipated for your scenario.</span></span>
<span data-ttu-id="18872-167">En fait, en supposant que le nombre maximal de hello de partitions est une approche valide.</span><span class="sxs-lookup"><span data-stu-id="18872-167">In fact, assuming hello maximum number of partitions is a valid approach.</span></span>

<span data-ttu-id="18872-168">Bien que ces cas soient rares, il peut arriver que vous ayez besoin de plus de partitions que prévu.</span><span class="sxs-lookup"><span data-stu-id="18872-168">In rare cases, you may end up needing more partitions than you have initially chosen.</span></span> <span data-ttu-id="18872-169">Vous ne pouvez pas modifier le nombre de partitions hello après les faits hello, vous devez tooapply certaines approches partition avancées, telles que la création d’une nouvelle instance de service de hello même type de service.</span><span class="sxs-lookup"><span data-stu-id="18872-169">As you cannot change hello partition count after hello fact, you would need tooapply some advanced partition approaches, such as creating a new service instance of hello same service type.</span></span> <span data-ttu-id="18872-170">Vous devez également tooimplement une logique côté client qui achemine hello toohello correct instance de service, en fonction des connaissances côté client que votre code client doit gérer les demandes.</span><span class="sxs-lookup"><span data-stu-id="18872-170">You would also need tooimplement some client-side logic that routes hello requests toohello correct service instance, based on client-side knowledge that your client code must maintain.</span></span>

<span data-ttu-id="18872-171">Une autre considération pour le partitionnement de planification est ressources de l’ordinateur disponible hello.</span><span class="sxs-lookup"><span data-stu-id="18872-171">Another consideration for partitioning planning is hello available computer resources.</span></span> <span data-ttu-id="18872-172">État de hello besoins toobe accès et au stockage, vous êtes toofollow liée :</span><span class="sxs-lookup"><span data-stu-id="18872-172">As hello state needs toobe accessed and stored, you are bound toofollow:</span></span>

* <span data-ttu-id="18872-173">Les limites de bande passante du réseau</span><span class="sxs-lookup"><span data-stu-id="18872-173">Network bandwidth limits</span></span>
* <span data-ttu-id="18872-174">Les limites de mémoire système</span><span class="sxs-lookup"><span data-stu-id="18872-174">System memory limits</span></span>
* <span data-ttu-id="18872-175">Les limites de stockage du disque</span><span class="sxs-lookup"><span data-stu-id="18872-175">Disk storage limits</span></span>

<span data-ttu-id="18872-176">Que se passe-t-il si vous rencontrez des contraintes de ressources dans un cluster en cours d’exécution ? les réponses Hello sont que vous pouvez simplement faire évoluer hello tooaccommodate hello nouvelle configuration requise des clusters.</span><span class="sxs-lookup"><span data-stu-id="18872-176">So what happens if you run into resource constraints in a running cluster? hello answer is that you can simply scale out hello cluster tooaccommodate hello new requirements.</span></span>

<span data-ttu-id="18872-177">[guide de planification de capacité Hello](service-fabric-capacity-planning.md) propose des conseils sur la manière de toodetermine le nombre de nœuds a besoin de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="18872-177">[hello capacity planning guide](service-fabric-capacity-planning.md) offers guidance for how toodetermine how many nodes your cluster needs.</span></span>

## <a name="get-started-with-partitioning"></a><span data-ttu-id="18872-178">Prise en main du partitionnement</span><span class="sxs-lookup"><span data-stu-id="18872-178">Get started with partitioning</span></span>
<span data-ttu-id="18872-179">Cette section décrit comment tooget démarrer avec le partitionnement de votre service.</span><span class="sxs-lookup"><span data-stu-id="18872-179">This section describes how tooget started with partitioning your service.</span></span>

<span data-ttu-id="18872-180">Service Fabric propose trois schémas de partition, au choix :</span><span class="sxs-lookup"><span data-stu-id="18872-180">Service Fabric offers a choice of three partition schemes:</span></span>

* <span data-ttu-id="18872-181">Partitionnement par plage (également appelé UniformInt64Partition).</span><span class="sxs-lookup"><span data-stu-id="18872-181">Ranged partitioning (otherwise known as UniformInt64Partition).</span></span>
* <span data-ttu-id="18872-182">Partitionnement nommé.</span><span class="sxs-lookup"><span data-stu-id="18872-182">Named partitioning.</span></span> <span data-ttu-id="18872-183">Les applications qui utilisent ce modèle comportent généralement des données qui peuvent être compartimentées au sein d’un ensemble limité.</span><span class="sxs-lookup"><span data-stu-id="18872-183">Applications using this model usually have data that can be bucketed, within a bounded set.</span></span> <span data-ttu-id="18872-184">Les régions, les codes postaux, les groupes de clients ou les autres limites de l’entreprise constituent des exemples courants de champs de données utilisés comme clés de partition nommées.</span><span class="sxs-lookup"><span data-stu-id="18872-184">Some common examples of data fields used as named partition keys would be regions, postal codes, customer groups, or other business boundaries.</span></span>
* <span data-ttu-id="18872-185">Partitionnement singleton.</span><span class="sxs-lookup"><span data-stu-id="18872-185">Singleton partitioning.</span></span> <span data-ttu-id="18872-186">Les partitions singleton sont généralement utilisées lorsque le service de hello ne nécessite pas un routage supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="18872-186">Singleton partitions are typically used when hello service does not require any additional routing.</span></span> <span data-ttu-id="18872-187">Par exemple, les services sans état utilisent ce schéma de partitionnement par défaut.</span><span class="sxs-lookup"><span data-stu-id="18872-187">For example, stateless services use this partitioning scheme by default.</span></span>

<span data-ttu-id="18872-188">Les schémas de partitionnement nommé et singleton sont des formes spéciales de partitions par plage.</span><span class="sxs-lookup"><span data-stu-id="18872-188">Named and Singleton partitioning schemes are special forms of ranged partitions.</span></span> <span data-ttu-id="18872-189">Par défaut, les modèles de Visual Studio hello pour une utilisation de l’infrastructure de Service trouver le partitionnement, car il s’agit de hello celle la plus courante et utile.</span><span class="sxs-lookup"><span data-stu-id="18872-189">By default, hello Visual Studio templates for Service Fabric use ranged partitioning, as it is hello most common and useful one.</span></span> <span data-ttu-id="18872-190">reste Hello de cet article se concentre sur le schéma de partitionnement méthode hello.</span><span class="sxs-lookup"><span data-stu-id="18872-190">hello remainder of this article focuses on hello ranged partitioning scheme.</span></span>

### <a name="ranged-partitioning-scheme"></a><span data-ttu-id="18872-191">Schéma de partitionnement par plage</span><span class="sxs-lookup"><span data-stu-id="18872-191">Ranged partitioning scheme</span></span>
<span data-ttu-id="18872-192">Il s’agit de toospecify utilisé entier plage (identifiées par une clé faible et une clé haute) et un nombre de partitions (n).</span><span class="sxs-lookup"><span data-stu-id="18872-192">This is used toospecify an integer range (identified by a low key and high key) and a number of partitions (n).</span></span> <span data-ttu-id="18872-193">Il crée des partitions n, chacun d'entre eux une sous-plage sans chevauchement de hello globale de plage de clés de partition.</span><span class="sxs-lookup"><span data-stu-id="18872-193">It creates n partitions, each responsible for a non-overlapping subrange of hello overall partition key range.</span></span> <span data-ttu-id="18872-194">Par exemple, un schéma de partitionnement par plage doté d’une clé basse de 0, d’une clé haute de 99 et d’un nombre total de 4 créera quatre partitions, telles qu’elles sont illustrées ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="18872-194">For example, a ranged partitioning scheme with a low key of 0, a high key of 99, and a count of 4 would create four partitions, as shown below.</span></span>

![Partitionnement par plage](./media/service-fabric-concepts-partitioning/range-partitioning.png)

<span data-ttu-id="18872-196">Une approche courante consiste à toocreate un hachage basé sur une clé unique dans le jeu de données hello.</span><span class="sxs-lookup"><span data-stu-id="18872-196">A common approach is toocreate a hash based on a unique key within hello data set.</span></span> <span data-ttu-id="18872-197">Un numéro d’immatriculation de véhicule, l’identifiant d’un d’employé ou une chaîne unique sont des exemples courants de clés.</span><span class="sxs-lookup"><span data-stu-id="18872-197">Some common examples of keys would be a vehicle identification number (VIN), an employee ID, or a unique string.</span></span> <span data-ttu-id="18872-198">À l’aide de cette clé unique, vous puis génère un code de hachage, plage de clés modulo hello toouse comme clé.</span><span class="sxs-lookup"><span data-stu-id="18872-198">By using this unique key, you would then generate a hash code, modulus hello key range, toouse as your key.</span></span> <span data-ttu-id="18872-199">Vous pouvez spécifier hello supérieur et les limites inférieures de hello autorisée plage de clés.</span><span class="sxs-lookup"><span data-stu-id="18872-199">You can specify hello upper and lower bounds of hello allowed key range.</span></span>

### <a name="select-a-hash-algorithm"></a><span data-ttu-id="18872-200">Sélection d’un algorithme de hachage</span><span class="sxs-lookup"><span data-stu-id="18872-200">Select a hash algorithm</span></span>
<span data-ttu-id="18872-201">Une partie importante du hachage consiste à sélectionner l'algorithme de hachage.</span><span class="sxs-lookup"><span data-stu-id="18872-201">An important part of hashing is selecting your hash algorithm.</span></span> <span data-ttu-id="18872-202">Un facteur important n’est l’objectif de hello toogroup des clés similaires proches (localité sensibles hachage)--ou si l’activité doit être distribuée globalement sur toutes les partitions (hachage de distribution), ce qui est plus courant.</span><span class="sxs-lookup"><span data-stu-id="18872-202">A consideration is whether hello goal is toogroup similar keys near each other (locality sensitive hashing)--or if activity should be distributed broadly across all partitions (distribution hashing), which is more common.</span></span>

<span data-ttu-id="18872-203">caractéristiques de Hello un bonne distribution d’algorithme de hachage sont qu’il est facile toocompute, il est peu de collisions, et il distribue uniformément les clés de hello.</span><span class="sxs-lookup"><span data-stu-id="18872-203">hello characteristics of a good distribution hashing algorithm are that it is easy toocompute, it has few collisions, and it distributes hello keys evenly.</span></span> <span data-ttu-id="18872-204">Un bon exemple d’un algorithme de hachage efficace est hello [FNV-1](https://en.wikipedia.org/wiki/Fowler%E2%80%93Noll%E2%80%93Vo_hash_function) algorithme de hachage.</span><span class="sxs-lookup"><span data-stu-id="18872-204">A good example of an efficient hash algorithm is hello [FNV-1](https://en.wikipedia.org/wiki/Fowler%E2%80%93Noll%E2%80%93Vo_hash_function) hash algorithm.</span></span>

<span data-ttu-id="18872-205">Une bonne ressource pour le choix d’algorithme de code de hachage général est hello [page Wikipedia sur les fonctions de hachage](http://en.wikipedia.org/wiki/Hash_function).</span><span class="sxs-lookup"><span data-stu-id="18872-205">A good resource for general hash code algorithm choices is hello [Wikipedia page on hash functions](http://en.wikipedia.org/wiki/Hash_function).</span></span>

## <a name="build-a-stateful-service-with-multiple-partitions"></a><span data-ttu-id="18872-206">Création d’un service avec état avec plusieurs partitions</span><span class="sxs-lookup"><span data-stu-id="18872-206">Build a stateful service with multiple partitions</span></span>
<span data-ttu-id="18872-207">Nous allons créer le premier service fiable avec état à plusieurs partitions.</span><span class="sxs-lookup"><span data-stu-id="18872-207">Let's create your first reliable stateful service with multiple partitions.</span></span> <span data-ttu-id="18872-208">Dans cet exemple, vous allez générer une application très simple où vous souhaitez toostore tous les noms qui commencent par Bonjour identique Bonjour même partition.</span><span class="sxs-lookup"><span data-stu-id="18872-208">In this example, you will build a very simple application where you want toostore all last names that start with hello same letter in hello same partition.</span></span>

<span data-ttu-id="18872-209">Avant d’écrire de code, vous devez toothink sur les partitions hello et les clés de partition.</span><span class="sxs-lookup"><span data-stu-id="18872-209">Before you write any code, you need toothink about hello partitions and partition keys.</span></span> <span data-ttu-id="18872-210">Vous avez besoin de 26 partitions (une pour chaque lettre dans l’alphabet de hello), mais comment faire sur hello clés haute et basse ?</span><span class="sxs-lookup"><span data-stu-id="18872-210">You need 26 partitions (one for each letter in hello alphabet), but what about hello low and high keys?</span></span>
<span data-ttu-id="18872-211">Comme nous voulons littéralement toohave une seule partition par lettre, nous pouvons utiliser 0 comme clé basse de hello et 25 en tant que clé haute de hello, car chaque lettre est sa propre clé.</span><span class="sxs-lookup"><span data-stu-id="18872-211">As we literally want toohave one partition per letter, we can use 0 as hello low key and 25 as hello high key, as each letter is its own key.</span></span>

> [!NOTE]
> <span data-ttu-id="18872-212">Il s’agit d’un scénario simplifié, comme dans la réalité, distribution de hello serait irréguliers.</span><span class="sxs-lookup"><span data-stu-id="18872-212">This is a simplified scenario, as in reality hello distribution would be uneven.</span></span> <span data-ttu-id="18872-213">Noms commençant par les lettres hello « S » ou « M » sont plus courantes que hello ceux commençant par « X » ou « Y ».</span><span class="sxs-lookup"><span data-stu-id="18872-213">Last names starting with hello letters "S" or "M" are more common than hello ones starting with "X" or "Y".</span></span>
> 
> 

1. <span data-ttu-id="18872-214">Ouvrez **Visual Studio** > **Fichier** > **Nouveau** > **Projet**.</span><span class="sxs-lookup"><span data-stu-id="18872-214">Open **Visual Studio** > **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="18872-215">Bonjour **nouveau projet** boîte de dialogue, choisissez l’application de Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="18872-215">In hello **New Project** dialog box, choose hello Service Fabric application.</span></span>
3. <span data-ttu-id="18872-216">Appelez le projet de hello « AlphabetPartitions ».</span><span class="sxs-lookup"><span data-stu-id="18872-216">Call hello project "AlphabetPartitions".</span></span>
4. <span data-ttu-id="18872-217">Bonjour **créer un Service** boîte de dialogue, choisissez **avec état** de service et appelez-le « Alphabet.Processing » comme indiqué dans l’image hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="18872-217">In hello **Create a Service** dialog box, choose **Stateful** service and call it "Alphabet.Processing" as shown in hello image below.</span></span>
       <span data-ttu-id="18872-218">![Boîte de dialogue Nouveau service dans Visual Studio][1]</span><span class="sxs-lookup"><span data-stu-id="18872-218">![New service dialog in Visual Studio][1]</span></span>

  <!--  ![Stateful service screenshot](./media/service-fabric-concepts-partitioning/createstateful.png)-->

5. <span data-ttu-id="18872-219">Définir le nombre hello de partitions.</span><span class="sxs-lookup"><span data-stu-id="18872-219">Set hello number of partitions.</span></span> <span data-ttu-id="18872-220">Fichier Applicationmanifest.xml de hello ouvrir situé dans hello dossier ApplicationPackageRoot hello AlphabetPartitions mise à jour et projet hello du paramètre de Processing_PartitionCount too26 comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="18872-220">Open hello Applicationmanifest.xml file located in hello ApplicationPackageRoot folder of hello AlphabetPartitions project and update hello parameter Processing_PartitionCount too26 as shown below.</span></span>
   
    ```xml
    <Parameter Name="Processing_PartitionCount" DefaultValue="26" />
    ```
   
    <span data-ttu-id="18872-221">Vous devez également tooupdate hello LowKey et HighKey des propriétés d’élément de StatefulService hello Bonjour ApplicationManifest.xml comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="18872-221">You also need tooupdate hello LowKey and HighKey properties of hello StatefulService element in hello ApplicationManifest.xml as shown below.</span></span>
   
    ```xml
    <Service Name="Processing">
      <StatefulService ServiceTypeName="ProcessingType" TargetReplicaSetSize="[Processing_TargetReplicaSetSize]" MinReplicaSetSize="[Processing_MinReplicaSetSize]">
        <UniformInt64Partition PartitionCount="[Processing_PartitionCount]" LowKey="0" HighKey="25" />
      </StatefulService>
    </Service>
    ```
6. <span data-ttu-id="18872-222">Pour toobe de service hello accessible, ouvrez un point de terminaison sur un port en ajoutant l’élément de point de terminaison hello de ServiceManifest.xml (situé dans le dossier de PackageRoot hello) pour hello Alphabet.Processing service comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="18872-222">For hello service toobe accessible, open up an endpoint on a port by adding hello endpoint element of ServiceManifest.xml (located in hello PackageRoot folder) for hello Alphabet.Processing service as shown below:</span></span>
   
    ```xml
    <Endpoint Name="ProcessingServiceEndpoint" Port="8089" Protocol="http" Type="Internal" />
    ```
   
    <span data-ttu-id="18872-223">Service de hello est désormais un point de terminaison configuré toolisten tooan interne avec 26 partitions.</span><span class="sxs-lookup"><span data-stu-id="18872-223">Now hello service is configured toolisten tooan internal endpoint with 26 partitions.</span></span>
7. <span data-ttu-id="18872-224">Ensuite, vous devez toooverride hello `CreateServiceReplicaListeners()` méthode de classe de traitement hello.</span><span class="sxs-lookup"><span data-stu-id="18872-224">Next, you need toooverride hello `CreateServiceReplicaListeners()` method of hello Processing class.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="18872-225">Pour cet exemple, supposons que vous utilisiez un HttpCommunicationListener simple.</span><span class="sxs-lookup"><span data-stu-id="18872-225">For this sample, we assume that you are using a simple HttpCommunicationListener.</span></span> <span data-ttu-id="18872-226">Pour plus d’informations sur la communication fiable, consultez [modèle de communication de Service fiable hello](service-fabric-reliable-services-communication.md).</span><span class="sxs-lookup"><span data-stu-id="18872-226">For more information on reliable service communication, see [hello Reliable Service communication model](service-fabric-reliable-services-communication.md).</span></span>
   > 
   > 
8. <span data-ttu-id="18872-227">Un modèle recommandé pour les URL hello qui écoute un réplica est hello suivant le format : `{scheme}://{nodeIp}:{port}/{partitionid}/{replicaid}/{guid}`.</span><span class="sxs-lookup"><span data-stu-id="18872-227">A recommended pattern for hello URL that a replica listens on is hello following format: `{scheme}://{nodeIp}:{port}/{partitionid}/{replicaid}/{guid}`.</span></span>
    <span data-ttu-id="18872-228">Vous pouvez tooconfigure votre toolisten d’écouteur de communication sur les points de terminaison corrects hello et avec ce modèle.</span><span class="sxs-lookup"><span data-stu-id="18872-228">So you want tooconfigure your communication listener toolisten on hello correct endpoints and with this pattern.</span></span>
   
    <span data-ttu-id="18872-229">Plusieurs réplicas de ce service peuvent être hébergés sur hello même ordinateur, par conséquent, cette adresse doit toobe toohello unique réplica.</span><span class="sxs-lookup"><span data-stu-id="18872-229">Multiple replicas of this service may be hosted on hello same computer, so this address needs toobe unique toohello replica.</span></span> <span data-ttu-id="18872-230">C’est pourquoi l’ID de partition + ID de réplica est dans l’URL de hello.</span><span class="sxs-lookup"><span data-stu-id="18872-230">This is why   partition ID + replica ID are in hello URL.</span></span> <span data-ttu-id="18872-231">HttpListener peut écouter sur plusieurs adresses hello que même port tant que préfixe d’URL hello est unique.</span><span class="sxs-lookup"><span data-stu-id="18872-231">HttpListener can listen on multiple addresses on hello same port as long as hello URL prefix    is unique.</span></span>
   
    <span data-ttu-id="18872-232">Hello qu'existe-t-il GUID supplémentaire pour des cas où les réplicas secondaires écoutent également pour les demandes en lecture seule.</span><span class="sxs-lookup"><span data-stu-id="18872-232">hello extra GUID is there for an advanced case where secondary replicas also listen for read-only requests.</span></span> <span data-ttu-id="18872-233">Lorsque c’est le cas de hello, vous souhaitez toomake qu’une nouvelle adresse unique est utilisé lors du passage d’une adresse de principal toosecondary tooforce clients toore résoudre hello.</span><span class="sxs-lookup"><span data-stu-id="18872-233">When that's hello case, you want toomake sure that a new unique address is used when transitioning from primary toosecondary tooforce clients toore-resolve hello address.</span></span> <span data-ttu-id="18872-234">'+' est utilisée comme adresse hello ici afin que hello réplica écoute sur tous les ordinateurs hôtes disponibles (IP, FQDM, localhost, etc.) hello de code ci-dessous montre un exemple.</span><span class="sxs-lookup"><span data-stu-id="18872-234">'+' is used as hello address here so that hello replica listens on all available hosts (IP, FQDM, localhost, etc.) hello code below shows an example.</span></span>
   
    ```CSharp
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
         return new[] { new ServiceReplicaListener(context => this.CreateInternalListener(context))};
    }
    private ICommunicationListener CreateInternalListener(ServiceContext context)
    {
   
         EndpointResourceDescription internalEndpoint = context.CodePackageActivationContext.GetEndpoint("ProcessingServiceEndpoint");
         string uriPrefix = String.Format(
                "{0}://+:{1}/{2}/{3}-{4}/",
                internalEndpoint.Protocol,
                internalEndpoint.Port,
                context.PartitionId,
                context.ReplicaOrInstanceId,
                Guid.NewGuid());
   
         string nodeIP = FabricRuntime.GetNodeContext().IPAddressOrFQDN;
   
         string uriPublished = uriPrefix.Replace("+", nodeIP);
         return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInternalRequest);
    }
    ```
   
    <span data-ttu-id="18872-235">Il est également important de noter que hello publié URL est légèrement différente de préfixe d’URL hello écoute.</span><span class="sxs-lookup"><span data-stu-id="18872-235">It's also worth noting that hello published URL is slightly different from hello listening URL prefix.</span></span>
    <span data-ttu-id="18872-236">URL d’écoute Hello est donné tooHttpListener.</span><span class="sxs-lookup"><span data-stu-id="18872-236">hello listening URL is given tooHttpListener.</span></span> <span data-ttu-id="18872-237">Hello que publiée URL est hello qui est publiée toohello Service Naming Service Fabric, qui est utilisé pour la découverte de service.</span><span class="sxs-lookup"><span data-stu-id="18872-237">hello published URL is hello URL that is published toohello Service Fabric Naming Service, which is used for service discovery.</span></span> <span data-ttu-id="18872-238">Les clients demanderont cette adresse via ce service de découverte.</span><span class="sxs-lookup"><span data-stu-id="18872-238">Clients will ask for this address through that discovery service.</span></span> <span data-ttu-id="18872-239">adresse Hello que les clients obtiennent des besoins toohave hello réel l’adresse IP ou nom de domaine complet du nœud de hello dans l’ordre tooconnect.</span><span class="sxs-lookup"><span data-stu-id="18872-239">hello address that clients get needs toohave hello actual IP or FQDN of hello node in order tooconnect.</span></span> <span data-ttu-id="18872-240">Par conséquent, vous devez tooreplace '+' avec hello du nœud à l’adresse IP ou nom de domaine complet comme indiqué ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="18872-240">So you need tooreplace '+' with hello node's IP or FQDN as shown above.</span></span>
9. <span data-ttu-id="18872-241">dernière étape de Hello est hello tooadd logique toohello service comme indiqué ci-dessous de traitement.</span><span class="sxs-lookup"><span data-stu-id="18872-241">hello last step is tooadd hello processing logic toohello service as shown below.</span></span>
   
    ```CSharp
    private async Task ProcessInternalRequest(HttpListenerContext context, CancellationToken cancelRequest)
    {
        string output = null;
        string user = context.Request.QueryString["lastname"].ToString();
   
        try
        {
            output = await this.AddUserAsync(user);
        }
        catch (Exception ex)
        {
            output = ex.Message;
        }
   
        using (HttpListenerResponse response = context.Response)
        {
            if (output != null)
            {
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    private async Task<string> AddUserAsync(string user)
    {
        IReliableDictionary<String, String> dictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<String, String>>("dictionary");
   
        using (ITransaction tx = this.StateManager.CreateTransaction())
        {
            bool addResult = await dictionary.TryAddAsync(tx, user.ToUpperInvariant(), user);
   
            await tx.CommitAsync();
   
            return String.Format(
                "User {0} {1}",
                user,
                addResult ? "sucessfully added" : "already exists");
        }
    }
    ```
   
    <span data-ttu-id="18872-242">`ProcessInternalRequest`lectures hello valeurs hello requête chaîne paramètre utilisé toocall hello partition et les appels `AddUserAsync` dictionnaire fiable de tooadd hello lastname toohello `dictionary`.</span><span class="sxs-lookup"><span data-stu-id="18872-242">`ProcessInternalRequest` reads hello values of hello query string parameter used toocall hello partition and calls `AddUserAsync` tooadd hello lastname toohello reliable dictionary `dictionary`.</span></span>
10. <span data-ttu-id="18872-243">Vous allez ajouter un toosee de projet de service sans état toohello comment vous pouvez appeler une partition particulière.</span><span class="sxs-lookup"><span data-stu-id="18872-243">Let's add a stateless service toohello project toosee how you can call a particular partition.</span></span>
    
    <span data-ttu-id="18872-244">Ce service sert à une interface web simple qui accepte lastname hello comme paramètre de chaîne de requête, détermine la clé de partition hello et il envoie le service de Alphabet.Processing toohello pour le traitement.</span><span class="sxs-lookup"><span data-stu-id="18872-244">This service serves as a simple web interface that accepts hello lastname as a query string parameter, determines hello partition key, and sends it toohello Alphabet.Processing service for processing.</span></span>
11. <span data-ttu-id="18872-245">Bonjour **créer un Service** boîte de dialogue, choisissez **Stateless** de service et appelez-le « Alphabet.Web » comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="18872-245">In hello **Create a Service** dialog box, choose **Stateless** service and call it "Alphabet.Web" as shown below.</span></span>
    
    ![Capture d’écran de service sans état](./media/service-fabric-concepts-partitioning/createnewstateless.png)<span data-ttu-id="18872-247">.</span><span class="sxs-lookup"><span data-stu-id="18872-247">.</span></span>
12. <span data-ttu-id="18872-248">Mettre à jour les informations de point de terminaison hello Bonjour ServiceManifest.xml de hello Alphabet.WebApi service tooopen configuration d’un port comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="18872-248">Update hello endpoint information in hello ServiceManifest.xml of hello Alphabet.WebApi service tooopen up a port as shown below.</span></span>
    
    ```xml
    <Endpoint Name="WebApiServiceEndpoint" Protocol="http" Port="8081"/>
    ```
13. <span data-ttu-id="18872-249">Vous devez tooreturn une collection de ServiceInstanceListeners dans la classe de hello Web.</span><span class="sxs-lookup"><span data-stu-id="18872-249">You need tooreturn a collection of ServiceInstanceListeners in hello class Web.</span></span> <span data-ttu-id="18872-250">Là encore, vous pouvez choisir tooimplement un HttpCommunicationListener simple.</span><span class="sxs-lookup"><span data-stu-id="18872-250">Again, you can choose tooimplement a simple HttpCommunicationListener.</span></span>
    
    ```CSharp
    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        return new[] {new ServiceInstanceListener(context => this.CreateInputListener(context))};
    }
    private ICommunicationListener CreateInputListener(ServiceContext context)
    {
        // Service instance's URL is hello node's IP & desired port
        EndpointResourceDescription inputEndpoint = context.CodePackageActivationContext.GetEndpoint("WebApiServiceEndpoint")
        string uriPrefix = String.Format("{0}://+:{1}/alphabetpartitions/", inputEndpoint.Protocol, inputEndpoint.Port);
        var uriPublished = uriPrefix.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);
        return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInputRequest);
    }
    ```
14. <span data-ttu-id="18872-251">Vous devez maintenant la logique de traitement tooimplement hello.</span><span class="sxs-lookup"><span data-stu-id="18872-251">Now you need tooimplement hello processing logic.</span></span> <span data-ttu-id="18872-252">Hello HttpCommunicationListener appelle `ProcessInputRequest` lorsqu’une demande arrive.</span><span class="sxs-lookup"><span data-stu-id="18872-252">hello HttpCommunicationListener calls `ProcessInputRequest` when a request comes in.</span></span> <span data-ttu-id="18872-253">Par conséquent, commençons et ajoutez le code hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="18872-253">So let's go ahead and add hello code below.</span></span>
    
    ```CSharp
    private async Task ProcessInputRequest(HttpListenerContext context, CancellationToken cancelRequest)
    {
        String output = null;
        try
        {
            string lastname = context.Request.QueryString["lastname"];
            char firstLetterOfLastName = lastname.First();
            ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    
            ResolvedServicePartition partition = await this.servicePartitionResolver.ResolveAsync(alphabetServiceUri, partitionKey, cancelRequest);
            ResolvedServiceEndpoint ep = partition.GetEndpoint();
    
            JObject addresses = JObject.Parse(ep.Address);
            string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
            UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
            primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
            string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    
            output = String.Format(
                    "Result: {0}. <p>Partition key: '{1}' generated from hello first letter '{2}' of input value '{3}'. <br>Processing service partition ID: {4}. <br>Processing service replica address: {5}",
                    result,
                    partitionKey,
                    firstLetterOfLastName,
                    lastname,
                    partition.Info.Id,
                    primaryReplicaAddress);
        }
        catch (Exception ex) { output = ex.Message; }
    
        using (var response = context.Response)
        {
            if (output != null)
            {
                output = output + "added tooPartition: " + primaryReplicaAddress;
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    ```
    
    <span data-ttu-id="18872-254">Voici la procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="18872-254">Let's walk through it step by step.</span></span> <span data-ttu-id="18872-255">code de Hello lit hello première lettre du paramètre de chaîne de requête hello `lastname` en char.</span><span class="sxs-lookup"><span data-stu-id="18872-255">hello code reads hello first letter of hello query string parameter `lastname` into a char.</span></span> <span data-ttu-id="18872-256">Ensuite, il détermine la clé de partition hello pour cette lettre en soustrayant la valeur hexadécimale hello `A` à partir de la valeur hexadécimale hello initiales des noms de famille hello.</span><span class="sxs-lookup"><span data-stu-id="18872-256">Then, it determines hello partition key for this letter by subtracting hello hexadecimal value of `A` from hello hexadecimal value of hello last names' first letter.</span></span>
    
    ```CSharp
    string lastname = context.Request.QueryString["lastname"];
    char firstLetterOfLastName = lastname.First();
    ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    ```
    
    <span data-ttu-id="18872-257">N’oubliez pas que, dans cet exemple, nous utilisons 26 partitions avec une seule clé de partition par partition.</span><span class="sxs-lookup"><span data-stu-id="18872-257">Remember, for this example, we are using 26 partitions with one partition key per partition.</span></span>
    <span data-ttu-id="18872-258">Ensuite, nous obtenons la partition de service hello `partition` pour cette clé à l’aide de hello `ResolveAsync` méthode sur hello `servicePartitionResolver` objet.</span><span class="sxs-lookup"><span data-stu-id="18872-258">Next, we obtain hello service partition `partition` for this key by using hello `ResolveAsync` method on hello `servicePartitionResolver` object.</span></span> <span data-ttu-id="18872-259">`servicePartitionResolver` est défini comme</span><span class="sxs-lookup"><span data-stu-id="18872-259">`servicePartitionResolver` is defined as</span></span>
    
    ```CSharp
    private readonly ServicePartitionResolver servicePartitionResolver = ServicePartitionResolver.GetDefault();
    ```
    
    <span data-ttu-id="18872-260">Hello `ResolveAsync` méthode prend hello URI du service, clé de partition hello et un jeton d’annulation en tant que paramètres.</span><span class="sxs-lookup"><span data-stu-id="18872-260">hello `ResolveAsync` method takes hello service URI, hello partition key, and a cancellation token as parameters.</span></span> <span data-ttu-id="18872-261">Hello URI du service de service de traitement de hello est `fabric:/AlphabetPartitions/Processing`.</span><span class="sxs-lookup"><span data-stu-id="18872-261">hello service URI for hello processing service is `fabric:/AlphabetPartitions/Processing`.</span></span> <span data-ttu-id="18872-262">Ensuite, nous obtenons le point de terminaison hello de partition de hello.</span><span class="sxs-lookup"><span data-stu-id="18872-262">Next, we get hello endpoint of hello partition.</span></span>
    
    ```CSharp
    ResolvedServiceEndpoint ep = partition.GetEndpoint()
    ```
    
    <span data-ttu-id="18872-263">Enfin, nous générer des URL de point de terminaison hello plus hello querystring et appeler le service de traitement de hello.</span><span class="sxs-lookup"><span data-stu-id="18872-263">Finally, we build hello endpoint URL plus hello querystring and call hello processing service.</span></span>
    
    ```CSharp
    JObject addresses = JObject.Parse(ep.Address);
    string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
    UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
    primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
    string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    ```
    
    <span data-ttu-id="18872-264">Une fois que le traitement de hello est terminé, nous réécrire les sortie hello.</span><span class="sxs-lookup"><span data-stu-id="18872-264">Once hello processing is done, we write hello output back.</span></span>
15. <span data-ttu-id="18872-265">dernière étape de Hello est service de hello tootest.</span><span class="sxs-lookup"><span data-stu-id="18872-265">hello last step is tootest hello service.</span></span> <span data-ttu-id="18872-266">Visual Studio utilise les paramètres d’application pour un déploiement local et sur le cloud.</span><span class="sxs-lookup"><span data-stu-id="18872-266">Visual Studio uses application parameters for local and cloud deployment.</span></span> <span data-ttu-id="18872-267">service de hello tootest avec des 26 partitions localement, vous devez tooupdate hello `Local.xml` fichier dans le dossier de ApplicationParameters de hello du projet de AlphabetPartitions hello, comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="18872-267">tootest hello service with 26 partitions locally, you need tooupdate hello `Local.xml` file in hello ApplicationParameters folder of hello AlphabetPartitions project as shown below:</span></span>
    
    ```xml
    <Parameters>
      <Parameter Name="Processing_PartitionCount" Value="26" />
      <Parameter Name="WebApi_InstanceCount" Value="1" />
    </Parameters>
    ```
16. <span data-ttu-id="18872-268">Une fois que vous avez terminé le déploiement, vous pouvez vérifier le service de hello et toutes ses partitions Bonjour Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="18872-268">Once you finish deployment, you can check hello service and all of its partitions in hello Service Fabric Explorer.</span></span>
    
    ![Capture d’écran de l’explorateur Service Fabric](./media/service-fabric-concepts-partitioning/sfxpartitions.png)
17. <span data-ttu-id="18872-270">Dans un navigateur, vous pouvez tester hello partitionnement logique en entrant `http://localhost:8081/?lastname=somename`.</span><span class="sxs-lookup"><span data-stu-id="18872-270">In a browser, you can test hello partitioning logic by entering `http://localhost:8081/?lastname=somename`.</span></span> <span data-ttu-id="18872-271">Vous verrez que chaque nom qui commence par hello même lettre sont stockée dans hello même partition.</span><span class="sxs-lookup"><span data-stu-id="18872-271">You will see that each last name that starts with hello same letter is being stored in hello same partition.</span></span>
    
    ![Capture d’écran du navigateur](./media/service-fabric-concepts-partitioning/samplerunning.png)

<span data-ttu-id="18872-273">code source entière de Hello de l’exemple hello est disponible sur [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span><span class="sxs-lookup"><span data-stu-id="18872-273">hello entire source code of hello sample is available on [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span></span>

## <a name="next-steps"></a><span data-ttu-id="18872-274">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="18872-274">Next steps</span></span>
<span data-ttu-id="18872-275">Pour plus d’informations sur les concepts de l’infrastructure de Service, voir hello :</span><span class="sxs-lookup"><span data-stu-id="18872-275">For information on Service Fabric concepts, see hello following:</span></span>

* [<span data-ttu-id="18872-276">Disponibilité des services Service Fabric</span><span class="sxs-lookup"><span data-stu-id="18872-276">Availability of Service Fabric services</span></span>](service-fabric-availability-services.md)
* [<span data-ttu-id="18872-277">Extensibilité des services Service Fabric</span><span class="sxs-lookup"><span data-stu-id="18872-277">Scalability of Service Fabric services</span></span>](service-fabric-concepts-scalability.md)
* [<span data-ttu-id="18872-278">Planification de la capacité pour les applications Service Fabric</span><span class="sxs-lookup"><span data-stu-id="18872-278">Capacity planning for Service Fabric applications</span></span>](service-fabric-capacity-planning.md)

[wikipartition]: https://en.wikipedia.org/wiki/Partition_(database)

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png