---
title: aaaBalance votre cluster Azure Service Fabric | Documents Microsoft
description: "Une présentation toobalancing votre cluster avec hello Gestionnaire de ressources du Cluster Service Fabric."
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
ms.openlocfilehash: 5f7ad2f5cf4cfb3751a860f5293b03d2d5266d99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="balancing-your-service-fabric-cluster"></a><span data-ttu-id="51eb6-103">Équilibrage de votre cluster Service Fabric</span><span class="sxs-lookup"><span data-stu-id="51eb6-103">Balancing your service fabric cluster</span></span>
<span data-ttu-id="51eb6-104">Hello, Gestionnaire de ressources du Cluster Service Fabric prend en charge les modifications de la charge dynamique, réaction tooadditions ou les suppressions de nœuds ou des services.</span><span class="sxs-lookup"><span data-stu-id="51eb6-104">hello Service Fabric Cluster Resource Manager supports dynamic load changes, reacting tooadditions or removals of nodes or services.</span></span> <span data-ttu-id="51eb6-105">Elle corrige également automatiquement les violations de contrainte et rééquilibrage de façon proactive les cluster hello.</span><span class="sxs-lookup"><span data-stu-id="51eb6-105">It also automatically corrects constraint violations, and proactively rebalances hello cluster.</span></span> <span data-ttu-id="51eb6-106">Mais à quelle fréquence ces actions sont-elles effectuées, et quel en est l’élément déclencheur ?</span><span class="sxs-lookup"><span data-stu-id="51eb6-106">But how often are these actions taken, and what triggers them?</span></span>

<span data-ttu-id="51eb6-107">Il existe trois différentes catégories de travail que hello effectue de gestionnaire de ressources du Cluster.</span><span class="sxs-lookup"><span data-stu-id="51eb6-107">There are three different categories of work that hello Cluster Resource Manager performs.</span></span> <span data-ttu-id="51eb6-108">Il s'agit de :</span><span class="sxs-lookup"><span data-stu-id="51eb6-108">They are:</span></span>

1. <span data-ttu-id="51eb6-109">Positionnement : cette étape a trait au placement des réplicas avec état ou des instances sans état manquants.</span><span class="sxs-lookup"><span data-stu-id="51eb6-109">Placement – this stage deals with placing any stateful replicas or stateless instances that are missing.</span></span> <span data-ttu-id="51eb6-110">Le positionnement inclut non seulement les nouveaux services, mais aussi les réplicas avec état ou les instances sans état qui ont échoué.</span><span class="sxs-lookup"><span data-stu-id="51eb6-110">Placement includes both new services and handling stateful replicas or stateless instances that have failed.</span></span> <span data-ttu-id="51eb6-111">La suppression et l’annulation des réplicas ou des instances sont gérées ici.</span><span class="sxs-lookup"><span data-stu-id="51eb6-111">Deleting and dropping replicas or instances are handled here.</span></span>
2. <span data-ttu-id="51eb6-112">Contrainte vérifie – cette étape vérifie et corrige les violations de contraintes de positionnement différents hello (règles) dans le système de hello.</span><span class="sxs-lookup"><span data-stu-id="51eb6-112">Constraint Checks – this stage checks for and corrects violations of hello different placement constraints (rules) within hello system.</span></span> <span data-ttu-id="51eb6-113">Le non-dépassement de la capacité des nœuds et le respect des contraintes de positionnement d’un service sont des exemples de règles.</span><span class="sxs-lookup"><span data-stu-id="51eb6-113">Examples of rules are things like ensuring that nodes are not over capacity and that a service’s placement constraints are met.</span></span>
3. <span data-ttu-id="51eb6-114">Équilibrage – cette étape vérifie toosee si rééquilibrage est nécessaire en fonction de hello configuré souhaité au niveau du solde pour les mesures de différents.</span><span class="sxs-lookup"><span data-stu-id="51eb6-114">Balancing – this stage checks toosee if rebalancing is necessary based on hello configured desired level of balance for different metrics.</span></span> <span data-ttu-id="51eb6-115">Cas dans ce, il tente toofind AGENCEMENT Bonjour de cluster qui est plus équilibrée.</span><span class="sxs-lookup"><span data-stu-id="51eb6-115">If so it attempts toofind an arrangement in hello cluster that is more balanced.</span></span>

## <a name="configuring-cluster-resource-manager-timers"></a><span data-ttu-id="51eb6-116">Configuration des minuteurs Cluster Resource Manager</span><span class="sxs-lookup"><span data-stu-id="51eb6-116">Configuring Cluster Resource Manager Timers</span></span>
<span data-ttu-id="51eb6-117">Hello premier ensemble de contrôles autour de l’équilibrage sont un ensemble d’événements d’horloge.</span><span class="sxs-lookup"><span data-stu-id="51eb6-117">hello first set of controls around balancing are a set of timers.</span></span> <span data-ttu-id="51eb6-118">Ces minuteries régissent la fréquence à laquelle hello Gestionnaire de ressources du Cluster examine le cluster de hello et effectue des actions correctives.</span><span class="sxs-lookup"><span data-stu-id="51eb6-118">These timers govern how often hello Cluster Resource Manager examines hello cluster and takes corrective actions.</span></span>

