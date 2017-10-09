---
title: aaaAzure Service Fabric la gouvernance de ressources pour les conteneurs et les Services | Documents Microsoft
description: "Azure Service Fabric vous permet de toospecify les limites de ressources pour les services en cours d’exécution interne ou externes conteneurs."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 34e368211d98ff6b5b294c9c8b3af5ca30eeb20c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="resource-governance"></a><span data-ttu-id="0af2f-103">Gouvernance des ressources</span><span class="sxs-lookup"><span data-stu-id="0af2f-103">Resource governance</span></span> 

<span data-ttu-id="0af2f-104">Lorsque plusieurs services en cours d’exécution hello même nœud ou un cluster, il est possible qu’un seul service peut consommer davantage de ressources priver les autres services.</span><span class="sxs-lookup"><span data-stu-id="0af2f-104">When running multiple services on hello same node or cluster, it is possible that one service might consume more resources starving other services.</span></span> <span data-ttu-id="0af2f-105">Ce problème est référencé tooas hello syndrome du voisin.</span><span class="sxs-lookup"><span data-stu-id="0af2f-105">This problem is referred tooas hello noisy-neighbor problem.</span></span> <span data-ttu-id="0af2f-106">Service Fabric permet les réservations toospecify hello développeur et les limites par service tooguarantee ressources et également limiter son utilisation des ressources.</span><span class="sxs-lookup"><span data-stu-id="0af2f-106">Service Fabric allows hello developer toospecify reservations and limits per service tooguarantee resources and also limit its resource usage.</span></span> 

## <a name="resource-governance-metrics"></a><span data-ttu-id="0af2f-107">Mesures de la gouvernance des ressources</span><span class="sxs-lookup"><span data-stu-id="0af2f-107">Resource governance metrics</span></span> 

