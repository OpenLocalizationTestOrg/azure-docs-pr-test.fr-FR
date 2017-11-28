---
title: "paramètres de métriques et la sélection élective aaaSpecify dans Azure microservices | Documents Microsoft"
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
ms.openlocfilehash: c633518b5dbf0c7b84e0d46c06bf1f92365d184d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-cluster-resource-manager-settings-for-service-fabric-services"></a><span data-ttu-id="88cbb-103">Configuration des paramètres Cluster Resource Manager pour les services Service Fabric</span><span class="sxs-lookup"><span data-stu-id="88cbb-103">Configuring cluster resource manager settings for Service Fabric services</span></span>
<span data-ttu-id="88cbb-104">Hello, Gestionnaire de ressources du Cluster Service Fabric permet un contrôle affiné sur les règles hello qui régissent chaque personne désignée de service.</span><span class="sxs-lookup"><span data-stu-id="88cbb-104">hello Service Fabric Cluster Resource Manager allows fine-grained control over hello rules that govern every individual named service.</span></span> <span data-ttu-id="88cbb-105">Chaque service nommé peut spécifier des règles de la façon dont il doit être allouée dans le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="88cbb-105">Each named service can specify rules for how it should be allocated in hello cluster.</span></span> <span data-ttu-id="88cbb-106">Chaque service nommé peut également définir hello métriques qu’elles souhaitent tooreport, y compris la façon dont ils sont importants toothat service.</span><span class="sxs-lookup"><span data-stu-id="88cbb-106">Each named service can also define hello set of metrics that it wants tooreport, including how important they are toothat service.</span></span> <span data-ttu-id="88cbb-107">La configuration des services se décompose en trois tâches :</span><span class="sxs-lookup"><span data-stu-id="88cbb-107">Configuring services breaks down into three different tasks:</span></span>

1. <span data-ttu-id="88cbb-108">Configuration des contraintes de positionnement</span><span class="sxs-lookup"><span data-stu-id="88cbb-108">Configuring placement constraints</span></span>
2. <span data-ttu-id="88cbb-109">Configuration des mesures</span><span class="sxs-lookup"><span data-stu-id="88cbb-109">Configuring metrics</span></span>
3. <span data-ttu-id="88cbb-110">Configuration des stratégies et des autres règles de positionnement avancées (moins fréquent)</span><span class="sxs-lookup"><span data-stu-id="88cbb-110">Configuring advanced placement policies and other rules (less common)</span></span>

## <a name="placement-constraints"></a><span data-ttu-id="88cbb-111">Contraintes de placement</span><span class="sxs-lookup"><span data-stu-id="88cbb-111">Placement constraints</span></span>
<span data-ttu-id="88cbb-112">Contraintes de placement sont toocontrol utilisé les nœuds de cluster de hello un service peut s’exécuter sur.</span><span class="sxs-lookup"><span data-stu-id="88cbb-112">Placement constraints are used toocontrol which nodes in hello cluster a service can actually run on.</span></span> <span data-ttu-id="88cbb-113">Généralement, un particulier nommé l’instance de service ou de tous les services d’un toorun de la contrainte de type donné sur un type de nœud particulier.</span><span class="sxs-lookup"><span data-stu-id="88cbb-113">Typically a particular named service instance or all services of a given type constrained toorun on a particular type of node.</span></span> <span data-ttu-id="88cbb-114">Les contraintes de placement sont extensibles.</span><span class="sxs-lookup"><span data-stu-id="88cbb-114">Placement constraints are extensible.</span></span> <span data-ttu-id="88cbb-115">Vous pouvez définir n’importe quel jeu de propriétés par type de nœud, puis les sélectionner avec des contraintes lors de la création de services.</span><span class="sxs-lookup"><span data-stu-id="88cbb-115">You can define any set of properties per  node type, and then select for them with constraints when creating services.</span></span> <span data-ttu-id="88cbb-116">Vous pouvez également modifier les contraintes de placement d’un service en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="88cbb-116">You can also change a service's placement constraints while it is running.</span></span> <span data-ttu-id="88cbb-117">Cela vous permet de toochanges toorespond dans le cluster de hello ou exigences hello du service de hello.</span><span class="sxs-lookup"><span data-stu-id="88cbb-117">THis allows you toorespond toochanges in hello cluster or hello requirements of hello service.</span></span> <span data-ttu-id="88cbb-118">propriétés Hello d’un nœud donné peuvent également être mis à jour dynamiquement dans le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="88cbb-118">hello properties of a given node can also be updated dynamically in hello cluster.</span></span> <span data-ttu-id="88cbb-119">Plus d’informations sur les contraintes de placement et comment tooconfigure les trouverez dans [cet article](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints)</span><span class="sxs-lookup"><span data-stu-id="88cbb-119">More information on placement constraints and how tooconfigure them can be found in [this article](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints)</span></span>

