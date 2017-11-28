---
title: "aaaService Gestionnaire de ressources de Cluster de l’ensemble fibre optique - groupes d’applications | Documents Microsoft"
description: "Vue d’ensemble de fonctionnalités de groupe d’applications dans le Gestionnaire de ressources du Cluster Service Fabric de hello de hello"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 4cae2370-77b3-49ce-bf40-030400c4260d
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: b4f068862d962b53a0b3ea813b89bb13ee395681
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooapplication-groups"></a><span data-ttu-id="2ae87-103">Introduction tooApplication groupes</span><span class="sxs-lookup"><span data-stu-id="2ae87-103">Introduction tooApplication Groups</span></span>
<span data-ttu-id="2ae87-104">Gestionnaire de ressources de Cluster du service Fabric gère en général des ressources de cluster en répartissant la charge de hello (représenté par [métriques](service-fabric-cluster-resource-manager-metrics.md)) uniformément dans l’ensemble de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="2ae87-104">Service Fabric's Cluster Resource Manager typically manages cluster resources by spreading hello load (represented via [Metrics](service-fabric-cluster-resource-manager-metrics.md)) evenly throughout hello cluster.</span></span> <span data-ttu-id="2ae87-105">L’infrastructure de service gère la capacité hello des nœuds hello hello et hello clusters dans sa globalité via [capacité](service-fabric-cluster-resource-manager-cluster-description.md).</span><span class="sxs-lookup"><span data-stu-id="2ae87-105">Service Fabric manages hello capacity of hello nodes in hello cluster and hello cluster as a whole via [capacity](service-fabric-cluster-resource-manager-cluster-description.md).</span></span> <span data-ttu-id="2ae87-106">Les mesures et la capacité sont idéales pour divers types de charges de travail, mais les modèles qui utilisent beaucoup d’instances d’application Service Fabric différentes imposent parfois des conditions supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="2ae87-106">Metrics and capacity work great for many workloads, but patterns that make heavy use of different Service Fabric Application Instances sometimes bring in additional requirements.</span></span> <span data-ttu-id="2ae87-107">Par exemple, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="2ae87-107">For example you may want to:</span></span>

- <span data-ttu-id="2ae87-108">Réservation de capacité sur les nœuds hello dans un cluster de hello pour les services de hello dans certaines instances de l’application nommée</span><span class="sxs-lookup"><span data-stu-id="2ae87-108">Reserve some capacity on hello nodes in hello cluster for hello services within some named application instance</span></span>
- <span data-ttu-id="2ae87-109">Limiter le nombre total de hello de nœuds services hello dans une instance de l’application nommée exécutent (au lieu de les répartir les sur l’intégralité du cluster hello)</span><span class="sxs-lookup"><span data-stu-id="2ae87-109">Limit hello total number of nodes that hello services within a named application instance run on (instead of spreading them out over hello entire cluster)</span></span>
- <span data-ttu-id="2ae87-110">Définir des capacités sur l’instance d’application nommée hello lui-même nombre de hello de toolimit services ou le nombre total de consommation des ressources des services hello qu’il contient</span><span class="sxs-lookup"><span data-stu-id="2ae87-110">Define capacities on hello named application instance itself toolimit hello number of services or total resource consumption of hello services inside it</span></span>

<span data-ttu-id="2ae87-111">toomeet ces exigences, hello Gestionnaire de ressources du Cluster Service Fabric prend en charge une fonctionnalité appelée groupes d’applications.</span><span class="sxs-lookup"><span data-stu-id="2ae87-111">toomeet these requirements, hello Service Fabric Cluster Resource Manager supports a feature called Application Groups.</span></span>

## <a name="limiting-hello-maximum-number-of-nodes"></a><span data-ttu-id="2ae87-112">Hello le nombre maximal de nœuds</span><span class="sxs-lookup"><span data-stu-id="2ae87-112">Limiting hello maximum number of nodes</span></span>
<span data-ttu-id="2ae87-113">cas d’utilisation la plus simple Hello pour la capacité de l’Application est lorsqu’une instance d’application doit toobe limitée tooa certain nombre maximal de nœuds.</span><span class="sxs-lookup"><span data-stu-id="2ae87-113">hello simplest use case for Application capacity is when an application instance needs toobe limited tooa certain maximum number of nodes.</span></span> <span data-ttu-id="2ae87-114">Cela consolide tous les services au sein de cette instance d’application sur un nombre défini d’ordinateurs.</span><span class="sxs-lookup"><span data-stu-id="2ae87-114">This consolidates all services within that application instance onto a set number of machines.</span></span> <span data-ttu-id="2ae87-115">Consolidation est utile lorsque vous essayez de toopredict ou imposer l’utilisation des ressources physiques par les services au sein de cette instance de l’application nommée hello.</span><span class="sxs-lookup"><span data-stu-id="2ae87-115">Consolidation is useful when you're trying toopredict or cap physical resource use by hello services within that named application instance.</span></span> 

