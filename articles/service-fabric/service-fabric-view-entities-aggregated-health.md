---
title: "entités aaaHow tooview Azure Service Fabric agrégé d’intégrité | Documents Microsoft"
description: "Décrit comment tooquery, lecture et l’évaluation d’intégrité agrégé des entités Azure Service Fabric, par le biais de requêtes d’intégrité et des requêtes générales."
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: fa34c52d-3a74-4b90-b045-ad67afa43fe5
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: oanapl
ms.openlocfilehash: add810551cac26d2b4ff81b57d94ddd780c2cc2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="view-service-fabric-health-reports"></a><span data-ttu-id="b9a9d-103">Affichage rapports d’intégrité de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b9a9d-103">View Service Fabric health reports</span></span>
<span data-ttu-id="b9a9d-104">Azure Service Fabric propose un [modèle d’intégrité](service-fabric-health-introduction.md) avec des entités d’intégrité sur lesquelles les composants système et les agents de surveillance peuvent signaler les conditions locales qu’ils surveillent.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-104">Azure Service Fabric introduces a [health model](service-fabric-health-introduction.md) with health entities on which system components and watchdogs can report local conditions that they are monitoring.</span></span> <span data-ttu-id="b9a9d-105">Hello [magasin de contrôle d’intégrité](service-fabric-health-introduction.md#health-store) regroupe tous les toodetermine de données de contrôle d’intégrité si les entités sont intègres.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-105">hello [health store](service-fabric-health-introduction.md#health-store) aggregates all health data toodetermine whether entities are healthy.</span></span>

<span data-ttu-id="b9a9d-106">cluster de Hello est automatiquement remplie avec les rapports d’intégrité envoyés par les composants du système hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-106">hello cluster is automatically populated with health reports sent by hello system components.</span></span> <span data-ttu-id="b9a9d-107">En savoir plus sur [tootroubleshoot des rapports d’intégrité du système utilisez](service-fabric-understand-and-troubleshoot-with-system-health-reports.md).</span><span class="sxs-lookup"><span data-stu-id="b9a9d-107">Read more at [Use system health reports tootroubleshoot](service-fabric-understand-and-troubleshoot-with-system-health-reports.md).</span></span>

<span data-ttu-id="b9a9d-108">Service Fabric fournit plusieurs façons tooget hello agrégé d’intégrité des entités de hello :</span><span class="sxs-lookup"><span data-stu-id="b9a9d-108">Service Fabric provides multiple ways tooget hello aggregated health of hello entities:</span></span>

* <span data-ttu-id="b9a9d-109">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) ou d’autres outils de visualisation</span><span class="sxs-lookup"><span data-stu-id="b9a9d-109">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) or other visualization tools</span></span>
* <span data-ttu-id="b9a9d-110">Requêtes d’intégrité (via PowerShell, API ou REST)</span><span class="sxs-lookup"><span data-stu-id="b9a9d-110">Health queries (through PowerShell, API, or REST)</span></span>
* <span data-ttu-id="b9a9d-111">Général requêtes qui retournent une liste des entités qui ont le contrôle d’intégrité en tant qu’une des propriétés hello (via PowerShell, API ou REST)</span><span class="sxs-lookup"><span data-stu-id="b9a9d-111">General queries that return a list of entities that have health as one of hello properties (through PowerShell, API, or REST)</span></span>

