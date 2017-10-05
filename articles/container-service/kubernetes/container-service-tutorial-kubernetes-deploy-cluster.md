---
title: "Didacticiel Azure Container Service - Déployer un cluster | Microsoft Docs"
description: "Didacticiel Azure Container Service - Déployer un cluster"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, conteneurs, micro-services, Kubernetes, DC/OS, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/21/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 472697c1f0c18859087d7b448e1786d85c27aca0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-a-kubernetes-cluster-in-azure-container-service"></a><span data-ttu-id="653d3-104">Déployer un cluster Kubernetes dans Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="653d3-104">Deploy a Kubernetes cluster in Azure Container Service</span></span>

<span data-ttu-id="653d3-105">Kubernetes fournit une plateforme distribuée destinée aux applications en conteneur.</span><span class="sxs-lookup"><span data-stu-id="653d3-105">Kubernetes provides a distributed platform for containerized applications.</span></span> <span data-ttu-id="653d3-106">Avec Azure Container Service, l’approvisionnement d’un cluster Kubernetes prêt pour la production est une opération simple et rapide.</span><span class="sxs-lookup"><span data-stu-id="653d3-106">With Azure Container Service, provisioning of a production ready Kubernetes cluster is simple and quick.</span></span> <span data-ttu-id="653d3-107">Dans ce didacticiel (le troisième d’une série de sept), un cluster Azure Container Service Kubernetes est déployé.</span><span class="sxs-lookup"><span data-stu-id="653d3-107">In this tutorial, part 3 of 7, an Azure Container Service Kubernetes cluster is deployed.</span></span> <span data-ttu-id="653d3-108">Les étapes terminées sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="653d3-108">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="653d3-109">Déploiement d’un cluster ACS Kubernetes</span><span class="sxs-lookup"><span data-stu-id="653d3-109">Deploying a Kubernetes ACS cluster</span></span>
> * <span data-ttu-id="653d3-110">Installation de l’interface de ligne de commande Kubernetes (kubectl)</span><span class="sxs-lookup"><span data-stu-id="653d3-110">Installation of the Kubernetes CLI (kubectl)</span></span>
> * <span data-ttu-id="653d3-111">Configuration de kubectl</span><span class="sxs-lookup"><span data-stu-id="653d3-111">Configuration of kubectl</span></span>

<span data-ttu-id="653d3-112">Dans les didacticiels suivants, l’application Azure Vote est déployée sur le cluster, puis mise à l’échelle et mise à jour. En outre, Operations Management Suite est configuré pour la surveillance du cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="653d3-112">In subsequent tutorials, the Azure Vote application is deployed to the cluster, scaled, updated, and Operations Management Suite is configured to monitor the Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="653d3-113">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="653d3-113">Before you begin</span></span>