<span data-ttu-id="2ae87-116">Hello image suivante montre une instance d’application avec et sans un nombre maximal de nœuds définis :</span><span class="sxs-lookup"><span data-stu-id="2ae87-116">hello following image shows an application instance with and without a maximum number of nodes defined:</span></span>

<span data-ttu-id="2ae87-117"><center>
![Instance d’application définissant le nombre maximal de nœuds][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="2ae87-117"><center>
![Application Instance Defining Maximum Number of Nodes][Image1]
</center></span></span>

<span data-ttu-id="2ae87-118">Dans l’exemple de gauche hello, application hello n’a pas un nombre maximal de nœuds définis, et il a trois services.</span><span class="sxs-lookup"><span data-stu-id="2ae87-118">In hello left example, hello application doesn’t have a maximum number of nodes defined, and it has three services.</span></span> <span data-ttu-id="2ae87-119">Hello, Gestionnaire de ressources du Cluster a distribuées tous les réplicas sur six nœuds disponibles tooachieve hello meilleur équilibre dans le cluster hello (comportement par défaut de hello).</span><span class="sxs-lookup"><span data-stu-id="2ae87-119">hello Cluster Resource Manager has spread out all replicas across six available nodes tooachieve hello best balance in hello cluster (hello default behavior).</span></span> <span data-ttu-id="2ae87-120">Dans l’exemple de droite hello, nous constatons hello même application limitée toothree nœuds.</span><span class="sxs-lookup"><span data-stu-id="2ae87-120">In hello right example, we see hello same application limited toothree nodes.</span></span>

<span data-ttu-id="2ae87-121">paramètre Hello qui contrôle ce comportement est appelé MaximumNodes.</span><span class="sxs-lookup"><span data-stu-id="2ae87-121">hello parameter that controls this behavior is called MaximumNodes.</span></span> <span data-ttu-id="2ae87-122">Ce paramètre peut être défini lors de la création de l’application, ou mis à jour pour une instance d’application qui était déjà en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="2ae87-122">This parameter can be set during application creation, or updated for an application instance that was already running.</span></span>

<span data-ttu-id="2ae87-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2ae87-123">Powershell</span></span>

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MaximumNodes 3
Update-ServiceFabricApplication –Name fabric:/AppName –MaximumNodes 5
```

<span data-ttu-id="2ae87-124">C#</span><span class="sxs-lookup"><span data-stu-id="2ae87-124">C#</span></span>

``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";
ad.MaximumNodes = 3;
await fc.ApplicationManager.CreateApplicationAsync(ad);

ApplicationUpdateDescription adUpdate = new ApplicationUpdateDescription(new Uri("fabric:/AppName"));
adUpdate.MaximumNodes = 5;
await fc.ApplicationManager.UpdateApplicationAsync(adUpdate);

```

<span data-ttu-id="2ae87-125">Dans le jeu de nœuds de hello, hello Gestionnaire de ressources de Cluster ne garantit pas placés ensemble les objets de service ou les nœuds obtient utilisés.</span><span class="sxs-lookup"><span data-stu-id="2ae87-125">Within hello set of nodes, hello Cluster Resource Manager doesn't guarantee which service objects get placed together or which nodes get used.</span></span>

## <a name="application-metrics-load-and-capacity"></a><span data-ttu-id="2ae87-126">Mesures, charge et capacité d’application</span><span class="sxs-lookup"><span data-stu-id="2ae87-126">Application Metrics, Load, and Capacity</span></span>
<span data-ttu-id="2ae87-127">Groupes d’applications vous permettent également les métriques de toodefine associées à une instance d’application nommé donné et la capacité de cette instance de l’application de ces mesures.</span><span class="sxs-lookup"><span data-stu-id="2ae87-127">Application Groups also allow you toodefine metrics associated with a given named application instance, and that application instance's capacity for those metrics.</span></span> <span data-ttu-id="2ae87-128">Mesures de l’application vous permettent de tootrack, réserver et limite la consommation des ressources hello de services hello à l’intérieur de cette instance d’application.</span><span class="sxs-lookup"><span data-stu-id="2ae87-128">Application metrics allow you tootrack, reserve, and limit hello resource consumption of hello services inside that application instance.</span></span>

<span data-ttu-id="2ae87-129">Pour chaque mesure d’application, il existe deux valeurs qui peuvent être définies :</span><span class="sxs-lookup"><span data-stu-id="2ae87-129">For each application metric, there are two values that can be set:</span></span>

- <span data-ttu-id="2ae87-130">**Nombre total de capacité de l’Application** : ce paramètre représente la capacité totale de hello d’application hello pour une mesure particulière.</span><span class="sxs-lookup"><span data-stu-id="2ae87-130">**Total Application Capacity** – This setting represents hello total capacity of hello application for a particular metric.</span></span> <span data-ttu-id="2ae87-131">Hello, Gestionnaire de ressources de Cluster n’autorise pas la création de hello de nouveaux services au sein de cette instance d’application qui provoquerait tooexceed de la charge totale de cette valeur.</span><span class="sxs-lookup"><span data-stu-id="2ae87-131">hello Cluster Resource Manager disallows hello creation of any new services within this application instance that would cause total load tooexceed this value.</span></span> <span data-ttu-id="2ae87-132">Par exemple, supposons qu’instance de l’application hello avait une capacité de 10 et bénéficie déjà d’un chargement de cinq.</span><span class="sxs-lookup"><span data-stu-id="2ae87-132">For example, let's say hello application instance had a capacity of 10 and already had load of five.</span></span> <span data-ttu-id="2ae87-133">Création de Hello d’un service avec une charge de total par défaut de 10 est pas autorisée.</span><span class="sxs-lookup"><span data-stu-id="2ae87-133">hello creation of a service with a total default load of 10 would be disallowed.</span></span>
- <span data-ttu-id="2ae87-134">**Capacité maximale de nœud** – ce paramètre spécifie la charge totale maximale de hello pour une application hello sur un nœud unique.</span><span class="sxs-lookup"><span data-stu-id="2ae87-134">**Maximum Node Capacity** – This setting specifies hello maximum total load for hello application on a single node.</span></span> <span data-ttu-id="2ae87-135">Si la charge dépasse cette capacité, hello Gestionnaire de ressources de Cluster déplace les nœuds tooother de réplicas afin que hello charge diminue.</span><span class="sxs-lookup"><span data-stu-id="2ae87-135">If load goes over this capacity, hello Cluster Resource Manager moves replicas tooother nodes so that hello load decreases.</span></span>


<span data-ttu-id="2ae87-136">PowerShell :</span><span class="sxs-lookup"><span data-stu-id="2ae87-136">Powershell:</span></span>

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -Metrics @("MetricName:Metric1,MaximumNodeCapacity:100,MaximumApplicationCapacity:1000")
```

<span data-ttu-id="2ae87-137">C# :</span><span class="sxs-lookup"><span data-stu-id="2ae87-137">C#:</span></span>

``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";

var appMetric = new ApplicationMetricDescription();
appMetric.Name = "Metric1";
appMetric.TotalApplicationCapacity = 1000;
appMetric.MaximumNodeCapacity = 100;
ad.Metrics.Add(appMetric);
await fc.ApplicationManager.CreateApplicationAsync(ad);
```

## <a name="reserving-capacity"></a><span data-ttu-id="2ae87-138">Capacité réservée</span><span class="sxs-lookup"><span data-stu-id="2ae87-138">Reserving Capacity</span></span>
<span data-ttu-id="2ae87-139">Une autre utilisation courante pour les groupes d’applications est tooensure que les ressources au sein de hello cluster sont réservés pour une instance d’une application donnée.</span><span class="sxs-lookup"><span data-stu-id="2ae87-139">Another common use for application groups is tooensure that resources within hello cluster are reserved for a given application instance.</span></span> <span data-ttu-id="2ae87-140">Hello espace est toujours réservé lors de la création d’instance de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="2ae87-140">hello space is always reserved when hello application instance is created.</span></span>

<span data-ttu-id="2ae87-141">Réservation d’espace dans le cluster de hello pour application hello se produit immédiatement, même lorsque :</span><span class="sxs-lookup"><span data-stu-id="2ae87-141">Reserving space in hello cluster for hello application happens immediately even when:</span></span>
- <span data-ttu-id="2ae87-142">instance de l’application Hello est créée mais n’avez pas encore tous les services qu’il contient</span><span class="sxs-lookup"><span data-stu-id="2ae87-142">hello application instance is created but doesn't have any services within it yet</span></span>
- <span data-ttu-id="2ae87-143">nombre de Hello de services au sein de l’instance de l’application hello change chaque fois</span><span class="sxs-lookup"><span data-stu-id="2ae87-143">hello number of services within hello application instance changes every time</span></span> 
- <span data-ttu-id="2ae87-144">services de Hello existent mais ne sont pas consomment des ressources de hello</span><span class="sxs-lookup"><span data-stu-id="2ae87-144">hello services exist but aren't consuming hello resources</span></span> 

<span data-ttu-id="2ae87-145">La réservation de ressources pour une instance d’application implique de spécifier deux paramètres supplémentaires : *MinimumNodes* et *NodeReservationCapacity*</span><span class="sxs-lookup"><span data-stu-id="2ae87-145">Reserving resources for an application instance requires specifying two additional parameters: *MinimumNodes* and *NodeReservationCapacity*</span></span>

- <span data-ttu-id="2ae87-146">**MinimumNodes** -définit le nombre minimal de hello de nœuds hello application instance doit être exécutée.</span><span class="sxs-lookup"><span data-stu-id="2ae87-146">**MinimumNodes** - Defines hello minimum number of nodes that hello application instance should run on.</span></span>  
- <span data-ttu-id="2ae87-147">**NodeReservationCapacity** -ce paramètre est défini par la mesure de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="2ae87-147">**NodeReservationCapacity** - This setting is per metric for hello application.</span></span> <span data-ttu-id="2ae87-148">valeur de Hello est hello cette métrique réservée à l’application hello sur n’importe quel nœud où hello services dans cette application à exécuter.</span><span class="sxs-lookup"><span data-stu-id="2ae87-148">hello value is hello amount of that metric reserved for hello application on any node where that hello services in that application run.</span></span>

<span data-ttu-id="2ae87-149">Combinaison de **MinimumNodes** et **NodeReservationCapacity** garantit une réservation d’une charge minimale pour une application hello au sein du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="2ae87-149">Combining **MinimumNodes** and **NodeReservationCapacity** guarantees a minimum load reservation for hello application within hello cluster.</span></span> <span data-ttu-id="2ae87-150">S’il existe moins restant capacité Bonjour de cluster que réservation total de hello requis, la création d’une application hello échoue.</span><span class="sxs-lookup"><span data-stu-id="2ae87-150">If there's less remaining capacity in hello cluster than hello total reservation required, creation of hello application fails.</span></span> 

<span data-ttu-id="2ae87-151">Voyons un exemple de réservation de capacité :</span><span class="sxs-lookup"><span data-stu-id="2ae87-151">Let's look at an example of capacity reservation:</span></span>

<span data-ttu-id="2ae87-152"><center>
![Instances d’application définissant la capacité de réserve][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="2ae87-152"><center>
![Application Instances Defining Reserved Capacity][Image2]
</center></span></span>

<span data-ttu-id="2ae87-153">Dans l’exemple de gauche hello, les applications n’ont pas de toute capacité de l’Application définie.</span><span class="sxs-lookup"><span data-stu-id="2ae87-153">In hello left example, applications do not have any Application Capacity defined.</span></span> <span data-ttu-id="2ae87-154">tous les éléments selon les règles toonormal équilibre la Hello Gestionnaire de ressources du Cluster.</span><span class="sxs-lookup"><span data-stu-id="2ae87-154">hello Cluster Resource Manager balances everything according toonormal rules.</span></span>

<span data-ttu-id="2ae87-155">Dans l’exemple hello sur hello droite, disons que Application1 a été créé avec hello suivant les paramètres :</span><span class="sxs-lookup"><span data-stu-id="2ae87-155">In hello example on hello right, let's say that Application1 was created with hello following settings:</span></span>

- <span data-ttu-id="2ae87-156">MinimumNodes ensemble tootwo</span><span class="sxs-lookup"><span data-stu-id="2ae87-156">MinimumNodes set tootwo</span></span>
- <span data-ttu-id="2ae87-157">Une mesure d’application définie avec</span><span class="sxs-lookup"><span data-stu-id="2ae87-157">An application Metric defined with</span></span>
  - <span data-ttu-id="2ae87-158">NodeReservationCapacity sur 20</span><span class="sxs-lookup"><span data-stu-id="2ae87-158">NodeReservationCapacity of 20</span></span>

<span data-ttu-id="2ae87-159">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2ae87-159">Powershell</span></span>

 ``` posh
 New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MinimumNodes 2 -Metrics @("MetricName:Metric1,NodeReservationCapacity:20")
 ```

<span data-ttu-id="2ae87-160">C#</span><span class="sxs-lookup"><span data-stu-id="2ae87-160">C#</span></span>

 ``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";
ad.MinimumNodes = 2;

var appMetric = new ApplicationMetricDescription();
appMetric.Name = "Metric1";
appMetric.NodeReservationCapacity = 20;

ad.Metrics.Add(appMetric);

await fc.ApplicationManager.CreateApplicationAsync(ad);
```

<span data-ttu-id="2ae87-161">Service Fabric réserves de ressources de capacité sur les deux nœuds pour Application1 et n’autorise pas les services à partir de l’Application2 tooconsume cette capacité même si il n’y a qu'aucun charge n’est consommée par les services hello Application1 au moment de hello.</span><span class="sxs-lookup"><span data-stu-id="2ae87-161">Service Fabric reserves capacity on two nodes for Application1, and doesn't allow services from Application2 tooconsume that capacity even if there are no load is being consumed by hello services inside Application1 at hello time.</span></span> <span data-ttu-id="2ae87-162">Cette capacité réservée d’application est considérée comme consommé et déduit du nombre de hello capacité sur ce nœud et dans le cluster de hello restante.</span><span class="sxs-lookup"><span data-stu-id="2ae87-162">This reserved application capacity is considered consumed  and counts against hello remaining capacity on that node and within hello cluster.</span></span>  <span data-ttu-id="2ae87-163">réservation de Hello est déduite hello restant immédiatement de la capacité de cluster, mais hello réservé consommation est déduite de capacité hello d’un nœud spécifique uniquement lorsque l’objet d’au moins un service est placé sur celui-ci.</span><span class="sxs-lookup"><span data-stu-id="2ae87-163">hello reservation is deducted from hello remaining cluster capacity immediately, however hello reserved consumption is deducted from hello capacity of a specific node only when at least one service object is placed on it.</span></span> <span data-ttu-id="2ae87-164">Cette dernière réservation permet plus de flexibilité et une meilleure utilisation des ressources dans la mesure où les ressources sont réservées uniquement sur des nœuds lorsque cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="2ae87-164">This later reservation allows for flexibility and better resource utilization since resources are only reserved on nodes when needed.</span></span>

## <a name="obtaining-hello-application-load-information"></a><span data-ttu-id="2ae87-165">Obtention des informations de charge de l’application hello</span><span class="sxs-lookup"><span data-stu-id="2ae87-165">Obtaining hello application load information</span></span>
<span data-ttu-id="2ae87-166">Pour chaque application qui a une capacité de l’Application définie pour une ou plusieurs mesures, vous pouvez obtenir des informations de hello sur la charge globale de hello signalé par les réplicas de ses services.</span><span class="sxs-lookup"><span data-stu-id="2ae87-166">For each application that has an Application Capacity defined for one or more metrics you can obtain hello information about hello aggregate load reported by replicas of its services.</span></span>

<span data-ttu-id="2ae87-167">PowerShell :</span><span class="sxs-lookup"><span data-stu-id="2ae87-167">Powershell:</span></span>

``` posh
Get-ServiceFabricApplicationLoad –ApplicationName fabric:/MyApplication1
```

<span data-ttu-id="2ae87-168">C#</span><span class="sxs-lookup"><span data-stu-id="2ae87-168">C#</span></span>

``` csharp
var v = await fc.QueryManager.GetApplicationLoadInformationAsync("fabric:/MyApplication1");
var metrics = v.ApplicationLoadMetricInformation;
foreach (ApplicationLoadMetricInformation metric in metrics)
{
    Console.WriteLine(metric.ApplicationCapacity);  //total capacity for this metric in this application instance
    Console.WriteLine(metric.ReservationCapacity);  //reserved capacity for this metric in this application instance
    Console.WriteLine(metric.ApplicationLoad);  //current load for this metric in this application instance
}
```

<span data-ttu-id="2ae87-169">requête de ApplicationLoad Hello retourne des informations de base de hello sur la capacité d’Application qui a été spécifié pour l’application hello.</span><span class="sxs-lookup"><span data-stu-id="2ae87-169">hello ApplicationLoad query returns hello basic information about Application Capacity that was specified for hello application.</span></span> <span data-ttu-id="2ae87-170">Ces informations comprennent des informations sur les nœuds de valeur minimale et maximale hello et le numéro de hello application hello est actuellement occupée par.</span><span class="sxs-lookup"><span data-stu-id="2ae87-170">This information includes hello Minimum Nodes and Maximum Nodes info, and hello number that hello application is currently occupying.</span></span> <span data-ttu-id="2ae87-171">Elles comprennent également des informations sur chaque mesure de charge d’application, notamment :</span><span class="sxs-lookup"><span data-stu-id="2ae87-171">It also includes information about each application load metric, including:</span></span>

* <span data-ttu-id="2ae87-172">: Métrique nom de métrique de hello.</span><span class="sxs-lookup"><span data-stu-id="2ae87-172">Metric Name: Name of hello metric.</span></span>
* <span data-ttu-id="2ae87-173">Capacité de réservation : La capacité de Cluster qui est réservée dans le cluster de hello pour cette Application.</span><span class="sxs-lookup"><span data-stu-id="2ae87-173">Reservation Capacity: Cluster Capacity that is reserved in hello cluster for this Application.</span></span>
* <span data-ttu-id="2ae87-174">Charge de l’application : la charge totale des réplicas enfants de cette application.</span><span class="sxs-lookup"><span data-stu-id="2ae87-174">Application Load: Total Load of this Application’s child replicas.</span></span>
* <span data-ttu-id="2ae87-175">Capacité d’application : la valeur maximale autorisée pour la charge de l’application.</span><span class="sxs-lookup"><span data-stu-id="2ae87-175">Application Capacity: Maximum permitted value of Application Load.</span></span>

## <a name="removing-application-capacity"></a><span data-ttu-id="2ae87-176">Suppression de la capacité d’application</span><span class="sxs-lookup"><span data-stu-id="2ae87-176">Removing Application Capacity</span></span>
<span data-ttu-id="2ae87-177">Une fois les paramètres de capacité de l’Application hello définies pour une application, ils peuvent être supprimés à l’aide des API d’Application de mise à jour ou des cmdlets PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2ae87-177">Once hello Application Capacity parameters are set for an application, they can be removed using Update Application APIs or PowerShell cmdlets.</span></span> <span data-ttu-id="2ae87-178">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="2ae87-178">For example:</span></span>

``` posh
Update-ServiceFabricApplication –Name fabric:/MyApplication1 –RemoveApplicationCapacity

```

<span data-ttu-id="2ae87-179">Cette commande supprime tous les paramètres de gestion de capacité Application à partir de l’instance de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="2ae87-179">This command removes all Application capacity management parameters from hello application instance.</span></span> <span data-ttu-id="2ae87-180">Cela inclut MinimumNodes, MaximumNodes et les mesures de l’Application hello, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="2ae87-180">This includes MinimumNodes, MaximumNodes, and hello Application's metrics, if any.</span></span> <span data-ttu-id="2ae87-181">effet Hello de commande hello est immédiate.</span><span class="sxs-lookup"><span data-stu-id="2ae87-181">hello effect of hello command is immediate.</span></span> <span data-ttu-id="2ae87-182">Une fois cette commande terminée, hello Gestionnaire de ressources de Cluster utilise le comportement de par défaut hello pour la gestion des applications.</span><span class="sxs-lookup"><span data-stu-id="2ae87-182">After this command completes, hello Cluster Resource Manager uses hello default behavior for managing applications.</span></span> <span data-ttu-id="2ae87-183">Les paramètres de capacité d’application peuvent être spécifiés à nouveau via `Update-ServiceFabricApplication`/`System.Fabric.FabricClient.ApplicationManagementClient.UpdateApplicationAsync()`.</span><span class="sxs-lookup"><span data-stu-id="2ae87-183">Application Capacity parameters can be specified again via `Update-ServiceFabricApplication`/`System.Fabric.FabricClient.ApplicationManagementClient.UpdateApplicationAsync()`.</span></span>

### <a name="restrictions-on-application-capacity"></a><span data-ttu-id="2ae87-184">Restrictions sur la capacité d’application</span><span class="sxs-lookup"><span data-stu-id="2ae87-184">Restrictions on Application Capacity</span></span>
<span data-ttu-id="2ae87-185">Il existe plusieurs restrictions à respecter concernant les paramètres de capacité d’application.</span><span class="sxs-lookup"><span data-stu-id="2ae87-185">There are several restrictions on Application Capacity parameters that must be respected.</span></span> <span data-ttu-id="2ae87-186">En cas d’erreurs de validation, aucune modification n’est appliquée.</span><span class="sxs-lookup"><span data-stu-id="2ae87-186">If there are validation errors no changes take place.</span></span>

- <span data-ttu-id="2ae87-187">Tous les paramètres entiers doivent être des nombres positifs.</span><span class="sxs-lookup"><span data-stu-id="2ae87-187">All integer parameters must be non-negative numbers.</span></span>
- <span data-ttu-id="2ae87-188">La valeur du paramètre MinimumNodes ne doit jamais être supérieure à celle du paramètre MaximumNodes.</span><span class="sxs-lookup"><span data-stu-id="2ae87-188">MinimumNodes must never be greater than MaximumNodes.</span></span>
- <span data-ttu-id="2ae87-189">Si les capacités d’une mesure de charge sont définies, elles doivent respecter les règles suivantes :</span><span class="sxs-lookup"><span data-stu-id="2ae87-189">If capacities for a load metric are defined, then they must follow these rules:</span></span>
  - <span data-ttu-id="2ae87-190">La capacité de réservation de nœud ne doit pas être supérieure à la capacité maximale de nœud.</span><span class="sxs-lookup"><span data-stu-id="2ae87-190">Node Reservation Capacity must not be greater than Maximum Node Capacity.</span></span> <span data-ttu-id="2ae87-191">Par exemple, vous ne peut pas limiter la capacité de hello pour métrique hello « UC » sur des unités de tootwo nœud hello et essayez tooreserve trois unités sur chaque nœud.</span><span class="sxs-lookup"><span data-stu-id="2ae87-191">For example, you cannot limit hello capacity for hello metric “CPU” on hello node tootwo units and try tooreserve three units on each node.</span></span>
  - <span data-ttu-id="2ae87-192">Si MaximumNodes est spécifié, produit hello de MaximumNodes et la capacité maximale de nœud ne doit pas être supérieure à la capacité de l’Application.</span><span class="sxs-lookup"><span data-stu-id="2ae87-192">If MaximumNodes is specified, then hello product of MaximumNodes and Maximum Node Capacity must not be greater than Total Application Capacity.</span></span> <span data-ttu-id="2ae87-193">Par exemple, supposons hello capacité maximale de nœud pour la métrique de charge « UC » a la valeur tooeight.</span><span class="sxs-lookup"><span data-stu-id="2ae87-193">For example, let's say hello Maximum Node Capacity for load metric “CPU” is set tooeight.</span></span> <span data-ttu-id="2ae87-194">Supposons également que vous définissez hello too10 de nœuds au Maximum.</span><span class="sxs-lookup"><span data-stu-id="2ae87-194">Let's also say you set hello Maximum Nodes too10.</span></span> <span data-ttu-id="2ae87-195">Dans ce cas, la capacité totale de l’application doit être supérieure à 80 pour cette mesure de charge.</span><span class="sxs-lookup"><span data-stu-id="2ae87-195">In this case, Total Application Capacity must be greater than 80 for this load metric.</span></span>

<span data-ttu-id="2ae87-196">restrictions de Hello sont appliquées à la fois au cours des mises à jour et la création d’application.</span><span class="sxs-lookup"><span data-stu-id="2ae87-196">hello restrictions are enforced both during application creation and updates.</span></span>

## <a name="how-not-toouse-application-capacity"></a><span data-ttu-id="2ae87-197">Comment pas toouse capacité de l’Application</span><span class="sxs-lookup"><span data-stu-id="2ae87-197">How not toouse Application Capacity</span></span>
- <span data-ttu-id="2ae87-198">N’essayez pas de toouse hello groupe d’applications fonctionnalités tooconstrain hello application tooa _spécifique_ sous-ensemble de nœuds.</span><span class="sxs-lookup"><span data-stu-id="2ae87-198">Do not try toouse hello Application Group features tooconstrain hello application tooa _specific_ subset of nodes.</span></span> <span data-ttu-id="2ae87-199">En d’autres termes, vous pouvez spécifier que l’application hello s’exécute au maximum cinq nœuds, mais pas les cinq nœuds spécifiques dans un cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="2ae87-199">In other words, you can specify that hello application runs on at most five nodes, but not which specific five nodes in hello cluster.</span></span> <span data-ttu-id="2ae87-200">Contraint un toospecific application nœuds peuvent être obtenus à l’aide des contraintes de placement des services.</span><span class="sxs-lookup"><span data-stu-id="2ae87-200">Constraining an application toospecific nodes can be achieved using placement constraints for services.</span></span>
- <span data-ttu-id="2ae87-201">N’essayez pas de tooensure de capacité de l’Application hello toouse que deux services de hello même application sont placés sur hello mêmes nœuds.</span><span class="sxs-lookup"><span data-stu-id="2ae87-201">Do not try toouse hello Application Capacity tooensure that two services from hello same application are placed on hello same nodes.</span></span> <span data-ttu-id="2ae87-202">Utilisez plutôt l’[affinité](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md) ou les [contraintes de placement](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints).</span><span class="sxs-lookup"><span data-stu-id="2ae87-202">Instead use [affinity](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md) or [placement constraints](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2ae87-203">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2ae87-203">Next steps</span></span>
- <span data-ttu-id="2ae87-204">Pour plus d’informations sur la configuration des services, consultez la rubrique [En savoir plus sur la configuration des services](service-fabric-cluster-resource-manager-configure-services.md)</span><span class="sxs-lookup"><span data-stu-id="2ae87-204">For more information on configuring services, [Learn about configuring Services](service-fabric-cluster-resource-manager-configure-services.md)</span></span>
- <span data-ttu-id="2ae87-205">toofind out sur comment hello Gestionnaire de ressources de Cluster gère et équilibre la charge du cluster de hello, consultez l’article de hello sur [équilibrage de charge](service-fabric-cluster-resource-manager-balancing.md)</span><span class="sxs-lookup"><span data-stu-id="2ae87-205">toofind out about how hello Cluster Resource Manager manages and balances load in hello cluster, check out hello article on [balancing load](service-fabric-cluster-resource-manager-balancing.md)</span></span>
- <span data-ttu-id="2ae87-206">Démarrer à partir du début de hello et [obtenir une présentation de toohello Gestionnaire de ressources du Cluster Service Fabric](service-fabric-cluster-resource-manager-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="2ae87-206">Start from hello beginning and [get an Introduction toohello Service Fabric Cluster Resource Manager](service-fabric-cluster-resource-manager-introduction.md)</span></span>
- <span data-ttu-id="2ae87-207">Pour plus d’informations sur le fonctionnement des mesures en général, consultez les informations sur les [mesures de charge Service Fabric](service-fabric-cluster-resource-manager-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="2ae87-207">For more information on how metrics work generally, read up on [Service Fabric Load Metrics](service-fabric-cluster-resource-manager-metrics.md)</span></span>
- <span data-ttu-id="2ae87-208">Hello, Gestionnaire de ressources du Cluster possède de nombreuses options permettant de décrire le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="2ae87-208">hello Cluster Resource Manager has many options for describing hello cluster.</span></span> <span data-ttu-id="2ae87-209">toofind plus d’informations à leur sujet, consultez cet article sur [décrivant un cluster Service Fabric](service-fabric-cluster-resource-manager-cluster-description.md)</span><span class="sxs-lookup"><span data-stu-id="2ae87-209">toofind out more about them, check out this article on [describing a Service Fabric cluster](service-fabric-cluster-resource-manager-cluster-description.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-max-nodes.png
[Image2]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-reserved-capacity.png