<span data-ttu-id="51eb6-119">Chacune de ces différents types de hello corrections Gestionnaire de ressources de Cluster peuvent rendre est contrôlé par un minuteur différent qui détermine sa fréquence.</span><span class="sxs-lookup"><span data-stu-id="51eb6-119">Each of these different types of corrections hello Cluster Resource Manager can make is controlled by a different timer that governs its frequency.</span></span> <span data-ttu-id="51eb6-120">Lorsque chaque se déclenche, la tâche hello est planifiée.</span><span class="sxs-lookup"><span data-stu-id="51eb6-120">When each timer fires, hello task is scheduled.</span></span> <span data-ttu-id="51eb6-121">Par défaut hello Gestionnaire de ressources :</span><span class="sxs-lookup"><span data-stu-id="51eb6-121">By default hello Resource Manager:</span></span>

* <span data-ttu-id="51eb6-122">analyse son état et applique des mises à jour (comme l’enregistrement de l’arrêt d’un nœud) tous les dixièmes de seconde ;</span><span class="sxs-lookup"><span data-stu-id="51eb6-122">scans its state and applies updates (like recording that a node is down) every 1/10th of a second</span></span>
* <span data-ttu-id="51eb6-123">définit l’indicateur de vérification de la sélection élective hello</span><span class="sxs-lookup"><span data-stu-id="51eb6-123">sets hello placement check flag</span></span> 
* <span data-ttu-id="51eb6-124">définit d’indicateur de vérification de contrainte hello par seconde</span><span class="sxs-lookup"><span data-stu-id="51eb6-124">sets hello constraint check flag every second</span></span>
* <span data-ttu-id="51eb6-125">définit hello équilibrage indicateur toutes les cinq secondes.</span><span class="sxs-lookup"><span data-stu-id="51eb6-125">sets hello balancing flag every five seconds.</span></span>

<span data-ttu-id="51eb6-126">Exemples de configuration hello régissant ces minuteries sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="51eb6-126">Examples of hello configuration governing these timers are below:</span></span>

<span data-ttu-id="51eb6-127">ClusterManifest.xml :</span><span class="sxs-lookup"><span data-stu-id="51eb6-127">ClusterManifest.xml:</span></span>

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="PLBRefreshGap" Value="0.1" />
            <Parameter Name="MinPlacementInterval" Value="1.0" />
            <Parameter Name="MinConstraintCheckInterval" Value="1.0" />
            <Parameter Name="MinLoadBalancingInterval" Value="5.0" />
        </Section>