<span data-ttu-id="0af2f-108">Dans Service Fabric, la gouvernance des ressources est prise en charge par [package de service](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="0af2f-108">Resource governance is supported in Service Fabric per [Service Package](service-fabric-application-model.md).</span></span> <span data-ttu-id="0af2f-109">ressources Hello assignés tooService Package peuvent être réparties entre les packages de code.</span><span class="sxs-lookup"><span data-stu-id="0af2f-109">hello resources that are assigned tooService Package can be further divided between code packages.</span></span> <span data-ttu-id="0af2f-110">limites des ressources Hello spécifiés implique également la réservation hello des ressources de hello.</span><span class="sxs-lookup"><span data-stu-id="0af2f-110">hello resource limits specified also mean hello reservation of hello resources.</span></span> <span data-ttu-id="0af2f-111">Service Fabric prend en charge la spécification des ressources processeur et mémoire par package de service à l’aide de deux [mesures](service-fabric-cluster-resource-manager-metrics.md) intégrées :</span><span class="sxs-lookup"><span data-stu-id="0af2f-111">Service Fabric supports specifying CPU and Memory per service package, using two built-in [metrics](service-fabric-cluster-resource-manager-metrics.md):</span></span>

* <span data-ttu-id="0af2f-112">Processeur (nom de métrique `ServiceFabric:/_CpuCores`) : un noyau est un cœur logique qui est disponible sur l’ordinateur hôte hello, et tous les cœurs sur tous les nœuds sont pondérées hello identiques.</span><span class="sxs-lookup"><span data-stu-id="0af2f-112">CPU (metric name `ServiceFabric:/_CpuCores`): A core is a logical core that is available on hello host machine, and all cores across all nodes are weighted hello same.</span></span>
* <span data-ttu-id="0af2f-113">Mémoire (nom de métrique `ServiceFabric:/_MemoryInMB`) : mémoire est exprimée en mégaoctets et mappe toophysical mémoire disponible sur l’ordinateur de hello.</span><span class="sxs-lookup"><span data-stu-id="0af2f-113">Memory (metric name `ServiceFabric:/_MemoryInMB`): Memory is expressed in megabytes, and it maps toophysical memory that is available on hello machine.</span></span>

<span data-ttu-id="0af2f-114">Uniquement les garanties de réservation logicielle sont proposés - hello runtime rejette lors de l’ouverture du nouveau service dépassés des ressources disponibles des packages.</span><span class="sxs-lookup"><span data-stu-id="0af2f-114">Only soft reservation guarantees are provided - hello runtime rejects opening of new service packages available resources are exceeded.</span></span> <span data-ttu-id="0af2f-115">Toutefois, si un autre fichier exécutable ou un conteneur est placé sur le nœud de hello, qui peut violer les garanties de réservation d’origine hello.</span><span class="sxs-lookup"><span data-stu-id="0af2f-115">However, if another executable or container is placed on hello node, that may violate hello original reservation guarantees.</span></span>

<span data-ttu-id="0af2f-116">Pour ces deux mesures, hello [Gestionnaire de ressources du Cluster](service-fabric-cluster-resource-manager-cluster-description.md) effectue le suivi de la capacité totale de cluster, charge hello sur chaque nœud de cluster de hello, et, le reste des ressources de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="0af2f-116">For these two metrics, hello [Cluster Resource Manager](service-fabric-cluster-resource-manager-cluster-description.md) tracks total cluster capacity, hello load on each node in hello cluster, and, remaining resources in hello cluster.</span></span> <span data-ttu-id="0af2f-117">Ces deux mesures est équivalente tooany autre utilisateur ou une métrique personnalisée et toutes les fonctionnalités existantes peuvent être utilisées avec les :</span><span class="sxs-lookup"><span data-stu-id="0af2f-117">These two metrics are equivalent tooany other user or custom metric and all existing features can be used with them:</span></span>
* <span data-ttu-id="0af2f-118">Cluster peut être [équilibrées](service-fabric-cluster-resource-manager-balancing.md) en fonction des métriques de toothese deux (comportement par défaut).</span><span class="sxs-lookup"><span data-stu-id="0af2f-118">Cluster can be [balanced](service-fabric-cluster-resource-manager-balancing.md) according toothese two metrics (default behavior).</span></span>
* <span data-ttu-id="0af2f-119">Cluster peut être [défragmentés](service-fabric-cluster-resource-manager-defragmentation-metrics.md) en fonction des métriques de toothese deux.</span><span class="sxs-lookup"><span data-stu-id="0af2f-119">Cluster can be [defragmented](service-fabric-cluster-resource-manager-defragmentation-metrics.md) according toothese two metrics.</span></span>
* <span data-ttu-id="0af2f-120">Lors de la [description d’un cluster](service-fabric-cluster-resource-manager-cluster-description.md), la capacité mise en mémoire tampon peut être définie pour ces deux mesures.</span><span class="sxs-lookup"><span data-stu-id="0af2f-120">When [describing a cluster](service-fabric-cluster-resource-manager-cluster-description.md), buffered capacity can be set for these two metrics.</span></span>

<span data-ttu-id="0af2f-121">Le [rapport de charge dynamique](service-fabric-cluster-resource-manager-metrics.md) n’est pas pris en charge pour ces mesures et les charges de ces mesures sont définies lors de la création.</span><span class="sxs-lookup"><span data-stu-id="0af2f-121">[Dynamic load reporting](service-fabric-cluster-resource-manager-metrics.md) is not supported for these metrics, and loads for these metrics are defined at creation time.</span></span>

## <a name="cluster-set-up-for-enabling-resource-governance"></a><span data-ttu-id="0af2f-122">Configuration du cluster pour l’activation de la gouvernance des ressources</span><span class="sxs-lookup"><span data-stu-id="0af2f-122">Cluster set up for enabling resource governance</span></span>

<span data-ttu-id="0af2f-123">La capacité doit être définie manuellement dans chaque type de nœud de cluster de hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="0af2f-123">Capacity should be defined manually in each node type in hello cluster as follows:</span></span>

```xml
    <NodeType Name="MyNodeType">
      <Capacities>
        <Capacity Name="ServiceFabric:/_CpuCores" Value="4"/>
        <Capacity Name="ServiceFabric:/_MemoryInMB" Value="2048"/>
      </Capacities>
    </NodeType>
```
 
<span data-ttu-id="0af2f-124">La gouvernance des ressources est autorisée uniquement sur les services de l’utilisateur, et non sur les services système.</span><span class="sxs-lookup"><span data-stu-id="0af2f-124">Resource governance is allowed only on user services and not on any system services.</span></span> <span data-ttu-id="0af2f-125">Lorsque vous spécifiez la capacité, vous devez désallouer certains cœurs et une partie de la mémoire pour les services système.</span><span class="sxs-lookup"><span data-stu-id="0af2f-125">When specifying capacity, some cores and memory must be left unallocated for system services.</span></span> <span data-ttu-id="0af2f-126">Pour des performances optimales, hello suivant le paramètre doit également être activé dans le manifeste du cluster hello :</span><span class="sxs-lookup"><span data-stu-id="0af2f-126">For optimal performance, hello following setting should also be turned on in hello cluster manifest:</span></span> 

```xml
<Section Name="PlacementAndLoadBalancing">
    <Parameter Name="PreventTransientOvercommit" Value="true" /> 
    <Parameter Name="AllowConstraintCheckFixesDuringApplicationUpgrade" Value="true" />
</Section>
```


## <a name="specifying-resource-governance"></a><span data-ttu-id="0af2f-127">Spécification de la gouvernance des ressources</span><span class="sxs-lookup"><span data-stu-id="0af2f-127">Specifying resource governance</span></span> 

<span data-ttu-id="0af2f-128">Les limites de gouvernance des ressources sont spécifiés dans le manifeste d’application hello (section ServiceManifestImport), comme indiqué dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="0af2f-128">Resource governance limits are specified in hello application manifest (ServiceManifestImport section) as shown in hello following example:</span></span>

```xml
<?xml version='1.0' encoding='UTF-8'?>
<ApplicationManifest ApplicationTypeName='TestAppTC1' ApplicationTypeVersion='vTC1' xsi:schemaLocation='http://schemas.microsoft.com/2011/01/fabric ServiceFabricServiceModel.xsd' xmlns='http://schemas.microsoft.com/2011/01/fabric' xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance'>
  <Parameters>
  </Parameters>
  <!--
  ServicePackageA has hello number of CPU cores defined, but doesn't have hello MemoryInMB defined.
  In this case, Service Fabric will sum hello limits on code packages and uses hello sum as 
  hello overall ServicePackage limit.
  -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName='ServicePackageA' ServiceManifestVersion='v1'/>
    <Policies>
      <ServicePackageResourceGovernancePolicy CpuCores="1"/>
      <ResourceGovernancePolicy CodePackageRef="CodeA1" CpuShares="512" MemoryInMB="1000" />
      <ResourceGovernancePolicy CodePackageRef="CodeA2" CpuShares="256" MemoryInMB="1000" />
    </Policies>
  </ServiceManifestImport>
```
  
<span data-ttu-id="0af2f-129">Dans cet exemple, le package de service ServicePackageA Obtient un cœur sur les nœuds hello où il est placé.</span><span class="sxs-lookup"><span data-stu-id="0af2f-129">In this example, service package ServicePackageA gets one core on hello nodes where it is placed.</span></span> <span data-ttu-id="0af2f-130">Ce package de service contient deux packages de code (CodeA1 et CodeA2), et tous deux spécifient hello `CpuShares` paramètre.</span><span class="sxs-lookup"><span data-stu-id="0af2f-130">This service package contains two code packages (CodeA1 and CodeA2), and both specify hello `CpuShares` parameter.</span></span> <span data-ttu-id="0af2f-131">proportion de Hello de CpuShares 512:256 divise les noyaux hello entre les deux packages de code hello.</span><span class="sxs-lookup"><span data-stu-id="0af2f-131">hello proportion of CpuShares 512:256  divides hello core across hello two code packages.</span></span> <span data-ttu-id="0af2f-132">Par conséquent, dans cet exemple, CodeA1 obtient deux tiers d’un cœur, CodeA2 Obtient un tiers d’un cœur (et une réservation soft-garantie de hello même).</span><span class="sxs-lookup"><span data-stu-id="0af2f-132">Thus, in this example, CodeA1 gets two-thirds of a core, and  CodeA2 gets one-third of a core (and a soft-guarantee reservation of hello same).</span></span> <span data-ttu-id="0af2f-133">Lorsque les CpuShares ne sont pas spécifiés pour les packages de code, Service Fabric divise cœurs hello équitablement entre eux.</span><span class="sxs-lookup"><span data-stu-id="0af2f-133">In case when CpuShares are not specified for code packages, Service Fabric divides hello cores equally among them.</span></span>

<span data-ttu-id="0af2f-134">Limites de la mémoire étant absolus, les deux packages de code sont limitées too1024 Mo de mémoire (et une réservation soft-garantie de hello même).</span><span class="sxs-lookup"><span data-stu-id="0af2f-134">Memory limits are absolute, so both code packages are limited too1024 MB of memory (and a soft-guarantee reservation of hello same).</span></span> <span data-ttu-id="0af2f-135">Packages de code (conteneurs ou processus) ne sont pas en mesure de tooallocate plus de mémoire que cette limite et de tenter de toodo engendre une exception de mémoire insuffisante.</span><span class="sxs-lookup"><span data-stu-id="0af2f-135">Code packages (containers or processes) are not able tooallocate more memory than this limit, and attempting toodo so results in an out-of-memory exception.</span></span> <span data-ttu-id="0af2f-136">Pour toowork de mise en œuvre de limite de ressource, tous les packages de code au sein d’un package de service doivent avoir des limites de mémoire spécifiées.</span><span class="sxs-lookup"><span data-stu-id="0af2f-136">For resource limit enforcement toowork, all code packages within a service package should have memory limits specified.</span></span>


## <a name="next-steps"></a><span data-ttu-id="0af2f-137">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0af2f-137">Next steps</span></span>
* <span data-ttu-id="0af2f-138">toolearn plus sur Cluster Gestionnaire de ressources, lire ce [article](service-fabric-cluster-resource-manager-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0af2f-138">toolearn more about Cluster Resource Manager, read this [article](service-fabric-cluster-resource-manager-introduction.md).</span></span>
* <span data-ttu-id="0af2f-139">toolearn en savoir plus sur le modèle d’application, de packages de service, de packages de code et de toothem de correspondances de réplicas de lire ce [article](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="0af2f-139">toolearn more about application model, service packages, code packages and how replicas map toothem read this [article](service-fabric-application-model.md).</span></span>
