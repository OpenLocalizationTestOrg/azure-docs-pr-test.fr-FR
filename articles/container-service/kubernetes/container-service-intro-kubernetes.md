---
title: aaaIntroduction tooAzure Service de conteneur pour Kubernetes | Documents Microsoft
description: "Service de conteneur Azure pour Kubernetes toodeploy simple et de gérer les applications basées sur le conteneur sur Azure."
services: container-service
documentationcenter: 
author: gabrtv
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Kubernetes, docker, conteneurs, microservices, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/21/2017
ms.author: gamonroy
ms.custom: mvc
ms.openlocfilehash: bfc85a180bdf4a405c9047eb882d3eed01640dd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-container-service-for-kubernetes"></a><span data-ttu-id="ec129-104">Introduction tooAzure Service de conteneur pour Kubernetes</span><span class="sxs-lookup"><span data-stu-id="ec129-104">Introduction tooAzure Container Service for Kubernetes</span></span>
<span data-ttu-id="ec129-105">Service de conteneur Azure pour Kubernetes rend toocreate simple, configurer et gérer un cluster d’ordinateurs virtuels qui sont des applications préconfigurés toorun placées dans des conteneurs.</span><span class="sxs-lookup"><span data-stu-id="ec129-105">Azure Container Service for Kubernetes makes it simple toocreate, configure, and manage a cluster of virtual machines that are preconfigured toorun containerized applications.</span></span> <span data-ttu-id="ec129-106">Ainsi vous toouse vos compétences existantes, ou appuyer sur un corps important et croissant d’expertise de la Communauté, toodeploy et gérer les applications de conteneur basé sur Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="ec129-106">This enables you toouse your existing skills, or draw upon a large and growing body of community expertise, toodeploy and manage container-based applications on Microsoft Azure.</span></span>

<span data-ttu-id="ec129-107">En utilisant le Service de conteneur Azure, vous pouvez tirer parti des hello entreprise fonctionnalités d’Azure, tout en conservant la portabilité des applications via Kubernetes et hello format d’image Docker.</span><span class="sxs-lookup"><span data-stu-id="ec129-107">By using Azure Container Service, you can take advantage of hello enterprise-grade features of Azure, while still maintaining application portability through Kubernetes and hello Docker image format.</span></span>

## <a name="using-azure-container-service-for-kubernetes"></a><span data-ttu-id="ec129-108">Utilisation d’Azure Container Service pour Kubernetes</span><span class="sxs-lookup"><span data-stu-id="ec129-108">Using Azure Container Service for Kubernetes</span></span>
<span data-ttu-id="ec129-109">L’objectif de Service de conteneur Azure est tooprovide un environnement d’hébergement de conteneur à l’aide d’outils open-source et les technologies adoptés par nos clients aujourd'hui.</span><span class="sxs-lookup"><span data-stu-id="ec129-109">Our goal with Azure Container Service is tooprovide a container hosting environment by using open-source tools and technologies that are popular among our customers today.</span></span> <span data-ttu-id="ec129-110">toothis fin, nous présentons les points de terminaison Kubernetes API standard hello.</span><span class="sxs-lookup"><span data-stu-id="ec129-110">toothis end, we expose hello standard Kubernetes API endpoints.</span></span> <span data-ttu-id="ec129-111">À l’aide de ces points de terminaison standard, vous pouvez exploiter tout logiciel qui est capable de communiquer avec tooa Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="ec129-111">By using these standard endpoints, you can leverage any software that is capable of talking tooa Kubernetes cluster.</span></span> <span data-ttu-id="ec129-112">Par exemple, vous pourriez choisir [kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/), [helm](https://helm.sh/), ou [draft](https://github.com/Azure/draft).</span><span class="sxs-lookup"><span data-stu-id="ec129-112">For example, you might choose [kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/), [helm](https://helm.sh/), or [draft](https://github.com/Azure/draft).</span></span>

