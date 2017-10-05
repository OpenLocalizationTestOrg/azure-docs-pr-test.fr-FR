---
title: "Équilibrer un cluster Azure Service Fabric | Microsoft Docs"
description: "Présentation de l’équilibrage de votre cluster avec Service Fabric Cluster Resource Manager."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 030b1465-6616-4c0b-8bc7-24ed47d054c0
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 34eacb29f324025c1d2803c9690600227d3ec457
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="balancing-your-service-fabric-cluster"></a><span data-ttu-id="046c3-103">Équilibrage de votre cluster Service Fabric</span><span class="sxs-lookup"><span data-stu-id="046c3-103">Balancing your service fabric cluster</span></span>
<span data-ttu-id="046c3-104">Service Fabric Cluster Resource Manager permet de modifier la charge dynamique, de réagir aux ajouts ou aux suppressions de nœuds ou de services.</span><span class="sxs-lookup"><span data-stu-id="046c3-104">The Service Fabric Cluster Resource Manager supports dynamic load changes, reacting to additions or removals of nodes or services.</span></span> <span data-ttu-id="046c3-105">Il corrige également automatiquement les violations de contrainte et rééquilibre de façon proactive le cluster.</span><span class="sxs-lookup"><span data-stu-id="046c3-105">It also automatically corrects constraint violations, and proactively rebalances the cluster.</span></span> <span data-ttu-id="046c3-106">Mais à quelle fréquence ces actions sont-elles effectuées, et quel en est l’élément déclencheur ?</span><span class="sxs-lookup"><span data-stu-id="046c3-106">But how often are these actions taken, and what triggers them?</span></span>

<span data-ttu-id="046c3-107">Il existe trois différentes catégories de tâches exécutées par Cluster Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="046c3-107">There are three different categories of work that the Cluster Resource Manager performs.</span></span> <span data-ttu-id="046c3-108">Il s'agit de :</span><span class="sxs-lookup"><span data-stu-id="046c3-108">They are:</span></span>

1. <span data-ttu-id="046c3-109">Positionnement : cette étape a trait au placement des réplicas avec état ou des instances sans état manquants.</span><span class="sxs-lookup"><span data-stu-id="046c3-109">Placement – this stage deals with placing any stateful replicas or stateless instances that are missing.</span></span> <span data-ttu-id="046c3-110">Le positionnement inclut non seulement les nouveaux services, mais aussi les réplicas avec état ou les instances sans état qui ont échoué.</span><span class="sxs-lookup"><span data-stu-id="046c3-110">Placement includes both new services and handling stateful replicas or stateless instances that have failed.</span></span> <span data-ttu-id="046c3-111">La suppression et l’annulation des réplicas ou des instances sont gérées ici.</span><span class="sxs-lookup"><span data-stu-id="046c3-111">Deleting and dropping replicas or instances are handled here.</span></span>
2. <span data-ttu-id="046c3-112">Vérifications de contrainte : cette étape recherche les violations des différentes contraintes (règles) de placement au sein du système et apporte les corrections nécessaires.</span><span class="sxs-lookup"><span data-stu-id="046c3-112">Constraint Checks – this stage checks for and corrects violations of the different placement constraints (rules) within the system.</span></span> <span data-ttu-id="046c3-113">Le non-dépassement de la capacité des nœuds et le respect des contraintes de positionnement d’un service sont des exemples de règles.</span><span class="sxs-lookup"><span data-stu-id="046c3-113">Examples of rules are things like ensuring that nodes are not over capacity and that a service’s placement constraints are met.</span></span>
3. <span data-ttu-id="046c3-114">Équilibrage : cette étape vérifie si un rééquilibrage est nécessaire en fonction du niveau d’équilibrage désiré qui a été configuré pour différentes mesures.</span><span class="sxs-lookup"><span data-stu-id="046c3-114">Balancing – this stage checks to see if rebalancing is necessary based on the configured desired level of balance for different metrics.</span></span> <span data-ttu-id="046c3-115">Si c’est le cas, elle tente de trouver une disposition plus équilibrée dans le cluster.</span><span class="sxs-lookup"><span data-stu-id="046c3-115">If so it attempts to find an arrangement in the cluster that is more balanced.</span></span>

## <a name="configuring-cluster-resource-manager-timers"></a><span data-ttu-id="046c3-116">Configuration des minuteurs Cluster Resource Manager</span><span class="sxs-lookup"><span data-stu-id="046c3-116">Configuring Cluster Resource Manager Timers</span></span>
<span data-ttu-id="046c3-117">Le premier ensemble de contrôles autour d’équilibrage sont un ensemble de minuteurs.</span><span class="sxs-lookup"><span data-stu-id="046c3-117">The first set of controls around balancing are a set of timers.</span></span> <span data-ttu-id="046c3-118">Ces minuteurs déterminent la fréquence à laquelle Cluster Resource Manager examine le cluster et mène des actions correctives.</span><span class="sxs-lookup"><span data-stu-id="046c3-118">These timers govern how often the Cluster Resource Manager examines the cluster and takes corrective actions.</span></span>

