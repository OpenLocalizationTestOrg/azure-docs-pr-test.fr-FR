---
title: aaaMonitor un Kubernetes Azure cluster avec CoScale | Documents Microsoft
description: "Surveiller un cluster Kubernetes dans Azure Container Service à l’aide de CoScale"
services: container-service
documentationcenter: 
author: fryckbos
manager: 
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: f835e82d2be3afe1d85070bd0bf69649cc6dd2ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-with-coscale"></a><span data-ttu-id="e3f90-103">Surveiller un cluster Kubernetes Azure Container Service avec CoScale</span><span class="sxs-lookup"><span data-stu-id="e3f90-103">Monitor an Azure Container Service Kubernetes cluster with CoScale</span></span>

<span data-ttu-id="e3f90-104">Dans cet article, nous vous indiquons comment toodeploy hello [CoScale](https://www.coscale.com/) toomonitor agent tous les nœuds et les conteneurs dans votre Kubernetes de cluster dans le conteneur de Service Azure.</span><span class="sxs-lookup"><span data-stu-id="e3f90-104">In this article, we show you how toodeploy hello [CoScale](https://www.coscale.com/) agent toomonitor all nodes and containers in your Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="e3f90-105">Vous avez besoin d’un compte CoScale pour cette configuration.</span><span class="sxs-lookup"><span data-stu-id="e3f90-105">You need an account with CoScale for this configuration.</span></span> 


## <a name="about-coscale"></a><span data-ttu-id="e3f90-106">À propos de CoScale</span><span class="sxs-lookup"><span data-stu-id="e3f90-106">About CoScale</span></span> 

<span data-ttu-id="e3f90-107">CoScale est une plateforme de surveillance qui collecte les mesures et les événements de tous les conteneurs dans plusieurs plateformes d’orchestration.</span><span class="sxs-lookup"><span data-stu-id="e3f90-107">CoScale is a monitoring platform that gathers metrics and events from all containers in several orchestration platforms.</span></span> <span data-ttu-id="e3f90-108">CoScale offre une surveillance complète pour les environnements Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="e3f90-108">CoScale offers full-stack monitoring for Kubernetes environments.</span></span> <span data-ttu-id="e3f90-109">Il fournit des visualisations et analytique pour toutes les couches de la pile de hello : hello du système d’exploitation, Kubernetes, Docker et les applications en cours d’exécution à l’intérieur de vos conteneurs.</span><span class="sxs-lookup"><span data-stu-id="e3f90-109">It provides visualizations and analytics for all layers in hello stack: hello OS, Kubernetes, Docker, and applications running inside your containers.</span></span> <span data-ttu-id="e3f90-110">CoScale offre plusieurs analyse tableaux de bord intégrés et il a des opérateurs de tooallow de détection d’anomalie intégrés et les problèmes aux développeurs toofind infrastructure et d’application rapidement.</span><span class="sxs-lookup"><span data-stu-id="e3f90-110">CoScale offers several built-in monitoring dashboards, and it has built-in anomaly detection tooallow operators and developers toofind infrastructure and application issues fast.</span></span>

![Interface utilisateur CoScale](./media/container-service-kubernetes-coscale/coscale.png)

<span data-ttu-id="e3f90-112">Comme indiqué dans cet article, vous pouvez installer des agents sur un toorun de cluster Kubernetes CoScale comme une solution SaaS.</span><span class="sxs-lookup"><span data-stu-id="e3f90-112">As shown in this article, you can install agents on a Kubernetes cluster toorun CoScale as a SaaS solution.</span></span> <span data-ttu-id="e3f90-113">Si vous souhaitez tookeep vos données sur site, CoScale est également disponible pour l’installation locale.</span><span class="sxs-lookup"><span data-stu-id="e3f90-113">If you want tookeep your data on-site, CoScale is also available for on-premises installation.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="e3f90-114">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e3f90-114">Prerequisites</span></span>

<span data-ttu-id="e3f90-115">Vous devez tout d’abord trop[créer un compte CoScale](https://www.coscale.com/free-trial).</span><span class="sxs-lookup"><span data-stu-id="e3f90-115">You first need too[create a CoScale account](https://www.coscale.com/free-trial).</span></span>

<span data-ttu-id="e3f90-116">Cette procédure pas à pas suppose que vous avez [créé un cluster Kubernetes à l’aide d’Azure Container Service](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="e3f90-116">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="e3f90-117">Il suppose également que vous avez hello `az` CLI d’Azure et `kubectl` outils sont installés.</span><span class="sxs-lookup"><span data-stu-id="e3f90-117">It also assumes that you have hello `az` Azure CLI and `kubectl` tools installed.</span></span>

<span data-ttu-id="e3f90-118">Vous pouvez tester si vous avez hello `az` outil est installé en exécutant :</span><span class="sxs-lookup"><span data-stu-id="e3f90-118">You can test if you have hello `az` tool installed by running:</span></span>

```azurecli
az --version
```

<span data-ttu-id="e3f90-119">Si vous n’avez pas hello `az` outil est installé, il existe des instructions [ici](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e3f90-119">If you don't have hello `az` tool installed, there are instructions [here](/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="e3f90-120">Vous pouvez tester si vous avez hello `kubectl` outil est installé en exécutant :</span><span class="sxs-lookup"><span data-stu-id="e3f90-120">You can test if you have hello `kubectl` tool installed by running:</span></span>

```bash
kubectl version
```

<span data-ttu-id="e3f90-121">Si `kubectl` n’est pas installé, vous pouvez exécuter :</span><span class="sxs-lookup"><span data-stu-id="e3f90-121">If you don't have `kubectl` installed, you can run:</span></span>

```azurecli
az acs kubernetes install-cli
```

## <a name="installing-hello-coscale-agent-with-a-daemonset"></a><span data-ttu-id="e3f90-122">L’installation de l’agent de hello CoScale avec un DaemonSet</span><span class="sxs-lookup"><span data-stu-id="e3f90-122">Installing hello CoScale agent with a DaemonSet</span></span>
<span data-ttu-id="e3f90-123">[DaemonSets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) sont utilisés par Kubernetes toorun une instance unique d’un conteneur sur chaque hôte de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="e3f90-123">[DaemonSets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) are used by Kubernetes toorun a single instance of a container on each host in hello cluster.</span></span>
<span data-ttu-id="e3f90-124">Ils conviennent parfaitement pour l’exécution des agents de surveillance de l’agent de CoScale hello.</span><span class="sxs-lookup"><span data-stu-id="e3f90-124">They're perfect for running monitoring agents such as hello CoScale agent.</span></span>

<span data-ttu-id="e3f90-125">Une fois que vous vous connectez tooCoScale, accédez à toohello [page de l’agent](https://app.coscale.com/) agents de CoScale tooinstall sur votre cluster à l’aide d’un DaemonSet.</span><span class="sxs-lookup"><span data-stu-id="e3f90-125">After you log in tooCoScale, go toohello [agent page](https://app.coscale.com/) tooinstall CoScale agents on your cluster using a DaemonSet.</span></span> <span data-ttu-id="e3f90-126">Hello CoScale UI fournit toocreate des étapes de configuration interactive un agent et le démarrer l’analyse complète de votre cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="e3f90-126">hello CoScale UI provides guided configuration steps toocreate an agent and start monitoring your complete Kubernetes cluster.</span></span>

![Configuration de l’agent CoScale](./media/container-service-kubernetes-coscale/installation.png)

<span data-ttu-id="e3f90-128">agent de hello toostart sur cluster hello, exécutez la commande hello fourni :</span><span class="sxs-lookup"><span data-stu-id="e3f90-128">toostart hello agent on hello cluster, run hello supplied command:</span></span>

![Démarrer l’agent de hello CoScale](./media/container-service-kubernetes-coscale/agent_script.png)

<span data-ttu-id="e3f90-130">Et voilà !</span><span class="sxs-lookup"><span data-stu-id="e3f90-130">That's it!</span></span> <span data-ttu-id="e3f90-131">Une fois que les agents hello sont en cours d’exécution, vous devez voir les données dans la console hello dans quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="e3f90-131">Once hello agents are up and running, you should see data in hello console in a few minutes.</span></span> <span data-ttu-id="e3f90-132">Visitez hello [page de l’agent](https://app.coscale.com/) toosee un résumé de votre cluster, effectuez les étapes de configuration supplémentaires et consultez les tableaux de bord telles que hello **Kubernetes présentation des clusters**.</span><span class="sxs-lookup"><span data-stu-id="e3f90-132">Visit hello [agent page](https://app.coscale.com/) toosee a summary of your cluster, perform additional configuration steps, and see dashboards such as hello **Kubernetes cluster overview**.</span></span>

![Vue d’ensemble du cluster Kubernetes](./media/container-service-kubernetes-coscale/dashboard_clusteroverview.png)

<span data-ttu-id="e3f90-134">Hello CoScale agent est automatiquement déployé sur des ordinateurs dans un cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="e3f90-134">hello CoScale agent is automatically deployed on new machines in hello cluster.</span></span> <span data-ttu-id="e3f90-135">Hello agent mises à jour automatiquement lorsqu’une nouvelle version est disponible.</span><span class="sxs-lookup"><span data-stu-id="e3f90-135">hello agent updates automatically when a new version is released.</span></span>


## <a name="next-steps"></a><span data-ttu-id="e3f90-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e3f90-136">Next steps</span></span>

<span data-ttu-id="e3f90-137">Consultez hello [CoScale documentation](http://docs.coscale.com/) et [blog](https://www.coscale.com/blog) pour plus d’informations sur la surveillance des solutions de CoScale.</span><span class="sxs-lookup"><span data-stu-id="e3f90-137">See hello [CoScale documentation](http://docs.coscale.com/) and [blog](https://www.coscale.com/blog) for more more information about CoScale monitoring solutions.</span></span> 

