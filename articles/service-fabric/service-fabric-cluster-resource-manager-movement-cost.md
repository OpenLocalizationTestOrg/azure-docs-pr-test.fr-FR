---
title: "Gestionnaire des ressources de cluster Service Fabric : coût du déplacement | Microsoft Docs"
description: "Présentation du coût du mouvement pour les services Service Fabric"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: f022f258-7bc0-4db4-aa85-8c6c8344da32
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 5de07c259d1d327d0211338c2911804445dd6b60
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="service-movement-cost"></a><span data-ttu-id="a5af3-103">Coût du déplacement de services</span><span class="sxs-lookup"><span data-stu-id="a5af3-103">Service movement cost</span></span>
<span data-ttu-id="a5af3-104">L’un des facteurs que Service Fabric Cluster Resource Manager prend en compte pour déterminer les modifications à apporter à un cluster est leur coût.</span><span class="sxs-lookup"><span data-stu-id="a5af3-104">A factor that the Service Fabric Cluster Resource Manager considers when trying to determine what changes to make to a cluster is the cost of those changes.</span></span> <span data-ttu-id="a5af3-105">La notion de « coût » est mise en balance avec la capacité d’amélioration du cluster.</span><span class="sxs-lookup"><span data-stu-id="a5af3-105">The notion of "cost" is traded off against how much the cluster can be improved.</span></span> <span data-ttu-id="a5af3-106">Le coût est pris en compte lors du déplacement de services à des fins d’équilibrage, de défragmentation ou autres.</span><span class="sxs-lookup"><span data-stu-id="a5af3-106">Cost is factored in when moving services for balancing, defragmentation, and other requirements.</span></span> <span data-ttu-id="a5af3-107">L’objectif est de répondre aux exigences en limitant les perturbations et le coût.</span><span class="sxs-lookup"><span data-stu-id="a5af3-107">The goal is to meet the requirements in the least disruptive or expensive way.</span></span> 

<span data-ttu-id="a5af3-108">Le déplacement de services coûte au minimum du temps processeur et de la bande passante réseau.</span><span class="sxs-lookup"><span data-stu-id="a5af3-108">Moving services costs CPU time and network bandwidth at a minimum.</span></span> <span data-ttu-id="a5af3-109">Pour les services avec état, il suppose de copier l’état de ces services, ce qui consomme davantage de mémoire et de disque.</span><span class="sxs-lookup"><span data-stu-id="a5af3-109">For stateful services, it requires copying the state of those services, consuming additional memory and disk.</span></span> <span data-ttu-id="a5af3-110">Réduire le coût des solutions fournies par Azure Service Fabric Cluster Resource Manager permet de s’assurer que les ressources du cluster ne sont pas exploitées inutilement.</span><span class="sxs-lookup"><span data-stu-id="a5af3-110">Minimizing the cost of solutions that the Azure Service Fabric Cluster Resource Manager comes up with helps ensure that the cluster's resources aren't spent unnecessarily.</span></span> <span data-ttu-id="a5af3-111">Mais il ne faut pas non plus ignorer les solutions qui pourraient améliorer considérablement l’allocation de ressources dans le cluster.</span><span class="sxs-lookup"><span data-stu-id="a5af3-111">However, you also don’t want to ignore solutions that would significantly improve the allocation of resources in the cluster.</span></span>

<span data-ttu-id="a5af3-112">Cluster Resource Manager dispose de deux modes de calcul et de limitation des coûts lorsqu’il gère le cluster.</span><span class="sxs-lookup"><span data-stu-id="a5af3-112">The Cluster Resource Manager has two ways of computing costs and limiting them while it tries to manage the cluster.</span></span> <span data-ttu-id="a5af3-113">Le premier mécanisme consiste simplement à compter chacun des déplacements qui seraient effectués.</span><span class="sxs-lookup"><span data-stu-id="a5af3-113">The first mechanism is simply counting every move that it would make.</span></span> <span data-ttu-id="a5af3-114">Si deux solutions présentant à peu près le même solde (score) sont générées, Cluster Resource Manager préfère celle qui affiche le coût le plus bas (nombre total de déplacements).</span><span class="sxs-lookup"><span data-stu-id="a5af3-114">If two solutions are generated with about the same balance (score), then the Cluster Resource Manager prefers the one with the lowest cost (total number of moves).</span></span>

