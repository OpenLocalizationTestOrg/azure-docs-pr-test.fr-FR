---
title: "Spécifier des mesures et des paramètres de positionnement dans les microservices Azure | Microsoft Docs"
description: "Description d’un service Service Fabric en spécifiant des mesures, des contraintes de positionnement et d’autres stratégies de positionnement."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 16e135c1-a00a-4c6f-9302-6651a090571a
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 807ae469e0555de542212532b829f464c9813598
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="configuring-cluster-resource-manager-settings-for-service-fabric-services"></a><span data-ttu-id="64d68-103">Configuration des paramètres Cluster Resource Manager pour les services Service Fabric</span><span class="sxs-lookup"><span data-stu-id="64d68-103">Configuring cluster resource manager settings for Service Fabric services</span></span>
<span data-ttu-id="64d68-104">Service Fabric Cluster Resource Manager assure un contrôle précis des règles qui régissent chaque service nommé individuel.</span><span class="sxs-lookup"><span data-stu-id="64d68-104">The Service Fabric Cluster Resource Manager allows fine-grained control over the rules that govern every individual named service.</span></span> <span data-ttu-id="64d68-105">Chaque service nommé peut spécifier des règles pour son allocation dans le cluster.</span><span class="sxs-lookup"><span data-stu-id="64d68-105">Each named service can specify rules for how it should be allocated in the cluster.</span></span> <span data-ttu-id="64d68-106">Chaque service nommé peut également définir l’ensemble de mesures à inclure dans ses rapports, notamment leur importance pour ce service.</span><span class="sxs-lookup"><span data-stu-id="64d68-106">Each named service can also define the set of metrics that it wants to report, including how important they are to that service.</span></span> <span data-ttu-id="64d68-107">La configuration des services se décompose en trois tâches :</span><span class="sxs-lookup"><span data-stu-id="64d68-107">Configuring services breaks down into three different tasks:</span></span>

1. <span data-ttu-id="64d68-108">Configuration des contraintes de positionnement</span><span class="sxs-lookup"><span data-stu-id="64d68-108">Configuring placement constraints</span></span>
2. <span data-ttu-id="64d68-109">Configuration des mesures</span><span class="sxs-lookup"><span data-stu-id="64d68-109">Configuring metrics</span></span>
3. <span data-ttu-id="64d68-110">Configuration des stratégies et des autres règles de positionnement avancées (moins fréquent)</span><span class="sxs-lookup"><span data-stu-id="64d68-110">Configuring advanced placement policies and other rules (less common)</span></span>

## <a name="placement-constraints"></a><span data-ttu-id="64d68-111">Contraintes de placement</span><span class="sxs-lookup"><span data-stu-id="64d68-111">Placement constraints</span></span>
<span data-ttu-id="64d68-112">Les contraintes de placement sont utilisées pour contrôler sur quels nœuds du cluster un service peut s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="64d68-112">Placement constraints are used to control which nodes in the cluster a service can actually run on.</span></span> <span data-ttu-id="64d68-113">En général, l’exécution d’une instance de service nommé spécifique ou de tous les services d’un type donné est limitée à un type de nœud particulier.</span><span class="sxs-lookup"><span data-stu-id="64d68-113">Typically a particular named service instance or all services of a given type constrained to run on a particular type of node.</span></span> <span data-ttu-id="64d68-114">Les contraintes de placement sont extensibles.</span><span class="sxs-lookup"><span data-stu-id="64d68-114">Placement constraints are extensible.</span></span> <span data-ttu-id="64d68-115">Vous pouvez définir n’importe quel jeu de propriétés par type de nœud, puis les sélectionner avec des contraintes lors de la création de services.</span><span class="sxs-lookup"><span data-stu-id="64d68-115">You can define any set of properties per  node type, and then select for them with constraints when creating services.</span></span> <span data-ttu-id="64d68-116">Vous pouvez également modifier les contraintes de placement d’un service en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="64d68-116">You can also change a service's placement constraints while it is running.</span></span> <span data-ttu-id="64d68-117">Cela vous permet de répondre aux modifications apportées dans le cluster ou aux exigences du service.</span><span class="sxs-lookup"><span data-stu-id="64d68-117">THis allows you to respond to changes in the cluster or the requirements of the service.</span></span> <span data-ttu-id="64d68-118">Les propriétés d’un nœud donné peuvent également être mises à jour dynamiquement dans le cluster.</span><span class="sxs-lookup"><span data-stu-id="64d68-118">The properties of a given node can also be updated dynamically in the cluster.</span></span> <span data-ttu-id="64d68-119">Vous trouverez plus d’informations sur les contraintes de placement et leur configuration dans [cet article](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints).</span><span class="sxs-lookup"><span data-stu-id="64d68-119">More information on placement constraints and how to configure them can be found in [this article](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints)</span></span>

