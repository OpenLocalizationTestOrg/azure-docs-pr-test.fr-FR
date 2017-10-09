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
ms.openlocfilehash: 65d4ac73efffcf7b25b1e95da6f9012a9238cb75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-movement-cost"></a><span data-ttu-id="0dc7a-103">Coût du déplacement de services</span><span class="sxs-lookup"><span data-stu-id="0dc7a-103">Service movement cost</span></span>
<span data-ttu-id="0dc7a-104">Un facteur qui hello du Gestionnaire de ressources du Cluster Service Fabric prend en compte lors de la tentative de toodetermine quel cluster de tooa toomake modifications est coût hello de ces modifications.</span><span class="sxs-lookup"><span data-stu-id="0dc7a-104">A factor that hello Service Fabric Cluster Resource Manager considers when trying toodetermine what changes toomake tooa cluster is hello cost of those changes.</span></span> <span data-ttu-id="0dc7a-105">notion Hello de « coût » est échangée hors tension par rapport à la quantité cluster hello peut être améliorée.</span><span class="sxs-lookup"><span data-stu-id="0dc7a-105">hello notion of "cost" is traded off against how much hello cluster can be improved.</span></span> <span data-ttu-id="0dc7a-106">Le coût est pris en compte lors du déplacement de services à des fins d’équilibrage, de défragmentation ou autres.</span><span class="sxs-lookup"><span data-stu-id="0dc7a-106">Cost is factored in when moving services for balancing, defragmentation, and other requirements.</span></span> <span data-ttu-id="0dc7a-107">Hello vise toomeet les exigences de hello Bonjour moins moyen d’interruption ou coûteuse.</span><span class="sxs-lookup"><span data-stu-id="0dc7a-107">hello goal is toomeet hello requirements in hello least disruptive or expensive way.</span></span> 

<span data-ttu-id="0dc7a-108">Le déplacement de services coûte au minimum du temps processeur et de la bande passante réseau.</span><span class="sxs-lookup"><span data-stu-id="0dc7a-108">Moving services costs CPU time and network bandwidth at a minimum.</span></span> <span data-ttu-id="0dc7a-109">Pour les services avec état, il requiert la copie état hello de ces services, l’utilisation du disque et mémoire supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="0dc7a-109">For stateful services, it requires copying hello state of those services, consuming additional memory and disk.</span></span> <span data-ttu-id="0dc7a-110">En réduisant les coûts de hello de solutions que hello Gestionnaire de ressources de Cluster Azure Service Fabric s’affiche avec permet de s’assurer que les ressources du cluster hello ne sont pas inutilement passées.</span><span class="sxs-lookup"><span data-stu-id="0dc7a-110">Minimizing hello cost of solutions that hello Azure Service Fabric Cluster Resource Manager comes up with helps ensure that hello cluster's resources aren't spent unnecessarily.</span></span> <span data-ttu-id="0dc7a-111">Toutefois, vous n’également tooignore solutions sont d’améliorer considérablement l’allocation des ressources de cluster de hello hello.</span><span class="sxs-lookup"><span data-stu-id="0dc7a-111">However, you also don’t want tooignore solutions that would significantly improve hello allocation of resources in hello cluster.</span></span>

<span data-ttu-id="0dc7a-112">Hello, Gestionnaire de ressources de Cluster de deux façons de coûts informatiques et en les limitant pendant qu’il essaie de cluster de hello toomanage.</span><span class="sxs-lookup"><span data-stu-id="0dc7a-112">hello Cluster Resource Manager has two ways of computing costs and limiting them while it tries toomanage hello cluster.</span></span> <span data-ttu-id="0dc7a-113">mécanisme de première Hello est simplement le comptage chaque déplacement serait.</span><span class="sxs-lookup"><span data-stu-id="0dc7a-113">hello first mechanism is simply counting every move that it would make.</span></span> <span data-ttu-id="0dc7a-114">Si les deux solutions sont générées avec sur hello même équilibrer (score), puis hello Gestionnaire du Cluster de ressource préféré hello une avec hello plus faible coût (nombre total de déplacements).</span><span class="sxs-lookup"><span data-stu-id="0dc7a-114">If two solutions are generated with about hello same balance (score), then hello Cluster Resource Manager prefers hello one with hello lowest cost (total number of moves).</span></span>