<span data-ttu-id="a5af3-115">Cette stratégie fonctionne bien.</span><span class="sxs-lookup"><span data-stu-id="a5af3-115">This strategy works well.</span></span> <span data-ttu-id="a5af3-116">Mais, comme avec les charges par défaut ou statiques, il est peu probable dans n’importe quel système complexe que tous les déplacements soient égaux.</span><span class="sxs-lookup"><span data-stu-id="a5af3-116">But as with default or static loads, it's unlikely in any complex system that all moves are equal.</span></span> <span data-ttu-id="a5af3-117">Certains sont susceptibles d’être beaucoup plus coûteux.</span><span class="sxs-lookup"><span data-stu-id="a5af3-117">Some are likely to be much more expensive.</span></span>

## <a name="setting-move-costs"></a><span data-ttu-id="a5af3-118">Définir les coûts de déplacement</span><span class="sxs-lookup"><span data-stu-id="a5af3-118">Setting Move Costs</span></span> 
<span data-ttu-id="a5af3-119">Vous pouvez spécifier le coût par défaut de déplacement d’un service lors de sa création :</span><span class="sxs-lookup"><span data-stu-id="a5af3-119">You can specify the default move cost for a service when it is created:</span></span>

<span data-ttu-id="a5af3-120">PowerShell :</span><span class="sxs-lookup"><span data-stu-id="a5af3-120">PowerShell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -DefaultMoveCost Medium
```

<span data-ttu-id="a5af3-121">C# :</span><span class="sxs-lookup"><span data-stu-id="a5af3-121">C#:</span></span> 

```csharp
FabricClient fabricClient = new FabricClient();
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
//set up the rest of the ServiceDescription
serviceDescription.DefaultMoveCost = MoveCost.Medium;
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

<span data-ttu-id="a5af3-122">Vous pouvez également spécifier ou mettre à jour dynamiquement MoveCost pour un service après sa création :</span><span class="sxs-lookup"><span data-stu-id="a5af3-122">You can also specify or update MoveCost dynamically for a service after the service has been created:</span></span> 

<span data-ttu-id="a5af3-123">PowerShell :</span><span class="sxs-lookup"><span data-stu-id="a5af3-123">PowerShell:</span></span> 

```posh
Update-ServiceFabricService -Stateful -ServiceName "fabric:/AppName/ServiceName" -DefaultMoveCost High
```

<span data-ttu-id="a5af3-124">C# :</span><span class="sxs-lookup"><span data-stu-id="a5af3-124">C#:</span></span>

```csharp
StatefulServiceUpdateDescription updateDescription = new StatefulServiceUpdateDescription();
updateDescription.DefaultMoveCost = MoveCost.High;
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/AppName/ServiceName"), updateDescription);
```

## <a name="dynamically-specifying-move-cost-on-a-per-replica-basis"></a><span data-ttu-id="a5af3-125">Spécifier dynamiquement le coût de déplacement pour chaque réplica</span><span class="sxs-lookup"><span data-stu-id="a5af3-125">Dynamically specifying move cost on a per-replica basis</span></span>

<span data-ttu-id="a5af3-126">Les extraits de code précédents permettent tous de spécifier MoveCost pour la totalité d’un service d’un seul coup en dehors du service proprement dit.</span><span class="sxs-lookup"><span data-stu-id="a5af3-126">The preceding snippets are all for specifying MoveCost for a whole service at once from outside the service itself.</span></span> <span data-ttu-id="a5af3-127">Toutefois, le coût de déplacement prend toute son utilité lorsque, pour un objet de service donné, il change au cours de sa vie.</span><span class="sxs-lookup"><span data-stu-id="a5af3-127">However, move cost is most useful is when the move cost of a specific service object changes over its lifespan.</span></span> <span data-ttu-id="a5af3-128">Étant donné que ce sont probablement les services eux-mêmes qui sont les mieux placés pour savoir combien coûte leur déplacement à un instant t, il existe une API qui permet aux services de signaler leur propre coût de déplacement à l’exécution.</span><span class="sxs-lookup"><span data-stu-id="a5af3-128">Since the services themselves probably have the best idea of how costly they are to move a given time, there's an API for services to report their own individual move cost during runtime.</span></span> 

