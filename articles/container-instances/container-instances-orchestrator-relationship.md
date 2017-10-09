---
title: "les Instances de conteneurs aaaAzure et l’Orchestration de conteneur"
description: "En savoir plus sur l’interaction entre Azure Container Instances et les orchestrateurs de conteneurs"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 69a39edc6f14d885c1ac300990ed1399002ccfee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-instances-and-container-orchestrators"></a><span data-ttu-id="5be70-103">Azure Container Instances et les orchestrateurs de conteneurs</span><span class="sxs-lookup"><span data-stu-id="5be70-103">Azure Container Instances and container orchestrators</span></span>

<span data-ttu-id="5be70-104">En raison de leur taille réduite et de leur orientation d’application, les conteneurs conviennent parfaitement aux environnements de distribution agiles et aux architectures basées sur les microservices.</span><span class="sxs-lookup"><span data-stu-id="5be70-104">Because of their small size and application orientation, containers are well suited for agile delivery environments and microservice-based architectures.</span></span> <span data-ttu-id="5be70-105">tâche Hello d’automatiser et de gérer un grand nombre de conteneurs et la façon dont ils interagissent est appelé *orchestration*.</span><span class="sxs-lookup"><span data-stu-id="5be70-105">hello task of automating and managing a large number of containers and how they interact is known as *orchestration*.</span></span> <span data-ttu-id="5be70-106">Orchestrators de conteneur populaires incluent Kubernetes, contrôleur de domaine/système d’exploitation et Docker Swarm, qui sont disponibles dans hello [Service de conteneur Azure](https://docs.microsoft.com/azure/container-service/).</span><span class="sxs-lookup"><span data-stu-id="5be70-106">Popular container orchestrators include Kubernetes, DC/OS, and Docker Swarm, all of which are available in hello [Azure Container Service](https://docs.microsoft.com/azure/container-service/).</span></span>

<span data-ttu-id="5be70-107">Les Instances du conteneur Azure fournit des hello base planification des capacités de plateformes d’orchestration, mais il ne couvre pas les services de plus grande valeur hello que ces plateformes fournissent et peuvent en fait être complémentaires avec eux.</span><span class="sxs-lookup"><span data-stu-id="5be70-107">Azure Container Instances provides some of hello basic scheduling capabilities of orchestration platforms, but it does not cover hello higher-value services that those platforms provide and can in fact be complementary with them.</span></span> <span data-ttu-id="5be70-108">Cet article décrit l’étendue de hello de ce que les Instances du conteneur Azure gère et le taux de remplissage orchestrators de conteneur peuvent interagir avec lui.</span><span class="sxs-lookup"><span data-stu-id="5be70-108">This article describes hello scope of what Azure Container Instances handles and how full container orchestrators might interact with it.</span></span>

## <a name="traditional-orchestration"></a><span data-ttu-id="5be70-109">Orchestration traditionnelle</span><span class="sxs-lookup"><span data-stu-id="5be70-109">Traditional orchestration</span></span>

<span data-ttu-id="5be70-110">définition de la norme Hello d’orchestration inclut hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="5be70-110">hello standard definition of orchestration includes hello following tasks:</span></span>

- <span data-ttu-id="5be70-111">**Planification**: étant donné une image de conteneur et une demande de ressource, ordinateur approprié sur le conteneur de hello toorun est introuvable.</span><span class="sxs-lookup"><span data-stu-id="5be70-111">**Scheduling**: Given a container image and a resource request, find a suitable machine on which toorun hello container.</span></span>
- <span data-ttu-id="5be70-112">**Affinité/Anti-affinité** : spécifier qu’un ensemble de conteneurs doivent s’exécuter à proximité les uns des autres (à des fins de performances) ou suffisamment éloignés les uns des autres (à des fins de disponibilité).</span><span class="sxs-lookup"><span data-stu-id="5be70-112">**Affinity/Anti-affinity**: Specify that a set of containers should run nearby each other (for performance) or sufficiently far apart (for availability).</span></span>
- <span data-ttu-id="5be70-113">**Contrôle d’intégrité** : détecter les échecs de conteneur et les replanifier automatiquement.</span><span class="sxs-lookup"><span data-stu-id="5be70-113">**Health monitoring**: Watch for container failures and automatically reschedule them.</span></span>
- <span data-ttu-id="5be70-114">**Basculement**: effectuer le suivi de ce qui s’exécute sur chaque ordinateur et de replanification des conteneurs à partir des nœuds de toohealthy machines ayant échoué.</span><span class="sxs-lookup"><span data-stu-id="5be70-114">**Failover**: Keep track of what is running on each machine and reschedule containers from failed machines toohealthy nodes.</span></span>
- <span data-ttu-id="5be70-115">**Mise à l’échelle**: ajouter ou supprimer la demande de conteneur instances toomatch, manuellement ou automatiquement.</span><span class="sxs-lookup"><span data-stu-id="5be70-115">**Scaling**: Add or remove container instances toomatch demand, either manually or automatically.</span></span>
- <span data-ttu-id="5be70-116">**Mise en réseau**: fournir une surcouche réseau pour la coordination des conteneurs toocommunicate sur plusieurs ordinateurs hôtes.</span><span class="sxs-lookup"><span data-stu-id="5be70-116">**Networking**: Provide an overlay network for coordinating containers toocommunicate across multiple host machines.</span></span>
- <span data-ttu-id="5be70-117">**Détection du service**: activer des conteneurs toolocate eux automatiquement même si elles déplacement entre des ordinateurs hôtes et modifier les adresses IP.</span><span class="sxs-lookup"><span data-stu-id="5be70-117">**Service discovery**: Enable containers toolocate each other automatically even as they move between host machines and change IP addresses.</span></span>
- <span data-ttu-id="5be70-118">**Coordination des mises à niveau de l’application**: gestion d’application de tooavoid de mises à niveau conteneur temps d’arrêt et permettre la restauration si une erreur survient.</span><span class="sxs-lookup"><span data-stu-id="5be70-118">**Coordinated application upgrades**: Manage container upgrades tooavoid application down time and enable rollback if something goes wrong.</span></span>

## <a name="orchestration-with-azure-container-instances-a-layered-approach"></a><span data-ttu-id="5be70-119">Orchestration avec Azure Container Instances : une approche en couches</span><span class="sxs-lookup"><span data-stu-id="5be70-119">Orchestration with Azure Container Instances: A layered approach</span></span>

<span data-ttu-id="5be70-120">Les Instances du conteneur Azure permet une approche en couches tooorchestration, fournissant tous les hello planification et fonctionnalités de gestion requis toorun un seul conteneur, tout en autorisant des tâches de conteneur de plusieurs plateformes toomanage par-dessus orchestrator.</span><span class="sxs-lookup"><span data-stu-id="5be70-120">Azure Container Instances enables a layered approach tooorchestration, providing all of hello scheduling and management capabilities required toorun a single container, while allowing orchestrator platforms toomanage multi-container tasks on top of it.</span></span>

<span data-ttu-id="5be70-121">Étant donné que tous les hello sous-jacent d’infrastructure pour les Instances du conteneur est géré par Azure, une plate-forme orchestrator n’a pas besoin tooconcern lui-même sur la recherche d’un ordinateur hôte approprié sur le toorun un seul conteneur.</span><span class="sxs-lookup"><span data-stu-id="5be70-121">Because all of hello underlying infrastructure for Container Instances is managed by Azure, an orchestrator platform does not need tooconcern itself with finding an appropriate host machine on which toorun a single container.</span></span> <span data-ttu-id="5be70-122">élasticité Hello du cloud de hello garantit que l’une est toujours disponible.</span><span class="sxs-lookup"><span data-stu-id="5be70-122">hello elasticity of hello cloud ensures that one is always available.</span></span> <span data-ttu-id="5be70-123">Au lieu de cela, orchestrator de hello peut se concentrer sur les tâches de hello qui simplifient le développement hello de conteneur plusieurs architectures, notamment la mise à l’échelle et de coordonner les mises à niveau.</span><span class="sxs-lookup"><span data-stu-id="5be70-123">Instead, hello orchestrator can focus on hello tasks that simplify hello development of multi-container architectures, including scaling and coordinated upgrades.</span></span>



## <a name="potential-scenarios"></a><span data-ttu-id="5be70-124">Scénarios potentiels</span><span class="sxs-lookup"><span data-stu-id="5be70-124">Potential scenarios</span></span>

<span data-ttu-id="5be70-125">Bien que l’intégration d’orchestrateur avec Azure Container Instances en soit encore à sa phase initiale, nous prévoyons l’émergence de plusieurs environnements différents :</span><span class="sxs-lookup"><span data-stu-id="5be70-125">While orchestrator integration with Azure Container Instances is still nascent, we anticipate that a few different environments may emerge:</span></span>

### <a name="orchestration-of-container-instances-exclusively"></a><span data-ttu-id="5be70-126">Orchestration exclusive de Container Instances</span><span class="sxs-lookup"><span data-stu-id="5be70-126">Orchestration of Container Instances exclusively</span></span>

<span data-ttu-id="5be70-127">Deuxième car elles démarrent rapidement et de facturation par hello, un environnement basé uniquement sur les Instances du conteneur Azure offre tooget de manière plus rapide hello démarré et toodeal avec des charges de travail très variables.</span><span class="sxs-lookup"><span data-stu-id="5be70-127">Because they start quickly and bill by hello second, an environment based exclusively on Azure Container Instances offers hello fastest way tooget started and toodeal with highly variable workloads.</span></span>

### <a name="combination-of-container-instances-and-containers-in-virtual-machines"></a><span data-ttu-id="5be70-128">Combinaison de Container Instances et de conteneurs sur des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="5be70-128">Combination of Container Instances and Containers in Virtual Machines</span></span>

<span data-ttu-id="5be70-129">Pour la durée d’exécution longue stables les charges de travail, en orchestrant des conteneurs dans un cluster de machines virtuelles dédiées seront généralement moins chers que l’exécution des mêmes conteneurs hello avec des Instances de conteneur.</span><span class="sxs-lookup"><span data-stu-id="5be70-129">For long-running, stable workloads, orchestrating containers in a cluster of dedicated virtual machines will typically be cheaper than running hello same containers with Container Instances.</span></span> <span data-ttu-id="5be70-130">Toutefois, les Instances de conteneurs offrent une excellente solution pour développer rapidement et de contraction votre toodeal capacité globale avec inattendue ou de courte durée de vie des pics d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="5be70-130">However, Container Instances offer a great solution for quickly expanding and contracting your overall capacity toodeal with unexpected or short-lived spikes in usage.</span></span> <span data-ttu-id="5be70-131">Au lieu de la montée en puissance parallèle de nombre hello d’ordinateurs virtuels dans votre cluster, puis déployer des conteneurs supplémentaires sur ces ordinateurs, hello orchestrator peut simplement planifier hello autres conteneurs à l’aide d’Instances de conteneurs et les supprimer lorsqu’elles sont aucun plus nécessaire.</span><span class="sxs-lookup"><span data-stu-id="5be70-131">Rather than scaling out hello number of virtual machines in your cluster, then deploying additional containers onto those machines, hello orchestrator can simply schedule hello additional containers using Container Instances and delete them when they're no longer needed.</span></span>

## <a name="sample-implementation-azure-container-instances-connector-for-kubernetes"></a><span data-ttu-id="5be70-132">Exemple d’implémentation : connecteur Azure Container Instances pour Kubernetes</span><span class="sxs-lookup"><span data-stu-id="5be70-132">Sample implementation: Azure Container Instances Connector for Kubernetes</span></span>

<span data-ttu-id="5be70-133">toodemonstrate comment intégrer les plates-formes d’orchestration conteneur avec les Instances du conteneur Azure, nous avons démarré construction un [exemple de connecteur pour Kubernetes][aci-connector-k8s].</span><span class="sxs-lookup"><span data-stu-id="5be70-133">toodemonstrate how container orchestration platforms can integrate with Azure Container Instances, we have started building a [sample connector for Kubernetes][aci-connector-k8s].</span></span> 

<span data-ttu-id="5be70-134">Hello connecteur pour Kubernetes imite hello [kubelet] [ kubelet-doc] par l’inscription en tant que nœud avec une capacité illimitée et la distribution de la création de hello de [POD] [ pod-doc] en tant que groupes du conteneur dans les Instances du conteneur Azure.</span><span class="sxs-lookup"><span data-stu-id="5be70-134">hello connector for Kubernetes mimics hello [kubelet][kubelet-doc] by registering as a node with unlimited capacity and dispatching hello creation of [pods][pod-doc] as container groups in Azure Container Instances.</span></span> 

<!-- ![ACI Connector for Kubernetes][aci-connector-k8s-gif] -->

<span data-ttu-id="5be70-135">Connecteurs pour les autres orchestrators peut être créés de la même façon intégré à la puissance plateforme primitives toocombine hello orchestrator de hello API avec une fréquence de hello et simplicité de gestion des conteneurs dans les Instances du conteneur Azure.</span><span class="sxs-lookup"><span data-stu-id="5be70-135">Connectors for other orchestrators could be built that similarly integrated with platform primitives toocombine hello power of hello orchestrator API with hello speed and simplicity of managing containers in Azure Container Instances.</span></span>

> [!WARNING]
> <span data-ttu-id="5be70-136">Hello connecteur ACI pour Kubernetes est *expérimentale* et ne doit pas être utilisé en production.</span><span class="sxs-lookup"><span data-stu-id="5be70-136">hello ACI connector for Kubernetes is *experimental* and should not be used in production.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5be70-137">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5be70-137">Next steps</span></span>

<span data-ttu-id="5be70-138">Créer votre premier conteneur avec des Instances de conteneur Azure à l’aide de hello [guide de démarrage rapide](container-instances-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="5be70-138">Create your first container with Azure Container Instances using hello [quick start guide](container-instances-quickstart.md).</span></span>

<!-- IMAGES -->
[aci-connector-k8s-gif]: ./media/container-instances-orchestrator-relationship/aci-connector-k8s.gif

<!-- LINKS -->
[aci-connector-k8s]: https://github.com/azure/aci-connector-k8s
[kubelet-doc]: https://kubernetes.io/docs/admin/kubelet/
[pod-doc]: https://kubernetes.io/docs/concepts/workloads/pods/pod/