<span data-ttu-id="046c3-119">Chacun de ces différents types de corrections offerts par Cluster Resource Manager est contrôlé par un minuteur différent qui détermine sa fréquence.</span><span class="sxs-lookup"><span data-stu-id="046c3-119">Each of these different types of corrections the Cluster Resource Manager can make is controlled by a different timer that governs its frequency.</span></span> <span data-ttu-id="046c3-120">Lorsque chaque minuteur se déclenche, la tâche est planifiée.</span><span class="sxs-lookup"><span data-stu-id="046c3-120">When each timer fires, the task is scheduled.</span></span> <span data-ttu-id="046c3-121">Par défaut, Resource Manager :</span><span class="sxs-lookup"><span data-stu-id="046c3-121">By default the Resource Manager:</span></span>

* <span data-ttu-id="046c3-122">analyse son état et applique des mises à jour (comme l’enregistrement de l’arrêt d’un nœud) tous les dixièmes de seconde ;</span><span class="sxs-lookup"><span data-stu-id="046c3-122">scans its state and applies updates (like recording that a node is down) every 1/10th of a second</span></span>
* <span data-ttu-id="046c3-123">définit l’indicateur de contrôle du placement</span><span class="sxs-lookup"><span data-stu-id="046c3-123">sets the placement check flag</span></span> 
* <span data-ttu-id="046c3-124">définit l’indicateur de contrôle de la contrainte chaque seconde</span><span class="sxs-lookup"><span data-stu-id="046c3-124">sets the constraint check flag every second</span></span>
* <span data-ttu-id="046c3-125">définit l’indicateur d’équilibrage toutes les cinq secondes.</span><span class="sxs-lookup"><span data-stu-id="046c3-125">sets the balancing flag every five seconds.</span></span>

<span data-ttu-id="046c3-126">Voici des exemples de configuration qui définit ces minuteurs :</span><span class="sxs-lookup"><span data-stu-id="046c3-126">Examples of the configuration governing these timers are below:</span></span>

<span data-ttu-id="046c3-127">ClusterManifest.xml :</span><span class="sxs-lookup"><span data-stu-id="046c3-127">ClusterManifest.xml:</span></span>

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="PLBRefreshGap" Value="0.1" />
            <Parameter Name="MinPlacementInterval" Value="1.0" />
            <Parameter Name="MinConstraintCheckInterval" Value="1.0" />
            <Parameter Name="MinLoadBalancingInterval" Value="5.0" />
        </Section>
```

<span data-ttu-id="046c3-128">via ClusterConfig.json pour les déploiements autonomes ou Template.json pour les clusters hébergés sur Azure :</span><span class="sxs-lookup"><span data-stu-id="046c3-128">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "PLBRefreshGap",
          "value": "0.10"
      },
      {
          "name": "MinPlacementInterval",
          "value": "1.0"
      },
      {
          "name": "MinConstraintCheckInterval",
          "value": "1.0"
      },
      {
          "name": "MinLoadBalancingInterval",
          "value": "5.0"
      }
    ]
  }
]
```

<span data-ttu-id="046c3-129">À l’heure actuelle, Cluster Resource Manager effectue uniquement l’une de ces actions à la fois, séquentiellement.</span><span class="sxs-lookup"><span data-stu-id="046c3-129">Today the Cluster Resource Manager only performs one of these actions at a time, sequentially.</span></span> <span data-ttu-id="046c3-130">C’est pourquoi nous faisons référence à ces minuteurs en tant qu’« intervalles minimaux » et les actions effectuées lorsque les minuteurs sont déclenchés représentent des « indicateurs de paramètre ».</span><span class="sxs-lookup"><span data-stu-id="046c3-130">This is why we refer to these timers as “minimum intervals” and the actions that get taken when the timers go off as "setting flags".</span></span> <span data-ttu-id="046c3-131">Par exemple, Cluster Resource Manager traite les demandes de création de services en attente avant d’équilibrer le cluster.</span><span class="sxs-lookup"><span data-stu-id="046c3-131">For example, the Cluster Resource Manager takes care of pending requests to create services before balancing the cluster.</span></span> <span data-ttu-id="046c3-132">Comme en témoignent les intervalles de temps par défaut spécifiés, Cluster Resource Manager analyse fréquemment ce qu’il a à faire.</span><span class="sxs-lookup"><span data-stu-id="046c3-132">As you can see by the default time intervals specified, the Cluster Resource Manager scans for anything it needs to do frequently.</span></span> <span data-ttu-id="046c3-133">Par conséquent, les modifications apportées à la fin de chaque étape sont généralement mineures.</span><span class="sxs-lookup"><span data-stu-id="046c3-133">Normally this means that the set of changes made during each step is small.</span></span> <span data-ttu-id="046c3-134">L’apport fréquent de modifications mineures rend Cluster Resource Manager réactif aux événements qui se produisent dans le cluster.</span><span class="sxs-lookup"><span data-stu-id="046c3-134">Making small changes frequently allows the Cluster Resource Manager to be responsive when things happen in the cluster.</span></span> <span data-ttu-id="046c3-135">Les compteurs par défaut assurent en partie un traitement par lot, car un grand nombre d’événements du même type ont tendance à se produire simultanément.</span><span class="sxs-lookup"><span data-stu-id="046c3-135">The default timers provide some batching since many of the same types of events tend to occur simultaneously.</span></span> 