<span data-ttu-id="a5af3-129">C# :</span><span class="sxs-lookup"><span data-stu-id="a5af3-129">C#:</span></span>

```csharp
this.Partition.ReportMoveCost(MoveCost.Medium);
```

## <a name="impact-of-move-cost"></a><span data-ttu-id="a5af3-130">Impact du coût de déplacement</span><span class="sxs-lookup"><span data-stu-id="a5af3-130">Impact of move cost</span></span>
<span data-ttu-id="a5af3-131">MoveCost a quatre niveaux : zéro, faible, moyen et élevé.</span><span class="sxs-lookup"><span data-stu-id="a5af3-131">MoveCost has four levels: Zero, Low, Medium, and High.</span></span> <span data-ttu-id="a5af3-132">À l’exception de zéro, ces niveaux MoveCost sont liés les uns aux autres.</span><span class="sxs-lookup"><span data-stu-id="a5af3-132">MoveCosts are relative to each other, except for Zero.</span></span> <span data-ttu-id="a5af3-133">Un coût de déplacement de zéro signifie que le déplacement est gratuit et ne doit pas compter dans le score de la solution.</span><span class="sxs-lookup"><span data-stu-id="a5af3-133">Zero move cost means that movement is free and should not count against the score of the solution.</span></span> <span data-ttu-id="a5af3-134">Le fait de définir le coût élevé ne garantit *pas* que le réplica reste au même endroit.</span><span class="sxs-lookup"><span data-stu-id="a5af3-134">Setting your move cost to High does *not* guarantee that the replica stays in one place.</span></span>