<span data-ttu-id="b9a9d-112">toodemonstrate ces options, nous allons utiliser un cluster local avec cinq nœuds et hello [fabric : / WordCount application](http://aka.ms/servicefabric-wordcountapp).</span><span class="sxs-lookup"><span data-stu-id="b9a9d-112">toodemonstrate these options, let's use a local cluster with five nodes and hello [fabric:/WordCount application](http://aka.ms/servicefabric-wordcountapp).</span></span> <span data-ttu-id="b9a9d-113">Hello **fabric : / WordCount** application contient deux services par défaut, un service avec état de type `WordCountServiceType`et un service sans état du type `WordCountWebServiceType`.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-113">hello **fabric:/WordCount** application contains two default services, a stateful service of type `WordCountServiceType`, and a stateless service of type `WordCountWebServiceType`.</span></span> <span data-ttu-id="b9a9d-114">J’ai modifié hello `ApplicationManifest.xml` toorequire sept des réplicas de cibles pour un service avec état hello et une partition.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-114">I changed hello `ApplicationManifest.xml` toorequire seven target replicas for hello stateful service and one partition.</span></span> <span data-ttu-id="b9a9d-115">Étant donné que cinq nœuds de cluster de hello, composants du système hello signalent un avertissement sur la partition de service hello, car il est sous le nombre de cibles hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-115">Because there are only five nodes in hello cluster, hello system components report a warning on hello service partition because it is below hello target count.</span></span>

```xml
<Service Name="WordCountService">
<<<<<<< HEAD
    <StatefulService ServiceTypeName="WordCountServiceType" TargetReplicaSetSize="7" MinReplicaSetSize="3">
      <UniformInt64Partition PartitionCount="1" LowKey="1" HighKey="26" />
    </StatefulService>
=======
  <StatefulService ServiceTypeName="WordCountServiceType" TargetReplicaSetSize="7" MinReplicaSetSize="2">
    <UniformInt64Partition PartitionCount="[WordCountService_PartitionCount]" LowKey="1" HighKey="26" />
  </StatefulService>
>>>>>>> 5e84dbdd8e45a5d6b36f435a550b7433b873bf11
</Service>
```

## <a name="health-in-service-fabric-explorer"></a><span data-ttu-id="b9a9d-116">Intégrité dans Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="b9a9d-116">Health in Service Fabric Explorer</span></span>
<span data-ttu-id="b9a9d-117">Service Fabric Explorer fournit un affichage visuel du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-117">Service Fabric Explorer provides a visual view of hello cluster.</span></span> <span data-ttu-id="b9a9d-118">Dans l’image hello ci-dessous, vous pouvez voir que :</span><span class="sxs-lookup"><span data-stu-id="b9a9d-118">In hello image below, you can see that:</span></span>

* <span data-ttu-id="b9a9d-119">Hello application **fabric : / WordCount** est rouge (erreur), car il possède un événement d’erreur signalé par **MyWatchdog** pour la propriété de hello **disponibilité**.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-119">hello application **fabric:/WordCount** is red (in error) because it has an error event reported by **MyWatchdog** for hello property **Availability**.</span></span>
* <span data-ttu-id="b9a9d-120">L’un de ses services, **fabric:/WordCount/WordCountService** apparaît en jaune (avertissement).</span><span class="sxs-lookup"><span data-stu-id="b9a9d-120">One of its services, **fabric:/WordCount/WordCountService** is yellow (in warning).</span></span> <span data-ttu-id="b9a9d-121">service de Hello est configuré avec des sept réplicas et cluster de hello a cinq nœuds, deux repicas ne peut pas être placés.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-121">hello service is configured with seven replicas and hello cluster has five nodes, so two repicas can't be placed.</span></span> <span data-ttu-id="b9a9d-122">Bien que cela n’est pas indiqué ici, partition de service hello est jaune en raison d’un rapport du système à partir de `System.FM` indiquant que `Partition is below target replica or instance count`.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-122">Although it's not shown here, hello service partition is yellow because of a system report from `System.FM` saying that `Partition is below target replica or instance count`.</span></span> <span data-ttu-id="b9a9d-123">déclencheurs de partition jaune Hello hello service jaune.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-123">hello yellow partition triggers hello yellow service.</span></span>
* <span data-ttu-id="b9a9d-124">cluster de Hello est rouge en raison de l’application hello rouge.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-124">hello cluster is red because of hello red application.</span></span>

<span data-ttu-id="b9a9d-125">évaluation de Hello utilise des stratégies par défaut de manifeste du cluster hello et manifeste d’application.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-125">hello evaluation uses default policies from hello cluster manifest and application manifest.</span></span> <span data-ttu-id="b9a9d-126">Il s’agit de stratégies strictes qui ne tolèrent aucun échec.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-126">They are strict policies and do not tolerate any failure.</span></span>

<span data-ttu-id="b9a9d-127">Affichage du cluster Service Fabric Explorer hello :</span><span class="sxs-lookup"><span data-stu-id="b9a9d-127">View of hello cluster with Service Fabric Explorer:</span></span>

![Affichage du cluster Service Fabric Explorer hello.][1]

[1]: ./media/service-fabric-view-entities-aggregated-health/servicefabric-explorer-cluster-health.png


> [!NOTE]
> <span data-ttu-id="b9a9d-129">En savoir plus sur [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="b9a9d-129">Read more about [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
>
>

## <a name="health-queries"></a><span data-ttu-id="b9a9d-130">Requêtes d'intégrité</span><span class="sxs-lookup"><span data-stu-id="b9a9d-130">Health queries</span></span>
<span data-ttu-id="b9a9d-131">L’infrastructure de service expose les requêtes d’intégrité pour chacun des hello pris en charge [types d’entités](service-fabric-health-introduction.md#health-entities-and-hierarchy).</span><span class="sxs-lookup"><span data-stu-id="b9a9d-131">Service Fabric exposes health queries for each of hello supported [entity types](service-fabric-health-introduction.md#health-entities-and-hierarchy).</span></span> <span data-ttu-id="b9a9d-132">Ils sont accessibles via hello API, à l’aide des méthodes sur [FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet), applets de commande PowerShell et REST.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-132">They can be accessed through hello API, using methods on [FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet), PowerShell cmdlets, and REST.</span></span> <span data-ttu-id="b9a9d-133">Ces requêtes retournent entièrement l’intégrité des informations sur l’entité de hello : hello agrégé de l’état d’intégrité, événements de contrôle d’intégrité d’entité, les États d’intégrité enfant (le cas échéant), évaluations non intègres (lorsque l’entité de hello n’est pas intègre) et les statistiques d’intégrité enfants (lorsque applicable).</span><span class="sxs-lookup"><span data-stu-id="b9a9d-133">These queries return complete health information about hello entity: hello aggregated health state, entity health events, child health states (when applicable), unhealthy evaluations (when hello entity is not healthy), and children health statistics (when applicable).</span></span>

> [!NOTE]
> <span data-ttu-id="b9a9d-134">Une entité de contrôle d’intégrité est retournée s’il est entièrement rempli dans le magasin de contrôle d’intégrité hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-134">A health entity is returned when it is fully populated in hello health store.</span></span> <span data-ttu-id="b9a9d-135">entité de Hello doit être active (ne pas supprimé) et disposez d’un rapport du système.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-135">hello entity must be active (not deleted) and have a system report.</span></span> <span data-ttu-id="b9a9d-136">Ses entités parent sur la chaîne de hiérarchie hello doivent également avoir des rapports sur le système.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-136">Its parent entities on hello hierarchy chain must also have system reports.</span></span> <span data-ttu-id="b9a9d-137">Si une de ces conditions ne sont pas satisfaite, le contrôle d’intégrité hello requêtes retournent un [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception) avec [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound` qui montre pourquoi les entités hello ne sont pas renvoyée.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-137">If any of these conditions are not satisfied, hello health queries return a [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception) with [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound` that shows why hello entity is not returned.</span></span>
>
>

<span data-ttu-id="b9a9d-138">requêtes d’intégrité de Hello doivent passer dans un identificateur d’entité hello, qui varie selon le type d’entité hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-138">hello health queries must pass in hello entity identifier, which depends on hello entity type.</span></span> <span data-ttu-id="b9a9d-139">les requêtes Hello acceptent des paramètres de stratégie d’intégrité facultatifs.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-139">hello queries accept optional health policy parameters.</span></span> <span data-ttu-id="b9a9d-140">Si aucune stratégie de contrôle d’intégrité n’est spécifiés, hello [stratégies d’intégrité](service-fabric-health-introduction.md#health-policies) à partir du manifeste de cluster ou une application hello sont utilisées pour l’évaluation.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-140">If no health policies are specified, hello [health policies](service-fabric-health-introduction.md#health-policies) from hello cluster or application manifest are used for evaluation.</span></span> <span data-ttu-id="b9a9d-141">Si les manifestes hello ne contiennent pas de définition pour les stratégies d’intégrité, les stratégies de contrôle d’intégrité par défaut hello sont utilisées pour l’évaluation.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-141">If hello manifests don't contain a definition for health policies, hello default health policies are used for evaluation.</span></span> <span data-ttu-id="b9a9d-142">stratégies de contrôle d’intégrité par défaut Hello ne tolèrent pas les échecs.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-142">hello default health policies do not tolerate any failures.</span></span> <span data-ttu-id="b9a9d-143">les requêtes de Hello acceptent également des filtres pour retourner uniquement les enfants partielles ou événements--hello ceux qui respectent hello filtres spécifiés.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-143">hello queries also accept filters for returning only partial children or events--hello ones that respect hello specified filters.</span></span> <span data-ttu-id="b9a9d-144">Un autre filtre permet à l’exclusion des statistiques de hello enfants.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-144">Another filter allows excluding hello children statistics.</span></span>

> [!NOTE]
> <span data-ttu-id="b9a9d-145">filtres de sortie Hello sont appliquées côté serveur de hello, taille de la réponse message hello est réduit.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-145">hello output filters are applied on hello server side, so hello message reply size is reduced.</span></span> <span data-ttu-id="b9a9d-146">Il est recommandé d’utiliser des filtres de sortie hello toolimit hello données retournent, plutôt qu’appliquent des filtres côté client de hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-146">We recommended that you use hello output filters toolimit hello data returned, rather than apply filters on hello client side.</span></span>
>
>

<span data-ttu-id="b9a9d-147">Les données d’intégrité d’une entité incluent les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="b9a9d-147">An entity's health contains:</span></span>

* <span data-ttu-id="b9a9d-148">Bonjour état d’intégrité agrégé de l’entité de hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-148">hello aggregated health state of hello entity.</span></span> <span data-ttu-id="b9a9d-149">Calculée par le magasin de contrôle d’intégrité hello basé sur les rapports d’intégrité d’entité, telles que les États d’intégrité enfant (le cas échéant) et stratégies d’intégrité.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-149">Computed by hello health store based on entity health reports, child health states (when applicable), and health policies.</span></span> <span data-ttu-id="b9a9d-150">En savoir plus sur l’ [évaluation de l’intégrité de l’entité](service-fabric-health-introduction.md#health-evaluation).</span><span class="sxs-lookup"><span data-stu-id="b9a9d-150">Read more about [entity health evaluation](service-fabric-health-introduction.md#health-evaluation).</span></span>  
* <span data-ttu-id="b9a9d-151">événements de contrôle d’intégrité Hello sur l’entité de hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-151">hello health events on hello entity.</span></span>
* <span data-ttu-id="b9a9d-152">collection de Hello des États d’intégrité de tous les enfants pour les entités hello qui peuvent avoir des enfants.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-152">hello collection of health states of all children for hello entities that can have children.</span></span> <span data-ttu-id="b9a9d-153">les États d’intégrité Hello contiennent les identificateurs d’entité et hello état d’intégrité agrégé.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-153">hello health states contain entity identifiers and hello aggregated health state.</span></span> <span data-ttu-id="b9a9d-154">tooget entièrement l’intégrité pour un enfant, appeler un contrôle d’intégrité de la requête hello pour le type d’entité enfant hello et transmettez identificateur enfant de hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-154">tooget complete health for a child, call hello query health for hello child entity type and pass in hello child identifier.</span></span>
* <span data-ttu-id="b9a9d-155">les évaluations non intègres Hello toohello de ce point de rapport qui a déclenché état hello d’entité de hello, si l’entité de hello n’est pas intègre.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-155">hello unhealthy evaluations that point toohello report that triggered hello state of hello entity, if hello entity is not healthy.</span></span> <span data-ttu-id="b9a9d-156">les évaluations de Hello sont récursifs, contenant les évaluations d’intégrité hello enfants qui a déclenché l’état d’intégrité actuel.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-156">hello evaluations are recursive, containing hello children health evaluations that triggered current health state.</span></span> <span data-ttu-id="b9a9d-157">Par exemple, un agent de surveillance a signalé une erreur sur un réplica.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-157">For example, a watchdog reported an error against a replica.</span></span> <span data-ttu-id="b9a9d-158">intégrité des applications Hello montre une évaluation défectueuse en raison de service non intègre de tooan ; service de Hello est défectueux en raison de la partition tooa erreur ; partition de Hello est défectueux en raison de réplica tooa erreur ; réplica de Hello est défectueux en raison de l’état d’intégrité toohello surveillance erreur.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-158">hello application health shows an unhealthy evaluation due tooan unhealthy service; hello service is unhealthy due tooa partition in error; hello partition is unhealthy due tooa replica in error; hello replica is unhealthy due toohello watchdog error health report.</span></span>
* <span data-ttu-id="b9a9d-159">statistiques de contrôle d’intégrité Hello pour tous les types enfants d’entités hello qui ont des enfants.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-159">hello health statistics for all children types of hello entities that have children.</span></span> <span data-ttu-id="b9a9d-160">Par exemple, l’intégrité du cluster affiche hello le nombre total d’applications, services, partitions, les réplicas et déployé des entités dans un cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-160">For example, cluster health shows hello total number of applications, services, partitions, replicas, and deployed entities in hello cluster.</span></span> <span data-ttu-id="b9a9d-161">L’intégrité du service indique le nombre total de hello de partitions et réplicas sous hello de service spécifié.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-161">Service health shows hello total number of partitions and replicas under hello specified service.</span></span>

## <a name="get-cluster-health"></a><span data-ttu-id="b9a9d-162">Obtenir les données d’intégrité du cluster</span><span class="sxs-lookup"><span data-stu-id="b9a9d-162">Get cluster health</span></span>
<span data-ttu-id="b9a9d-163">Retourne hello d’intégrité de l’entité de cluster hello et contient les États d’intégrité hello d’applications et les nœuds (enfants de cluster de hello).</span><span class="sxs-lookup"><span data-stu-id="b9a9d-163">Returns hello health of hello cluster entity and contains hello health states of applications and nodes (children of hello cluster).</span></span> <span data-ttu-id="b9a9d-164">Entrée :</span><span class="sxs-lookup"><span data-stu-id="b9a9d-164">Input:</span></span>

* <span data-ttu-id="b9a9d-165">Stratégie de contrôle d’intégrité du cluster hello [facultatif] utilisé des nœuds de hello tooevaluate et les événements de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-165">[Optional] hello cluster health policy used tooevaluate hello nodes and hello cluster events.</span></span>
* <span data-ttu-id="b9a9d-166">Mappage de stratégie d’intégrité [facultatif] hello application, avec des stratégies de contrôle d’intégrité hello utilisé stratégies manifeste d’application hello toooverride.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-166">[Optional] hello application health policy map, with hello health policies used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="b9a9d-167">[Facultatif] Les filtres des événements, les nœuds et les applications qui spécifient les entrées sont dignes d’intérêt et doivent être retournés dans le résultat de hello (par exemple, uniquement, les erreurs ou avertissements et erreurs).</span><span class="sxs-lookup"><span data-stu-id="b9a9d-167">[Optional] Filters for events, nodes, and applications that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="b9a9d-168">Tous les événements, les nœuds et les applications sont utilisées tooevaluate hello entité agrégée contrôle d’intégrité, quel que soit le filtre de hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-168">All events, nodes, and applications are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="b9a9d-169">[Facultatif] Filtrer les statistiques d’intégrité tooexclude.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-169">[Optional] Filter tooexclude health statistics.</span></span>
* <span data-ttu-id="b9a9d-170">[Facultatif] Filtrer l’ensemble fibre optique tooinclude : / statistiques d’intégrité système dans hello statistiques d’intégrité.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-170">[Optional] Filter tooinclude fabric:/System health statistics in hello health statistics.</span></span> <span data-ttu-id="b9a9d-171">Applicable uniquement lorsque les statistiques d’intégrité hello ne sont pas exclus.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-171">Only applicable when hello health statistics are not excluded.</span></span> <span data-ttu-id="b9a9d-172">Par défaut, les statistiques d’intégrité hello incluent uniquement les statistiques pour les applications utilisateur et application du système de hello pas.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-172">By default, hello health statistics include only statistics for user applications and not hello System application.</span></span>

### <a name="api"></a><span data-ttu-id="b9a9d-173">API</span><span class="sxs-lookup"><span data-stu-id="b9a9d-173">API</span></span>
<span data-ttu-id="b9a9d-174">tooget d’intégrité de cluster, créez un `FabricClient` et appel hello [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) méthode sur son **HealthManager**.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-174">tooget cluster health, create a `FabricClient` and call hello [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) method on its **HealthManager**.</span></span>

<span data-ttu-id="b9a9d-175">Hello appel suivant reçoit l’intégrité du cluster hello :</span><span class="sxs-lookup"><span data-stu-id="b9a9d-175">hello following call gets hello cluster health:</span></span>

```csharp
ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync();
```

<span data-ttu-id="b9a9d-176">Bonjour de code suivant obtient l’intégrité du cluster hello en utilisant une stratégie de contrôle d’intégrité de cluster personnalisé et les filtres pour les nœuds et les applications.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-176">hello following code gets hello cluster health by using a custom cluster health policy and filters for nodes and applications.</span></span> <span data-ttu-id="b9a9d-177">Il spécifie que les statistiques d’intégrité hello incluent l’ensemble fibre optique hello : / statistiques du système.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-177">It specifies that hello health statistics include hello fabric:/System statistics.</span></span> <span data-ttu-id="b9a9d-178">Il crée [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription), qui contient des informations d’entrée de hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-178">It creates [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription), which contains hello input information.</span></span>

```csharp
var policy = new ClusterHealthPolicy()
{
    MaxPercentUnhealthyNodes = 20
};
var nodesFilter = new NodeHealthStatesFilter()
{
    HealthStateFilterValue = HealthStateFilter.Error | HealthStateFilter.Warning
};
var applicationsFilter = new ApplicationHealthStatesFilter()
{
    HealthStateFilterValue = HealthStateFilter.Error
};
var healthStatisticsFilter = new ClusterHealthStatisticsFilter()
{
    ExcludeHealthStatistics = false,
    IncludeSystemApplicationHealthStatistics = true
};
var queryDescription = new ClusterHealthQueryDescription()
{
    HealthPolicy = policy,
    ApplicationsFilter = applicationsFilter,
    NodesFilter = nodesFilter,
    HealthStatisticsFilter = healthStatisticsFilter
};

ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="b9a9d-179">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b9a9d-179">PowerShell</span></span>
<span data-ttu-id="b9a9d-180">intégrité de cluster hello Hello applet de commande tooget [Get-ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth).</span><span class="sxs-lookup"><span data-stu-id="b9a9d-180">hello cmdlet tooget hello cluster health is [Get-ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth).</span></span> <span data-ttu-id="b9a9d-181">Tout d’abord, connectez toohello cluster à l’aide de hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-181">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="b9a9d-182">Hello état du cluster de hello est cinq nœuds, l’application système hello et fabric : / WordCount configurée comme décrit.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-182">hello state of hello cluster is five nodes, hello system application, and fabric:/WordCount configured as described.</span></span>

<span data-ttu-id="b9a9d-183">Hello suivant l’applet de commande Obtient l’intégrité du cluster à l’aide de stratégies de contrôle d’intégrité par défaut.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-183">hello following cmdlet gets cluster health by using default health policies.</span></span> <span data-ttu-id="b9a9d-184">Hello état d’intégrité agrégé est un avertissement, car l’ensemble fibre optique de hello : WordCount application est avertissement.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-184">hello aggregated health state is warning, because hello fabric:/WordCount application is in warning.</span></span> <span data-ttu-id="b9a9d-185">Notez comment les évaluations non intègres hello fournissent des détails sur les conditions de hello qui a déclenché la santé hello agrégée.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-185">Note how hello unhealthy evaluations provide details on hello conditions that triggered hello aggregated health.</span></span>

```xml
PS D:\ServiceFabric> Get-ServiceFabricClusterHealth


AggregatedHealthState   : Warning
UnhealthyEvaluations    : 
                          Unhealthy applications: 100% (1/1), MaxPercentUnhealthyApplications=0%.
                          
                          Unhealthy application: ApplicationName='fabric:/WordCount', AggregatedHealthState='Warning'.
                          
                            Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                          
                            Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Warning'.
                          
                                Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                          
                                Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                          
                                    Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                          
                          
NodeHealthStates        : 
                          NodeName              : _Node_4
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_3
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_2
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_1
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_0
                          AggregatedHealthState : Ok
                          
ApplicationHealthStates : 
                          ApplicationName       : fabric:/System
                          AggregatedHealthState : Ok
                          
                          ApplicationName       : fabric:/WordCount
                          AggregatedHealthState : Warning
                          
HealthEvents            : None
HealthStatistics        : 
                          Node                  : 5 Ok, 0 Warning, 0 Error
                          Replica               : 6 Ok, 0 Warning, 0 Error
                          Partition             : 1 Ok, 1 Warning, 0 Error
                          Service               : 1 Ok, 1 Warning, 0 Error
                          DeployedServicePackage : 6 Ok, 0 Warning, 0 Error
                          DeployedApplication   : 5 Ok, 0 Warning, 0 Error
                          Application           : 0 Ok, 1 Warning, 0 Error
```

<span data-ttu-id="b9a9d-186">Hello applet de commande PowerShell suivante obtient hello état d’intégrité du cluster de hello en utilisant une stratégie d’application personnalisée.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-186">hello following PowerShell cmdlet gets hello health of hello cluster by using a custom application policy.</span></span> <span data-ttu-id="b9a9d-187">Il filtre les résultats tooget seules les applications et les nœuds d’erreur ou un avertissement.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-187">It filters results tooget only applications and nodes in error or warning.</span></span> <span data-ttu-id="b9a9d-188">En conséquence, aucun nœud n’est renvoyé puisqu’ils sont tous sains.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-188">As a result, no nodes are returned, as they are all healthy.</span></span> <span data-ttu-id="b9a9d-189">Uniquement hello fabric : / WordCount application respecte le filtre d’applications hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-189">Only hello fabric:/WordCount application respects hello applications filter.</span></span> <span data-ttu-id="b9a9d-190">Étant donné que la stratégie personnalisée de hello spécifie tooconsider avertissements comme des erreurs pour l’ensemble fibre optique hello : / application WordCount, application hello est évaluée comme erronée, et est donc de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-190">Because hello custom policy specifies tooconsider warnings as errors for hello fabric:/WordCount application, hello application is evaluated as in error, and so is hello cluster.</span></span>

```powershell
PS D:\ServiceFabric> $appHealthPolicy = New-Object -TypeName System.Fabric.Health.ApplicationHealthPolicy
$appHealthPolicy.ConsiderWarningAsError = $true
$appHealthPolicyMap = New-Object -TypeName System.Fabric.Health.ApplicationHealthPolicyMap
$appUri1 = New-Object -TypeName System.Uri -ArgumentList "fabric:/WordCount"
$appHealthPolicyMap.Add($appUri1, $appHealthPolicy)
Get-ServiceFabricClusterHealth -ApplicationHealthPolicyMap $appHealthPolicyMap -ApplicationsFilter "Warning,Error" -NodesFilter "Warning,Error" -ExcludeHealthStatistics


AggregatedHealthState   : Error
UnhealthyEvaluations    : 
                          Unhealthy applications: 100% (1/1), MaxPercentUnhealthyApplications=0%.
                          
                          Unhealthy application: ApplicationName='fabric:/WordCount', AggregatedHealthState='Error'.
                          
                            Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                          
                            Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                          
                                Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                          
                                Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                          
                                    Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=true.
                          
                          
NodeHealthStates        : None
ApplicationHealthStates : 
                          ApplicationName       : fabric:/WordCount
                          AggregatedHealthState : Error
                          
HealthEvents            : None
```

### <a name="rest"></a><span data-ttu-id="b9a9d-191">REST</span><span class="sxs-lookup"><span data-stu-id="b9a9d-191">REST</span></span>
<span data-ttu-id="b9a9d-192">Vous pouvez obtenir l’intégrité du cluster avec un [demande GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster) ou un [demande POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy) qui inclut les stratégies de contrôle d’intégrité décrits dans le corps de hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-192">You can get cluster health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-node-health"></a><span data-ttu-id="b9a9d-193">Obtenir les données d’intégrité du nœud</span><span class="sxs-lookup"><span data-stu-id="b9a9d-193">Get node health</span></span>
<span data-ttu-id="b9a9d-194">Retourne hello d’intégrité d’une entité de nœud et contient des événements de contrôle d’intégrité hello signalés sur le nœud de hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-194">Returns hello health of a node entity and contains hello health events reported on hello node.</span></span> <span data-ttu-id="b9a9d-195">Entrée :</span><span class="sxs-lookup"><span data-stu-id="b9a9d-195">Input:</span></span>

* <span data-ttu-id="b9a9d-196">Nom du nœud hello [obligatoire] qui identifie le nœud de hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-196">[Required] hello node name that identifies hello node.</span></span>
* <span data-ttu-id="b9a9d-197">Paramètres de stratégie de contrôle d’intégrité de cluster [facultatif] hello utilisé tooevaluate intégrité.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-197">[Optional] hello cluster health policy settings used tooevaluate health.</span></span>
* <span data-ttu-id="b9a9d-198">[Facultatif] Filtres pour les événements qui indiquent les entrées sont dignes d’intérêt et doivent être retournés dans le résultat de hello (par exemple, uniquement, les erreurs ou avertissements et erreurs).</span><span class="sxs-lookup"><span data-stu-id="b9a9d-198">[Optional] Filters for events that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="b9a9d-199">Tous les événements sont utilisés tooevaluate hello entité agrégée contrôle d’intégrité, quel que soit le filtre de hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-199">All events are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>

### <a name="api"></a><span data-ttu-id="b9a9d-200">API</span><span class="sxs-lookup"><span data-stu-id="b9a9d-200">API</span></span>
<span data-ttu-id="b9a9d-201">contrôle d’intégrité de nœud tooget via hello API, créez un `FabricClient` et appel hello [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) méthode sur son HealthManager.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-201">tooget node health through hello API, create a `FabricClient` and call hello [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="b9a9d-202">Hello de code suivant obtient d’intégrité de nœud hello pour le nom du nœud spécifié hello :</span><span class="sxs-lookup"><span data-stu-id="b9a9d-202">hello following code gets hello node health for hello specified node name:</span></span>

```csharp
NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(nodeName);
```

<span data-ttu-id="b9a9d-203">Hello de code suivant obtient le contrôle d’intégrité de nœud hello pour hello spécifié de nom de nœud et passe dans le filtre d’événements et de stratégie personnalisée à l’aide [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):</span><span class="sxs-lookup"><span data-stu-id="b9a9d-203">hello following code gets hello node health for hello specified node name and passes in events filter and custom policy through [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):</span></span>

```csharp
var queryDescription = new NodeHealthQueryDescription(nodeName)
{
    HealthPolicy = new ClusterHealthPolicy() {  ConsiderWarningAsError = true },
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.Warning },
};

NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="b9a9d-204">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b9a9d-204">PowerShell</span></span>
<span data-ttu-id="b9a9d-205">intégrité de nœud hello Hello applet de commande tooget [Get-ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth).</span><span class="sxs-lookup"><span data-stu-id="b9a9d-205">hello cmdlet tooget hello node health is [Get-ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth).</span></span> <span data-ttu-id="b9a9d-206">Tout d’abord, connectez toohello cluster à l’aide de hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-206">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>
<span data-ttu-id="b9a9d-207">Hello suivant l’applet de commande Obtient le contrôle d’intégrité de nœud hello à l’aide de stratégies de contrôle d’intégrité par défaut :</span><span class="sxs-lookup"><span data-stu-id="b9a9d-207">hello following cmdlet gets hello node health by using default health policies:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricNodeHealth _Node_1


NodeName              : _Node_1
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 3
                        SentAt                : 7/13/2017 4:39:23 PM
                        ReceivedAt            : 7/13/2017 4:40:47 PM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 4:40:47 PM, LastWarning = 1/1/0001 12:00:00 AM
```

<span data-ttu-id="b9a9d-208">Hello applet de commande suivante obtient hello état d’intégrité de tous les nœuds de cluster de hello :</span><span class="sxs-lookup"><span data-stu-id="b9a9d-208">hello following cmdlet gets hello health of all nodes in hello cluster:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricNode | Get-ServiceFabricNodeHealth | select NodeName, AggregatedHealthState | ft -AutoSize

NodeName AggregatedHealthState
-------- ---------------------
_Node_4                     Ok
_Node_3                     Ok
_Node_2                     Ok
_Node_1                     Ok
_Node_0                     Ok
```

### <a name="rest"></a><span data-ttu-id="b9a9d-209">REST</span><span class="sxs-lookup"><span data-stu-id="b9a9d-209">REST</span></span>
<span data-ttu-id="b9a9d-210">Vous pouvez obtenir l’intégrité du nœud avec un [demande GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node) ou un [demande POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy) qui inclut les stratégies de contrôle d’intégrité décrits dans le corps de hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-210">You can get node health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-application-health"></a><span data-ttu-id="b9a9d-211">Obtenir les données d’intégrité des applications</span><span class="sxs-lookup"><span data-stu-id="b9a9d-211">Get application health</span></span>
<span data-ttu-id="b9a9d-212">Hello retourne l’intégrité d’une entité de l’application.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-212">Returns hello health of an application entity.</span></span> <span data-ttu-id="b9a9d-213">Il contient les États d’intégrité de hello de l’application hello déployé et les enfants de service.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-213">It contains hello health states of hello deployed application and service children.</span></span> <span data-ttu-id="b9a9d-214">Entrée :</span><span class="sxs-lookup"><span data-stu-id="b9a9d-214">Input:</span></span>

* <span data-ttu-id="b9a9d-215">Hello [obligatoire] nom de l’application (URI) qui identifie l’application hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-215">[Required] hello application name (URI) that identifies hello application.</span></span>
* <span data-ttu-id="b9a9d-216">Stratégie de contrôle d’intégrité d’application hello [facultatif] utilisé des stratégies de manifeste d’application toooverride hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-216">[Optional] hello application health policy used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="b9a9d-217">[Facultatif] Les filtres des événements, les services et les applications déployées, spécifient les entrées sont dignes d’intérêt et doivent être retournés dans le résultat de hello (par exemple, uniquement, les erreurs ou avertissements et erreurs).</span><span class="sxs-lookup"><span data-stu-id="b9a9d-217">[Optional] Filters for events, services, and deployed applications that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="b9a9d-218">Tous les événements, les services et les applications déployées sont l’intégrité de l’entité agrégée d’hello tooevaluate utilisé, quel que soit le filtre de hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-218">All events, services, and deployed applications are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="b9a9d-219">[Facultatif] Filtrer les statistiques d’intégrité tooexclude hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-219">[Optional] Filter tooexclude hello health statistics.</span></span> <span data-ttu-id="b9a9d-220">Si non spécifié, les statistiques d’intégrité hello incluent OK de hello, d’avertissement et nombre d’erreurs pour tous les enfants de l’application : services, partitions, les réplicas, des applications déployées et déployé des packages de service.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-220">If not specified, hello health statistics include hello ok, warning, and error count for all application children: services, partitions, replicas, deployed applications, and deployed service packages.</span></span>

### <a name="api"></a><span data-ttu-id="b9a9d-221">API</span><span class="sxs-lookup"><span data-stu-id="b9a9d-221">API</span></span>
<span data-ttu-id="b9a9d-222">intégrité d’application tooget, créer un `FabricClient` et appel hello [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) méthode sur son HealthManager.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-222">tooget application health, create a `FabricClient` and call hello [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="b9a9d-223">Hello de code suivant obtient l’intégrité d’applications hello pour le nom d’application spécifié hello (URI) :</span><span class="sxs-lookup"><span data-stu-id="b9a9d-223">hello following code gets hello application health for hello specified application name (URI):</span></span>

```csharp
ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(applicationName);
```

<span data-ttu-id="b9a9d-224">Hello de code suivant obtient l’intégrité d’applications hello pour le nom d’application spécifié hello (URI), avec des filtres et des stratégies personnalisées spécifié via [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="b9a9d-224">hello following code gets hello application health for hello specified application name (URI), with filters and custom policies specified via [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription).</span></span>

```csharp
HealthStateFilter warningAndErrors = HealthStateFilter.Error | HealthStateFilter.Warning;
var serviceTypePolicy = new ServiceTypeHealthPolicy()
{
    MaxPercentUnhealthyPartitionsPerService = 0,
    MaxPercentUnhealthyReplicasPerPartition = 5,
    MaxPercentUnhealthyServices = 0,
};
var policy = new ApplicationHealthPolicy()
{
    ConsiderWarningAsError = false,
    DefaultServiceTypeHealthPolicy = serviceTypePolicy,
    MaxPercentUnhealthyDeployedApplications = 0,
};

var queryDescription = new ApplicationHealthQueryDescription(applicationName)
{
    HealthPolicy = policy,
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = warningAndErrors },
    ServicesFilter = new ServiceHealthStatesFilter() { HealthStateFilterValue = warningAndErrors },
    DeployedApplicationsFilter = new DeployedApplicationHealthStatesFilter() { HealthStateFilterValue = warningAndErrors },
};

ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="b9a9d-225">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b9a9d-225">PowerShell</span></span>
<span data-ttu-id="b9a9d-226">intégrité des applications Hello applet de commande tooget hello est [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="b9a9d-226">hello cmdlet tooget hello application health is [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps).</span></span> <span data-ttu-id="b9a9d-227">Tout d’abord, connectez toohello cluster à l’aide de hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-227">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="b9a9d-228">applet de commande suivante Hello retourne intégrité hello hello **fabric : / WordCount** application :</span><span class="sxs-lookup"><span data-stu-id="b9a9d-228">hello following cmdlet returns hello health of hello **fabric:/WordCount** application:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth fabric:/WordCount


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Warning
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Warning'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                                  
                                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                                  
ServiceHealthStates             : 
                                  ServiceName           : fabric:/WordCount/WordCountWebService
                                  AggregatedHealthState : Ok
                                  
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Warning
                                  
DeployedApplicationHealthStates : 
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_4
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_3
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_0
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_2
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_1
                                  AggregatedHealthState : Ok
                                  
HealthEvents                    : 
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 282
                                  SentAt                : 7/13/2017 5:57:05 PM
                                  ReceivedAt            : 7/13/2017 5:57:05 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 7/13/2017 5:57:05 PM, LastWarning = 1/1/0001 12:00:00 AM
                                  
HealthStatistics                : 
                                  Replica               : 6 Ok, 0 Warning, 0 Error
                                  Partition             : 1 Ok, 1 Warning, 0 Error
                                  Service               : 1 Ok, 1 Warning, 0 Error
                                  DeployedServicePackage : 6 Ok, 0 Warning, 0 Error
                                  DeployedApplication   : 5 Ok, 0 Warning, 0 Error
```

<span data-ttu-id="b9a9d-229">Hello suivant passe d’applet de commande PowerShell dans les stratégies personnalisées.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-229">hello following PowerShell cmdlet passes in custom policies.</span></span> <span data-ttu-id="b9a9d-230">filtre les enfants et les événements.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-230">It also filters children and events.</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth -ApplicationName fabric:/WordCount -ConsiderWarningAsError $true -ServicesFilter Error -EventsFilter Error -DeployedApplicationsFilter Error -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                                  
                                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=true.
                                  
ServiceHealthStates             : 
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Error
                                  
DeployedApplicationHealthStates : None
HealthEvents                    : None
```

### <a name="rest"></a><span data-ttu-id="b9a9d-231">REST</span><span class="sxs-lookup"><span data-stu-id="b9a9d-231">REST</span></span>
<span data-ttu-id="b9a9d-232">Vous pouvez obtenir le contrôle d’intégrité de l’application avec un [demande GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application) ou un [demande POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy) qui inclut les stratégies de contrôle d’intégrité décrits dans le corps de hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-232">You can get application health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-service-health"></a><span data-ttu-id="b9a9d-233">Obtenir l’état d’intégrité du service</span><span class="sxs-lookup"><span data-stu-id="b9a9d-233">Get service health</span></span>
<span data-ttu-id="b9a9d-234">Hello retourne l’intégrité d’une entité de service.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-234">Returns hello health of a service entity.</span></span> <span data-ttu-id="b9a9d-235">Il contient les États d’intégrité de partition hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-235">It contains hello partition health states.</span></span> <span data-ttu-id="b9a9d-236">Entrée :</span><span class="sxs-lookup"><span data-stu-id="b9a9d-236">Input:</span></span>

* <span data-ttu-id="b9a9d-237">Hello [obligatoire] nom de service (URI) qui identifie le service de hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-237">[Required] hello service name (URI) that identifies hello service.</span></span>
* <span data-ttu-id="b9a9d-238">Stratégie de contrôle d’intégrité d’application hello [facultatif] utilisé stratégie manifeste d’application hello toooverride.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-238">[Optional] hello application health policy used toooverride hello application manifest policy.</span></span>
* <span data-ttu-id="b9a9d-239">[Facultatif] Filtres pour les événements et les partitions qui spécifient les entrées sont dignes d’intérêt et doivent être retournés dans le résultat de hello (par exemple, uniquement, les erreurs ou avertissements et erreurs).</span><span class="sxs-lookup"><span data-stu-id="b9a9d-239">[Optional] Filters for events and partitions that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="b9a9d-240">Tous les événements et les partitions sont utilisées tooevaluate hello entité agrégée contrôle d’intégrité, quel que soit le filtre de hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-240">All events and partitions are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="b9a9d-241">[Facultatif] Filtrer les statistiques d’intégrité tooexclude.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-241">[Optional] Filter tooexclude health statistics.</span></span> <span data-ttu-id="b9a9d-242">Si non spécifié, hello hello d’afficher l’intégrité des statistiques OK, avertissement et erreur compter pour toutes les partitions et réplicas du service de hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-242">If not specified, hello health statistics show hello ok, warning, and error count for all partitions and replicas of hello service.</span></span>

### <a name="api"></a><span data-ttu-id="b9a9d-243">API</span><span class="sxs-lookup"><span data-stu-id="b9a9d-243">API</span></span>
<span data-ttu-id="b9a9d-244">l’intégrité du service tooget via hello API, créez un `FabricClient` et appel hello [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) méthode sur son HealthManager.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-244">tooget service health through hello API, create a `FabricClient` and call hello [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="b9a9d-245">Hello exemple suivant obtient le contrôle d’intégrité hello d’un service avec le nom de service spécifié (URI) :</span><span class="sxs-lookup"><span data-stu-id="b9a9d-245">hello following example gets hello health of a service with specified service name (URI):</span></span>

```charp
ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(serviceName);
```

<span data-ttu-id="b9a9d-246">Hello de code suivant obtient hello l’intégrité du service pour le nom de service spécifié hello (URI), en spécifiant des filtres et stratégie personnalisée via [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):</span><span class="sxs-lookup"><span data-stu-id="b9a9d-246">hello following code gets hello service health for hello specified service name (URI), specifying filters and custom policy via [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):</span></span>

```csharp
var queryDescription = new ServiceHealthQueryDescription(serviceName)
{
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.All },
    PartitionsFilter = new PartitionHealthStatesFilter() { HealthStateFilterValue = HealthStateFilter.Error },
};

ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="b9a9d-247">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b9a9d-247">PowerShell</span></span>
<span data-ttu-id="b9a9d-248">contrôle d’intégrité du service de hello tooget Hello applet de commande est [Get-ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth).</span><span class="sxs-lookup"><span data-stu-id="b9a9d-248">hello cmdlet tooget hello service health is [Get-ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth).</span></span> <span data-ttu-id="b9a9d-249">Tout d’abord, connectez toohello cluster à l’aide de hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-249">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="b9a9d-250">Hello suivant l’applet de commande Obtient l’intégrité du service hello à l’aide de stratégies de contrôle d’intégrité par défaut :</span><span class="sxs-lookup"><span data-stu-id="b9a9d-250">hello following cmdlet gets hello service health by using default health policies:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricServiceHealth -ServiceName fabric:/WordCount/WordCountService


ServiceName           : fabric:/WordCount/WordCountService
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                        
                        Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                        
                            Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
PartitionHealthStates : 
                        PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
                        AggregatedHealthState : Warning
                        
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 15
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Service has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                        
HealthStatistics      : 
                        Replica               : 5 Ok, 0 Warning, 0 Error
                        Partition             : 0 Ok, 1 Warning, 0 Error
```

### <a name="rest"></a><span data-ttu-id="b9a9d-251">REST</span><span class="sxs-lookup"><span data-stu-id="b9a9d-251">REST</span></span>
<span data-ttu-id="b9a9d-252">Vous pouvez obtenir l’intégrité du service avec un [demande GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service) ou un [demande POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy) qui inclut les stratégies de contrôle d’intégrité décrits dans le corps de hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-252">You can get service health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-partition-health"></a><span data-ttu-id="b9a9d-253">Obtenir l'intégrité de la partition</span><span class="sxs-lookup"><span data-stu-id="b9a9d-253">Get partition health</span></span>
<span data-ttu-id="b9a9d-254">Hello retourne l’intégrité d’une entité de la partition.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-254">Returns hello health of a partition entity.</span></span> <span data-ttu-id="b9a9d-255">Il contient les États d’intégrité de réplica hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-255">It contains hello replica health states.</span></span> <span data-ttu-id="b9a9d-256">Entrée :</span><span class="sxs-lookup"><span data-stu-id="b9a9d-256">Input:</span></span>

* <span data-ttu-id="b9a9d-257">Partition hello [obligatoire] ID (GUID) qui identifie la partition de hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-257">[Required] hello partition ID (GUID) that identifies hello partition.</span></span>
* <span data-ttu-id="b9a9d-258">Stratégie de contrôle d’intégrité d’application hello [facultatif] utilisé stratégie manifeste d’application hello toooverride.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-258">[Optional] hello application health policy used toooverride hello application manifest policy.</span></span>
* <span data-ttu-id="b9a9d-259">[Facultatif] Filtres des réplicas qui spécifient les entrées et les événements sont dignes d’intérêt et doivent être retournés dans le résultat de hello (par exemple, uniquement, les erreurs ou avertissements et erreurs).</span><span class="sxs-lookup"><span data-stu-id="b9a9d-259">[Optional] Filters for events and replicas that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="b9a9d-260">Tous les événements et les réplicas sont utilisés tooevaluate hello entité agrégée contrôle d’intégrité, quel que soit le filtre de hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-260">All events and replicas are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="b9a9d-261">[Facultatif] Filtrer les statistiques d’intégrité tooexclude.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-261">[Optional] Filter tooexclude health statistics.</span></span> <span data-ttu-id="b9a9d-262">Si non spécifié, les statistiques d’intégrité hello indiquent le nombre de réplicas dans OK, avertissement et erreur États.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-262">If not specified, hello health statistics show how many replicas are in ok, warning, and error states.</span></span>

### <a name="api"></a><span data-ttu-id="b9a9d-263">API</span><span class="sxs-lookup"><span data-stu-id="b9a9d-263">API</span></span>
<span data-ttu-id="b9a9d-264">contrôle d’intégrité de la partition tooget via hello API, créez un `FabricClient` et appel hello [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) méthode sur son HealthManager.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-264">tooget partition health through hello API, create a `FabricClient` and call hello [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) method on its HealthManager.</span></span> <span data-ttu-id="b9a9d-265">créer des paramètres facultatifs de toospecify, [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="b9a9d-265">toospecify optional parameters, create [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription).</span></span>

```csharp
PartitionHealth partitionHealth = await fabricClient.HealthManager.GetPartitionHealthAsync(partitionId);
```

### <a name="powershell"></a><span data-ttu-id="b9a9d-266">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b9a9d-266">PowerShell</span></span>
<span data-ttu-id="b9a9d-267">intégrité de partition hello Hello applet de commande tooget [Get-ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth).</span><span class="sxs-lookup"><span data-stu-id="b9a9d-267">hello cmdlet tooget hello partition health is [Get-ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth).</span></span> <span data-ttu-id="b9a9d-268">Tout d’abord, connectez toohello cluster à l’aide de hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-268">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="b9a9d-269">Hello applet de commande suivante obtient hello pour toutes les partitions de hello **fabric : / WordCount/WordCountService** service et exclut les États d’intégrité de réplica :</span><span class="sxs-lookup"><span data-stu-id="b9a9d-269">hello following cmdlet gets hello health for all partitions of hello **fabric:/WordCount/WordCountService** service and filters out replica health states:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricPartitionHealth -ReplicasFilter None

PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Warning
                        SequenceNumber        : 72
                        SentAt                : 7/13/2017 5:57:29 PM
                        ReceivedAt            : 7/13/2017 5:57:48 PM
                        TTL                   : Infinite
                        Description           : Partition is below target replica or instance count.
                        fabric:/WordCount/WordCountService 7 2 af2e3e44-a8f8-45ac-9f31-4093eb897600
                          N/P RD _Node_2 Up 131444422260002646
                          N/S RD _Node_4 Up 131444422293113678
                          N/S RD _Node_3 Up 131444422293113679
                          N/S RD _Node_1 Up 131444422293118720
                          N/S RD _Node_0 Up 131444422293118721
                          (Showing 5 out of 5 replicas. Total available replicas: 5.)
                        
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Ok->Warning = 7/13/2017 5:57:48 PM, LastError = 1/1/0001 12:00:00 AM
                        
                        SourceId              : System.PLB
                        Property              : ServiceReplicaUnplacedHealth_Secondary_af2e3e44-a8f8-45ac-9f31-4093eb897600
                        HealthState           : Warning
                        SequenceNumber        : 131444445174851664
                        SentAt                : 7/13/2017 6:35:17 PM
                        ReceivedAt            : 7/13/2017 6:35:18 PM
                        TTL                   : 00:01:05
                        Description           : hello Load Balancer was unable toofind a placement for one or more of hello Service's Replicas:
                        Secondary replica could not be placed due toohello following constraints and properties:  
                        TargetReplicaSetSize: 7
                        Placement Constraint: N/A
                        Parent Service: N/A
                        
                        Constraint Elimination Sequence:
                        Existing Secondary Replicas eliminated 4 possible node(s) for placement -- 1/5 node(s) remain.
                        Existing Primary Replica eliminated 1 possible node(s) for placement -- 0/5 node(s) remain.
                        
                        Nodes Eliminated By Constraints:
                        
                        Existing Secondary Replicas -- Nodes with Partition's Existing Secondary Replicas/Instances:
                        --
                        FaultDomain:fd:/4 NodeName:_Node_4 NodeType:NodeType4 UpgradeDomain:4 UpgradeDomain: ud:/4 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/3 NodeName:_Node_3 NodeType:NodeType3 UpgradeDomain:3 UpgradeDomain: ud:/3 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/1 NodeName:_Node_1 NodeType:NodeType1 UpgradeDomain:1 UpgradeDomain: ud:/1 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/0 NodeName:_Node_0 NodeType:NodeType0 UpgradeDomain:0 UpgradeDomain: ud:/0 Deactivation Intent/Status: None/None
                        
                        Existing Primary Replica -- Nodes with Partition's Existing Primary Replica or Secondary Replicas:
                        --
                        FaultDomain:fd:/2 NodeName:_Node_2 NodeType:NodeType2 UpgradeDomain:2 UpgradeDomain: ud:/2 Deactivation Intent/Status: None/None
                        
                        
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/13/2017 5:57:48 PM, LastOk = 1/1/0001 12:00:00 AM
                        
HealthStatistics      : 
                        Replica               : 5 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a><span data-ttu-id="b9a9d-270">REST</span><span class="sxs-lookup"><span data-stu-id="b9a9d-270">REST</span></span>
<span data-ttu-id="b9a9d-271">Vous pouvez obtenir le contrôle d’intégrité de la partition avec un [demande GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition) ou un [demande POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy) qui inclut les stratégies de contrôle d’intégrité décrits dans le corps de hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-271">You can get partition health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-replica-health"></a><span data-ttu-id="b9a9d-272">Obtenir les données d’intégrité des réplicas</span><span class="sxs-lookup"><span data-stu-id="b9a9d-272">Get replica health</span></span>
<span data-ttu-id="b9a9d-273">Retourne le contrôle d’intégrité hello d’un réplica de service avec état ou d’une instance de service sans état.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-273">Returns hello health of a stateful service replica or a stateless service instance.</span></span> <span data-ttu-id="b9a9d-274">Entrée :</span><span class="sxs-lookup"><span data-stu-id="b9a9d-274">Input:</span></span>

* <span data-ttu-id="b9a9d-275">Hello [obligatoire] ID (GUID) et le réplica ID de partition qui identifie le réplica de hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-275">[Required] hello partition ID (GUID) and replica ID that identifies hello replica.</span></span>
* <span data-ttu-id="b9a9d-276">Les paramètres de stratégie de contrôle d’intégrité application hello [facultatif] utilisé des stratégies de manifeste d’application toooverride hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-276">[Optional] hello application health policy parameters used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="b9a9d-277">[Facultatif] Filtres pour les événements qui indiquent les entrées sont dignes d’intérêt et doivent être retournés dans le résultat de hello (par exemple, uniquement, les erreurs ou avertissements et erreurs).</span><span class="sxs-lookup"><span data-stu-id="b9a9d-277">[Optional] Filters for events that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="b9a9d-278">Tous les événements sont utilisés tooevaluate hello entité agrégée contrôle d’intégrité, quel que soit le filtre de hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-278">All events are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>

### <a name="api"></a><span data-ttu-id="b9a9d-279">API</span><span class="sxs-lookup"><span data-stu-id="b9a9d-279">API</span></span>
<span data-ttu-id="b9a9d-280">contrôle d’intégrité du réplica tooget hello via hello API, créez un `FabricClient` et appel hello [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) méthode sur son HealthManager.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-280">tooget hello replica health through hello API, create a `FabricClient` and call hello [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) method on its HealthManager.</span></span> <span data-ttu-id="b9a9d-281">toospecify avancée des paramètres, utilisez [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="b9a9d-281">toospecify advanced parameters, use [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription).</span></span>

```csharp
ReplicaHealth replicaHealth = await fabricClient.HealthManager.GetReplicaHealthAsync(partitionId, replicaId);
```

### <a name="powershell"></a><span data-ttu-id="b9a9d-282">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b9a9d-282">PowerShell</span></span>
<span data-ttu-id="b9a9d-283">intégrité de réplica hello Hello applet de commande tooget [Get-ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth).</span><span class="sxs-lookup"><span data-stu-id="b9a9d-283">hello cmdlet tooget hello replica health is [Get-ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth).</span></span> <span data-ttu-id="b9a9d-284">Tout d’abord, connectez toohello cluster à l’aide de hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-284">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="b9a9d-285">Hello applet de commande suivante obtient hello du réplica principal de hello pour toutes les partitions du service de hello :</span><span class="sxs-lookup"><span data-stu-id="b9a9d-285">hello following cmdlet gets hello health of hello primary replica for all partitions of hello service:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricReplica | where {$_.ReplicaRole -eq "Primary"} | Get-ServiceFabricReplicaHealth


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422260002646
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131444422263668344
                        SentAt                : 7/13/2017 5:57:06 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_2
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a><span data-ttu-id="b9a9d-286">REST</span><span class="sxs-lookup"><span data-stu-id="b9a9d-286">REST</span></span>
<span data-ttu-id="b9a9d-287">Vous pouvez obtenir l’intégrité du réplica avec une [demande GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica) ou un [demande POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy) qui inclut les stratégies de contrôle d’intégrité décrits dans le corps de hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-287">You can get replica health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-deployed-application-health"></a><span data-ttu-id="b9a9d-288">Obtenir les données d’intégrité des applications déployées</span><span class="sxs-lookup"><span data-stu-id="b9a9d-288">Get deployed application health</span></span>
<span data-ttu-id="b9a9d-289">Hello retourne l’intégrité d’une application déployée sur une entité de nœud.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-289">Returns hello health of an application deployed on a node entity.</span></span> <span data-ttu-id="b9a9d-290">Il contient les États de fonctionnement de package de service hello déployé.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-290">It contains hello deployed service package health states.</span></span> <span data-ttu-id="b9a9d-291">Entrée :</span><span class="sxs-lookup"><span data-stu-id="b9a9d-291">Input:</span></span>

* <span data-ttu-id="b9a9d-292">Nom de l’application hello [obligatoire] (URI) et le nom de nœud (chaîne) qui identifient hello déploiement l’application.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-292">[Required] hello application name (URI) and node name (string) that identify hello deployed application.</span></span>
* <span data-ttu-id="b9a9d-293">Stratégie de contrôle d’intégrité d’application hello [facultatif] utilisé des stratégies de manifeste d’application toooverride hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-293">[Optional] hello application health policy used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="b9a9d-294">[Facultatif] Filtres pour les événements et les packages de service déployé qui spécifient les entrées sont dignes d’intérêt et doivent être retournés dans le résultat de hello (par exemple, uniquement, les erreurs ou avertissements et erreurs).</span><span class="sxs-lookup"><span data-stu-id="b9a9d-294">[Optional] Filters for events and deployed service packages that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="b9a9d-295">Tous les événements et les packages de service déployé sont l’intégrité de l’entité agrégée d’hello tooevaluate utilisé, quel que soit le filtre de hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-295">All events and deployed service packages are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="b9a9d-296">[Facultatif] Filtrer les statistiques d’intégrité tooexclude.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-296">[Optional] Filter tooexclude health statistics.</span></span> <span data-ttu-id="b9a9d-297">Si non spécifié, les statistiques d’intégrité hello affichent nombre hello des packages de service déployé dans les États d’intégrité OK, avertissement et erreur.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-297">If not specified, hello health statistics show hello number of deployed service packages in ok, warning, and error health states.</span></span>

### <a name="api"></a><span data-ttu-id="b9a9d-298">API</span><span class="sxs-lookup"><span data-stu-id="b9a9d-298">API</span></span>
<span data-ttu-id="b9a9d-299">contrôle d’intégrité de hello tooget d’une application déployée sur un nœud via hello API, créez un `FabricClient` et appel hello [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) méthode sur son HealthManager.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-299">tooget hello health of an application deployed on a node through hello API, create a `FabricClient` and call hello [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) method on its HealthManager.</span></span> <span data-ttu-id="b9a9d-300">utiliser des paramètres facultatifs de toospecify, [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="b9a9d-300">toospecify optional parameters, use [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription).</span></span>

```csharp
DeployedApplicationHealth health = await fabricClient.HealthManager.GetDeployedApplicationHealthAsync(
    new DeployedApplicationHealthQueryDescription(applicationName, nodeName));
```

### <a name="powershell"></a><span data-ttu-id="b9a9d-301">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b9a9d-301">PowerShell</span></span>
<span data-ttu-id="b9a9d-302">Bonjour applet de commande tooget hello déployé l’intégrité d’applications est [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="b9a9d-302">hello cmdlet tooget hello deployed application health is [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps).</span></span> <span data-ttu-id="b9a9d-303">Tout d’abord, connectez toohello cluster à l’aide de hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-303">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="b9a9d-304">toofind out où une application est déployée, exécutez [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) et examinez hello déployé des enfants de l’application.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-304">toofind out where an application is deployed, run [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) and look at hello deployed application children.</span></span>

<span data-ttu-id="b9a9d-305">Hello applet de commande suivante obtient intégrité hello hello **fabric : / WordCount** application déployée sur **_Node_2**.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-305">hello following cmdlet gets hello health of hello **fabric:/WordCount** application deployed on **_Node_2**.</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricDeployedApplicationHealth -ApplicationName fabric:/WordCount -NodeName _Node_0


ApplicationName                    : fabric:/WordCount
NodeName                           : _Node_0
AggregatedHealthState              : Ok
DeployedServicePackageHealthStates : 
                                     ServiceManifestName   : WordCountServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_0
                                     AggregatedHealthState : Ok
                                     
                                     ServiceManifestName   : WordCountWebServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_0
                                     AggregatedHealthState : Ok
                                     
HealthEvents                       : 
                                     SourceId              : System.Hosting
                                     Property              : Activation
                                     HealthState           : Ok
                                     SequenceNumber        : 131444422261848308
                                     SentAt                : 7/13/2017 5:57:06 PM
                                     ReceivedAt            : 7/13/2017 5:57:17 PM
                                     TTL                   : Infinite
                                     Description           : hello application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/13/2017 5:57:17 PM, LastWarning = 1/1/0001 12:00:00 AM
                                     
HealthStatistics                   : 
                                     DeployedServicePackage : 2 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a><span data-ttu-id="b9a9d-306">REST</span><span class="sxs-lookup"><span data-stu-id="b9a9d-306">REST</span></span>
<span data-ttu-id="b9a9d-307">Vous pouvez obtenir le contrôle d’intégrité de l’application déployée avec une [demande GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application) ou un [demande POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy) qui inclut les stratégies de contrôle d’intégrité décrits dans le corps de hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-307">You can get deployed application health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-deployed-service-package-health"></a><span data-ttu-id="b9a9d-308">Obtenir les données d’intégrité d’un package de services déployé</span><span class="sxs-lookup"><span data-stu-id="b9a9d-308">Get deployed service package health</span></span>
<span data-ttu-id="b9a9d-309">Retourne hello d’intégrité d’une entité de package de service déployé.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-309">Returns hello health of a deployed service package entity.</span></span> <span data-ttu-id="b9a9d-310">Entrée :</span><span class="sxs-lookup"><span data-stu-id="b9a9d-310">Input:</span></span>

* <span data-ttu-id="b9a9d-311">Nom de l’application hello [obligatoire] (URI), le nom de nœud (chaîne) et nom de manifeste de service (chaîne) qui identifient hello déploiement le package de service.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-311">[Required] hello application name (URI), node name (string), and service manifest name (string) that identify hello deployed service package.</span></span>
* <span data-ttu-id="b9a9d-312">Stratégie de contrôle d’intégrité d’application hello [facultatif] utilisé stratégie manifeste d’application hello toooverride.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-312">[Optional] hello application health policy used toooverride hello application manifest policy.</span></span>
* <span data-ttu-id="b9a9d-313">[Facultatif] Filtres pour les événements qui indiquent les entrées sont dignes d’intérêt et doivent être retournés dans le résultat de hello (par exemple, uniquement, les erreurs ou avertissements et erreurs).</span><span class="sxs-lookup"><span data-stu-id="b9a9d-313">[Optional] Filters for events that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="b9a9d-314">Tous les événements sont utilisés tooevaluate hello entité agrégée contrôle d’intégrité, quel que soit le filtre de hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-314">All events are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>

### <a name="api"></a><span data-ttu-id="b9a9d-315">API</span><span class="sxs-lookup"><span data-stu-id="b9a9d-315">API</span></span>
<span data-ttu-id="b9a9d-316">contrôle d’intégrité de hello tooget d’un package de service déployé via hello API, créez un `FabricClient` et appel hello [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) méthode sur son HealthManager.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-316">tooget hello health of a deployed service package through hello API, create a `FabricClient` and call hello [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) method on its HealthManager.</span></span> <span data-ttu-id="b9a9d-317">utiliser des paramètres facultatifs de toospecify, [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="b9a9d-317">toospecify optional parameters, use [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription).</span></span>

```csharp
DeployedServicePackageHealth health = await fabricClient.HealthManager.GetDeployedServicePackageHealthAsync(
    new DeployedServicePackageHealthQueryDescription(applicationName, nodeName, serviceManifestName));
```

### <a name="powershell"></a><span data-ttu-id="b9a9d-318">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b9a9d-318">PowerShell</span></span>
<span data-ttu-id="b9a9d-319">Bonjour applet de commande tooget hello déployé package l’intégrité du service est [Get-ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth).</span><span class="sxs-lookup"><span data-stu-id="b9a9d-319">hello cmdlet tooget hello deployed service package health is [Get-ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth).</span></span> <span data-ttu-id="b9a9d-320">Tout d’abord, connectez toohello cluster à l’aide de hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-320">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="b9a9d-321">toosee où une application est déployée, exécutez [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) et examinez les applications hello déployé.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-321">toosee where an application is deployed, run [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) and look at hello deployed applications.</span></span> <span data-ttu-id="b9a9d-322">toosee qui packages de service figurent dans une application, recherchez à hello déployé enfants de package de service Bonjour [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps) sortie.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-322">toosee which service packages are in an application, look at hello deployed service package children in hello [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps) output.</span></span>

<span data-ttu-id="b9a9d-323">Hello applet de commande suivante obtient intégrité hello hello **WordCountServicePkg** package de service de hello **fabric : / WordCount** application déployée sur **_Node_2**.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-323">hello following cmdlet gets hello health of hello **WordCountServicePkg** service package of hello **fabric:/WordCount** application deployed on **_Node_2**.</span></span> <span data-ttu-id="b9a9d-324">entité de Hello a **System.Hosting** des rapports d’activation d’un package de service et de point d’entrée et une inscription réussie de type de service.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-324">hello entity has **System.Hosting** reports for successful service-package and entry-point activation, and successful service-type registration.</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricDeployedApplication -ApplicationName fabric:/WordCount -NodeName _Node_2 | Get-ServiceFabricDeployedServicePackageHealth -ServiceManifestName WordCountServicePkg


ApplicationName            : fabric:/WordCount
ServiceManifestName        : WordCountServicePkg
ServicePackageActivationId : 
NodeName                   : _Node_2
AggregatedHealthState      : Ok
HealthEvents               : 
                             SourceId              : System.Hosting
                             Property              : Activation
                             HealthState           : Ok
                             SequenceNumber        : 131444422267693359
                             SentAt                : 7/13/2017 5:57:06 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : hello ServicePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : CodePackageActivation:Code:EntryPoint
                             HealthState           : Ok
                             SequenceNumber        : 131444422267903345
                             SentAt                : 7/13/2017 5:57:06 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : hello CodePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : ServiceTypeRegistration:WordCountServiceType
                             HealthState           : Ok
                             SequenceNumber        : 131444422272458374
                             SentAt                : 7/13/2017 5:57:07 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : hello ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a><span data-ttu-id="b9a9d-325">REST</span><span class="sxs-lookup"><span data-stu-id="b9a9d-325">REST</span></span>
<span data-ttu-id="b9a9d-326">Vous pouvez obtenir l’intégrité de package de service déployé avec un [demande GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package) ou un [demande POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy) qui inclut les stratégies de contrôle d’intégrité décrits dans le corps de hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-326">You can get deployed service package health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="health-chunk-queries"></a><span data-ttu-id="b9a9d-327">Requêtes par segment d’intégrité</span><span class="sxs-lookup"><span data-stu-id="b9a9d-327">Health chunk queries</span></span>
<span data-ttu-id="b9a9d-328">les requêtes de bloc de contrôle d’intégrité Hello peuvent retourner des enfants de cluster à plusieurs niveaux (de manière récursive), par les filtres d’entrée.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-328">hello health chunk queries can return multi-level cluster children (recursively), per input filters.</span></span> <span data-ttu-id="b9a9d-329">Il prend en charge les filtres avancés qui permettent une grande souplesse dans le choix des enfants de hello toobe retourné.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-329">It supports advanced filters that allow a lot of flexibility in choosing hello children toobe returned.</span></span> <span data-ttu-id="b9a9d-330">les filtres de Hello peuvent spécifier des enfants en identificateur hello ou par d’autres identificateurs de groupe et/ou les États d’intégrité.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-330">hello filters can specify children by hello unique identifier or by other group identifiers and/or health states.</span></span> <span data-ttu-id="b9a9d-331">Par défaut, aucun enfant n’est inclus, que les commandes toohealth opposés qui incluent toujours les enfants de premier niveau.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-331">By default, no children are included, as opposed toohealth commands that always include first-level children.</span></span>

<span data-ttu-id="b9a9d-332">Hello [requêtes d’intégrité](service-fabric-view-entities-aggregated-health.md#health-queries) retournés enfants de premier niveau uniquement de hello spécifié entité par les filtres requis.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-332">hello [health queries](service-fabric-view-entities-aggregated-health.md#health-queries) return only first-level children of hello specified entity per required filters.</span></span> <span data-ttu-id="b9a9d-333">tooget hello les enfants des enfants de hello, vous devez appeler d’intégrité supplémentaires API pour chaque entité d’intérêt.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-333">tooget hello children of hello children, you must call additional health APIs for each entity of interest.</span></span> <span data-ttu-id="b9a9d-334">De même, la santé hello tooget des entités spécifiques, vous devez appeler d’intégrité une d’API pour chaque entité de votre choix.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-334">Similarly, tooget hello health of specific entities, you must call one health API for each desired entity.</span></span> <span data-ttu-id="b9a9d-335">Hello segment requête filtrage avancé vous permet de toorequest plusieurs éléments d’intérêt dans une requête, en réduisant la taille des messages hello et nombre hello de messages.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-335">hello chunk query advanced filtering allows you toorequest multiple items of interest in one query, minimizing hello message size and hello number of messages.</span></span>

<span data-ttu-id="b9a9d-336">valeur de Hello de requête de segment hello est que vous pouvez obtenir l’état d’intégrité pour plusieurs entités de cluster (potentiellement toutes les entités de cluster en commençant à la racine requis) dans un seul appel.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-336">hello value of hello chunk query is that you can get health state for more cluster entities (potentially all cluster entities starting at required root) in one call.</span></span> <span data-ttu-id="b9a9d-337">Vous pouvez transmettre des requêtes d’intégrité complexes, comme :</span><span class="sxs-lookup"><span data-stu-id="b9a9d-337">You can express complex health query such as:</span></span>

* <span data-ttu-id="b9a9d-338">Retourner uniquement les applications ayant des erreurs, et pour ces applications inclure l’ensemble des services affichant un état d’avertissement ou d’erreur.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-338">Return only applications in error, and for those applications include all services in warning or error.</span></span> <span data-ttu-id="b9a9d-339">Pour les services renvoyés, inclure l’ensemble des partitions.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-339">For returned services, include all partitions.</span></span>
* <span data-ttu-id="b9a9d-340">Retourner uniquement hello contrôle d’intégrité de quatre applications, spécifiée par leurs noms.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-340">Return only hello health of four applications, specified by their names.</span></span>
* <span data-ttu-id="b9a9d-341">Retourner uniquement hello contrôle d’intégrité des applications d’un type de l’application souhaitée.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-341">Return only hello health of applications of a desired application type.</span></span>
* <span data-ttu-id="b9a9d-342">Renvoyer l’ensemble des entités déployées sur un nœud.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-342">Return all deployed entities on a node.</span></span> <span data-ttu-id="b9a9d-343">Retourne toutes les applications, toutes les applications déployées sur le nœud spécifié de hello et tous les packages de service hello déployé sur ce nœud.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-343">Returns all applications, all deployed applications on hello specified node and all hello deployed service packages on that node.</span></span>
* <span data-ttu-id="b9a9d-344">Retourner l’ensemble des réplicas présentant l’état d’erreur.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-344">Return all replicas in error.</span></span> <span data-ttu-id="b9a9d-345">L’ensemble des applications, des services, des partitions et uniquement les réplicas présentant un état d’erreur sont retournés.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-345">Returns all applications, services, partitions, and only replicas in error.</span></span>
* <span data-ttu-id="b9a9d-346">Renvoyer l’ensemble des applications.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-346">Return all applications.</span></span> <span data-ttu-id="b9a9d-347">Pour un service spécifié, inclure l’ensemble des partitions.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-347">For a specified service, include all partitions.</span></span>

<span data-ttu-id="b9a9d-348">Actuellement, requête de bloc de contrôle d’intégrité hello est exposé uniquement pour les entités de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-348">Currently, hello health chunk query is exposed only for hello cluster entity.</span></span> <span data-ttu-id="b9a9d-349">Elle renvoie un segment d’intégrité de cluster, qui comprend :</span><span class="sxs-lookup"><span data-stu-id="b9a9d-349">It returns a cluster health chunk, which contains:</span></span>

* <span data-ttu-id="b9a9d-350">état d’intégrité de cluster agrégée Hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-350">hello cluster aggregated health state.</span></span>
* <span data-ttu-id="b9a9d-351">liste de segment état Hello d’intégrité des nœuds qui respectent les filtres d’entrée.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-351">hello health state chunk list of nodes that respect input filters.</span></span>
* <span data-ttu-id="b9a9d-352">liste de segment état Hello d’intégrité des applications qui respectent les filtres d’entrée.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-352">hello health state chunk list of applications that respect input filters.</span></span> <span data-ttu-id="b9a9d-353">Chaque segment d’état de santé application contient une liste de blocs avec tous les services qui respectent les filtres d’entrée et une liste de blocs avec toutes les applications déployées qui respectent les filtres hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-353">Each application health state chunk contains a chunk list with all services that respect input filters and a chunk list with all deployed applications that respect hello filters.</span></span> <span data-ttu-id="b9a9d-354">Même pour les enfants hello des services et des applications déployées.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-354">Same for hello children of services and deployed applications.</span></span> <span data-ttu-id="b9a9d-355">De cette manière, toutes les entités dans un cluster de hello peuvent être potentiellement retournées si nécessaire, de manière hiérarchique.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-355">This way, all entities in hello cluster can be potentially returned if requested, in a hierarchical fashion.</span></span>

### <a name="cluster-health-chunk-query"></a><span data-ttu-id="b9a9d-356">Requête par segment d’intégrité de cluster</span><span class="sxs-lookup"><span data-stu-id="b9a9d-356">Cluster health chunk query</span></span>
<span data-ttu-id="b9a9d-357">Retourne hello d’intégrité de l’entité de cluster hello et contient des segments d’état d’intégrité hiérarchique hello des enfants obligatoires.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-357">Returns hello health of hello cluster entity and contains hello hierarchical health state chunks of required children.</span></span> <span data-ttu-id="b9a9d-358">Entrée :</span><span class="sxs-lookup"><span data-stu-id="b9a9d-358">Input:</span></span>

* <span data-ttu-id="b9a9d-359">Stratégie de contrôle d’intégrité du cluster hello [facultatif] utilisé des nœuds de hello tooevaluate et les événements de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-359">[Optional] hello cluster health policy used tooevaluate hello nodes and hello cluster events.</span></span>
* <span data-ttu-id="b9a9d-360">Mappage de stratégie d’intégrité [facultatif] hello application, avec des stratégies de contrôle d’intégrité hello utilisé stratégies manifeste d’application hello toooverride.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-360">[Optional] hello application health policy map, with hello health policies used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="b9a9d-361">[Facultatif] Filtres pour les nœuds et les applications qui spécifient les entrées sont dignes d’intérêt et doivent être retournés dans le résultat de hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-361">[Optional] Filters for nodes and applications that specify which entries are of interest and should be returned in hello result.</span></span> <span data-ttu-id="b9a9d-362">filtres de Hello sont spécifiques tooan entité/groupe d’entités ou entités tooall applicable à ce niveau.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-362">hello filters are specific tooan entity/group of entities or are applicable tooall entities at that level.</span></span> <span data-ttu-id="b9a9d-363">liste de Hello de filtres peut contenir un seul filtre général et/ou des filtres pour les entités de granularité toofine identificateurs spécifique retournées par la requête de hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-363">hello list of filters can contain one general filter and/or filters for specific identifiers toofine-grain entities returned by hello query.</span></span> <span data-ttu-id="b9a9d-364">Si elle est vide, les enfants de hello ne sont pas retournés par défaut.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-364">If empty, hello children are not returned by default.</span></span>
  <span data-ttu-id="b9a9d-365">En savoir plus sur les filtres de hello au [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) et [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter).</span><span class="sxs-lookup"><span data-stu-id="b9a9d-365">Read more about hello filters at [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) and [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter).</span></span> <span data-ttu-id="b9a9d-366">récursive de Hello application des filtres peuvent spécifier des filtres avancés pour les enfants.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-366">hello application filters can recursively specify advanced filters for children.</span></span>

<span data-ttu-id="b9a9d-367">résultat de segment Hello inclut enfants hello qui respectent les filtres hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-367">hello chunk result includes hello children that respect hello filters.</span></span>

<span data-ttu-id="b9a9d-368">Actuellement, requête de segment hello ne retourne pas les événements de l’entité ou les évaluations non intègres.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-368">Currently, hello chunk query does not return unhealthy evaluations or entity events.</span></span> <span data-ttu-id="b9a9d-369">Ces informations supplémentaires peuvent être obtenues à l’aide de la requête de contrôle d’intégrité de cluster existante hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-369">That extra information can be obtained using hello existing cluster health query.</span></span>

### <a name="api"></a><span data-ttu-id="b9a9d-370">API</span><span class="sxs-lookup"><span data-stu-id="b9a9d-370">API</span></span>
<span data-ttu-id="b9a9d-371">l’intégrité du cluster tooget segment, créez un `FabricClient` et appel hello [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) méthode sur son **HealthManager**.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-371">tooget cluster health chunk, create a `FabricClient` and call hello [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) method on its **HealthManager**.</span></span> <span data-ttu-id="b9a9d-372">Vous pouvez passer dans [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) toodescribe des stratégies d’intégrité et les filtres avancés.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-372">You can pass in [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) toodescribe health policies and advanced filters.</span></span>

<span data-ttu-id="b9a9d-373">Hello de code suivant obtient blocs de contrôle d’intégrité de cluster avec des filtres avancés.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-373">hello following code gets cluster health chunk with advanced filters.</span></span>

```csharp
var queryDescription = new ClusterHealthChunkQueryDescription();
queryDescription.ApplicationFilters.Add(new ApplicationHealthStateFilter()
    {
        // Return applications only if they are in error
        HealthStateFilter = HealthStateFilter.Error
    });

// Return all replicas
var wordCountServiceReplicaFilter = new ReplicaHealthStateFilter()
    {
        HealthStateFilter = HealthStateFilter.All
    };

// Return all replicas and all partitions
var wordCountServicePartitionFilter = new PartitionHealthStateFilter()
    {
        HealthStateFilter = HealthStateFilter.All
    };
wordCountServicePartitionFilter.ReplicaFilters.Add(wordCountServiceReplicaFilter);

// For specific service, return all partitions and all replicas
var wordCountServiceFilter = new ServiceHealthStateFilter()
{
    ServiceNameFilter = new Uri("fabric:/WordCount/WordCountService"),
};
wordCountServiceFilter.PartitionFilters.Add(wordCountServicePartitionFilter);

// Application filter: for specific application, return no services except hello ones of interest
var wordCountApplicationFilter = new ApplicationHealthStateFilter()
    {
        // Always return fabric:/WordCount application
        ApplicationNameFilter = new Uri("fabric:/WordCount"),
    };
wordCountApplicationFilter.ServiceFilters.Add(wordCountServiceFilter);

queryDescription.ApplicationFilters.Add(wordCountApplicationFilter);

var result = await fabricClient.HealthManager.GetClusterHealthChunkAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="b9a9d-374">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b9a9d-374">PowerShell</span></span>
<span data-ttu-id="b9a9d-375">intégrité de cluster hello Hello applet de commande tooget [Get-ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk).</span><span class="sxs-lookup"><span data-stu-id="b9a9d-375">hello cmdlet tooget hello cluster health is [Get-ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk).</span></span> <span data-ttu-id="b9a9d-376">Tout d’abord, connectez toohello cluster à l’aide de hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-376">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="b9a9d-377">Hello de code suivant obtient nœuds uniquement si elles sont dans l’erreur à l’exception d’un nœud spécifique, qui doit-elle être renvoyé.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-377">hello following code gets nodes only if they are in Error except for a specific node, which should always be returned.</span></span>

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$nodeFilter1 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{HealthStateFilter=$errorFilter}
$nodeFilter2 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{NodeNameFilter="_Node_1";HealthStateFilter=$allFilter}
# Create node filter list that will be passed in hello cmdlet
$nodeFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.NodeHealthStateFilter]
$nodeFilters.Add($nodeFilter1)
$nodeFilters.Add($nodeFilter2)

Get-ServiceFabricClusterHealthChunk -NodeFilters $nodeFilters


HealthState                  : Warning
NodeHealthStateChunks        : 
                               TotalCount            : 1
                               
                               NodeName              : _Node_1
                               HealthState           : Ok
                               
ApplicationHealthStateChunks : None
```

<span data-ttu-id="b9a9d-378">Hello suivant l’applet de commande Obtient le segment du cluster avec les filtres d’application.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-378">hello following cmdlet gets cluster chunk with application filters.</span></span>

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

# All replicas
$replicaFilter = New-Object System.Fabric.Health.ReplicaHealthStateFilter -Property @{HealthStateFilter=$allFilter}

# All partitions
$partitionFilter = New-Object System.Fabric.Health.PartitionHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$partitionFilter.ReplicaFilters.Add($replicaFilter)

# For WordCountService, return all partitions and all replicas
$svcFilter1 = New-Object System.Fabric.Health.ServiceHealthStateFilter -Property @{ServiceNameFilter="fabric:/WordCount/WordCountService"}
$svcFilter1.PartitionFilters.Add($partitionFilter)

$svcFilter2 = New-Object System.Fabric.Health.ServiceHealthStateFilter -Property @{HealthStateFilter=$errorFilter}

$appFilter = New-Object System.Fabric.Health.ApplicationHealthStateFilter -Property @{ApplicationNameFilter="fabric:/WordCount"}
$appFilter.ServiceFilters.Add($svcFilter1)
$appFilter.ServiceFilters.Add($svcFilter2)

$appFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.ApplicationHealthStateFilter]
$appFilters.Add($appFilter)

Get-ServiceFabricClusterHealthChunk -ApplicationFilters $appFilters


HealthState                  : Error
NodeHealthStateChunks        : None
ApplicationHealthStateChunks : 
                               TotalCount            : 1
                               
                               ApplicationName       : fabric:/WordCount
                               ApplicationTypeName   : WordCount
                               HealthState           : Error
                               ServiceHealthStateChunks : 
                                TotalCount            : 1
                               
                                ServiceName           : fabric:/WordCount/WordCountService
                                HealthState           : Error
                                PartitionHealthStateChunks : 
                                    TotalCount            : 1
                               
                                    PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
                                    HealthState           : Error
                                    ReplicaHealthStateChunks : 
                                        TotalCount            : 5
                               
                                        ReplicaOrInstanceId   : 131444422293118720
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293118721
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293113678
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293113679
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422260002646
                                        HealthState           : Error
```

<span data-ttu-id="b9a9d-379">Hello applet de commande suivante retourne déployées toutes les entités sur un nœud.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-379">hello following cmdlet returns all deployed entities on a node.</span></span>

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$dspFilter = New-Object System.Fabric.Health.DeployedServicePackageHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$daFilter =  New-Object System.Fabric.Health.DeployedApplicationHealthStateFilter -Property @{HealthStateFilter=$allFilter;NodeNameFilter="_Node_2"}
$daFilter.DeployedServicePackageFilters.Add($dspFilter)

$appFilter = New-Object System.Fabric.Health.ApplicationHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$appFilter.DeployedApplicationFilters.Add($daFilter)

$appFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.ApplicationHealthStateFilter]
$appFilters.Add($appFilter)
Get-ServiceFabricClusterHealthChunk -ApplicationFilters $appFilters


HealthState                  : Error
NodeHealthStateChunks        : None
ApplicationHealthStateChunks : 
                               TotalCount            : 2
                               
                               ApplicationName       : fabric:/System
                               HealthState           : Ok
                               DeployedApplicationHealthStateChunks : 
                                TotalCount            : 1
                               
                                NodeName              : _Node_2
                                HealthState           : Ok
                                DeployedServicePackageHealthStateChunks :
                                    TotalCount            : 1
                               
                                    ServiceManifestName   : FAS
                                    ServicePackageActivationId : 
                                    HealthState           : Ok
                               
                               
                               
                               ApplicationName       : fabric:/WordCount
                               ApplicationTypeName   : WordCount
                               HealthState           : Error
                               DeployedApplicationHealthStateChunks : 
                                TotalCount            : 1
                               
                                NodeName              : _Node_2
                                HealthState           : Ok
                                DeployedServicePackageHealthStateChunks :
                                    TotalCount            : 1
                               
                                    ServiceManifestName   : WordCountServicePkg
                                    ServicePackageActivationId : 
                                    HealthState           : Ok
```

### <a name="rest"></a><span data-ttu-id="b9a9d-380">REST</span><span class="sxs-lookup"><span data-stu-id="b9a9d-380">REST</span></span>
<span data-ttu-id="b9a9d-381">Vous pouvez obtenir le segment de contrôle d’intégrité de cluster avec un [demande GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks) ou un [demande POST](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster) qui inclut les stratégies d’intégrité et les filtres avancés, décrits dans le corps de hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-381">You can get cluster health chunk with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster) that includes health policies and advanced filters described in hello body.</span></span>

## <a name="general-queries"></a><span data-ttu-id="b9a9d-382">Requêtes générales</span><span class="sxs-lookup"><span data-stu-id="b9a9d-382">General queries</span></span>
<span data-ttu-id="b9a9d-383">Les requêtes générales renvoient la liste des entités Service Fabric d’un type spécifié.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-383">General queries return a list of Service Fabric entities of a specified type.</span></span> <span data-ttu-id="b9a9d-384">Elles sont exposées via hello API (via des méthodes hello sur **FabricClient.QueryManager**), applets de commande PowerShell et REST.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-384">They are exposed through hello API (via hello methods on **FabricClient.QueryManager**), PowerShell cmdlets, and REST.</span></span> <span data-ttu-id="b9a9d-385">Ces requêtes agrègent les sous-requêtes de plusieurs composants.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-385">These queries aggregate subqueries from multiple components.</span></span> <span data-ttu-id="b9a9d-386">Un d’eux est hello [magasin de contrôle d’intégrité](service-fabric-health-introduction.md#health-store), qui remplit hello agrégées l’état d’intégrité de chaque résultat de la requête.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-386">One of them is hello [health store](service-fabric-health-introduction.md#health-store), which populates hello aggregated health state for each query result.</span></span>  

> [!NOTE]
> <span data-ttu-id="b9a9d-387">Requêtes générales retournent hello agrégée état d’intégrité de l’entité de hello et ne contiennent pas de données d’intégrité riche.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-387">General queries return hello aggregated health state of hello entity and do not contain rich health data.</span></span> <span data-ttu-id="b9a9d-388">Si une entité n’est pas intègre, vous pouvez suivre avec tooget de requêtes d’intégrité toutes ses informations de contrôle d’intégrité, y compris les événements, les États d’intégrité enfant et évaluations non intègres.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-388">If an entity is not healthy, you can follow up with health queries tooget all its health information, including events, child health states, and unhealthy evaluations.</span></span>
>
>

<span data-ttu-id="b9a9d-389">Si des requêtes générales retournent un état d’intégrité inconnu pour une entité, il est possible de que ce magasin de contrôle d’intégrité hello n’a pas les données complètes sur l’entité de hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-389">If general queries return an unknown health state for an entity, it's possible that hello health store doesn't have complete data about hello entity.</span></span> <span data-ttu-id="b9a9d-390">Il est également possible qu’un magasin de contrôle d’intégrité de sous-requête toohello a échoué (par exemple, une erreur de communication s’est produite ou magasin de contrôle d’intégrité hello a été limitée).</span><span class="sxs-lookup"><span data-stu-id="b9a9d-390">It's also possible that a subquery toohello health store wasn't successful (for example, there was a communication error, or hello health store was throttled).</span></span> <span data-ttu-id="b9a9d-391">Effectuez le suivi avec une requête de contrôle d’intégrité d’entité de hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-391">Follow up with a health query for hello entity.</span></span> <span data-ttu-id="b9a9d-392">Si la sous-requête de hello a rencontré des erreurs temporaires, tels que des problèmes de réseau, cette requête de suivi peut réussir.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-392">If hello subquery encountered transient errors, such as network issues, this follow-up query may succeed.</span></span> <span data-ttu-id="b9a9d-393">Il peut également vous fournit plus de détails à partir du magasin de contrôle d’intégrité hello sur la raison pour laquelle les entités hello ne sont pas exposée.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-393">It may also give you more details from hello health store about why hello entity is not exposed.</span></span>

<span data-ttu-id="b9a9d-394">Hello des requêtes qui contiennent des **HealthState** pour les entités sont :</span><span class="sxs-lookup"><span data-stu-id="b9a9d-394">hello queries that contain **HealthState** for entities are:</span></span>

* <span data-ttu-id="b9a9d-395">Liste de nœuds : retourne les nœuds de liste hello cluster hello (paginée).</span><span class="sxs-lookup"><span data-stu-id="b9a9d-395">Node list: Returns hello list nodes in hello cluster (paged).</span></span>
  * <span data-ttu-id="b9a9d-396">API : [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)</span><span class="sxs-lookup"><span data-stu-id="b9a9d-396">API: [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)</span></span>
  * <span data-ttu-id="b9a9d-397">Powershell : Get-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="b9a9d-397">PowerShell: Get-ServiceFabricNode</span></span>
* <span data-ttu-id="b9a9d-398">Liste des applications : renvoie la liste des applications en cluster hello (paginée) hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-398">Application list: Returns hello list of applications in hello cluster (paged).</span></span>
  * <span data-ttu-id="b9a9d-399">API : [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)</span><span class="sxs-lookup"><span data-stu-id="b9a9d-399">API: [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)</span></span>
  * <span data-ttu-id="b9a9d-400">Powershell : Get-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="b9a9d-400">PowerShell: Get-ServiceFabricApplication</span></span>
* <span data-ttu-id="b9a9d-401">Liste de services : renvoie la liste des services dans une application (paginée) hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-401">Service list: Returns hello list of services in an application (paged).</span></span>
  * <span data-ttu-id="b9a9d-402">API : [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)</span><span class="sxs-lookup"><span data-stu-id="b9a9d-402">API: [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)</span></span>
  * <span data-ttu-id="b9a9d-403">Powershell : Get-ServiceFabricService</span><span class="sxs-lookup"><span data-stu-id="b9a9d-403">PowerShell: Get-ServiceFabricService</span></span>
* <span data-ttu-id="b9a9d-404">Liste de partitions : renvoie la liste de partitions dans un service (paginée) hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-404">Partition list: Returns hello list of partitions in a service (paged).</span></span>
  * <span data-ttu-id="b9a9d-405">API : [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)</span><span class="sxs-lookup"><span data-stu-id="b9a9d-405">API: [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)</span></span>
  * <span data-ttu-id="b9a9d-406">PowerShell : Get-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="b9a9d-406">PowerShell: Get-ServiceFabricPartition</span></span>
* <span data-ttu-id="b9a9d-407">Liste des réplicas : renvoie la liste de réplicas dans une partition (paginée) hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-407">Replica list: Returns hello list of replicas in a partition (paged).</span></span>
  * <span data-ttu-id="b9a9d-408">API : [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)</span><span class="sxs-lookup"><span data-stu-id="b9a9d-408">API: [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)</span></span>
  * <span data-ttu-id="b9a9d-409">PowerShell : Get-ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="b9a9d-409">PowerShell: Get-ServiceFabricReplica</span></span>
* <span data-ttu-id="b9a9d-410">Déployé la liste des applications : renvoie la liste des applications déployées sur un nœud hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-410">Deployed application list: Returns hello list of deployed applications on a node.</span></span>
  * <span data-ttu-id="b9a9d-411">API : [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)</span><span class="sxs-lookup"><span data-stu-id="b9a9d-411">API: [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)</span></span>
  * <span data-ttu-id="b9a9d-412">PowerShell : Get-ServiceFabricDeployedApplication</span><span class="sxs-lookup"><span data-stu-id="b9a9d-412">PowerShell: Get-ServiceFabricDeployedApplication</span></span>
* <span data-ttu-id="b9a9d-413">Déployé la liste des packages de service : renvoie la liste des packages de service dans une application déployée hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-413">Deployed service package list: Returns hello list of service packages in a deployed application.</span></span>
  * <span data-ttu-id="b9a9d-414">API : [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)</span><span class="sxs-lookup"><span data-stu-id="b9a9d-414">API: [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)</span></span>
  * <span data-ttu-id="b9a9d-415">PowerShell : Get-ServiceFabricDeployedApplication</span><span class="sxs-lookup"><span data-stu-id="b9a9d-415">PowerShell: Get-ServiceFabricDeployedApplication</span></span>

> [!NOTE]
> <span data-ttu-id="b9a9d-416">Certaines requêtes de hello retourner des résultats paginés.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-416">Some of hello queries return paged results.</span></span> <span data-ttu-id="b9a9d-417">retour de ces requêtes Hello est une liste dérivée [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1).</span><span class="sxs-lookup"><span data-stu-id="b9a9d-417">hello return of these queries is a list derived from [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1).</span></span> <span data-ttu-id="b9a9d-418">Si les résultats hello ne tiennent pas un message, une page est retournée et un ContinuationToken qui assure le suivi où l’énumération s’est arrêté.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-418">If hello results do not fit a message, only a page is returned and a ContinuationToken that tracks where enumeration stopped.</span></span> <span data-ttu-id="b9a9d-419">Continuer toocall hello même requête et que vous passez dans un jeton de continuation hello hello précédente résultats de requête tooget suivants.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-419">Continue toocall hello same query and pass in hello continuation token from hello previous query tooget next results.</span></span>
>
>

### <a name="examples"></a><span data-ttu-id="b9a9d-420">Exemples</span><span class="sxs-lookup"><span data-stu-id="b9a9d-420">Examples</span></span>
<span data-ttu-id="b9a9d-421">Hello de code suivant obtient les applications non intègres hello dans un cluster de hello :</span><span class="sxs-lookup"><span data-stu-id="b9a9d-421">hello following code gets hello unhealthy applications in hello cluster:</span></span>

```csharp
var applications = fabricClient.QueryManager.GetApplicationListAsync().Result.Where(
  app => app.HealthState == HealthState.Error);
```

<span data-ttu-id="b9a9d-422">Détails de l’application hello pour l’ensemble fibre optique hello obtient Hello applet de commande suivante : / WordCount application.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-422">hello following cmdlet gets hello application details for hello fabric:/WordCount application.</span></span> <span data-ttu-id="b9a9d-423">Notez l’état d’intégrité d’avertissement.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-423">Notice that health state is at warning.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplication -ApplicationName fabric:/WordCount

ApplicationName        : fabric:/WordCount
ApplicationTypeName    : WordCount
ApplicationTypeVersion : 1.0.0
ApplicationStatus      : Ready
HealthState            : Warning
ApplicationParameters  : { "WordCountWebService_InstanceCount" = "1";
                         "_WFDebugParams_" = "[{"ServiceManifestName":"WordCountWebServicePkg","CodePackageName":"Code","EntryPointType":"Main","Debug
                         ExePath":"C:\\Program Files (x86)\\Microsoft Visual Studio
                         14.0\\Common7\\Packages\\Debugger\\VsDebugLaunchNotify.exe","DebugArguments":" {74f7e5d5-71a9-47e2-a8cd-1878ec4734f1} -p
                         [ProcessId] -tid [ThreadId]","EnvironmentBlock":"_NO_DEBUG_HEAP=1\u0000"},{"ServiceManifestName":"WordCountServicePkg","CodeP
                         ackageName":"Code","EntryPointType":"Main","DebugExePath":"C:\\Program Files (x86)\\Microsoft Visual Studio
                         14.0\\Common7\\Packages\\Debugger\\VsDebugLaunchNotify.exe","DebugArguments":" {2ab462e6-e0d1-4fda-a844-972f561fe751} -p
                         [ProcessId] -tid [ThreadId]","EnvironmentBlock":"_NO_DEBUG_HEAP=1\u0000"}]" }
```

<span data-ttu-id="b9a9d-424">Hello applet de commande suivante obtient les services hello dont l’état d’intégrité de l’erreur :</span><span class="sxs-lookup"><span data-stu-id="b9a9d-424">hello following cmdlet gets hello services with a health state of error:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplication | Get-ServiceFabricService | where {$_.HealthState -eq "Error"}


ServiceName            : fabric:/WordCount/WordCountService
ServiceKind            : Stateful
ServiceTypeName        : WordCountServiceType
IsServiceGroup         : False
ServiceManifestVersion : 1.0.0
HasPersistedState      : True
ServiceStatus          : Active
HealthState            : Error
```

## <a name="cluster-and-application-upgrades"></a><span data-ttu-id="b9a9d-425">Mises à niveau d’applications et de clusters</span><span class="sxs-lookup"><span data-stu-id="b9a9d-425">Cluster and application upgrades</span></span>
<span data-ttu-id="b9a9d-426">Pendant une mise à niveau analysé du cluster de hello et application, Service Fabric vérifie tooensure de contrôle d’intégrité que tout est bonne.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-426">During a monitored upgrade of hello cluster and application, Service Fabric checks health tooensure that everything remains healthy.</span></span> <span data-ttu-id="b9a9d-427">Si une entité n’est pas sain telle qu’évaluée à l’aide de stratégies d’intégrité configurée, mise à niveau hello applique prochaine action des stratégies spécifiques à la mise à niveau toodetermine hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-427">If an entity is unhealthy as evaluated by using configured health policies, hello upgrade applies upgrade-specific policies toodetermine hello next action.</span></span> <span data-ttu-id="b9a9d-428">mise à niveau Hello peut être mis en pause tooallow intervention de l’utilisateur (par exemple, la fixation des conditions d’erreur ou la modification des stratégies), ou il peut automatiquement restaurer version correcte de toohello précédente.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-428">hello upgrade may be paused tooallow user interaction (such as fixing error conditions or changing policies), or it may automatically roll back toohello previous good version.</span></span>

<span data-ttu-id="b9a9d-429">Pendant un *cluster* mise à niveau, vous pouvez obtenir l’état de mise à niveau de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-429">During a *cluster* upgrade, you can get hello cluster upgrade status.</span></span> <span data-ttu-id="b9a9d-430">état de mise à niveau Hello inclut des évaluations non intègres, quels toowhat point est défectueux dans un cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-430">hello upgrade status includes unhealthy evaluations, which point toowhat is unhealthy in hello cluster.</span></span> <span data-ttu-id="b9a9d-431">Si la mise à niveau hello est restaurée en raison de problèmes de toohealth, état de mise à niveau hello souvient de raisons de fonctionnement anormal dernière hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-431">If hello upgrade is rolled back due toohealth issues, hello upgrade status remembers hello last unhealthy reasons.</span></span> <span data-ttu-id="b9a9d-432">Cette information peut aider les administrateurs à examiner la cause du problème après que la mise à niveau hello restaurée ou arrêté.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-432">This information can help administrators investigate what went wrong after hello upgrade rolled back or stopped.</span></span>

<span data-ttu-id="b9a9d-433">De même, pendant une *application* mise à niveau, les évaluations défectueuses sont contenues dans l’état de mise à niveau l’application hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-433">Similarly, during an *application* upgrade, any unhealthy evaluations are contained in hello application upgrade status.</span></span>

<span data-ttu-id="b9a9d-434">Hello Voici état de mise à niveau l’application hello pour une infrastructure modifiée : / WordCount application.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-434">hello following shows hello application upgrade status for a modified fabric:/WordCount application.</span></span> <span data-ttu-id="b9a9d-435">Un agent de surveillance a signalé une erreur sur l’un de ses réplicas.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-435">A watchdog reported an error on one of its replicas.</span></span> <span data-ttu-id="b9a9d-436">mise à niveau Hello est propagée, car les vérifications de contrôle d’intégrité hello ne sont pas respectées.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-436">hello upgrade is rolling back because hello health checks are not respected.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationUpgrade fabric:/WordCount

ApplicationName               : fabric:/WordCount
ApplicationTypeName           : WordCount
TargetApplicationTypeVersion  : 1.0.0.0
ApplicationParameters         : {}
StartTimestampUtc             : 4/21/2017 5:23:26 PM
FailureTimestampUtc           : 4/21/2017 5:23:37 PM
FailureReason                 : HealthCheck
UpgradeState                  : RollingBackInProgress
UpgradeDuration               : 00:00:23
CurrentUpgradeDomainDuration  : 00:00:00
CurrentUpgradeDomainProgress  : UD1

                                NodeName            : _Node_1
                                UpgradePhase        : Upgrading

                                NodeName            : _Node_2
                                UpgradePhase        : Upgrading

                                NodeName            : _Node_3
                                UpgradePhase        : PreUpgradeSafetyCheck
                                PendingSafetyChecks :
                                EnsurePartitionQuorum - PartitionId: 30db5be6-4e20-4698-8185-4bd7ca744020
NextUpgradeDomain             : UD2
UpgradeDomainsStatus          : { "UD1" = "Completed";
                                "UD2" = "Pending";
                                "UD3" = "Pending";
                                "UD4" = "Pending" }
UnhealthyEvaluations          :
                                Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.

                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.

                                      Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                      Unhealthy partition: PartitionId='a1f83a35-d6bf-4d39-b90d-28d15f39599b', AggregatedHealthState='Error'.

                                          Unhealthy replicas: 20% (1/5), MaxPercentUnhealthyReplicasPerPartition=0%.

                                          Unhealthy replica: PartitionId='a1f83a35-d6bf-4d39-b90d-28d15f39599b',
                                  ReplicaOrInstanceId='131031502346844058', AggregatedHealthState='Error'.

                                              Error event: SourceId='DiskWatcher', Property='Disk'.

UpgradeKind                   : Rolling
RollingUpgradeMode            : UnmonitoredAuto
ForceRestart                  : False
UpgradeReplicaSetCheckTimeout : 00:15:00
```

<span data-ttu-id="b9a9d-437">En savoir plus sur hello [mise à niveau de Service Fabric application](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="b9a9d-437">Read more about hello [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

## <a name="use-health-evaluations-tootroubleshoot"></a><span data-ttu-id="b9a9d-438">Utilisez tootroubleshoot d’évaluations d’intégrité</span><span class="sxs-lookup"><span data-stu-id="b9a9d-438">Use health evaluations tootroubleshoot</span></span>
<span data-ttu-id="b9a9d-439">Chaque fois qu’il existe un problème avec le cluster de hello ou d’une application, recherchez toopinpoint de contrôle d’intégrité de cluster ou une application hello quel est le problème.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-439">Whenever there is an issue with hello cluster or an application, look at hello cluster or application health toopinpoint what is wrong.</span></span> <span data-ttu-id="b9a9d-440">les évaluations non intègres Hello fournissent des détails sur l’état non intègre hello déclenchées en cours.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-440">hello unhealthy evaluations provide details about what triggered hello current unhealthy state.</span></span> <span data-ttu-id="b9a9d-441">Si vous le souhaitez, vous pouvez descendre dans la cause première enfants non intègres entités tooidentify hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-441">If you need to, you can drill down into unhealthy child entities tooidentify hello root cause.</span></span>

<span data-ttu-id="b9a9d-442">Par exemple, considérez une application comme non intègre du fait de l’existence d’un rapport d’erreurs sur l’un de ses réplicas.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-442">For example, consider an application unhealthy because there is an error report on one of its replicas.</span></span> <span data-ttu-id="b9a9d-443">Hello applet de commande Powershell suivante montre les évaluations non intègres hello :</span><span class="sxs-lookup"><span data-stu-id="b9a9d-443">hello following Powershell cmdlet shows hello unhealthy evaluations:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth fabric:/WordCount -EventsFilter None -ServicesFilter None -DeployedApplicationsFilter None -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                                  
                                        Unhealthy replicas: 20% (1/5), MaxPercentUnhealthyReplicasPerPartition=0%.
                                  
                                        Unhealthy replica: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', ReplicaOrInstanceId='131444422260002646', AggregatedHealthState='Error'.
                                  
                                            Error event: SourceId='MyWatchdog', Property='Memory'.
                                  
ServiceHealthStates             : None
DeployedApplicationHealthStates : None
HealthEvents                    : None
```

<span data-ttu-id="b9a9d-444">Vous pouvez examiner hello réplica tooget plus d’informations :</span><span class="sxs-lookup"><span data-stu-id="b9a9d-444">You can look at hello replica tooget more information:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricReplicaHealth -ReplicaOrInstanceId 131444422260002646 -PartitionId af2e3e44-a8f8-45ac-9f31-4093eb897600


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422260002646
AggregatedHealthState : Error
UnhealthyEvaluations  : 
                        Error event: SourceId='MyWatchdog', Property='Memory'.
                        
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131444422263668344
                        SentAt                : 7/13/2017 5:57:06 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_2
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                        
                        SourceId              : MyWatchdog
                        Property              : Memory
                        HealthState           : Error
                        SequenceNumber        : 131444451657749403
                        SentAt                : 7/13/2017 6:46:05 PM
                        ReceivedAt            : 7/13/2017 6:46:05 PM
                        TTL                   : Infinite
                        Description           : 
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Warning->Error = 7/13/2017 6:46:05 PM, LastOk = 1/1/0001 12:00:00 AM
```

> [!NOTE]
> <span data-ttu-id="b9a9d-445">Hello première raison évaluations non intègres afficher hello hello entité est évaluée toocurrent l’état d’intégrité.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-445">hello unhealthy evaluations show hello first reason hello entity is evaluated toocurrent health state.</span></span> <span data-ttu-id="b9a9d-446">Il peut y avoir plusieurs autres événements qui déclenchent cet état, mais ils ne sont pas reflétées dans les évaluations hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-446">There may be multiple other events that trigger this state, but they are not be reflected in hello evaluations.</span></span> <span data-ttu-id="b9a9d-447">tooget plus d’informations, développez hello intégrité entités toofigure tous les rapports défectueux hello dans un cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="b9a9d-447">tooget more information, drill down into hello health entities toofigure out all hello unhealthy reports in hello cluster.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="b9a9d-448">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b9a9d-448">Next steps</span></span>
[<span data-ttu-id="b9a9d-449">Utilisez tootroubleshoot de rapports d’intégrité système</span><span class="sxs-lookup"><span data-stu-id="b9a9d-449">Use system health reports tootroubleshoot</span></span>](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[<span data-ttu-id="b9a9d-450">Ajout de rapports d’intégrité Service Fabric personnalisés</span><span class="sxs-lookup"><span data-stu-id="b9a9d-450">Add custom Service Fabric health reports</span></span>](service-fabric-report-health.md)

[<span data-ttu-id="b9a9d-451">Comment tooreport et vérification du service d’intégrité</span><span class="sxs-lookup"><span data-stu-id="b9a9d-451">How tooreport and check service health</span></span>](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[<span data-ttu-id="b9a9d-452">Surveiller et diagnostiquer les services localement</span><span class="sxs-lookup"><span data-stu-id="b9a9d-452">Monitor and diagnose services locally</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="b9a9d-453">Mise à niveau des applications Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b9a9d-453">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)
