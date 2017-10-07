---
title: aaaAzure conteneur Instances conteneur de groupes
description: "Découvrez comment fonctionnent les groupes de conteneurs dans Azure Container Instances"
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
ms.date: 08/08/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 2b0e784609979045c8f77d7b6d0987ec3fee714c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="container-groups-in-azure-container-instances"></a><span data-ttu-id="c2d81-103">Groupes de conteneurs dans Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="c2d81-103">Container Groups in Azure Container Instances</span></span>

<span data-ttu-id="c2d81-104">ressources de niveau supérieur Hello dans les Instances du conteneur Azure est un groupe conteneur.</span><span class="sxs-lookup"><span data-stu-id="c2d81-104">hello top-level resource in Azure Container Instances is a container group.</span></span> <span data-ttu-id="c2d81-105">Cet article décrit les groupes de conteneurs et les types de scénarios associés.</span><span class="sxs-lookup"><span data-stu-id="c2d81-105">This article describes what container groups are and what types of scenarios they enable.</span></span>

## <a name="how-a-container-group-works"></a><span data-ttu-id="c2d81-106">Fonctionnement d’un groupe de conteneurs</span><span class="sxs-lookup"><span data-stu-id="c2d81-106">How a container group works</span></span>

<span data-ttu-id="c2d81-107">Un conteneur de groupe est une collection de conteneurs obtient planifiées sur hello héberger l’ordinateur et partager un cycle de vie, du réseau local et les volumes de stockage.</span><span class="sxs-lookup"><span data-stu-id="c2d81-107">A container group is a collection of containers that get scheduled on hello same host machine and share a lifecycle, local network, and storage volumes.</span></span> <span data-ttu-id="c2d81-108">Il est même concept toohello d’un *pod* dans [Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod/) et [DC/OS](https://dcos.io/docs/1.9/deploying-services/pods/).</span><span class="sxs-lookup"><span data-stu-id="c2d81-108">It is similar toohello concept of a *pod* in [Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod/) and [DC/OS](https://dcos.io/docs/1.9/deploying-services/pods/).</span></span>

<span data-ttu-id="c2d81-109">Hello diagramme suivant montre un exemple d’un groupe conteneur qui inclut plusieurs conteneurs.</span><span class="sxs-lookup"><span data-stu-id="c2d81-109">hello following diagram shows an example of a container group that includes multiple containers.</span></span>

![Exemple de groupe de conteneurs][container-groups-example]

<span data-ttu-id="c2d81-111">Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="c2d81-111">Note that:</span></span>

- <span data-ttu-id="c2d81-112">groupe de Hello est planifiée sur un ordinateur hôte unique.</span><span class="sxs-lookup"><span data-stu-id="c2d81-112">hello group is scheduled on a single host machine.</span></span>
- <span data-ttu-id="c2d81-113">groupe de Hello expose une adresse IP publique unique, avec un seul port exposé.</span><span class="sxs-lookup"><span data-stu-id="c2d81-113">hello group exposes a single public IP address, with one exposed port.</span></span>
- <span data-ttu-id="c2d81-114">groupe de Hello est constitué de deux conteneurs.</span><span class="sxs-lookup"><span data-stu-id="c2d81-114">hello group is made up of two containers.</span></span> <span data-ttu-id="c2d81-115">Un conteneur est à l’écoute sur le port 80, tandis que hello autres écoute le port 5000.</span><span class="sxs-lookup"><span data-stu-id="c2d81-115">One container listens on port 80, while hello other listens on port 5000.</span></span>
- <span data-ttu-id="c2d81-116">groupe de Hello inclut deux partages de fichiers Azure en tant que de montage de volume, et chaque conteneur monte un des partages hello localement.</span><span class="sxs-lookup"><span data-stu-id="c2d81-116">hello group includes two Azure file shares as volume mounts, and each container mounts one of hello shares locally.</span></span>

### <a name="networking"></a><span data-ttu-id="c2d81-117">Mise en réseau</span><span class="sxs-lookup"><span data-stu-id="c2d81-117">Networking</span></span>

<span data-ttu-id="c2d81-118">Les groupes du conteneur partagent une adresse IP et un espace de noms de port sur cette adresse IP.</span><span class="sxs-lookup"><span data-stu-id="c2d81-118">Container groups share an IP address and a port namespace on that IP address.</span></span> <span data-ttu-id="c2d81-119">tooreach de clients externes tooenable un conteneur au sein du groupe de hello, vous devez exposer le port hello sur l’adresse IP de hello et à partir du conteneur de hello.</span><span class="sxs-lookup"><span data-stu-id="c2d81-119">tooenable external clients tooreach a container within hello group, you must expose hello port on hello IP address and from hello container.</span></span> <span data-ttu-id="c2d81-120">Étant donné que les conteneurs au sein du groupe de hello partagent un espace de noms de port, mappage de port n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="c2d81-120">Because containers within hello group share a port namespace, port mapping is not supported.</span></span> <span data-ttu-id="c2d81-121">Conteneurs au sein d’un groupe peuvent atteindre l’autre via localhost sur hello ports dont ils ont exposés, même si ces ports ne sont pas exposés en externe sur l’adresse IP du groupe hello.</span><span class="sxs-lookup"><span data-stu-id="c2d81-121">Containers within a group can reach each other via localhost on hello ports that they have exposed, even if those ports are not exposed externally on hello group's IP address.</span></span>

### <a name="storage"></a><span data-ttu-id="c2d81-122">Storage</span><span class="sxs-lookup"><span data-stu-id="c2d81-122">Storage</span></span>

<span data-ttu-id="c2d81-123">Vous pouvez spécifier toomount volumes externes dans un groupe conteneur.</span><span class="sxs-lookup"><span data-stu-id="c2d81-123">You can specify external volumes toomount within a container group.</span></span> <span data-ttu-id="c2d81-124">Vous pouvez mapper ces volumes dans les chemins d’accès spécifiques dans des conteneurs individuels hello dans un groupe.</span><span class="sxs-lookup"><span data-stu-id="c2d81-124">You can map those volumes into specific paths within hello individual containers in a group.</span></span>

## <a name="common-scenarios"></a><span data-ttu-id="c2d81-125">Scénarios courants</span><span class="sxs-lookup"><span data-stu-id="c2d81-125">Common scenarios</span></span>

<span data-ttu-id="c2d81-126">Groupes du conteneur multiples sont utiles dans les cas où vous voulez toodivide une seule tâche fonctionnel dans un petit nombre d’images de conteneur, qui peuvent être fournis par différentes équipes et d’avoir des exigences de ressources distinct.</span><span class="sxs-lookup"><span data-stu-id="c2d81-126">Multi-container groups are useful in cases where you want toodivide up a single functional task into a small number of container images, which can be delivered by different teams and have separate resource requirements.</span></span> <span data-ttu-id="c2d81-127">Exemples d’utilisation :</span><span class="sxs-lookup"><span data-stu-id="c2d81-127">Example usage could include:</span></span>

- <span data-ttu-id="c2d81-128">Un conteneur d’applications et un conteneur de journalisation.</span><span class="sxs-lookup"><span data-stu-id="c2d81-128">An application container and a logging container.</span></span> <span data-ttu-id="c2d81-129">conteneur de journalisation Hello collecte des journaux de hello et de sortie de métriques par principale de l’application hello et les écrit toolong-terme.</span><span class="sxs-lookup"><span data-stu-id="c2d81-129">hello logging container collects hello logs and metrics output by hello main application and writes them toolong-term storage.</span></span>
- <span data-ttu-id="c2d81-130">Une application et un conteneur de surveillance.</span><span class="sxs-lookup"><span data-stu-id="c2d81-130">An application and a monitoring container.</span></span> <span data-ttu-id="c2d81-131">Hello surveillant conteneur régulièrement rend un tooensure d’application demande toohello qu’il est en cours d’exécution et répond correctement et déclenche une alerte si elle n’est pas.</span><span class="sxs-lookup"><span data-stu-id="c2d81-131">hello monitoring container periodically makes a request toohello application tooensure that it's running and responding correctly and raises an alert if it's not.</span></span>
- <span data-ttu-id="c2d81-132">Un conteneur servant d’une application web et un conteneur d’extraction de contenu le plus récent à partir du contrôle de code source hello.</span><span class="sxs-lookup"><span data-stu-id="c2d81-132">A container serving a web application and a container pulling hello latest content from source control.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c2d81-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c2d81-133">Next steps</span></span>

<span data-ttu-id="c2d81-134">Découvrez comment trop[déployer un groupe conteneur multi](container-instances-multi-container-group.md) avec un modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c2d81-134">Learn how too[deploy a multi-container group](container-instances-multi-container-group.md) with an Azure Resource Manager template.</span></span>

<!-- IMAGES -->

[container-groups-example]: ./media/container-instances-container-groups/container-groups-example.png