<span data-ttu-id="0dc7a-115">Cette stratégie fonctionne bien.</span><span class="sxs-lookup"><span data-stu-id="0dc7a-115">This strategy works well.</span></span> <span data-ttu-id="0dc7a-116">Mais, comme avec les charges par défaut ou statiques, il est peu probable dans n’importe quel système complexe que tous les déplacements soient égaux.</span><span class="sxs-lookup"><span data-stu-id="0dc7a-116">But as with default or static loads, it's unlikely in any complex system that all moves are equal.</span></span> <span data-ttu-id="0dc7a-117">Certaines sont probablement toobe beaucoup plus onéreuse.</span><span class="sxs-lookup"><span data-stu-id="0dc7a-117">Some are likely toobe much more expensive.</span></span>

## <a name="setting-move-costs"></a><span data-ttu-id="0dc7a-118">Définir les coûts de déplacement</span><span class="sxs-lookup"><span data-stu-id="0dc7a-118">Setting Move Costs</span></span> 
<span data-ttu-id="0dc7a-119">Vous pouvez spécifier le coût du déplacement hello par défaut pour un service lors de sa création :</span><span class="sxs-lookup"><span data-stu-id="0dc7a-119">You can specify hello default move cost for a service when it is created:</span></span>

<span data-ttu-id="0dc7a-120">PowerShell :</span><span class="sxs-lookup"><span data-stu-id="0dc7a-120">PowerShell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -DefaultMoveCost Medium
```

<span data-ttu-id="0dc7a-121">C# :</span><span class="sxs-lookup"><span data-stu-id="0dc7a-121">C#:</span></span> 

```csharp
FabricClient fabricClient = new FabricClient();
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
//set up hello rest of hello ServiceDescription
serviceDescription.DefaultMoveCost = MoveCost.Medium;
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

<span data-ttu-id="0dc7a-122">Vous pouvez également spécifier ou mettre à jour MoveCost dynamiquement pour un service après que hello service a été créé :</span><span class="sxs-lookup"><span data-stu-id="0dc7a-122">You can also specify or update MoveCost dynamically for a service after hello service has been created:</span></span> 

<span data-ttu-id="0dc7a-123">PowerShell :</span><span class="sxs-lookup"><span data-stu-id="0dc7a-123">PowerShell:</span></span> 

```posh
Update-ServiceFabricService -Stateful -ServiceName "fabric:/AppName/ServiceName" -DefaultMoveCost High
```

<span data-ttu-id="0dc7a-124">C# :</span><span class="sxs-lookup"><span data-stu-id="0dc7a-124">C#:</span></span>

```csharp
StatefulServiceUpdateDescription updateDescription = new StatefulServiceUpdateDescription();
updateDescription.DefaultMoveCost = MoveCost.High;
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/AppName/ServiceName"), updateDescription);
```

## <a name="dynamically-specifying-move-cost-on-a-per-replica-basis"></a><span data-ttu-id="0dc7a-125">Spécifier dynamiquement le coût de déplacement pour chaque réplica</span><span class="sxs-lookup"><span data-stu-id="0dc7a-125">Dynamically specifying move cost on a per-replica basis</span></span>

<span data-ttu-id="0dc7a-126">Hello des extraits de code précédents sont tous pour la spécification MoveCost pour un service entier en une seule fois à partir de service externe hello proprement dit.</span><span class="sxs-lookup"><span data-stu-id="0dc7a-126">hello preceding snippets are all for specifying MoveCost for a whole service at once from outside hello service itself.</span></span> <span data-ttu-id="0dc7a-127">Toutefois, déplacez le coût est plus utile est lorsque coût du déplacement d’un objet de service spécifique hello change au fil de sa durée de vie.</span><span class="sxs-lookup"><span data-stu-id="0dc7a-127">However, move cost is most useful is when hello move cost of a specific service object changes over its lifespan.</span></span> <span data-ttu-id="0dc7a-128">Puisque hello services eux-mêmes probablement judicieux de hello coût se toomove un moment donné, il est une API pour tooreport services leur propres mouvement coût pendant l’exécution.</span><span class="sxs-lookup"><span data-stu-id="0dc7a-128">Since hello services themselves probably have hello best idea of how costly they are toomove a given time, there's an API for services tooreport their own individual move cost during runtime.</span></span> 