<span data-ttu-id="046c3-136">Par exemple, lorsque des nœuds échouent, ils se produisent simultanément dans des domaines d’erreur entiers.</span><span class="sxs-lookup"><span data-stu-id="046c3-136">For example, when nodes fail they can do so entire fault domains at a time.</span></span> <span data-ttu-id="046c3-137">Tous ces échecs sont capturés à la prochaine mise à jour de l’état après *PLBRefreshGap*.</span><span class="sxs-lookup"><span data-stu-id="046c3-137">All these failures are captured during the next state update after the *PLBRefreshGap*.</span></span> <span data-ttu-id="046c3-138">Les corrections sont déterminées lorsque les prochaines opérations de placement, de contrôle des contraintes et d’équilibrage sont exécutées.</span><span class="sxs-lookup"><span data-stu-id="046c3-138">The corrections are determined during the following placement, constraint check, and balancing runs.</span></span> <span data-ttu-id="046c3-139">Par défaut, Cluster Resource Manager n’analyse pas les modifications qui ont eu lieu sur plusieurs heures dans le cluster et n’essaie pas de les traiter toutes en même temps.</span><span class="sxs-lookup"><span data-stu-id="046c3-139">By default the Cluster Resource Manager is not scanning through hours of changes in the cluster and trying to address all changes at once.</span></span> <span data-ttu-id="046c3-140">En effet, cela entraînerait des pics d’activité momentanés.</span><span class="sxs-lookup"><span data-stu-id="046c3-140">Doing so would lead to bursts of churn.</span></span>

<span data-ttu-id="046c3-141">Cluster Resource Manager a également besoin d’informations supplémentaires pour déterminer si le cluster est déséquilibré.</span><span class="sxs-lookup"><span data-stu-id="046c3-141">The Cluster Resource Manager also needs some additional information to determine if the cluster imbalanced.</span></span> <span data-ttu-id="046c3-142">Nous disposons pour cela de deux autres éléments de configuration : *BalancingThresholds* et *ActivityThresholds*.</span><span class="sxs-lookup"><span data-stu-id="046c3-142">For that we have two other pieces of configuration: *BalancingThresholds* and *ActivityThresholds*.</span></span>

## <a name="balancing-thresholds"></a><span data-ttu-id="046c3-143">Seuils d’équilibrage</span><span class="sxs-lookup"><span data-stu-id="046c3-143">Balancing thresholds</span></span>
<span data-ttu-id="046c3-144">Un seuil d’équilibrage est le principal contrôle utilisé pour déclencher le rééquilibrage.</span><span class="sxs-lookup"><span data-stu-id="046c3-144">A Balancing Threshold is the main control for triggering rebalancing.</span></span> <span data-ttu-id="046c3-145">Le seuil d’équilibrage pour une métrique est un _ratio_.</span><span class="sxs-lookup"><span data-stu-id="046c3-145">The Balancing Threshold for a metric is a _ratio_.</span></span> <span data-ttu-id="046c3-146">Si la charge d’une mesure sur le nœud le plus chargé, divisée par la quantité de charge sur le nœud le moins chargé, dépasse la valeur *BalancingThreshold* de cette mesure, le cluster est considéré comme déséquilibré.</span><span class="sxs-lookup"><span data-stu-id="046c3-146">If the load for a metric on the most loaded node divided by the amount of load on the least loaded node exceeds that metric's *BalancingThreshold*, then the cluster is imbalanced.</span></span> <span data-ttu-id="046c3-147">L’équilibrage est alors déclenché lorsque Cluster Resource Manager effectue sa vérification suivante.</span><span class="sxs-lookup"><span data-stu-id="046c3-147">As a result balancing is triggered the next time the Cluster Resource Manager checks.</span></span> <span data-ttu-id="046c3-148">Le minuteur *MinLoadBalancingInterval* détermine la fréquence à laquelle Cluster Resource Manager doit vérifier si un rééquilibrage est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="046c3-148">The *MinLoadBalancingInterval* timer defines how often the Cluster Resource Manager should check if rebalancing is necessary.</span></span> <span data-ttu-id="046c3-149">Cette vérification ne signifie pas que quelque chose se produit.</span><span class="sxs-lookup"><span data-stu-id="046c3-149">Checking doesn't mean that anything happens.</span></span> 