## <a name="metrics"></a><span data-ttu-id="64d68-120">Mesures</span><span class="sxs-lookup"><span data-stu-id="64d68-120">Metrics</span></span>
<span data-ttu-id="64d68-121">Les mesures correspondent à l’ensemble de ressources dont un de service nommé a besoin.</span><span class="sxs-lookup"><span data-stu-id="64d68-121">Metrics are the set of resources that a given named service needs.</span></span> <span data-ttu-id="64d68-122">La configuration de mesures d’un service détermine notamment la quantité d’une ressource que chaque réplica avec état ou instance sans état de ce service consomme par défaut.</span><span class="sxs-lookup"><span data-stu-id="64d68-122">A service's metric configuration includes how much of that resource each stateful replica or stateless instance of that service consumes by default.</span></span> <span data-ttu-id="64d68-123">Les mesures comprennent également un poids qui indique l’importance de l’équilibrage de la mesure pour le service, dans le cas où un compromis est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="64d68-123">Metrics also include a weight that indicates how important balancing that metric is to that service, in case tradeoffs are necessary.</span></span>

## <a name="advanced-placement-rules"></a><span data-ttu-id="64d68-124">Règles de placement avancées</span><span class="sxs-lookup"><span data-stu-id="64d68-124">Advanced placement rules</span></span>
<span data-ttu-id="64d68-125">Il existe d’autres types de règles de placement qui sont utiles dans des scénarios moins courants.</span><span class="sxs-lookup"><span data-stu-id="64d68-125">There are other types of placement rules that are useful in less common scenarios.</span></span> <span data-ttu-id="64d68-126">Voici quelques exemples :</span><span class="sxs-lookup"><span data-stu-id="64d68-126">Some examples are:</span></span>
- <span data-ttu-id="64d68-127">Contraintes utiles avec des clusters dispersés géographiquement</span><span class="sxs-lookup"><span data-stu-id="64d68-127">Constraints that help with geographically distributed clusters</span></span>
- <span data-ttu-id="64d68-128">Certaines architectures d’application</span><span class="sxs-lookup"><span data-stu-id="64d68-128">Certain application architectures</span></span>

<span data-ttu-id="64d68-129">La configuration des autres règles de positionnement s’effectue via Corrélations ou Stratégies.</span><span class="sxs-lookup"><span data-stu-id="64d68-129">Other placement rules are configured via either Correlations or Policies.</span></span>

## <a name="next-steps"></a><span data-ttu-id="64d68-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="64d68-130">Next steps</span></span>
- <span data-ttu-id="64d68-131">Les mesures représentent la façon dont Service Fabric Cluster Resource Manager gère la consommation et la capacité du cluster.</span><span class="sxs-lookup"><span data-stu-id="64d68-131">Metrics are how the Service Fabric Cluster Resource Manger manages consumption and capacity in the cluster.</span></span> <span data-ttu-id="64d68-132">Pour en savoir plus sur ces mesures et la façon de les configurer, consultez [cet article](service-fabric-cluster-resource-manager-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="64d68-132">To learn more about metrics and how to configure them, check out [this article](service-fabric-cluster-resource-manager-metrics.md)</span></span>
- <span data-ttu-id="64d68-133">L’affinité est un mode que vous pouvez configurer pour vos services.</span><span class="sxs-lookup"><span data-stu-id="64d68-133">Affinity is one mode you can configure for your services.</span></span> <span data-ttu-id="64d68-134">Ce n’est pas courant, mais si nécessaire, vous trouverez plus d’informations [ici](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md)</span><span class="sxs-lookup"><span data-stu-id="64d68-134">It is not common, but if you need it you can learn about it [here](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md)</span></span>
- <span data-ttu-id="64d68-135">Il existe de nombreuses règles de positionnement différentes qui peuvent être configurées sur votre service pour gérer des scénarios supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="64d68-135">There are many different placement rules that can be configured on your service to handle additional scenarios.</span></span> <span data-ttu-id="64d68-136">Vous trouverez plus d’informations sur ces différentes stratégies de positionnement [ici](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md)</span><span class="sxs-lookup"><span data-stu-id="64d68-136">You can find out about those different placement policies [here](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md)</span></span>
- <span data-ttu-id="64d68-137">Commencer au début et [obtenir une présentation de Service Fabric Cluster Resource Manager](service-fabric-cluster-resource-manager-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="64d68-137">Start from the beginning and [get an Introduction to the Service Fabric Cluster Resource Manager](service-fabric-cluster-resource-manager-introduction.md)</span></span>
- <span data-ttu-id="64d68-138">Pour en savoir plus sur la façon dont Cluster Resource Manager gère et équilibre la charge du cluster, consultez l’article sur [l’équilibrage de la charge](service-fabric-cluster-resource-manager-balancing.md)</span><span class="sxs-lookup"><span data-stu-id="64d68-138">To find out about how the Cluster Resource Manager manages and balances load in the cluster, check out the article on [balancing load](service-fabric-cluster-resource-manager-balancing.md)</span></span>
- <span data-ttu-id="64d68-139">Cluster Resource Manager comporte de nombreuses options permettant de décrire le cluster.</span><span class="sxs-lookup"><span data-stu-id="64d68-139">The Cluster Resource Manager has many options for describing the cluster.</span></span> <span data-ttu-id="64d68-140">Pour en savoir plus sur celles-ci, consultez cet article sur la [description d’un cluster Service Fabric](service-fabric-cluster-resource-manager-cluster-description.md).</span><span class="sxs-lookup"><span data-stu-id="64d68-140">To find out more about them, check out this article on [describing a Service Fabric cluster](service-fabric-cluster-resource-manager-cluster-description.md)</span></span>