<span data-ttu-id="0dc7a-129">C# :</span><span class="sxs-lookup"><span data-stu-id="0dc7a-129">C#:</span></span>

```csharp
this.Partition.ReportMoveCost(MoveCost.Medium);
```

## <a name="impact-of-move-cost"></a><span data-ttu-id="0dc7a-130">Impact du coût de déplacement</span><span class="sxs-lookup"><span data-stu-id="0dc7a-130">Impact of move cost</span></span>
<span data-ttu-id="0dc7a-131">MoveCost a quatre niveaux : zéro, faible, moyen et élevé.</span><span class="sxs-lookup"><span data-stu-id="0dc7a-131">MoveCost has four levels: Zero, Low, Medium, and High.</span></span> <span data-ttu-id="0dc7a-132">MoveCosts sont relatif tooeach autre, à l’exception de zéro.</span><span class="sxs-lookup"><span data-stu-id="0dc7a-132">MoveCosts are relative tooeach other, except for Zero.</span></span> <span data-ttu-id="0dc7a-133">Aucun coût de déplacement signifie que le déplacement des sont gratuit et ne doivent pas compter sur le score hello de solution de hello.</span><span class="sxs-lookup"><span data-stu-id="0dc7a-133">Zero move cost means that movement is free and should not count against hello score of hello solution.</span></span> <span data-ttu-id="0dc7a-134">Paramètre que vous déplacez votre coût tooHigh est *pas* garantit que le réplica hello reste dans un seul emplacement.</span><span class="sxs-lookup"><span data-stu-id="0dc7a-134">Setting your move cost tooHigh does *not* guarantee that hello replica stays in one place.</span></span>