<span data-ttu-id="046c3-150">Les seuils d’équilibrage sont définis par métrique dans le cadre de la définition du cluster.</span><span class="sxs-lookup"><span data-stu-id="046c3-150">Balancing Thresholds are defined on a per-metric basis as a part of the cluster definition.</span></span> <span data-ttu-id="046c3-151">Pour plus d’informations sur les mesures, consultez [cet article](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="046c3-151">For more information on metrics, check out [this article](service-fabric-cluster-resource-manager-metrics.md).</span></span>

<span data-ttu-id="046c3-152">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="046c3-152">ClusterManifest.xml</span></span>

```xml
    <Section Name="MetricBalancingThresholds">
      <Parameter Name="MetricName1" Value="2"/>
      <Parameter Name="MetricName2" Value="3.5"/>
    </Section>
```

<span data-ttu-id="046c3-153">via ClusterConfig.json pour les déploiements autonomes ou Template.json pour les clusters hébergés sur Azure :</span><span class="sxs-lookup"><span data-stu-id="046c3-153">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "MetricBalancingThresholds",
    "parameters": [
      {
          "name": "MetricName1",
          "value": "2"
      },
      {
          "name": "MetricName2",
          "value": "3.5"
      }
    ]
  }
]
```

<span data-ttu-id="046c3-154"><center>
Exemple de seuil d’équilibrage![][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="046c3-154"><center>
![Balancing Threshold Example][Image1]
</center></span></span>

<span data-ttu-id="046c3-155">Dans cet exemple, chaque service utilise une unité d’une mesure donnée.</span><span class="sxs-lookup"><span data-stu-id="046c3-155">In this example, each service is consuming one unit of some metric.</span></span> <span data-ttu-id="046c3-156">Dans l’exemple du haut, la charge maximale sur un nœud est égale à 5 et la valeur minimale à 2.</span><span class="sxs-lookup"><span data-stu-id="046c3-156">In the top example, the maximum load on a node is five and the minimum is two.</span></span> <span data-ttu-id="046c3-157">Supposons que le seuil d’équilibrage pour cette mesure soit égal à 3.</span><span class="sxs-lookup"><span data-stu-id="046c3-157">Let’s say that the balancing threshold for this metric is three.</span></span> <span data-ttu-id="046c3-158">Étant donné que le ratio dans le cluster est de 5/2 = 2,5, soit une valeur inférieure au seuil d’équilibrage de 3, le cluster est équilibré.</span><span class="sxs-lookup"><span data-stu-id="046c3-158">Since the ratio in the cluster is 5/2 = 2.5 and that is less than the specified balancing threshold of three, the cluster is balanced.</span></span> <span data-ttu-id="046c3-159">Aucun équilibrage n’est déclenché lorsque Cluster Resource Manager effectue sa vérification.</span><span class="sxs-lookup"><span data-stu-id="046c3-159">No balancing is triggered when the Cluster Resource Manager checks.</span></span>

<span data-ttu-id="046c3-160">Dans l’exemple du bas, la charge maximale sur un nœud est égale à 10 et la valeur minimale à 2, ce qui donne un ratio de 5.</span><span class="sxs-lookup"><span data-stu-id="046c3-160">In the bottom example, the maximum load on a node is 10, while the minimum is two, resulting in a ratio of five.</span></span> <span data-ttu-id="046c3-161">Cette valeur étant supérieure au seuil d’équilibrage de 3 spécifié pour cette mesure,</span><span class="sxs-lookup"><span data-stu-id="046c3-161">Five is greater than the designated balancing threshold of three for that metric.</span></span> <span data-ttu-id="046c3-162">l’exécution d’un rééquilibrage sera planifiée lors du prochain déclenchement du minuteur d’équilibrage.</span><span class="sxs-lookup"><span data-stu-id="046c3-162">As a result, a rebalancing run will be scheduled next time the balancing timer fires.</span></span> <span data-ttu-id="046c3-163">Dans une telle situation, une partie de la charge est généralement répartie sur le nœud Node3.</span><span class="sxs-lookup"><span data-stu-id="046c3-163">In a situation like this some load is usually distributed to Node3.</span></span> <span data-ttu-id="046c3-164">Comme Service Fabric Cluster Resource Manager utilise une approche prudente, une partie de la charge peut également être répartie sur le nœud Node2.</span><span class="sxs-lookup"><span data-stu-id="046c3-164">Because the Service Fabric Cluster Resource Manager doesn't use a greedy approach, some load could also be distributed to Node2.</span></span> 

<span data-ttu-id="046c3-165"><center>
Actions de l’exemple de seuil d’équilibrage![][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="046c3-165"><center>
![Balancing Threshold Example Actions][Image2]
</center></span></span>

> [!NOTE]
> <span data-ttu-id="046c3-166">« L’équilibrage » adopte deux stratégies différentes pour gérer la charge de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="046c3-166">"Balancing" handles two different strategies for managing load in your cluster.</span></span> <span data-ttu-id="046c3-167">La stratégie par défaut utilisée par Cluster Resource Manager consiste à répartir la charge sur les nœuds du cluster.</span><span class="sxs-lookup"><span data-stu-id="046c3-167">The default strategy that the Cluster Resource Manager uses is to distribute load across the nodes in the cluster.</span></span> <span data-ttu-id="046c3-168">L’autre stratégie est la [défragmentation](service-fabric-cluster-resource-manager-defragmentation-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="046c3-168">The other strategy is [defragmentation](service-fabric-cluster-resource-manager-defragmentation-metrics.md).</span></span> <span data-ttu-id="046c3-169">La défragmentation se produit en même temps que l’équilibrage.</span><span class="sxs-lookup"><span data-stu-id="046c3-169">Defragmentation is performed during the same balancing run.</span></span> <span data-ttu-id="046c3-170">Les stratégies d’équilibrage et de défragmentation peuvent être utilisées pour différentes mesures au sein du même cluster.</span><span class="sxs-lookup"><span data-stu-id="046c3-170">The balancing and defragmentation strategies can be used for different metrics within the same cluster.</span></span> <span data-ttu-id="046c3-171">Un service peut avoir à la fois des mesures d’équilibrage et de défragmentation.</span><span class="sxs-lookup"><span data-stu-id="046c3-171">A service can have both balancing and defragmentation metrics.</span></span> <span data-ttu-id="046c3-172">Pour les mesures de défragmentation, le ratio des charges dans le cluster déclenche un rééquilibrage lorsqu’il se situe _sous_ le seuil d’équilibrage.</span><span class="sxs-lookup"><span data-stu-id="046c3-172">For defragmentation metrics, the ratio of the loads in the cluster triggers rebalancing when it is _below_ the balancing threshold.</span></span> 
>

<span data-ttu-id="046c3-173">L’obtention d’une valeur inférieure au seuil d’équilibrage ne constitue pas un objectif explicite.</span><span class="sxs-lookup"><span data-stu-id="046c3-173">Getting below the balancing threshold is not an explicit goal.</span></span> <span data-ttu-id="046c3-174">Les seuils d’équilibrage ne sont qu’un *déclencheur*.</span><span class="sxs-lookup"><span data-stu-id="046c3-174">Balancing Thresholds are just a *trigger*.</span></span> <span data-ttu-id="046c3-175">Lors de l’équilibrage, Cluster Resource Manager détermine les améliorations possibles, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="046c3-175">When balancing runs, the Cluster Resource Manager determines what improvements it can make, if any.</span></span> <span data-ttu-id="046c3-176">Une analyse d’équilibrage ne signifie pas que des données sont déplacées.</span><span class="sxs-lookup"><span data-stu-id="046c3-176">Just because a balancing search is kicked off doesn't mean anything moves.</span></span> <span data-ttu-id="046c3-177">Parfois, le cluster est déséquilibré mais comporte trop de contraintes pour être corrigé.</span><span class="sxs-lookup"><span data-stu-id="046c3-177">Sometimes the cluster is imbalanced but too constrained to correct.</span></span> <span data-ttu-id="046c3-178">Les améliorations peuvent également nécessiter des mouvements trop [coûteux](service-fabric-cluster-resource-manager-movement-cost.md).</span><span class="sxs-lookup"><span data-stu-id="046c3-178">Alternatively, the improvements require movements that are too [costly](service-fabric-cluster-resource-manager-movement-cost.md)).</span></span>

## <a name="activity-thresholds"></a><span data-ttu-id="046c3-179">seuils d’activité</span><span class="sxs-lookup"><span data-stu-id="046c3-179">Activity thresholds</span></span>
<span data-ttu-id="046c3-180">Parfois, même si les nœuds sont relativement déséquilibrés, la quantité *totale* de charge dans le cluster est faible.</span><span class="sxs-lookup"><span data-stu-id="046c3-180">Sometimes, although nodes are relatively imbalanced, the *total* amount of load in the cluster is low.</span></span> <span data-ttu-id="046c3-181">La charge insuffisante peut correspondre à une baisse temporaire ou être due au fait qu’il s’agit d’un nouveau cluster qui vient juste d’être amorcé.</span><span class="sxs-lookup"><span data-stu-id="046c3-181">The lack of load could be a transient dip, or because the cluster is new and just getting bootstrapped.</span></span> <span data-ttu-id="046c3-182">Dans les deux cas, il n’est pas forcément judicieux de passer du temps à équilibrer le cluster, car les gains seront minimes.</span><span class="sxs-lookup"><span data-stu-id="046c3-182">In either case, you may not want to spend time balancing the cluster because there’s little to be gained.</span></span> <span data-ttu-id="046c3-183">Si le cluster a fait l’objet d’un équilibrage, vous consommerez des ressources réseau et de calcul pour déplacer des éléments sans que cela ait un impact *réel*.</span><span class="sxs-lookup"><span data-stu-id="046c3-183">If the cluster underwent balancing, you’d spend network and compute resources to move things around without making any large *absolute* difference.</span></span> <span data-ttu-id="046c3-184">Pour éviter ces mouvements inutiles, il existe un autre contrôle appelé « seuil d’activité ».</span><span class="sxs-lookup"><span data-stu-id="046c3-184">To avoid unnecessary moves, there’s another control known as Activity Thresholds.</span></span> <span data-ttu-id="046c3-185">Les seuils d’activité vous permettent de spécifier une limite inférieure absolue pour l’activité.</span><span class="sxs-lookup"><span data-stu-id="046c3-185">Activity Thresholds allows you to specify some absolute lower bound for activity.</span></span> <span data-ttu-id="046c3-186">Lorsqu’aucun nœud ne dépasse ce seuil, l’équilibrage n’est pas déclenché, même si le seuil d’équilibrage est atteint.</span><span class="sxs-lookup"><span data-stu-id="046c3-186">If no node is over this threshold, balancing isn't triggered even if the Balancing Threshold is met.</span></span>

<span data-ttu-id="046c3-187">Supposons que nous conservons notre seuil d’équilibrage de 3 pour cette mesure.</span><span class="sxs-lookup"><span data-stu-id="046c3-187">Let’s say that we retain our Balancing Threshold of three for this metric.</span></span> <span data-ttu-id="046c3-188">Supposons également que nous avons un seuil d’activité de 1 536.</span><span class="sxs-lookup"><span data-stu-id="046c3-188">Let's also say we have an Activity Threshold of 1536.</span></span> <span data-ttu-id="046c3-189">Dans le premier cas, bien que le cluster soit déséquilibré selon le seuil d’équilibrage, comme aucun nœud n’atteint le seuil d’activité, il ne se passe rien.</span><span class="sxs-lookup"><span data-stu-id="046c3-189">In the first case, while the cluster is imbalanced per the Balancing Threshold there's no node meets that Activity Threshold, so nothing happens.</span></span> <span data-ttu-id="046c3-190">Dans l’exemple du bas, le nœud Node1 dépasse le seuil d’activité.</span><span class="sxs-lookup"><span data-stu-id="046c3-190">In the bottom example, Node1 is over the Activity Threshold.</span></span> <span data-ttu-id="046c3-191">Comme le seuil d’équilibrage et le seuil d’activité pour la mesure sont tous deux dépassés, un équilibrage est planifié.</span><span class="sxs-lookup"><span data-stu-id="046c3-191">Since both the Balancing Threshold and the Activity Threshold for the metric are exceeded, balancing is scheduled.</span></span> <span data-ttu-id="046c3-192">Prenons pour exemple le schéma suivant :</span><span class="sxs-lookup"><span data-stu-id="046c3-192">As an example, let's look at the following diagram:</span></span> 

<span data-ttu-id="046c3-193"><center>
Exemple de seuil d’activité![][Image3]
</center></span><span class="sxs-lookup"><span data-stu-id="046c3-193"><center>
![Activity Threshold Example][Image3]
</center></span></span>

<span data-ttu-id="046c3-194">Au même titre que les seuils d’équilibrage, les seuils d’activité sont définis par métrique par l’intermédiaire de la définition du cluster :</span><span class="sxs-lookup"><span data-stu-id="046c3-194">Just like Balancing Thresholds, Activity Thresholds are defined per-metric via the cluster definition:</span></span>

<span data-ttu-id="046c3-195">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="046c3-195">ClusterManifest.xml</span></span>

``` xml
    <Section Name="MetricActivityThresholds">
      <Parameter Name="Memory" Value="1536"/>
    </Section>