## <a name="creating-a-kubernetes-cluster-using-azure-container-service"></a><span data-ttu-id="ec129-113">Création d’un cluster Kubernetes à l’aide d’Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="ec129-113">Creating a Kubernetes cluster using Azure Container Service</span></span>
<span data-ttu-id="ec129-114">toobegin à l’aide du Service de conteneur Azure, déployer un cluster de Service de conteneur Azure avec hello [Azure CLI 2.0](container-service-kubernetes-walkthrough.md) ou via le portail de hello (hello de recherche Marketplace pour **Service de conteneur Azure**).</span><span class="sxs-lookup"><span data-stu-id="ec129-114">toobegin using Azure Container Service, deploy an Azure Container Service cluster with hello [Azure CLI 2.0](container-service-kubernetes-walkthrough.md) or via hello portal (search hello Marketplace for **Azure Container Service**).</span></span> <span data-ttu-id="ec129-115">Si vous êtes un utilisateur expérimenté ayant besoin de davantage de contrôle sur les modèles Azure Resource Manager hello, vous pouvez utiliser d’ouvrir la source de hello [acs-moteur](https://github.com/Azure/acs-engine) projet toobuild vos propres Kubernetes personnalisées de cluster et le déployer via hello `az` CLI.</span><span class="sxs-lookup"><span data-stu-id="ec129-115">If you are an advanced user who needs more control over hello Azure Resource Manager templates, you can use hello open source [acs-engine](https://github.com/Azure/acs-engine) project toobuild your own custom Kubernetes cluster and deploy it via hello `az` CLI.</span></span>

### <a name="using-kubernetes"></a><span data-ttu-id="ec129-116">Utilisation de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="ec129-116">Using Kubernetes</span></span>
<span data-ttu-id="ec129-117">Kubernetes automatise le déploiement, la mise à l’échelle et la gestion des applications en conteneur.</span><span class="sxs-lookup"><span data-stu-id="ec129-117">Kubernetes automates deployment, scaling, and management of containerized applications.</span></span> <span data-ttu-id="ec129-118">Il possède un jeu complet de fonctionnalités, notamment :</span><span class="sxs-lookup"><span data-stu-id="ec129-118">It has a rich set of features including:</span></span>
* <span data-ttu-id="ec129-119">Binpacking automatique</span><span class="sxs-lookup"><span data-stu-id="ec129-119">Automatic binpacking</span></span>
* <span data-ttu-id="ec129-120">Réparation spontanée</span><span class="sxs-lookup"><span data-stu-id="ec129-120">Self-healing</span></span>
* <span data-ttu-id="ec129-121">Mise à l’échelle horizontale</span><span class="sxs-lookup"><span data-stu-id="ec129-121">Horizontal scaling</span></span>
* <span data-ttu-id="ec129-122">Détection de service et équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="ec129-122">Service discovery and load balancing</span></span>
* <span data-ttu-id="ec129-123">Déploiements et restaurations automatisés</span><span class="sxs-lookup"><span data-stu-id="ec129-123">Automated rollouts and rollbacks</span></span>
* <span data-ttu-id="ec129-124">Secret et gestion de la configuration</span><span class="sxs-lookup"><span data-stu-id="ec129-124">Secret and configuration management</span></span>
* <span data-ttu-id="ec129-125">Orchestration de stockage</span><span class="sxs-lookup"><span data-stu-id="ec129-125">Storage orchestration</span></span>
* <span data-ttu-id="ec129-126">Exécution Batch</span><span class="sxs-lookup"><span data-stu-id="ec129-126">Batch execution</span></span>

<span data-ttu-id="ec129-127">Diagramme architectural de Kubernetes déployé via Azure Container Service :</span><span class="sxs-lookup"><span data-stu-id="ec129-127">Architectural diagram of Kubernetes deployed via Azure Container Service:</span></span>

![Service de conteneur Azure configuré toouse Kubernetes.](media/acs-intro/kubernetes.png)

## <a name="videos"></a><span data-ttu-id="ec129-129">Vidéos</span><span class="sxs-lookup"><span data-stu-id="ec129-129">Videos</span></span>

<span data-ttu-id="ec129-130">Prise en charge de Kubernetes dans Azure Container Service (Azure Friday janvier 2017) :</span><span class="sxs-lookup"><span data-stu-id="ec129-130">Kubernetes Support in Azure Container Services (Azure Friday, January 2017):</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Kubernetes-Support-in-Azure-Container-Services/player]
>
>

<span data-ttu-id="ec129-131">Outils dédiés au développement et au déploiement d’applications sur Kubernetes (Azure OpenDev juin 2017) :</span><span class="sxs-lookup"><span data-stu-id="ec129-131">Tools for Developing and Deploying Applications on Kubernetes (Azure OpenDev, June 2017):</span></span>

> [!VIDEO https://channel9.msdn.com/Events/AzureOpenDev/June2017/Tools-for-Developing-and-Deploying-Applications-on-Kubernetes/player]
>
>

## <a name="next-steps"></a><span data-ttu-id="ec129-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ec129-132">Next steps</span></span>

<span data-ttu-id="ec129-133">Explorer hello [Kubernetes Quickstart](container-service-kubernetes-walkthrough.md) toobegin Explorer le Service de conteneur Azure aujourd'hui.</span><span class="sxs-lookup"><span data-stu-id="ec129-133">Explore hello [Kubernetes Quickstart](container-service-kubernetes-walkthrough.md) toobegin exploring Azure Container Service today.</span></span>
