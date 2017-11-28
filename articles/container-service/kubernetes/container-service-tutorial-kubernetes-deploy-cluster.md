---
title: "didacticiel de Service de conteneur aaaAzure - déployer un Cluster | Documents Microsoft"
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
ms.openlocfilehash: c4c8cc95c88d9c2077d0322f57e5d3159e2dd0ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-kubernetes-cluster-in-azure-container-service"></a><span data-ttu-id="dd311-104">Déployer un cluster Kubernetes dans Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="dd311-104">Deploy a Kubernetes cluster in Azure Container Service</span></span>

<span data-ttu-id="dd311-105">Kubernetes fournit une plateforme distribuée destinée aux applications en conteneur.</span><span class="sxs-lookup"><span data-stu-id="dd311-105">Kubernetes provides a distributed platform for containerized applications.</span></span> <span data-ttu-id="dd311-106">Avec Azure Container Service, l’approvisionnement d’un cluster Kubernetes prêt pour la production est une opération simple et rapide.</span><span class="sxs-lookup"><span data-stu-id="dd311-106">With Azure Container Service, provisioning of a production ready Kubernetes cluster is simple and quick.</span></span> <span data-ttu-id="dd311-107">Dans ce didacticiel (le troisième d’une série de sept), un cluster Azure Container Service Kubernetes est déployé.</span><span class="sxs-lookup"><span data-stu-id="dd311-107">In this tutorial, part 3 of 7, an Azure Container Service Kubernetes cluster is deployed.</span></span> <span data-ttu-id="dd311-108">Les étapes terminées sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="dd311-108">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="dd311-109">Déploiement d’un cluster ACS Kubernetes</span><span class="sxs-lookup"><span data-stu-id="dd311-109">Deploying a Kubernetes ACS cluster</span></span>
> * <span data-ttu-id="dd311-110">Installation de hello Kubernetes CLI (kubectl)</span><span class="sxs-lookup"><span data-stu-id="dd311-110">Installation of hello Kubernetes CLI (kubectl)</span></span>
> * <span data-ttu-id="dd311-111">Configuration de kubectl</span><span class="sxs-lookup"><span data-stu-id="dd311-111">Configuration of kubectl</span></span>

<span data-ttu-id="dd311-112">Dans les didacticiels suivants hello Vote Azure application est déployée toohello cluster, à l’échelle, de mettre à jour et Operations Management Suite est le cluster de Kubernetes hello toomonitor configuré.</span><span class="sxs-lookup"><span data-stu-id="dd311-112">In subsequent tutorials, hello Azure Vote application is deployed toohello cluster, scaled, updated, and Operations Management Suite is configured toomonitor hello Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="dd311-113">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="dd311-113">Before you begin</span></span>