```

<span data-ttu-id="046c3-196">via ClusterConfig.json pour les déploiements autonomes ou Template.json pour les clusters hébergés sur Azure :</span><span class="sxs-lookup"><span data-stu-id="046c3-196">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "MetricActivityThresholds",
    "parameters": [
      {
          "name": "Memory",
          "value": "1536"
      }
    ]
  }
]
```

<span data-ttu-id="046c3-197">Les seuils d’équilibrage et d’activité sont tous deux liés à une mesure spécifique : l’équilibrage n’est déclenché que si le seuil d’équilibrage et le seuil d’activité sont dépassés pour la même mesure.</span><span class="sxs-lookup"><span data-stu-id="046c3-197">Balancing and activity thresholds are both tied to a specific metric - balancing is triggered only if both the Balancing Threshold and Activity Threshold is exceeded for the same metric.</span></span>

## <a name="balancing-services-together"></a><span data-ttu-id="046c3-198">Équilibrage de plusieurs services en même temps</span><span class="sxs-lookup"><span data-stu-id="046c3-198">Balancing services together</span></span>
<span data-ttu-id="046c3-199">La détermination de l’état de déséquilibre du cluster est une décision qui porte sur l’ensemble du cluster.</span><span class="sxs-lookup"><span data-stu-id="046c3-199">Whether the cluster is imbalanced or not is a cluster-wide decision.</span></span> <span data-ttu-id="046c3-200">Cependant, la procédure suivie pour corriger un déséquilibre consiste à déplacer des instances et des réplicas de service individuels.</span><span class="sxs-lookup"><span data-stu-id="046c3-200">However, the way we go about fixing it is moving individual service replicas and instances around.</span></span> <span data-ttu-id="046c3-201">Logique, n’est-ce pas ?</span><span class="sxs-lookup"><span data-stu-id="046c3-201">This makes sense, right?</span></span> <span data-ttu-id="046c3-202">Si la mémoire est empilée sur un nœud, plusieurs réplicas ou instances peuvent être impliqués.</span><span class="sxs-lookup"><span data-stu-id="046c3-202">If memory is stacked up on one node, multiple replicas or instances could be contributing to it.</span></span> <span data-ttu-id="046c3-203">Pour corriger le déséquilibre, il peut donc être nécessaire de déplacer les réplicas avec état ou les instances sans état qui utilisent la mesure déséquilibrée.</span><span class="sxs-lookup"><span data-stu-id="046c3-203">Fixing the imbalance could require moving any of the stateful replicas or stateless instances that use the imbalanced metric.</span></span>