```

<span data-ttu-id="51eb6-128">via ClusterConfig.json pour les déploiements autonomes ou Template.json pour les clusters hébergés sur Azure :</span><span class="sxs-lookup"><span data-stu-id="51eb6-128">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

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

<span data-ttu-id="51eb6-129">Aujourd'hui hello Gestionnaire de ressources de Cluster effectue uniquement une de ces actions à la fois, séquentiellement.</span><span class="sxs-lookup"><span data-stu-id="51eb6-129">Today hello Cluster Resource Manager only performs one of these actions at a time, sequentially.</span></span> <span data-ttu-id="51eb6-130">C’est pourquoi nous font référence les minuteurs toothese en tant que « intervalles minimaux » et hello actions obtient effectuées lorsque les minuteurs hello se déclencher en tant que « définition des indicateurs ».</span><span class="sxs-lookup"><span data-stu-id="51eb6-130">This is why we refer toothese timers as “minimum intervals” and hello actions that get taken when hello timers go off as "setting flags".</span></span> <span data-ttu-id="51eb6-131">Par exemple, Gestionnaire de ressources de Cluster prend en charge en attente de hello demande des services de toocreate avant hello cluster d’équilibrage.</span><span class="sxs-lookup"><span data-stu-id="51eb6-131">For example, hello Cluster Resource Manager takes care of pending requests toocreate services before balancing hello cluster.</span></span> <span data-ttu-id="51eb6-132">Comme vous pouvez le voir par intervalles de temps par défaut hello spécifiés, hello Gestionnaire de ressources du Cluster de l’analyse pour tout élément besoins toodo fréquemment.</span><span class="sxs-lookup"><span data-stu-id="51eb6-132">As you can see by hello default time intervals specified, hello Cluster Resource Manager scans for anything it needs toodo frequently.</span></span> <span data-ttu-id="51eb6-133">Normalement, cela signifie que le jeu hello des modifications apportées à chaque étape est petite.</span><span class="sxs-lookup"><span data-stu-id="51eb6-133">Normally this means that hello set of changes made during each step is small.</span></span> <span data-ttu-id="51eb6-134">Apporter de petites modifications fréquemment permet hello toobe du Gestionnaire de ressources du Cluster réactif lorsque les événements se produisent dans le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="51eb6-134">Making small changes frequently allows hello Cluster Resource Manager toobe responsive when things happen in hello cluster.</span></span> <span data-ttu-id="51eb6-135">Hello minuteries de valeur par défaut fournissent certains le traitement par lot, car de nombreux hello même les types d’événements ont tendance toooccur simultanément.</span><span class="sxs-lookup"><span data-stu-id="51eb6-135">hello default timers provide some batching since many of hello same types of events tend toooccur simultaneously.</span></span> 

<span data-ttu-id="51eb6-136">Par exemple, lorsque des nœuds échouent, ils se produisent simultanément dans des domaines d’erreur entiers.</span><span class="sxs-lookup"><span data-stu-id="51eb6-136">For example, when nodes fail they can do so entire fault domains at a time.</span></span> <span data-ttu-id="51eb6-137">Ces échecs sont capturées au cours de l’état suivant de hello de mise à jour après hello *PLBRefreshGap*.</span><span class="sxs-lookup"><span data-stu-id="51eb6-137">All these failures are captured during hello next state update after hello *PLBRefreshGap*.</span></span> <span data-ttu-id="51eb6-138">corrections de Hello sont déterminées pendant hello après la sélection élective, vérification de contrainte et équilibrage s’exécute.</span><span class="sxs-lookup"><span data-stu-id="51eb6-138">hello corrections are determined during hello following placement, constraint check, and balancing runs.</span></span> <span data-ttu-id="51eb6-139">Par hello de valeur par défaut Gestionnaire de ressources du Cluster n’est pas analysant les heures des modifications dans un cluster de hello et la tentative de tooaddress toutes les modifications apportées à la fois.</span><span class="sxs-lookup"><span data-stu-id="51eb6-139">By default hello Cluster Resource Manager is not scanning through hours of changes in hello cluster and trying tooaddress all changes at once.</span></span> <span data-ttu-id="51eb6-140">Cela entraînerait toobursts d’évolution.</span><span class="sxs-lookup"><span data-stu-id="51eb6-140">Doing so would lead toobursts of churn.</span></span>

<span data-ttu-id="51eb6-141">Hello, Gestionnaire de ressources du Cluster doit également certaines toodetermine des informations supplémentaires si hello cluster déséquilibré.</span><span class="sxs-lookup"><span data-stu-id="51eb6-141">hello Cluster Resource Manager also needs some additional information toodetermine if hello cluster imbalanced.</span></span> <span data-ttu-id="51eb6-142">Nous disposons pour cela de deux autres éléments de configuration : *BalancingThresholds* et *ActivityThresholds*.</span><span class="sxs-lookup"><span data-stu-id="51eb6-142">For that we have two other pieces of configuration: *BalancingThresholds* and *ActivityThresholds*.</span></span>

## <a name="balancing-thresholds"></a><span data-ttu-id="51eb6-143">Seuils d’équilibrage</span><span class="sxs-lookup"><span data-stu-id="51eb6-143">Balancing thresholds</span></span>
<span data-ttu-id="51eb6-144">Un seuil d’équilibrage est contrôle principal de hello pour déclencher le rééquilibrage.</span><span class="sxs-lookup"><span data-stu-id="51eb6-144">A Balancing Threshold is hello main control for triggering rebalancing.</span></span> <span data-ttu-id="51eb6-145">Bonjour équilibrage de seuil pour une métrique est un _ratio_.</span><span class="sxs-lookup"><span data-stu-id="51eb6-145">hello Balancing Threshold for a metric is a _ratio_.</span></span> <span data-ttu-id="51eb6-146">Si charge hello pour une métrique de hello chargé plus divisé par quantité hello hello moins chargé de la charge de nœud nœud dépasse cette métrique *BalancingThreshold*, puis le cluster de hello est déséquilibré.</span><span class="sxs-lookup"><span data-stu-id="51eb6-146">If hello load for a metric on hello most loaded node divided by hello amount of load on hello least loaded node exceeds that metric's *BalancingThreshold*, then hello cluster is imbalanced.</span></span> <span data-ttu-id="51eb6-147">Équilibrage de charge ainsi est suivant hello de temps hello déclenchées vérifie du Gestionnaire de ressources du Cluster.</span><span class="sxs-lookup"><span data-stu-id="51eb6-147">As a result balancing is triggered hello next time hello Cluster Resource Manager checks.</span></span> <span data-ttu-id="51eb6-148">Hello *MinLoadBalancingInterval* minuteur définit la fréquence à laquelle hello Gestionnaire de ressources du Cluster doit vérifier s’il est nécessaire de rééquilibrage.</span><span class="sxs-lookup"><span data-stu-id="51eb6-148">hello *MinLoadBalancingInterval* timer defines how often hello Cluster Resource Manager should check if rebalancing is necessary.</span></span> <span data-ttu-id="51eb6-149">Cette vérification ne signifie pas que quelque chose se produit.</span><span class="sxs-lookup"><span data-stu-id="51eb6-149">Checking doesn't mean that anything happens.</span></span> 

<span data-ttu-id="51eb6-150">Équilibrage des seuils sont définis sur une base par métrique dans le cadre de la définition de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="51eb6-150">Balancing Thresholds are defined on a per-metric basis as a part of hello cluster definition.</span></span> <span data-ttu-id="51eb6-151">Pour plus d’informations sur les mesures, consultez [cet article](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="51eb6-151">For more information on metrics, check out [this article](service-fabric-cluster-resource-manager-metrics.md).</span></span>

<span data-ttu-id="51eb6-152">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="51eb6-152">ClusterManifest.xml</span></span>

```xml
    <Section Name="MetricBalancingThresholds">
      <Parameter Name="MetricName1" Value="2"/>
      <Parameter Name="MetricName2" Value="3.5"/>
    </Section>
