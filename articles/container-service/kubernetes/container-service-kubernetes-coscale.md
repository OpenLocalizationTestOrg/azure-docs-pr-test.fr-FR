---
title: "Surveiller un cluster Azure Kubernetes avec CoScale | Microsoft Docs"
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
ms.openlocfilehash: f894191baced710fc0f5a8c8692df98033341a48
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-with-coscale"></a><span data-ttu-id="09542-103">Surveiller un cluster Kubernetes Azure Container Service avec CoScale</span><span class="sxs-lookup"><span data-stu-id="09542-103">Monitor an Azure Container Service Kubernetes cluster with CoScale</span></span>

<span data-ttu-id="09542-104">Dans cet article, nous vous montrons comment déployer l’agent [CoScale](https://www.coscale.com/) pour surveiller tous les nœuds et tous les conteneurs de votre cluster Kubernetes dans Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="09542-104">In this article, we show you how to deploy the [CoScale](https://www.coscale.com/) agent to monitor all nodes and containers in your Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="09542-105">Vous avez besoin d’un compte CoScale pour cette configuration.</span><span class="sxs-lookup"><span data-stu-id="09542-105">You need an account with CoScale for this configuration.</span></span> 


## <a name="about-coscale"></a><span data-ttu-id="09542-106">À propos de CoScale</span><span class="sxs-lookup"><span data-stu-id="09542-106">About CoScale</span></span> 

<span data-ttu-id="09542-107">CoScale est une plateforme de surveillance qui collecte les mesures et les événements de tous les conteneurs dans plusieurs plateformes d’orchestration.</span><span class="sxs-lookup"><span data-stu-id="09542-107">CoScale is a monitoring platform that gathers metrics and events from all containers in several orchestration platforms.</span></span> <span data-ttu-id="09542-108">CoScale offre une surveillance complète pour les environnements Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="09542-108">CoScale offers full-stack monitoring for Kubernetes environments.</span></span> <span data-ttu-id="09542-109">Il fournit des visualisations et des analyses pour toutes les couches de la pile : le système d’exploitation Kubernetes, Docker et les applications qui s’exécutent dans vos conteneurs.</span><span class="sxs-lookup"><span data-stu-id="09542-109">It provides visualizations and analytics for all layers in the stack: the OS, Kubernetes, Docker, and applications running inside your containers.</span></span> <span data-ttu-id="09542-110">CoScale propose plusieurs tableaux de bord de surveillance intégrés, et fournit une fonctionnalité intégrée de détection des anomalies qui permet aux opérateurs et aux développeurs de détecter rapidement les problèmes liés aux infrastructures et aux applications.</span><span class="sxs-lookup"><span data-stu-id="09542-110">CoScale offers several built-in monitoring dashboards, and it has built-in anomaly detection to allow operators and developers to find infrastructure and application issues fast.</span></span>

![Interface utilisateur CoScale](./media/container-service-kubernetes-coscale/coscale.png)

<span data-ttu-id="09542-112">Comme indiqué dans cet article, vous pouvez installer des agents sur un cluster Kubernetes pour exécuter CoScale en tant que solution SaaS.</span><span class="sxs-lookup"><span data-stu-id="09542-112">As shown in this article, you can install agents on a Kubernetes cluster to run CoScale as a SaaS solution.</span></span> <span data-ttu-id="09542-113">Si vous souhaitez conserver vos données sur site, CoScale est également disponible pour une installation locale.</span><span class="sxs-lookup"><span data-stu-id="09542-113">If you want to keep your data on-site, CoScale is also available for on-premises installation.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="09542-114">Composants requis</span><span class="sxs-lookup"><span data-stu-id="09542-114">Prerequisites</span></span>

<span data-ttu-id="09542-115">Vous devez d’abord [créer un compte CoScale](https://www.coscale.com/free-trial).</span><span class="sxs-lookup"><span data-stu-id="09542-115">You first need to [create a CoScale account](https://www.coscale.com/free-trial).</span></span>

<span data-ttu-id="09542-116">Cette procédure pas à pas suppose que vous avez [créé un cluster Kubernetes à l’aide d’Azure Container Service](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="09542-116">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="09542-117">Elle suppose également que vous avez installé les outils de l’interface Azure CLI `az` et `kubectl`.</span><span class="sxs-lookup"><span data-stu-id="09542-117">It also assumes that you have the `az` Azure CLI and `kubectl` tools installed.</span></span>

<span data-ttu-id="09542-118">Vous pouvez tester si l’outil `az` est installé en exécutant :</span><span class="sxs-lookup"><span data-stu-id="09542-118">You can test if you have the `az` tool installed by running:</span></span>

```azurecli
az --version
```

<span data-ttu-id="09542-119">Si l’outil `az` n’est pas installé, suivez les instructions figurant [ici](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="09542-119">If you don't have the `az` tool installed, there are instructions [here](/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="09542-120">Vous pouvez tester si l’outil `kubectl` est installé en exécutant :</span><span class="sxs-lookup"><span data-stu-id="09542-120">You can test if you have the `kubectl` tool installed by running:</span></span>

```bash
kubectl version
```

<span data-ttu-id="09542-121">Si `kubectl` n’est pas installé, vous pouvez exécuter :</span><span class="sxs-lookup"><span data-stu-id="09542-121">If you don't have `kubectl` installed, you can run:</span></span>

```azurecli
az acs kubernetes install-cli
```

## <a name="installing-the-coscale-agent-with-a-daemonset"></a><span data-ttu-id="09542-122">Installation de l’agent CoScale avec un DaemonSet</span><span class="sxs-lookup"><span data-stu-id="09542-122">Installing the CoScale agent with a DaemonSet</span></span>
<span data-ttu-id="09542-123">Les [DaemonSets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) sont utilisés par Kubernetes pour exécuter une instance unique d’un conteneur sur chaque hôte du cluster.</span><span class="sxs-lookup"><span data-stu-id="09542-123">[DaemonSets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) are used by Kubernetes to run a single instance of a container on each host in the cluster.</span></span>
<span data-ttu-id="09542-124">Ils sont parfaits pour exécuter des agents de surveillance, tels que l’agent CoScale.</span><span class="sxs-lookup"><span data-stu-id="09542-124">They're perfect for running monitoring agents such as the CoScale agent.</span></span>

<span data-ttu-id="09542-125">Une fois que vous êtes connecté à CoScale, accédez à la [page de l’agent](https://app.coscale.com/) pour installer les agents CoScale sur votre cluster à l’aide d’un DaemonSet.</span><span class="sxs-lookup"><span data-stu-id="09542-125">After you log in to CoScale, go to the [agent page](https://app.coscale.com/) to install CoScale agents on your cluster using a DaemonSet.</span></span> <span data-ttu-id="09542-126">L’interface utilisateur CoScale fournit les étapes de configuration guidée pour créer un agent et entamer la surveillance de votre cluster Kubernetes complet.</span><span class="sxs-lookup"><span data-stu-id="09542-126">The CoScale UI provides guided configuration steps to create an agent and start monitoring your complete Kubernetes cluster.</span></span>

![Configuration de l’agent CoScale](./media/container-service-kubernetes-coscale/installation.png)

<span data-ttu-id="09542-128">Pour démarrer l’agent sur le cluster, exécutez la commande fournie :</span><span class="sxs-lookup"><span data-stu-id="09542-128">To start the agent on the cluster, run the supplied command:</span></span>

![Démarrez l’agent CoScale](./media/container-service-kubernetes-coscale/agent_script.png)

<span data-ttu-id="09542-130">Et voilà !</span><span class="sxs-lookup"><span data-stu-id="09542-130">That's it!</span></span> <span data-ttu-id="09542-131">Dès que les agents sont en cours d’exécution, des données s’affichent dans la console après quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="09542-131">Once the agents are up and running, you should see data in the console in a few minutes.</span></span> <span data-ttu-id="09542-132">Visitez la [page de l’agent](https://app.coscale.com/) pour afficher un résumé de votre cluster, effectuer les étapes de configuration supplémentaires et consulter les tableaux de bord, comme la **vue d’ensemble du cluster Kubernetes**.</span><span class="sxs-lookup"><span data-stu-id="09542-132">Visit the [agent page](https://app.coscale.com/) to see a summary of your cluster, perform additional configuration steps, and see dashboards such as the **Kubernetes cluster overview**.</span></span>

![Vue d’ensemble du cluster Kubernetes](./media/container-service-kubernetes-coscale/dashboard_clusteroverview.png)

<span data-ttu-id="09542-134">L’agent CoScale est déployé automatiquement sur les nouvelles machines dans le cluster.</span><span class="sxs-lookup"><span data-stu-id="09542-134">The CoScale agent is automatically deployed on new machines in the cluster.</span></span> <span data-ttu-id="09542-135">L’agent se met à jour automatiquement lorsqu’une nouvelle version est publiée.</span><span class="sxs-lookup"><span data-stu-id="09542-135">The agent updates automatically when a new version is released.</span></span>


## <a name="next-steps"></a><span data-ttu-id="09542-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="09542-136">Next steps</span></span>

<span data-ttu-id="09542-137">Consultez la [documentation CoScale](http://docs.coscale.com/) et le [blog](https://www.coscale.com/blog) pour en savoir plus sur les solutions de surveillance CoScale.</span><span class="sxs-lookup"><span data-stu-id="09542-137">See the [CoScale documentation](http://docs.coscale.com/) and [blog](https://www.coscale.com/blog) for more more information about CoScale monitoring solutions.</span></span> 