<span data-ttu-id="046c3-204">Occasionnellement pourtant, un service qui n’était pas déséquilibré lui-même est déplacé (voir la discussion sur les poids locaux et globaux plus haut).</span><span class="sxs-lookup"><span data-stu-id="046c3-204">Occasionally though, a service that wasn’t itself imbalanced gets moved (remember the discussion of local and global weights earlier).</span></span> <span data-ttu-id="046c3-205">Pourquoi un service serait-il déplacé si toutes les mesures de ce service ont été équilibrées ?</span><span class="sxs-lookup"><span data-stu-id="046c3-205">Why would a service get moved when all that service’s metrics were balanced?</span></span> <span data-ttu-id="046c3-206">Examinons un exemple :</span><span class="sxs-lookup"><span data-stu-id="046c3-206">Let’s see an example:</span></span>

- <span data-ttu-id="046c3-207">Prenons par exemple quatre services : Service1, Service2, Service3 et Service4.</span><span class="sxs-lookup"><span data-stu-id="046c3-207">Let's say there are four services, Service1, Service2, Service3, and Service4.</span></span> 
- <span data-ttu-id="046c3-208">Service1 signale les mesures Metric1 et Metric2.</span><span class="sxs-lookup"><span data-stu-id="046c3-208">Service1 reports metrics Metric1 and Metric2.</span></span> 
- <span data-ttu-id="046c3-209">Service2 signale les mesures Metric2 et Metric3.</span><span class="sxs-lookup"><span data-stu-id="046c3-209">Service2 reports metrics Metric2 and Metric3.</span></span> 
- <span data-ttu-id="046c3-210">Service3 signale les mesures Metric3 et Metric4.</span><span class="sxs-lookup"><span data-stu-id="046c3-210">Service3 reports metrics Metric3 and Metric4.</span></span>
- <span data-ttu-id="046c3-211">Service4 signale la mesure Metric99.</span><span class="sxs-lookup"><span data-stu-id="046c3-211">Service4 reports metric Metric99.</span></span> 