<span data-ttu-id="653d3-114">Dans les didacticiels précédents, une image conteneur a été créée et chargée dans une instance Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="653d3-114">In previous tutorials, a container image was created and uploaded to an Azure Container Registry instance.</span></span> <span data-ttu-id="653d3-115">Si vous n’avez pas accompli ces étapes et que vous souhaitez suivre cette procédure, revenez au [Didacticiel 1 – Créer des images conteneur](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="653d3-115">If you have not done these steps, and would like to follow along, return to [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span>

## <a name="create-kubernetes-cluster"></a><span data-ttu-id="653d3-116">Créer un cluster Kubernetes</span><span class="sxs-lookup"><span data-stu-id="653d3-116">Create Kubernetes cluster</span></span>

<span data-ttu-id="653d3-117">Dans le [didacticiel précédent](./container-service-tutorial-kubernetes-prepare-acr.md), un groupe de ressources nommé *myResourceGroup* a été créé.</span><span class="sxs-lookup"><span data-stu-id="653d3-117">In the [previous tutorial](./container-service-tutorial-kubernetes-prepare-acr.md), a resource group named *myResourceGroup* was created.</span></span> <span data-ttu-id="653d3-118">Si vous ne l’avez pas déjà fait, créez ce groupe de ressources maintenant.</span><span class="sxs-lookup"><span data-stu-id="653d3-118">If you have not done so, create this resource group now.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="653d3-119">Pour créer un cluster Kubernetes dans Azure Container Service, utilisez la commande [az acs create](/cli/azure/acs#create).</span><span class="sxs-lookup"><span data-stu-id="653d3-119">Create a Kubernetes cluster in Azure Container Service with the [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="653d3-120">L’exemple ci-après permet de créer un cluster nommé *myK8sCluster*, qui inclut un nœud maître Linux et trois nœuds agents Linux.</span><span class="sxs-lookup"><span data-stu-id="653d3-120">The following example creates a cluster named *myK8sCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive 
az acs create --orchestrator-type=kubernetes --resource-group myResourceGroup --name=myK8SCluster --generate-ssh-keys 
```

<span data-ttu-id="653d3-121">Au bout de quelques minutes, la commande se termine et retourne des informations au format JSON concernant le déploiement ACS.</span><span class="sxs-lookup"><span data-stu-id="653d3-121">After several minutes, the command completes, and returns json formatted information about the ACS deployment.</span></span>

## <a name="install-the-kubectl-cli"></a><span data-ttu-id="653d3-122">Installer l’interface de ligne de commande kubectl</span><span class="sxs-lookup"><span data-stu-id="653d3-122">Install the kubectl CLI</span></span>

<span data-ttu-id="653d3-123">Pour vous connecter au cluster Kubernetes à partir de votre ordinateur client, utilisez [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), le client de ligne de commande Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="653d3-123">To connect to the Kubernetes cluster from your client computer, use [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), the Kubernetes command-line client.</span></span> 

<span data-ttu-id="653d3-124">Si vous utilisez Azure CloudShell, l’outil `kubectl` est déjà installé.</span><span class="sxs-lookup"><span data-stu-id="653d3-124">If you're using Azure CloudShell, `kubectl` is already installed.</span></span> <span data-ttu-id="653d3-125">Pour l’installer en local, utilisez la commande [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli).</span><span class="sxs-lookup"><span data-stu-id="653d3-125">If you want to install it locally, use the [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span></span>

<span data-ttu-id="653d3-126">Avec Linux ou MacOS, vous devrez peut-être l’exécuter avec sudo.</span><span class="sxs-lookup"><span data-stu-id="653d3-126">If running in Linux or macOS, you may need to run with sudo.</span></span> <span data-ttu-id="653d3-127">Dans Windows, vérifiez que votre interpréteur de commandes a été exécuté en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="653d3-127">On Windows, ensure your shell has been run as administrator.</span></span>

```azurecli-interactive 
az acs kubernetes install-cli 
```

<span data-ttu-id="653d3-128">Dans Windows, l’installation par défaut est *c:\program files (x86)\kubectl.exe*.</span><span class="sxs-lookup"><span data-stu-id="653d3-128">On Windows, the default installation is *c:\program files (x86)\kubectl.exe*.</span></span> <span data-ttu-id="653d3-129">Vous devrez peut-être ajouter ce fichier au chemin de Windows.</span><span class="sxs-lookup"><span data-stu-id="653d3-129">You may need to add this file to the Windows path.</span></span> 

## <a name="connect-with-kubectl"></a><span data-ttu-id="653d3-130">Se connecter avec kubectl</span><span class="sxs-lookup"><span data-stu-id="653d3-130">Connect with kubectl</span></span>

<span data-ttu-id="653d3-131">Pour configurer le client `kubectl` afin qu’il se connecte à votre cluster Kubernetes, exécutez la commande [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials).</span><span class="sxs-lookup"><span data-stu-id="653d3-131">To configure `kubectl` to connect to your Kubernetes cluster, run the [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span>

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8SCluster
```

<span data-ttu-id="653d3-132">Pour vérifier la connexion à votre cluster, exécutez la commande [kubectl get nodes](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get).</span><span class="sxs-lookup"><span data-stu-id="653d3-132">To verify the connection to your cluster, run the [kubectl get nodes](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```azurecli-interactive
kubectl get nodes
```

<span data-ttu-id="653d3-133">Output:</span><span class="sxs-lookup"><span data-stu-id="653d3-133">Output:</span></span>

```bash
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.6.2
k8s-agent-98dc3136-1    Ready                      5m        v1.6.2
k8s-agent-98dc3136-2    Ready                      5m        v1.6.2
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.6.2
```

<span data-ttu-id="653d3-134">À l’issue du didacticiel, vous disposez d’un cluster ACS Kubernetes prêt pour les charges de travail.</span><span class="sxs-lookup"><span data-stu-id="653d3-134">At tutorial completion, you have an ACS Kubernetes cluster ready for workloads.</span></span> <span data-ttu-id="653d3-135">Dans les didacticiels suivants, une application à plusieurs conteneurs est déployée sur ce cluster, mise à l’échelle, mise à jour et surveillée.</span><span class="sxs-lookup"><span data-stu-id="653d3-135">In subsequent tutorials, a multi-container application is deployed to this cluster, scaled out, updated, and monitored.</span></span>

## <a name="next-steps"></a><span data-ttu-id="653d3-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="653d3-136">Next steps</span></span>

<span data-ttu-id="653d3-137">Dans ce didacticiel, un cluster Azure Container Service Kubernetes a été déployé.</span><span class="sxs-lookup"><span data-stu-id="653d3-137">In this tutorial, an Azure Container Service Kubernetes cluster was deployed.</span></span> <span data-ttu-id="653d3-138">Les étapes suivantes ont été effectuées :</span><span class="sxs-lookup"><span data-stu-id="653d3-138">The following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="653d3-139">Déploiement d’un cluster ACS Kubernetes</span><span class="sxs-lookup"><span data-stu-id="653d3-139">Deployed a Kubernetes ACS cluster</span></span>
> * <span data-ttu-id="653d3-140">Installation de l’interface de ligne de commande Kubernetes (kubectl)</span><span class="sxs-lookup"><span data-stu-id="653d3-140">Installed the Kubernetes CLI (kubectl)</span></span>
> * <span data-ttu-id="653d3-141">Configuration de kubectl</span><span class="sxs-lookup"><span data-stu-id="653d3-141">Configured kubectl</span></span>

<span data-ttu-id="653d3-142">Passez au didacticiel suivant pour en savoir plus sur l’exécution de l’application sur le cluster.</span><span class="sxs-lookup"><span data-stu-id="653d3-142">Advance to the next tutorial to learn about running application on the cluster.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="653d3-143">Déployer une application dans Kubernetes</span><span class="sxs-lookup"><span data-stu-id="653d3-143">Deploy application in Kubernetes</span></span>](./container-service-tutorial-kubernetes-deploy-application.md)