## <a name="metrics"></a><span data-ttu-id="88cbb-120">Mesures</span><span class="sxs-lookup"><span data-stu-id="88cbb-120">Metrics</span></span>
<span data-ttu-id="88cbb-121">Métriques sont ensemble hello de ressources qui a besoin d’un service nommé donné.</span><span class="sxs-lookup"><span data-stu-id="88cbb-121">Metrics are hello set of resources that a given named service needs.</span></span> <span data-ttu-id="88cbb-122">La configuration de mesures d’un service détermine notamment la quantité d’une ressource que chaque réplica avec état ou instance sans état de ce service consomme par défaut.</span><span class="sxs-lookup"><span data-stu-id="88cbb-122">A service's metric configuration includes how much of that resource each stateful replica or stateless instance of that service consumes by default.</span></span> <span data-ttu-id="88cbb-123">Mesures comprennent également une pondération qui indique l’importance cette métrique d’équilibrage toothat service, en cas de compromis sont nécessaires.</span><span class="sxs-lookup"><span data-stu-id="88cbb-123">Metrics also include a weight that indicates how important balancing that metric is toothat service, in case tradeoffs are necessary.</span></span>

## <a name="advanced-placement-rules"></a><span data-ttu-id="88cbb-124">Règles de placement avancées</span><span class="sxs-lookup"><span data-stu-id="88cbb-124">Advanced placement rules</span></span>
<span data-ttu-id="88cbb-125">Il existe d’autres types de règles de placement qui sont utiles dans des scénarios moins courants.</span><span class="sxs-lookup"><span data-stu-id="88cbb-125">There are other types of placement rules that are useful in less common scenarios.</span></span> <span data-ttu-id="88cbb-126">Voici quelques exemples :</span><span class="sxs-lookup"><span data-stu-id="88cbb-126">Some examples are:</span></span>
- <span data-ttu-id="88cbb-127">Contraintes utiles avec des clusters dispersés géographiquement</span><span class="sxs-lookup"><span data-stu-id="88cbb-127">Constraints that help with geographically distributed clusters</span></span>
- <span data-ttu-id="88cbb-128">Certaines architectures d’application</span><span class="sxs-lookup"><span data-stu-id="88cbb-128">Certain application architectures</span></span>

<span data-ttu-id="88cbb-129">La configuration des autres règles de positionnement s’effectue via Corrélations ou Stratégies.</span><span class="sxs-lookup"><span data-stu-id="88cbb-129">Other placement rules are configured via either Correlations or Policies.</span></span>

## <a name="next-steps"></a><span data-ttu-id="88cbb-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="88cbb-130">Next steps</span></span>
- <span data-ttu-id="88cbb-131">Les métriques sont comment hello Gestionnaire de ressources du Cluster Service Fabric gère la consommation et la capacité en cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="88cbb-131">Metrics are how hello Service Fabric Cluster Resource Manger manages consumption and capacity in hello cluster.</span></span> <span data-ttu-id="88cbb-132">toolearn plus d’informations sur les métriques et comment tooconfigure, extraire [cet article](service-fabric-cluster-resource-manager-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="88cbb-132">toolearn more about metrics and how tooconfigure them, check out [this article](service-fabric-cluster-resource-manager-metrics.md)</span></span>
- <span data-ttu-id="88cbb-133">L’affinité est un mode que vous pouvez configurer pour vos services.</span><span class="sxs-lookup"><span data-stu-id="88cbb-133">Affinity is one mode you can configure for your services.</span></span> <span data-ttu-id="88cbb-134">Ce n’est pas courant, mais si nécessaire, vous trouverez plus d’informations [ici](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md)</span><span class="sxs-lookup"><span data-stu-id="88cbb-134">It is not common, but if you need it you can learn about it [here](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md)</span></span>
- <span data-ttu-id="88cbb-135">Il existe de règles de positionnement différents qui peuvent être configurées sur votre service toohandle supplémentaires des scénarios.</span><span class="sxs-lookup"><span data-stu-id="88cbb-135">There are many different placement rules that can be configured on your service toohandle additional scenarios.</span></span> <span data-ttu-id="88cbb-136">Vous trouverez plus d’informations sur ces différentes stratégies de positionnement [ici](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md)</span><span class="sxs-lookup"><span data-stu-id="88cbb-136">You can find out about those different placement policies [here](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md)</span></span>
- <span data-ttu-id="88cbb-137">Démarrer à partir du début de hello et [obtenir une présentation de toohello Gestionnaire de ressources du Cluster Service Fabric](service-fabric-cluster-resource-manager-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="88cbb-137">Start from hello beginning and [get an Introduction toohello Service Fabric Cluster Resource Manager](service-fabric-cluster-resource-manager-introduction.md)</span></span>
- <span data-ttu-id="88cbb-138">toofind out sur comment hello Gestionnaire de ressources de Cluster gère et équilibre la charge du cluster de hello, consultez l’article de hello sur [équilibrage de charge](service-fabric-cluster-resource-manager-balancing.md)</span><span class="sxs-lookup"><span data-stu-id="88cbb-138">toofind out about how hello Cluster Resource Manager manages and balances load in hello cluster, check out hello article on [balancing load](service-fabric-cluster-resource-manager-balancing.md)</span></span>
- <span data-ttu-id="88cbb-139">Hello, Gestionnaire de ressources du Cluster possède de nombreuses options permettant de décrire le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="88cbb-139">hello Cluster Resource Manager has many options for describing hello cluster.</span></span> <span data-ttu-id="88cbb-140">toofind plus d’informations à leur sujet, consultez cet article sur [décrivant un cluster Service Fabric](service-fabric-cluster-resource-manager-cluster-description.md)</span><span class="sxs-lookup"><span data-stu-id="88cbb-140">toofind out more about them, check out this article on [describing a Service Fabric cluster](service-fabric-cluster-resource-manager-cluster-description.md)</span></span>