<span data-ttu-id="046c3-212">Vous voyez certainement où je veux en venir : il s’agit d’une chaîne !</span><span class="sxs-lookup"><span data-stu-id="046c3-212">Surely you can see where we’re going here: There's a chain!</span></span> <span data-ttu-id="046c3-213">Nous n’avons pas vraiment quatre services indépendants, mais plutôt trois services qui sont liés et un qui est indépendant.</span><span class="sxs-lookup"><span data-stu-id="046c3-213">We don’t really have four independent services, we have three services that are related and one that is off on its own.</span></span>

<span data-ttu-id="046c3-214"><center>
Équilibrage de plusieurs services en même temps![][Image4]
</center></span><span class="sxs-lookup"><span data-stu-id="046c3-214"><center>
![Balancing Services Together][Image4]
</center></span></span>

<span data-ttu-id="046c3-215">En raison de cette chaîne, il est donc possible qu’un déséquilibre dans les mesures 1 à 4 provoque le déplacement de réplicas ou d’instances appartenant aux services 1 à 3.</span><span class="sxs-lookup"><span data-stu-id="046c3-215">Because of this chain, it's possible that an imbalance in metrics 1-4 can cause replicas or instances belonging to services 1-3 to move around.</span></span> <span data-ttu-id="046c3-216">Nous savons également qu’un déséquilibre de la mesure Metric1, Metric2 ou Metric3 ne peut pas provoquer de déplacements pour le service Service4.</span><span class="sxs-lookup"><span data-stu-id="046c3-216">We also know that an imbalance in Metrics 1, 2, or 3 can't cause movements in Service4.</span></span> <span data-ttu-id="046c3-217">Cela n’aurait aucun intérêt, puisque le déplacement de réplicas ou d’instances appartenant au service Service4 n’a pas la moindre incidence sur l’équilibre de la mesure Metric1, Metric2 ou Metric3.</span><span class="sxs-lookup"><span data-stu-id="046c3-217">There would be no point since moving the replicas or instances belonging to Service4 around can do absolutely nothing to impact the balance of Metrics 1-3.</span></span>