```

<span data-ttu-id="51eb6-153">via ClusterConfig.json pour les déploiements autonomes ou Template.json pour les clusters hébergés sur Azure :</span><span class="sxs-lookup"><span data-stu-id="51eb6-153">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

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

<span data-ttu-id="51eb6-154"><center>
Exemple de seuil d’équilibrage![][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="51eb6-154"><center>
![Balancing Threshold Example][Image1]
</center></span></span>

<span data-ttu-id="51eb6-155">Dans cet exemple, chaque service utilise une unité d’une mesure donnée.</span><span class="sxs-lookup"><span data-stu-id="51eb6-155">In this example, each service is consuming one unit of some metric.</span></span> <span data-ttu-id="51eb6-156">Dans hello exemple supérieur, hello maximale de la charge sur un nœud est de cinq et minimum de hello est deux.</span><span class="sxs-lookup"><span data-stu-id="51eb6-156">In hello top example, hello maximum load on a node is five and hello minimum is two.</span></span> <span data-ttu-id="51eb6-157">Supposons que hello équilibrage seuil pour cette métrique est de trois.</span><span class="sxs-lookup"><span data-stu-id="51eb6-157">Let’s say that hello balancing threshold for this metric is three.</span></span> <span data-ttu-id="51eb6-158">Étant donné que le ratio hello dans un cluster de hello est 5/2 = 2.5 et qu’il est inférieure à celle spécifiée de hello équilibrage du seuil de trois, cluster de hello est équilibrée.</span><span class="sxs-lookup"><span data-stu-id="51eb6-158">Since hello ratio in hello cluster is 5/2 = 2.5 and that is less than hello specified balancing threshold of three, hello cluster is balanced.</span></span> <span data-ttu-id="51eb6-159">Aucun équilibrage n’est déclenchée lorsque hello Gestionnaire de ressources du Cluster vérifie.</span><span class="sxs-lookup"><span data-stu-id="51eb6-159">No balancing is triggered when hello Cluster Resource Manager checks.</span></span>

<span data-ttu-id="51eb6-160">Dans l’exemple hello du bas, charge maximale de hello sur un nœud est 10, alors que le minimum de hello est de deux, ce qui entraîne un ratio de cinq.</span><span class="sxs-lookup"><span data-stu-id="51eb6-160">In hello bottom example, hello maximum load on a node is 10, while hello minimum is two, resulting in a ratio of five.</span></span> <span data-ttu-id="51eb6-161">Cinq est supérieure au seuil de contrepartie désigné hello de trois pour cette métrique.</span><span class="sxs-lookup"><span data-stu-id="51eb6-161">Five is greater than hello designated balancing threshold of three for that metric.</span></span> <span data-ttu-id="51eb6-162">Par conséquent, une série de rééquilibrage sera planifiée hello temps suivant, l’équilibrage de minuteur se déclenche.</span><span class="sxs-lookup"><span data-stu-id="51eb6-162">As a result, a rebalancing run will be scheduled next time hello balancing timer fires.</span></span> <span data-ttu-id="51eb6-163">Dans une telle situation, une charge est généralement distribuées tooNode3.</span><span class="sxs-lookup"><span data-stu-id="51eb6-163">In a situation like this some load is usually distributed tooNode3.</span></span> <span data-ttu-id="51eb6-164">Étant donné que hello Gestionnaire de ressources du Cluster Service Fabric n’utilise pas une approche gourmande, une charge peut également être tooNode2 distribuée.</span><span class="sxs-lookup"><span data-stu-id="51eb6-164">Because hello Service Fabric Cluster Resource Manager doesn't use a greedy approach, some load could also be distributed tooNode2.</span></span> 

<span data-ttu-id="51eb6-165"><center>
Actions de l’exemple de seuil d’équilibrage![][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="51eb6-165"><center>
![Balancing Threshold Example Actions][Image2]
</center></span></span>

> [!NOTE]
> <span data-ttu-id="51eb6-166">« L’équilibrage » adopte deux stratégies différentes pour gérer la charge de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="51eb6-166">"Balancing" handles two different strategies for managing load in your cluster.</span></span> <span data-ttu-id="51eb6-167">stratégie par défaut Hello hello utilisations du Gestionnaire de ressources du Cluster est toodistribute charge sur les nœuds hello dans un cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="51eb6-167">hello default strategy that hello Cluster Resource Manager uses is toodistribute load across hello nodes in hello cluster.</span></span> <span data-ttu-id="51eb6-168">Hello autre stratégie est [défragmentation](service-fabric-cluster-resource-manager-defragmentation-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="51eb6-168">hello other strategy is [defragmentation](service-fabric-cluster-resource-manager-defragmentation-metrics.md).</span></span> <span data-ttu-id="51eb6-169">La défragmentation s’effectue pendant hello équilibrage de la même exécution.</span><span class="sxs-lookup"><span data-stu-id="51eb6-169">Defragmentation is performed during hello same balancing run.</span></span> <span data-ttu-id="51eb6-170">Hello défragmentation et équilibrage des stratégies peuvent être utilisés pour des mesures différentes dans hello même cluster.</span><span class="sxs-lookup"><span data-stu-id="51eb6-170">hello balancing and defragmentation strategies can be used for different metrics within hello same cluster.</span></span> <span data-ttu-id="51eb6-171">Un service peut avoir à la fois des mesures d’équilibrage et de défragmentation.</span><span class="sxs-lookup"><span data-stu-id="51eb6-171">A service can have both balancing and defragmentation metrics.</span></span> <span data-ttu-id="51eb6-172">Pour les métriques de défragmentation, rapport hello hello charge dans les déclencheurs de cluster hello rééquilibrage lorsqu’il est _ci-dessous_ hello équilibrage du seuil.</span><span class="sxs-lookup"><span data-stu-id="51eb6-172">For defragmentation metrics, hello ratio of hello loads in hello cluster triggers rebalancing when it is _below_ hello balancing threshold.</span></span> 
>

<span data-ttu-id="51eb6-173">Mise en route ci-dessous hello équilibrage seuil n’est pas un objectif explicit.</span><span class="sxs-lookup"><span data-stu-id="51eb6-173">Getting below hello balancing threshold is not an explicit goal.</span></span> <span data-ttu-id="51eb6-174">Les seuils d’équilibrage ne sont qu’un *déclencheur*.</span><span class="sxs-lookup"><span data-stu-id="51eb6-174">Balancing Thresholds are just a *trigger*.</span></span> <span data-ttu-id="51eb6-175">Lors de l’équilibrage de charge s’exécute hello Gestionnaire de ressources de Cluster détermine quelles améliorations possibles, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="51eb6-175">When balancing runs, hello Cluster Resource Manager determines what improvements it can make, if any.</span></span> <span data-ttu-id="51eb6-176">Une analyse d’équilibrage ne signifie pas que des données sont déplacées.</span><span class="sxs-lookup"><span data-stu-id="51eb6-176">Just because a balancing search is kicked off doesn't mean anything moves.</span></span> <span data-ttu-id="51eb6-177">Hello cluster est parfois toocorrect déséquilibré mais trop limitée.</span><span class="sxs-lookup"><span data-stu-id="51eb6-177">Sometimes hello cluster is imbalanced but too constrained toocorrect.</span></span> <span data-ttu-id="51eb6-178">Vous pouvez également les améliorations de hello requièrent les mouvements sont trop [coûteux](service-fabric-cluster-resource-manager-movement-cost.md)).</span><span class="sxs-lookup"><span data-stu-id="51eb6-178">Alternatively, hello improvements require movements that are too [costly](service-fabric-cluster-resource-manager-movement-cost.md)).</span></span>

## <a name="activity-thresholds"></a><span data-ttu-id="51eb6-179">seuils d’activité</span><span class="sxs-lookup"><span data-stu-id="51eb6-179">Activity thresholds</span></span>
<span data-ttu-id="51eb6-180">Dans certains cas, bien que les nœuds sont relativement déséquilibrés, hello *total* de charge dans le cluster de hello est faible.</span><span class="sxs-lookup"><span data-stu-id="51eb6-180">Sometimes, although nodes are relatively imbalanced, hello *total* amount of load in hello cluster is low.</span></span> <span data-ttu-id="51eb6-181">manque de Hello de charge peut être une adresse dip temporaire ou parce que le cluster de hello est nouveau et uniquement lors de l’obtention amorcé.</span><span class="sxs-lookup"><span data-stu-id="51eb6-181">hello lack of load could be a transient dip, or because hello cluster is new and just getting bootstrapped.</span></span> <span data-ttu-id="51eb6-182">Dans les deux cas, vous souhaiterez pas temps toospend équilibrage de cluster de hello, car il est peu toobe acquise.</span><span class="sxs-lookup"><span data-stu-id="51eb6-182">In either case, you may not want toospend time balancing hello cluster because there’s little toobe gained.</span></span> <span data-ttu-id="51eb6-183">Si le cluster de hello avoir subi l’équilibrage de vous consacrer réseau et éléments toomove ressources de calcul sans apporter tout grand *absolu* différence.</span><span class="sxs-lookup"><span data-stu-id="51eb6-183">If hello cluster underwent balancing, you’d spend network and compute resources toomove things around without making any large *absolute* difference.</span></span> <span data-ttu-id="51eb6-184">tooavoid inutile se déplace, il existe un autre contrôle appelé seuils d’activité.</span><span class="sxs-lookup"><span data-stu-id="51eb6-184">tooavoid unnecessary moves, there’s another control known as Activity Thresholds.</span></span> <span data-ttu-id="51eb6-185">Seuils d’activité vous permet de toospecify limite de certaines inférieure absolue pour l’activité.</span><span class="sxs-lookup"><span data-stu-id="51eb6-185">Activity Thresholds allows you toospecify some absolute lower bound for activity.</span></span> <span data-ttu-id="51eb6-186">Si aucun nœud ne se trouve sur ce seuil, l’équilibrage n’est pas déclenché même si hello équilibrage seuil est atteint.</span><span class="sxs-lookup"><span data-stu-id="51eb6-186">If no node is over this threshold, balancing isn't triggered even if hello Balancing Threshold is met.</span></span>

<span data-ttu-id="51eb6-187">Supposons que nous conservons notre seuil d’équilibrage de 3 pour cette mesure.</span><span class="sxs-lookup"><span data-stu-id="51eb6-187">Let’s say that we retain our Balancing Threshold of three for this metric.</span></span> <span data-ttu-id="51eb6-188">Supposons également que nous avons un seuil d’activité de 1 536.</span><span class="sxs-lookup"><span data-stu-id="51eb6-188">Let's also say we have an Activity Threshold of 1536.</span></span> <span data-ttu-id="51eb6-189">Dans le premier cas de hello, alors que le cluster de hello est déséquilibré par hello il seuil d’équilibrage n’est aucun répond aux nœuds de ce seuil d’activité, donc rien se produit.</span><span class="sxs-lookup"><span data-stu-id="51eb6-189">In hello first case, while hello cluster is imbalanced per hello Balancing Threshold there's no node meets that Activity Threshold, so nothing happens.</span></span> <span data-ttu-id="51eb6-190">Dans l’exemple hello du bas, Node1 se sur hello seuil de l’activité.</span><span class="sxs-lookup"><span data-stu-id="51eb6-190">In hello bottom example, Node1 is over hello Activity Threshold.</span></span> <span data-ttu-id="51eb6-191">Étant donné que deux hello seuil d’équilibrage et hello seuil de l’activité de mesure de hello sont atteints, l’équilibrage est planifié.</span><span class="sxs-lookup"><span data-stu-id="51eb6-191">Since both hello Balancing Threshold and hello Activity Threshold for hello metric are exceeded, balancing is scheduled.</span></span> <span data-ttu-id="51eb6-192">Par exemple, examinons hello suivant schéma :</span><span class="sxs-lookup"><span data-stu-id="51eb6-192">As an example, let's look at hello following diagram:</span></span> 

<span data-ttu-id="51eb6-193"><center>
Exemple de seuil d’activité![][Image3]
</center></span><span class="sxs-lookup"><span data-stu-id="51eb6-193"><center>
![Activity Threshold Example][Image3]
</center></span></span>

<span data-ttu-id="51eb6-194">Tout comme l’équilibrage des seuils, des seuils d’activité sont définies par le système métrique via la définition de cluster hello :</span><span class="sxs-lookup"><span data-stu-id="51eb6-194">Just like Balancing Thresholds, Activity Thresholds are defined per-metric via hello cluster definition:</span></span>

<span data-ttu-id="51eb6-195">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="51eb6-195">ClusterManifest.xml</span></span>

``` xml
    <Section Name="MetricActivityThresholds">
      <Parameter Name="Memory" Value="1536"/>
    </Section>