<span data-ttu-id="dd311-114">Dans les didacticiels précédents, une image de conteneur a été créée et téléchargé l’instance du Registre de conteneur Azure tooan.</span><span class="sxs-lookup"><span data-stu-id="dd311-114">In previous tutorials, a container image was created and uploaded tooan Azure Container Registry instance.</span></span> <span data-ttu-id="dd311-115">Si vous n’avez pas fait ces étapes et que vous aimeriez toofollow le long, retourner trop[didacticiel 1 : créer des images de conteneur](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="dd311-115">If you have not done these steps, and would like toofollow along, return too[Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span>

## <a name="create-kubernetes-cluster"></a><span data-ttu-id="dd311-116">Créer un cluster Kubernetes</span><span class="sxs-lookup"><span data-stu-id="dd311-116">Create Kubernetes cluster</span></span>

<span data-ttu-id="dd311-117">Bonjour [didacticiel précédent](./container-service-tutorial-kubernetes-prepare-acr.md), un groupe de ressources nommé *myResourceGroup* a été créé.</span><span class="sxs-lookup"><span data-stu-id="dd311-117">In hello [previous tutorial](./container-service-tutorial-kubernetes-prepare-acr.md), a resource group named *myResourceGroup* was created.</span></span> <span data-ttu-id="dd311-118">Si vous ne l’avez pas déjà fait, créez ce groupe de ressources maintenant.</span><span class="sxs-lookup"><span data-stu-id="dd311-118">If you have not done so, create this resource group now.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="dd311-119">Créer un cluster Kubernetes dans le Service de conteneur Azure avec hello [az acs créer](/cli/azure/acs#create) commande.</span><span class="sxs-lookup"><span data-stu-id="dd311-119">Create a Kubernetes cluster in Azure Container Service with hello [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="dd311-120">Hello exemple suivant crée un cluster nommé *myK8sCluster* avec un Linux maître nœud et trois nœuds de l’agent Linux.</span><span class="sxs-lookup"><span data-stu-id="dd311-120">hello following example creates a cluster named *myK8sCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive 
az acs create --orchestrator-type=kubernetes --resource-group myResourceGroup --name=myK8SCluster --generate-ssh-keys 
```

<span data-ttu-id="dd311-121">Après quelques minutes, commande hello se termine et retourne json mis en forme les informations sur le déploiement de hello ACS.</span><span class="sxs-lookup"><span data-stu-id="dd311-121">After several minutes, hello command completes, and returns json formatted information about hello ACS deployment.</span></span>

## <a name="install-hello-kubectl-cli"></a><span data-ttu-id="dd311-122">Installer hello kubectl CLI</span><span class="sxs-lookup"><span data-stu-id="dd311-122">Install hello kubectl CLI</span></span>

<span data-ttu-id="dd311-123">tooconnect toohello Kubernetes de cluster à partir de votre ordinateur client, utilisez [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), client de ligne de commande Kubernetes hello.</span><span class="sxs-lookup"><span data-stu-id="dd311-123">tooconnect toohello Kubernetes cluster from your client computer, use [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), hello Kubernetes command-line client.</span></span> 

<span data-ttu-id="dd311-124">Si vous utilisez Azure CloudShell, l’outil `kubectl` est déjà installé.</span><span class="sxs-lookup"><span data-stu-id="dd311-124">If you're using Azure CloudShell, `kubectl` is already installed.</span></span> <span data-ttu-id="dd311-125">Si vous souhaitez tooinstall il utiliser localement, hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) commande.</span><span class="sxs-lookup"><span data-stu-id="dd311-125">If you want tooinstall it locally, use hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span></span>

<span data-ttu-id="dd311-126">Si vous en Linux ou macOS, vous devrez peut-être toorun avec sudo.</span><span class="sxs-lookup"><span data-stu-id="dd311-126">If running in Linux or macOS, you may need toorun with sudo.</span></span> <span data-ttu-id="dd311-127">Dans Windows, vérifiez que votre interpréteur de commandes a été exécuté en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="dd311-127">On Windows, ensure your shell has been run as administrator.</span></span>

```azurecli-interactive 
az acs kubernetes install-cli 
```

<span data-ttu-id="dd311-128">Sous Windows, installation par défaut de hello est *c:\program files (x86)\kubectl.exe*.</span><span class="sxs-lookup"><span data-stu-id="dd311-128">On Windows, hello default installation is *c:\program files (x86)\kubectl.exe*.</span></span> <span data-ttu-id="dd311-129">Vous devrez peut-être tooadd ce chemin d’accès de fichier toohello Windows.</span><span class="sxs-lookup"><span data-stu-id="dd311-129">You may need tooadd this file toohello Windows path.</span></span> 

## <a name="connect-with-kubectl"></a><span data-ttu-id="dd311-130">Se connecter avec kubectl</span><span class="sxs-lookup"><span data-stu-id="dd311-130">Connect with kubectl</span></span>

<span data-ttu-id="dd311-131">tooconfigure `kubectl` tooconnect tooyour Kubernetes cluster exécuter hello [az acs kubernetes get-informations d’identification](/cli/azure/acs/kubernetes#get-credentials) commande.</span><span class="sxs-lookup"><span data-stu-id="dd311-131">tooconfigure `kubectl` tooconnect tooyour Kubernetes cluster, run hello [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span>

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8SCluster
```

<span data-ttu-id="dd311-132">cluster de tooyour connexion tooverify hello, exécutez hello [kubectl obtenir des nœuds](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) commande.</span><span class="sxs-lookup"><span data-stu-id="dd311-132">tooverify hello connection tooyour cluster, run hello [kubectl get nodes](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```azurecli-interactive
kubectl get nodes
```

<span data-ttu-id="dd311-133">Output:</span><span class="sxs-lookup"><span data-stu-id="dd311-133">Output:</span></span>

```bash
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.6.2
k8s-agent-98dc3136-1    Ready                      5m        v1.6.2
k8s-agent-98dc3136-2    Ready                      5m        v1.6.2
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.6.2
```

<span data-ttu-id="dd311-134">À l’issue du didacticiel, vous disposez d’un cluster ACS Kubernetes prêt pour les charges de travail.</span><span class="sxs-lookup"><span data-stu-id="dd311-134">At tutorial completion, you have an ACS Kubernetes cluster ready for workloads.</span></span> <span data-ttu-id="dd311-135">Dans les didacticiels suivants, une application conteneur multi est déployé toothis cluster monté en charge, mises à jour et analysées.</span><span class="sxs-lookup"><span data-stu-id="dd311-135">In subsequent tutorials, a multi-container application is deployed toothis cluster, scaled out, updated, and monitored.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd311-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="dd311-136">Next steps</span></span>

<span data-ttu-id="dd311-137">Dans ce didacticiel, un cluster Azure Container Service Kubernetes a été déployé.</span><span class="sxs-lookup"><span data-stu-id="dd311-137">In this tutorial, an Azure Container Service Kubernetes cluster was deployed.</span></span> <span data-ttu-id="dd311-138">Hello suit ont été effectuée :</span><span class="sxs-lookup"><span data-stu-id="dd311-138">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="dd311-139">Déploiement d’un cluster ACS Kubernetes</span><span class="sxs-lookup"><span data-stu-id="dd311-139">Deployed a Kubernetes ACS cluster</span></span>
> * <span data-ttu-id="dd311-140">Hello installé Kubernetes CLI (kubectl)</span><span class="sxs-lookup"><span data-stu-id="dd311-140">Installed hello Kubernetes CLI (kubectl)</span></span>
> * <span data-ttu-id="dd311-141">Configuration de kubectl</span><span class="sxs-lookup"><span data-stu-id="dd311-141">Configured kubectl</span></span>

<span data-ttu-id="dd311-142">Avance toohello toolearn de didacticiel suivant sur l’application en cours d’exécution sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="dd311-142">Advance toohello next tutorial toolearn about running application on hello cluster.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="dd311-143">Déployer une application dans Kubernetes</span><span class="sxs-lookup"><span data-stu-id="dd311-143">Deploy application in Kubernetes</span></span>](./container-service-tutorial-kubernetes-deploy-application.md)