<span data-ttu-id="0dc7a-135"><center>
![Coût du déplacement comme facteur de sélection des réplicas pour les déplacements][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="0dc7a-135"><center>
![Move cost as a factor in selecting replicas for movement][Image1]
</center></span></span>

<span data-ttu-id="0dc7a-136">MoveCost vous permet de trouver des solutions hello que cause hello globale des minimiser les interruptions et tooachieve plus simple lors toujours arrivant au solde équivalent.</span><span class="sxs-lookup"><span data-stu-id="0dc7a-136">MoveCost helps you find hello solutions that cause hello least disruption overall and are easiest tooachieve while still arriving at equivalent balance.</span></span> <span data-ttu-id="0dc7a-137">Notion d’un service de coût peut être réduire relatif.</span><span class="sxs-lookup"><span data-stu-id="0dc7a-137">A service’s notion of cost can be relative toomany things.</span></span> <span data-ttu-id="0dc7a-138">Hello facteurs courants dans le calcul du coût du déplacement sont :</span><span class="sxs-lookup"><span data-stu-id="0dc7a-138">hello most common factors in calculating your move cost are:</span></span>

- <span data-ttu-id="0dc7a-139">quantité de Hello d’état ou les données que le service de hello a toomove.</span><span class="sxs-lookup"><span data-stu-id="0dc7a-139">hello amount of state or data that hello service has toomove.</span></span>
- <span data-ttu-id="0dc7a-140">coût de Hello de déconnexion des clients.</span><span class="sxs-lookup"><span data-stu-id="0dc7a-140">hello cost of disconnection of clients.</span></span> <span data-ttu-id="0dc7a-141">Déplacement d’un réplica principal est généralement plus coûteuse que coût hello de déplacement d’un réplica secondaire.</span><span class="sxs-lookup"><span data-stu-id="0dc7a-141">Moving a primary replica is usually more costly than hello cost of moving a secondary replica.</span></span>
- <span data-ttu-id="0dc7a-142">coût Hello d’interruption d’une opération en cours.</span><span class="sxs-lookup"><span data-stu-id="0dc7a-142">hello cost of interrupting an in-flight operation.</span></span> <span data-ttu-id="0dc7a-143">Certaines opérations sur les données de salutation stocker au niveau du ou des opérations dans l’appel de réponse tooa client sont coûteuses.</span><span class="sxs-lookup"><span data-stu-id="0dc7a-143">Some operations at hello data store level or operations performed in response tooa client call are costly.</span></span> <span data-ttu-id="0dc7a-144">Après un certain point, vous ne souhaitez pas toostop les si vous n’êtes pas obligé.</span><span class="sxs-lookup"><span data-stu-id="0dc7a-144">After a certain point, you don’t want toostop them if you don’t have to.</span></span> <span data-ttu-id="0dc7a-145">Par conséquent, pendant les opération hello, vous augmentez coût du déplacement de cette probabilité hello tooreduce objet service qui il déplace hello.</span><span class="sxs-lookup"><span data-stu-id="0dc7a-145">So while hello operation is going on, you increase hello move cost of this service object tooreduce hello likelihood that it moves.</span></span> <span data-ttu-id="0dc7a-146">Lors de l’opération de hello, vous définissez toonormal arrière du coût hello.</span><span class="sxs-lookup"><span data-stu-id="0dc7a-146">When hello operation is done, you set hello cost back toonormal.</span></span>

## <a name="enabling-move-cost-in-your-cluster"></a><span data-ttu-id="0dc7a-147">Activer le coût de déplacement dans un cluster</span><span class="sxs-lookup"><span data-stu-id="0dc7a-147">Enabling move cost in your cluster</span></span>
<span data-ttu-id="0dc7a-148">Dans l’ordre pour hello plus granulaire MoveCosts toobe pris en compte, MoveCost doit être activé dans votre cluster.</span><span class="sxs-lookup"><span data-stu-id="0dc7a-148">In order for hello more granular MoveCosts toobe taken into account, MoveCost must be enabled in your cluster.</span></span> <span data-ttu-id="0dc7a-149">Sans ce paramètre, le mode par défaut hello de comptage des déplacements est utilisé pour calculer MoveCost et MoveCost États sont ignorés.</span><span class="sxs-lookup"><span data-stu-id="0dc7a-149">Without this setting, hello default mode of counting moves is used for calculating MoveCost, and MoveCost reports are ignored.</span></span>


<span data-ttu-id="0dc7a-150">ClusterManifest.xml :</span><span class="sxs-lookup"><span data-stu-id="0dc7a-150">ClusterManifest.xml:</span></span>

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="UseMoveCostReports" Value="true" />
        </Section>
```

<span data-ttu-id="0dc7a-151">via ClusterConfig.json pour les déploiements autonomes ou Template.json pour les clusters hébergés sur Azure :</span><span class="sxs-lookup"><span data-stu-id="0dc7a-151">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="0dc7a-152">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0dc7a-152">Next steps</span></span>
- <span data-ttu-id="0dc7a-153">Gestionnaire de ressources du Cluster service Fabric utilise la capacité et la consommation de métriques toomanage dans un cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="0dc7a-153">Service Fabric Cluster Resource Manger uses metrics toomanage consumption and capacity in hello cluster.</span></span> <span data-ttu-id="0dc7a-154">toolearn plus d’informations sur les métriques et comment tooconfigure, extraire [la gestion de la consommation des ressources et les charge dans l’infrastructure de Service avec les mesures de](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="0dc7a-154">toolearn more about metrics and how tooconfigure them, check out [Managing resource consumption and load in Service Fabric with metrics](service-fabric-cluster-resource-manager-metrics.md).</span></span>
- <span data-ttu-id="0dc7a-155">toolearn sur comment hello Gestionnaire de ressources de Cluster gère et équilibre la charge du cluster de hello, extraire [votre cluster Service Fabric d’équilibrage](service-fabric-cluster-resource-manager-balancing.md).</span><span class="sxs-lookup"><span data-stu-id="0dc7a-155">toolearn about how hello Cluster Resource Manager manages and balances load in hello cluster, check out [Balancing your Service Fabric cluster](service-fabric-cluster-resource-manager-balancing.md).</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-movement-cost/service-most-cost-example.png