```

<span data-ttu-id="51eb6-196">via ClusterConfig.json pour les déploiements autonomes ou Template.json pour les clusters hébergés sur Azure :</span><span class="sxs-lookup"><span data-stu-id="51eb6-196">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

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

<span data-ttu-id="51eb6-197">Seuils d’équilibrage et activité sont tous deux métrique spécifique de tooa liée - équilibrage est déclenchée uniquement si les deux hello seuil d’équilibrage et activité seuil est dépassée pour hello même mesure.</span><span class="sxs-lookup"><span data-stu-id="51eb6-197">Balancing and activity thresholds are both tied tooa specific metric - balancing is triggered only if both hello Balancing Threshold and Activity Threshold is exceeded for hello same metric.</span></span>

## <a name="balancing-services-together"></a><span data-ttu-id="51eb6-198">Équilibrage de plusieurs services en même temps</span><span class="sxs-lookup"><span data-stu-id="51eb6-198">Balancing services together</span></span>
<span data-ttu-id="51eb6-199">Si le cluster de hello est déséquilibré ou non est une décision à l’échelle du cluster.</span><span class="sxs-lookup"><span data-stu-id="51eb6-199">Whether hello cluster is imbalanced or not is a cluster-wide decision.</span></span> <span data-ttu-id="51eb6-200">Toutefois, moyen hello nous allez résoudre est le déplacement des réplicas de service individuels et les instances autour.</span><span class="sxs-lookup"><span data-stu-id="51eb6-200">However, hello way we go about fixing it is moving individual service replicas and instances around.</span></span> <span data-ttu-id="51eb6-201">Logique, n’est-ce pas ?</span><span class="sxs-lookup"><span data-stu-id="51eb6-201">This makes sense, right?</span></span> <span data-ttu-id="51eb6-202">Si la mémoire est empilée sur un nœud, plusieurs réplicas ou les instances pourraient être cause tooit.</span><span class="sxs-lookup"><span data-stu-id="51eb6-202">If memory is stacked up on one node, multiple replicas or instances could be contributing tooit.</span></span> <span data-ttu-id="51eb6-203">Déséquilibre de la correction hello peut nécessiter de déplacer les réplicas avec état de hello ou des instances sans état qui utilisent la métrique de déséquilibré hello.</span><span class="sxs-lookup"><span data-stu-id="51eb6-203">Fixing hello imbalance could require moving any of hello stateful replicas or stateless instances that use hello imbalanced metric.</span></span>

<span data-ttu-id="51eb6-204">À l’occasion Cependant, un service qui n’a pas été déséquilibré lui-même est déplacé (n’oubliez pas de discussion hello local et global des poids plus haut).</span><span class="sxs-lookup"><span data-stu-id="51eb6-204">Occasionally though, a service that wasn’t itself imbalanced gets moved (remember hello discussion of local and global weights earlier).</span></span> <span data-ttu-id="51eb6-205">Pourquoi un service serait-il déplacé si toutes les mesures de ce service ont été équilibrées ?</span><span class="sxs-lookup"><span data-stu-id="51eb6-205">Why would a service get moved when all that service’s metrics were balanced?</span></span> <span data-ttu-id="51eb6-206">Examinons un exemple :</span><span class="sxs-lookup"><span data-stu-id="51eb6-206">Let’s see an example:</span></span>

- <span data-ttu-id="51eb6-207">Prenons par exemple quatre services : Service1, Service2, Service3 et Service4.</span><span class="sxs-lookup"><span data-stu-id="51eb6-207">Let's say there are four services, Service1, Service2, Service3, and Service4.</span></span> 
- <span data-ttu-id="51eb6-208">Service1 signale les mesures Metric1 et Metric2.</span><span class="sxs-lookup"><span data-stu-id="51eb6-208">Service1 reports metrics Metric1 and Metric2.</span></span> 
- <span data-ttu-id="51eb6-209">Service2 signale les mesures Metric2 et Metric3.</span><span class="sxs-lookup"><span data-stu-id="51eb6-209">Service2 reports metrics Metric2 and Metric3.</span></span> 
- <span data-ttu-id="51eb6-210">Service3 signale les mesures Metric3 et Metric4.</span><span class="sxs-lookup"><span data-stu-id="51eb6-210">Service3 reports metrics Metric3 and Metric4.</span></span>
- <span data-ttu-id="51eb6-211">Service4 signale la mesure Metric99.</span><span class="sxs-lookup"><span data-stu-id="51eb6-211">Service4 reports metric Metric99.</span></span> 

<span data-ttu-id="51eb6-212">Vous voyez certainement où je veux en venir : il s’agit d’une chaîne !</span><span class="sxs-lookup"><span data-stu-id="51eb6-212">Surely you can see where we’re going here: There's a chain!</span></span> <span data-ttu-id="51eb6-213">Nous n’avons pas vraiment quatre services indépendants, mais plutôt trois services qui sont liés et un qui est indépendant.</span><span class="sxs-lookup"><span data-stu-id="51eb6-213">We don’t really have four independent services, we have three services that are related and one that is off on its own.</span></span>

<span data-ttu-id="51eb6-214"><center>
![Équilibrage de plusieurs services en même temps][Image4]
</center></span><span class="sxs-lookup"><span data-stu-id="51eb6-214"><center>
![Balancing Services Together][Image4]
</center></span></span>

<span data-ttu-id="51eb6-215">En raison de cette chaîne, il est possible qu’un déséquilibre de métriques de 1 à 4 peut provoquer des réplicas ou instances appartenant tooservices toomove 1-3 autour.</span><span class="sxs-lookup"><span data-stu-id="51eb6-215">Because of this chain, it's possible that an imbalance in metrics 1-4 can cause replicas or instances belonging tooservices 1-3 toomove around.</span></span> <span data-ttu-id="51eb6-216">Nous savons également qu’un déséquilibre de la mesure Metric1, Metric2 ou Metric3 ne peut pas provoquer de déplacements pour le service Service4.</span><span class="sxs-lookup"><span data-stu-id="51eb6-216">We also know that an imbalance in Metrics 1, 2, or 3 can't cause movements in Service4.</span></span> <span data-ttu-id="51eb6-217">Il serait absurde depuis le déplacement de réplicas de hello ou instances appartenant tooService4 autour peut faire rien tooimpact hello équilibre entre les mesures de 1 à 3.</span><span class="sxs-lookup"><span data-stu-id="51eb6-217">There would be no point since moving hello replicas or instances belonging tooService4 around can do absolutely nothing tooimpact hello balance of Metrics 1-3.</span></span>

<span data-ttu-id="51eb6-218">Hello, Gestionnaire de ressources de Cluster effectue automatiquement les services associés.</span><span class="sxs-lookup"><span data-stu-id="51eb6-218">hello Cluster Resource Manager automatically figures out what services are related.</span></span> <span data-ttu-id="51eb6-219">Ajout, suppression ou modification de métriques hello pour les services peuvent avoir un impact sur leurs relations.</span><span class="sxs-lookup"><span data-stu-id="51eb6-219">Adding, removing, or changing hello metrics for services can impact their relationships.</span></span> <span data-ttu-id="51eb6-220">Par exemple, entre deux exécutions de l’équilibrage de Service2 a peut-être été mis à jour tooremove Metric2.</span><span class="sxs-lookup"><span data-stu-id="51eb6-220">For example, between two runs of balancing Service2 may have been updated tooremove Metric2.</span></span> <span data-ttu-id="51eb6-221">Cela arrête la chaîne hello entre Service1 et Service2.</span><span class="sxs-lookup"><span data-stu-id="51eb6-221">This breaks hello chain between Service1 and Service2.</span></span> <span data-ttu-id="51eb6-222">Au lieu de deux groupes de services liés, vous en avez à présent trois :</span><span class="sxs-lookup"><span data-stu-id="51eb6-222">Now instead of two groups of related services, there are three:</span></span>

<span data-ttu-id="51eb6-223"><center>
![Équilibrage de plusieurs services en même temps][Image5]
</center></span><span class="sxs-lookup"><span data-stu-id="51eb6-223"><center>
![Balancing Services Together][Image5]
</center></span></span>

## <a name="next-steps"></a><span data-ttu-id="51eb6-224">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="51eb6-224">Next steps</span></span>
* <span data-ttu-id="51eb6-225">Les métriques sont comment hello Gestionnaire de ressources du Cluster Service Fabric gère la consommation et la capacité en cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="51eb6-225">Metrics are how hello Service Fabric Cluster Resource Manger manages consumption and capacity in hello cluster.</span></span> <span data-ttu-id="51eb6-226">toolearn plus d’informations sur les métriques et comment tooconfigure, extraire [cet article](service-fabric-cluster-resource-manager-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="51eb6-226">toolearn more about metrics and how tooconfigure them, check out [this article](service-fabric-cluster-resource-manager-metrics.md)</span></span>
* <span data-ttu-id="51eb6-227">Le coût du mouvement constitue une méthode de signalisation toohello Gestionnaire de ressources de Cluster que certains services sont toomove plus coûteuse que d’autres.</span><span class="sxs-lookup"><span data-stu-id="51eb6-227">Movement Cost is one way of signaling toohello Cluster Resource Manager that certain services are more expensive toomove than others.</span></span> <span data-ttu-id="51eb6-228">Pour plus d’informations sur le coût du mouvement, consultez trop[cet article](service-fabric-cluster-resource-manager-movement-cost.md)</span><span class="sxs-lookup"><span data-stu-id="51eb6-228">For more about movement cost, refer too[this article](service-fabric-cluster-resource-manager-movement-cost.md)</span></span>
* <span data-ttu-id="51eb6-229">Hello, Gestionnaire de ressources du Cluster a plusieurs limitations que vous pouvez configurer tooslow vers le bas de l’évolution du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="51eb6-229">hello Cluster Resource Manager has several throttles that you can configure tooslow down churn in hello cluster.</span></span> <span data-ttu-id="51eb6-230">Elles ne sont normalement pas nécessaires mais, si vous en avez besoin, vous pouvez en savoir plus sur ces limitations [ici](service-fabric-cluster-resource-manager-advanced-throttling.md)</span><span class="sxs-lookup"><span data-stu-id="51eb6-230">They're not normally necessary, but if you need them you can learn about them [here](service-fabric-cluster-resource-manager-advanced-throttling.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resrouce-manager-balancing-thresholds.png
[Image2]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-threshold-triggered-results.png
[Image3]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-activity-thresholds.png
[Image4]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together1.png
[Image5]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together2.png