<span data-ttu-id="046c3-218">Cluster Resource Manager identifie automatiquement les services associés.</span><span class="sxs-lookup"><span data-stu-id="046c3-218">The Cluster Resource Manager automatically figures out what services are related.</span></span> <span data-ttu-id="046c3-219">Ajouter, supprimer ou modifier les mesures des services peut avoir un impact sur leurs relations.</span><span class="sxs-lookup"><span data-stu-id="046c3-219">Adding, removing, or changing the metrics for services can impact their relationships.</span></span> <span data-ttu-id="046c3-220">Par exemple, entre deux équilibrages, la mesure Metric2 peut avoir été mise à jour pour être supprimée de la configuration du service Service2.</span><span class="sxs-lookup"><span data-stu-id="046c3-220">For example, between two runs of balancing Service2 may have been updated to remove Metric2.</span></span> <span data-ttu-id="046c3-221">La chaîne entre Service1 et Service2 est alors rompue.</span><span class="sxs-lookup"><span data-stu-id="046c3-221">This breaks the chain between Service1 and Service2.</span></span> <span data-ttu-id="046c3-222">Au lieu de deux groupes de services liés, vous en avez à présent trois :</span><span class="sxs-lookup"><span data-stu-id="046c3-222">Now instead of two groups of related services, there are three:</span></span>

<span data-ttu-id="046c3-223"><center>
Équilibrage de plusieurs services en même temps![][Image5]
</center></span><span class="sxs-lookup"><span data-stu-id="046c3-223"><center>
![Balancing Services Together][Image5]
</center></span></span>

## <a name="next-steps"></a><span data-ttu-id="046c3-224">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="046c3-224">Next steps</span></span>
* <span data-ttu-id="046c3-225">Les mesures représentent la façon dont Service Fabric Cluster Resource Manager gère la consommation et la capacité du cluster.</span><span class="sxs-lookup"><span data-stu-id="046c3-225">Metrics are how the Service Fabric Cluster Resource Manger manages consumption and capacity in the cluster.</span></span> <span data-ttu-id="046c3-226">Pour en savoir plus sur ces mesures et la façon de les configurer, consultez [cet article](service-fabric-cluster-resource-manager-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="046c3-226">To learn more about metrics and how to configure them, check out [this article](service-fabric-cluster-resource-manager-metrics.md)</span></span>
* <span data-ttu-id="046c3-227">Le coût du mouvement est une façon de signaler à Cluster Resource Manager que certains services sont plus coûteux à déplacer que d’autres.</span><span class="sxs-lookup"><span data-stu-id="046c3-227">Movement Cost is one way of signaling to the Cluster Resource Manager that certain services are more expensive to move than others.</span></span> <span data-ttu-id="046c3-228">Pour plus d’informations sur le coût lié aux déplacements, reportez-vous à [cet article](service-fabric-cluster-resource-manager-movement-cost.md).</span><span class="sxs-lookup"><span data-stu-id="046c3-228">For more about movement cost, refer to [this article](service-fabric-cluster-resource-manager-movement-cost.md)</span></span>
* <span data-ttu-id="046c3-229">Cluster Resource Manager a plusieurs limitations que vous pouvez configurer pour ralentir l’évolution dans le cluster.</span><span class="sxs-lookup"><span data-stu-id="046c3-229">The Cluster Resource Manager has several throttles that you can configure to slow down churn in the cluster.</span></span> <span data-ttu-id="046c3-230">Elles ne sont normalement pas nécessaires mais, si vous en avez besoin, vous pouvez en savoir plus sur ces limitations [ici](service-fabric-cluster-resource-manager-advanced-throttling.md)</span><span class="sxs-lookup"><span data-stu-id="046c3-230">They're not normally necessary, but if you need them you can learn about them [here](service-fabric-cluster-resource-manager-advanced-throttling.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resrouce-manager-balancing-thresholds.png
[Image2]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-threshold-triggered-results.png
[Image3]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-activity-thresholds.png
[Image4]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together1.png
[Image5]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together2.png