<span data-ttu-id="a5af3-135"><center>
![Coût du déplacement comme facteur de sélection des réplicas pour les déplacements][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="a5af3-135"><center>
![Move cost as a factor in selecting replicas for movement][Image1]
</center></span></span>

<span data-ttu-id="a5af3-136">MoveCost vous permet de rechercher les solutions qui provoquent globalement le moins de perturbations et qui sont les plus faciles à mettre en place tout en obtenant un équilibre équivalent.</span><span class="sxs-lookup"><span data-stu-id="a5af3-136">MoveCost helps you find the solutions that cause the least disruption overall and are easiest to achieve while still arriving at equivalent balance.</span></span> <span data-ttu-id="a5af3-137">La notion de coût d’un service peut être liée à beaucoup de choses.</span><span class="sxs-lookup"><span data-stu-id="a5af3-137">A service’s notion of cost can be relative to many things.</span></span> <span data-ttu-id="a5af3-138">Les facteurs les plus courants pour calculer le coût de déplacement sont :</span><span class="sxs-lookup"><span data-stu-id="a5af3-138">The most common factors in calculating your move cost are:</span></span>

- <span data-ttu-id="a5af3-139">La quantité d’état ou de données que le service doit déplacer.</span><span class="sxs-lookup"><span data-stu-id="a5af3-139">The amount of state or data that the service has to move.</span></span>
- <span data-ttu-id="a5af3-140">Le coût de déconnexion des clients.</span><span class="sxs-lookup"><span data-stu-id="a5af3-140">The cost of disconnection of clients.</span></span> <span data-ttu-id="a5af3-141">Le déplacement d’un réplica principal coûte généralement plus cher que celui d’un réplica secondaire.</span><span class="sxs-lookup"><span data-stu-id="a5af3-141">Moving a primary replica is usually more costly than the cost of moving a secondary replica.</span></span>
- <span data-ttu-id="a5af3-142">Le coût d’interruption d’une opération en cours.</span><span class="sxs-lookup"><span data-stu-id="a5af3-142">The cost of interrupting an in-flight operation.</span></span> <span data-ttu-id="a5af3-143">Certaines opérations au niveau du magasin de données ou en réponse à un appel du client sont coûteuses.</span><span class="sxs-lookup"><span data-stu-id="a5af3-143">Some operations at the data store level or operations performed in response to a client call are costly.</span></span> <span data-ttu-id="a5af3-144">Après un certain point, il est préférable de ne pas les arrêter si vous n’êtes pas obligé de le faire.</span><span class="sxs-lookup"><span data-stu-id="a5af3-144">After a certain point, you don’t want to stop them if you don’t have to.</span></span> <span data-ttu-id="a5af3-145">Par conséquent, pendant l’opération, vous augmentez le coût du déplacement de cet objet de service afin de réduire la probabilité qu’il se déplace.</span><span class="sxs-lookup"><span data-stu-id="a5af3-145">So while the operation is going on, you increase the move cost of this service object to reduce the likelihood that it moves.</span></span> <span data-ttu-id="a5af3-146">Lorsque l’opération se termine, vous rétablissez le coût normal.</span><span class="sxs-lookup"><span data-stu-id="a5af3-146">When the operation is done, you set the cost back to normal.</span></span>

## <a name="enabling-move-cost-in-your-cluster"></a><span data-ttu-id="a5af3-147">Activer le coût de déplacement dans un cluster</span><span class="sxs-lookup"><span data-stu-id="a5af3-147">Enabling move cost in your cluster</span></span>
<span data-ttu-id="a5af3-148">Pour que les coûts de déplacement pris en compte soient aussi précis que possible, MoveCost doit être activé dans le cluster.</span><span class="sxs-lookup"><span data-stu-id="a5af3-148">In order for the more granular MoveCosts to be taken into account, MoveCost must be enabled in your cluster.</span></span> <span data-ttu-id="a5af3-149">Sans ce paramètre, le mode par défaut, qui consiste à compter les déplacements, est utilisé pour calculer MoveCost, et les rapports MoveCost sont ignorés.</span><span class="sxs-lookup"><span data-stu-id="a5af3-149">Without this setting, the default mode of counting moves is used for calculating MoveCost, and MoveCost reports are ignored.</span></span>


<span data-ttu-id="a5af3-150">ClusterManifest.xml :</span><span class="sxs-lookup"><span data-stu-id="a5af3-150">ClusterManifest.xml:</span></span>

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="UseMoveCostReports" Value="true" />
        </Section>
```

<span data-ttu-id="a5af3-151">via ClusterConfig.json pour les déploiements autonomes ou Template.json pour les clusters hébergés sur Azure :</span><span class="sxs-lookup"><span data-stu-id="a5af3-151">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "UseMoveCostReports",
          "value": "true"
      }
    ]
  }
]
```

## <a name="next-steps"></a><span data-ttu-id="a5af3-152">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a5af3-152">Next steps</span></span>
- <span data-ttu-id="a5af3-153">Le Gestionnaire des ressources de cluster Service Fabric utilise des métriques pour gérer la consommation et la capacité du cluster.</span><span class="sxs-lookup"><span data-stu-id="a5af3-153">Service Fabric Cluster Resource Manger uses metrics to manage consumption and capacity in the cluster.</span></span> <span data-ttu-id="a5af3-154">Pour en savoir plus sur les métriques et leur configuration, consultez [Gestion de la charge et de la consommation des ressources dans Service Fabric avec des métriques](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="a5af3-154">To learn more about metrics and how to configure them, check out [Managing resource consumption and load in Service Fabric with metrics](service-fabric-cluster-resource-manager-metrics.md).</span></span>
- <span data-ttu-id="a5af3-155">Pour en savoir plus sur la façon dont le Gestionnaire des ressources de cluster gère et équilibre la charge du cluster, consultez [Équilibrage de votre cluster Service Fabric](service-fabric-cluster-resource-manager-balancing.md).</span><span class="sxs-lookup"><span data-stu-id="a5af3-155">To learn about how the Cluster Resource Manager manages and balances load in the cluster, check out [Balancing your Service Fabric cluster](service-fabric-cluster-resource-manager-balancing.md).</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-movement-cost/service-most-cost-example.png
