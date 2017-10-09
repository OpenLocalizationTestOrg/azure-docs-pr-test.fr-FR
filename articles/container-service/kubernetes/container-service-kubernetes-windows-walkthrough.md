---
title: aaaQuickstart - cluster Kubernetes de Azure pour Windows | Documents Microsoft
description: "En savoir plus rapidement les toocreate un cluster Kubernetes pour les conteneurs Windows dans le Service de conteneur Azure avec hello CLI d’Azure."
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 85fe65a46ae8c78797e8a8a097c2a37f06329335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-kubernetes-cluster-for-windows-containers"></a><span data-ttu-id="7d622-103">Déployer un cluster Azure Kubernetes pour des conteneurs Windows</span><span class="sxs-lookup"><span data-stu-id="7d622-103">Deploy Kubernetes cluster for Windows containers</span></span>

<span data-ttu-id="7d622-104">Hello CLI d’Azure est utilisé toocreate et gérer des ressources Azure à partir de la ligne de commande hello ou dans des scripts.</span><span class="sxs-lookup"><span data-stu-id="7d622-104">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="7d622-105">Ce guide décrit en détail à l’aide de hello CLI d’Azure toodeploy un [Kubernetes](https://kubernetes.io/docs/home/) du cluster dans [Service de conteneur Azure](../container-service-intro.md).</span><span class="sxs-lookup"><span data-stu-id="7d622-105">This guide details using hello Azure CLI toodeploy a [Kubernetes](https://kubernetes.io/docs/home/) cluster in [Azure Container Service](../container-service-intro.md).</span></span> <span data-ttu-id="7d622-106">Une fois que le cluster de hello est déployé, vous rejoignez tooit hello Kubernetes `kubectl` outil de ligne de commande et que vous déployez votre premier conteneur Windows.</span><span class="sxs-lookup"><span data-stu-id="7d622-106">Once hello cluster is deployed, you connect tooit with hello Kubernetes `kubectl` command-line tool, and you deploy your first Windows container.</span></span>

<span data-ttu-id="7d622-107">Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="7d622-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="7d622-108">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, ce démarrage rapide nécessite que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="7d622-108">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="7d622-109">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="7d622-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="7d622-110">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7d622-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

> [!NOTE]
> <span data-ttu-id="7d622-111">Le support des conteneurs Windows sur Kubernetes dans Azure Container Service est en préversion.</span><span class="sxs-lookup"><span data-stu-id="7d622-111">Support for Windows containers on Kubernetes in Azure Container Service is in preview.</span></span> 
>

## <a name="create-a-resource-group"></a><span data-ttu-id="7d622-112">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="7d622-112">Create a resource group</span></span>

<span data-ttu-id="7d622-113">Créer un groupe de ressources avec hello [création de groupe de az](/cli/azure/group#create) commande.</span><span class="sxs-lookup"><span data-stu-id="7d622-113">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="7d622-114">Un groupe de ressources Azure est un groupe logique dans lequel des ressources Azure sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="7d622-114">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="7d622-115">Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *eastus* emplacement.</span><span class="sxs-lookup"><span data-stu-id="7d622-115">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-kubernetes-cluster"></a><span data-ttu-id="7d622-116">Créer un cluster Kubernetes</span><span class="sxs-lookup"><span data-stu-id="7d622-116">Create Kubernetes cluster</span></span>
<span data-ttu-id="7d622-117">Créer un cluster Kubernetes dans le Service de conteneur Azure avec hello [az acs créer](/cli/azure/acs#create) commande.</span><span class="sxs-lookup"><span data-stu-id="7d622-117">Create a Kubernetes cluster in Azure Container Service with hello [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="7d622-118">Hello exemple suivant crée un cluster nommé *myK8sCluster* avec un Linux maître nœud et deux nœuds de l’agent de Windows.</span><span class="sxs-lookup"><span data-stu-id="7d622-118">hello following example creates a cluster named *myK8sCluster* with one Linux master node and two Windows agent nodes.</span></span> <span data-ttu-id="7d622-119">Cet exemple crée SSH maître de clés nécessaires tooconnect toohello Linux.</span><span class="sxs-lookup"><span data-stu-id="7d622-119">This example creates SSH keys needed tooconnect toohello Linux master.</span></span> <span data-ttu-id="7d622-120">Cet exemple utilise *azureuser* pour un nom d’utilisateur administratif et *myPassword12* comme mot de passe hello sur les nœuds de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="7d622-120">This example uses *azureuser* for an administrative user name and *myPassword12* as hello password on hello Windows nodes.</span></span> <span data-ttu-id="7d622-121">Mettre à jour ces environnement tooyour approprié de toosomething valeurs.</span><span class="sxs-lookup"><span data-stu-id="7d622-121">Update these values toosomething appropriate tooyour environment.</span></span> 



```azurecli-interactive 
az acs create --orchestrator-type=kubernetes \
    --resource-group myResourceGroup \
    --name=myK8sCluster \
    --agent-count=2 \
    --generate-ssh-keys \
    --windows --admin-username azureuser \
    --admin-password myPassword12
```

<span data-ttu-id="7d622-122">Après quelques minutes, commande hello se termine et présente des informations sur votre déploiement.</span><span class="sxs-lookup"><span data-stu-id="7d622-122">After several minutes, hello command completes, and shows you information about your deployment.</span></span>

## <a name="install-kubectl"></a><span data-ttu-id="7d622-123">Installer kubectl</span><span class="sxs-lookup"><span data-stu-id="7d622-123">Install kubectl</span></span>

<span data-ttu-id="7d622-124">tooconnect toohello Kubernetes de cluster à partir de votre ordinateur client, utilisez [ `kubectl` ](https://kubernetes.io/docs/user-guide/kubectl/), client de ligne de commande Kubernetes hello.</span><span class="sxs-lookup"><span data-stu-id="7d622-124">tooconnect toohello Kubernetes cluster from your client computer, use [`kubectl`](https://kubernetes.io/docs/user-guide/kubectl/), hello Kubernetes command-line client.</span></span> 

<span data-ttu-id="7d622-125">Si vous utilisez Azure CloudShell, l’outil `kubectl` est déjà installé.</span><span class="sxs-lookup"><span data-stu-id="7d622-125">If you're using Azure CloudShell, `kubectl` is already installed.</span></span> <span data-ttu-id="7d622-126">Si vous souhaitez tooinstall elle, vous pouvez utiliser localement hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) commande.</span><span class="sxs-lookup"><span data-stu-id="7d622-126">If you want tooinstall it locally, you can use hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span></span>

<span data-ttu-id="7d622-127">Hello suivant CLI d’Azure exemple installe `kubectl` tooyour système.</span><span class="sxs-lookup"><span data-stu-id="7d622-127">hello following Azure CLI example installs `kubectl` tooyour system.</span></span> <span data-ttu-id="7d622-128">Sur Windows, exécutez cette commande en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="7d622-128">On Windows, run this command as an administrator.</span></span>

```azurecli-interactive 
az acs kubernetes install-cli
```


## <a name="connect-with-kubectl"></a><span data-ttu-id="7d622-129">Se connecter avec kubectl</span><span class="sxs-lookup"><span data-stu-id="7d622-129">Connect with kubectl</span></span>

<span data-ttu-id="7d622-130">tooconfigure `kubectl` tooconnect tooyour Kubernetes cluster exécuter hello [az acs kubernetes get-informations d’identification](/cli/azure/acs/kubernetes#get-credentials) commande.</span><span class="sxs-lookup"><span data-stu-id="7d622-130">tooconfigure `kubectl` tooconnect tooyour Kubernetes cluster, run hello [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span> <span data-ttu-id="7d622-131">Hello exemple suivant télécharge configuration du cluster pour votre cluster Kubernetes hello.</span><span class="sxs-lookup"><span data-stu-id="7d622-131">hello following example downloads hello cluster configuration for your Kubernetes cluster.</span></span>

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

<span data-ttu-id="7d622-132">cluster de tooyour connexion tooverify hello à partir de votre ordinateur, essayez d’exécuter :</span><span class="sxs-lookup"><span data-stu-id="7d622-132">tooverify hello connection tooyour cluster from your machine, try running:</span></span>

```azurecli-interactive
kubectl get nodes
```

<span data-ttu-id="7d622-133">`kubectl`Répertorie les nœuds principal et l’agent hello.</span><span class="sxs-lookup"><span data-stu-id="7d622-133">`kubectl` lists hello master and agent nodes.</span></span>

```azurecli-interactive
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.5.3
k8s-agent-98dc3136-1    Ready                      5m        v1.5.3
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.5.3

```

## <a name="deploy-a-windows-iis-container"></a><span data-ttu-id="7d622-134">Déployer un conteneur Windows IIS</span><span class="sxs-lookup"><span data-stu-id="7d622-134">Deploy a Windows IIS container</span></span>

<span data-ttu-id="7d622-135">Vous pouvez exécuter un conteneur Docker à l’intérieur d’un *pod* Kubernetes, qui contient un ou plusieurs conteneurs.</span><span class="sxs-lookup"><span data-stu-id="7d622-135">You can run a Docker container inside a Kubernetes *pod*, which contains one or more containers.</span></span> 

<span data-ttu-id="7d622-136">Cet exemple de base utilise un toospecify de fichier JSON un conteneur Microsoft Internet Information Server (IIS) et crée ensuite des pod hello à l’aide de hello `kubctl apply` commande.</span><span class="sxs-lookup"><span data-stu-id="7d622-136">This basic example uses a JSON file toospecify a Microsoft Internet Information Server (IIS) container, and then creates hello pod using hello `kubctl apply` command.</span></span> 

<span data-ttu-id="7d622-137">Créer un fichier local nommé `iis.json` et hello de copie après le texte.</span><span class="sxs-lookup"><span data-stu-id="7d622-137">Create a local file named `iis.json` and copy hello following text.</span></span> <span data-ttu-id="7d622-138">Ce fichier indique Kubernetes toorun IIS sur Windows Server 2016 Nano Server, à l’aide d’une image de conteneur public [Hub Docker](https://hub.docker.com/r/nanoserver/iis/).</span><span class="sxs-lookup"><span data-stu-id="7d622-138">This file tells Kubernetes toorun IIS on Windows Server 2016 Nano Server, using a public container image from [Docker Hub](https://hub.docker.com/r/nanoserver/iis/).</span></span> <span data-ttu-id="7d622-139">conteneur de Hello utilise le port 80, mais initialement est uniquement accessible dans le réseau de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="7d622-139">hello container uses port 80, but initially is only accessible within hello cluster network.</span></span>

 ```JSON
 {
  "apiVersion": "v1",
  "kind": "Pod",
  "metadata": {
    "name": "iis",
    "labels": {
      "name": "iis"
    }
  },
  "spec": {
    "containers": [
      {
        "name": "iis",
        "image": "nanoserver/iis",
        "ports": [
          {
          "containerPort": 80
          }
        ]
      }
    ],
    "nodeSelector": {
     "beta.kubernetes.io/os": "windows"
     }
   }
 }
 ```

<span data-ttu-id="7d622-140">bloc de hello toostart, type :</span><span class="sxs-lookup"><span data-stu-id="7d622-140">toostart hello pod, type:</span></span>
  
```azurecli-interactive
kubectl apply -f iis.json
```  

<span data-ttu-id="7d622-141">déploiement de hello tootrack, type :</span><span class="sxs-lookup"><span data-stu-id="7d622-141">tootrack hello deployment, type:</span></span>
  
```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="7d622-142">Lors du déploiement de pod de hello, état de hello est `ContainerCreating`.</span><span class="sxs-lookup"><span data-stu-id="7d622-142">While hello pod is deploying, hello status is `ContainerCreating`.</span></span> <span data-ttu-id="7d622-143">Il peut prendre quelques minutes pour hello de hello conteneur tooenter `Running` état.</span><span class="sxs-lookup"><span data-stu-id="7d622-143">It can take a few minutes for hello container tooenter hello `Running` state.</span></span>

```azurecli-interactive
NAME     READY        STATUS        RESTARTS    AGE
iis      1/1          Running       0           32s
```

## <a name="view-hello-iis-welcome-page"></a><span data-ttu-id="7d622-144">Hello d’affichage page d’accueil IIS</span><span class="sxs-lookup"><span data-stu-id="7d622-144">View hello IIS welcome page</span></span>

<span data-ttu-id="7d622-145">tooexpose pod toohello Bonjour avec une adresse IP publique, hello type commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7d622-145">tooexpose hello pod toohello world with a public IP address, type hello following command:</span></span>

```azurecli-interactive
kubectl expose pods iis --port=80 --type=LoadBalancer
```

<span data-ttu-id="7d622-146">Cette commande Kubernetes crée un service et un [règle d’équilibreur de charge Azure](container-service-kubernetes-load-balancing.md) avec une adresse IP publique pour le service de hello.</span><span class="sxs-lookup"><span data-stu-id="7d622-146">With this command, Kubernetes creates a service and an [Azure load balancer rule](container-service-kubernetes-load-balancing.md) with a public IP address for hello service.</span></span> 

<span data-ttu-id="7d622-147">Exécutez hello suivant l’état du service de hello hello de toosee la commande.</span><span class="sxs-lookup"><span data-stu-id="7d622-147">Run hello following command toosee hello status of hello service.</span></span>

```azurecli-interactive
kubectl get svc
```

<span data-ttu-id="7d622-148">Adresse IP de hello s’affiche initialement en tant que `pending`.</span><span class="sxs-lookup"><span data-stu-id="7d622-148">Initially hello IP address appears as `pending`.</span></span> <span data-ttu-id="7d622-149">Après quelques minutes, hello adresse IP externe de hello `iis` pod est définie :</span><span class="sxs-lookup"><span data-stu-id="7d622-149">After a few minutes, hello external IP address of hello `iis` pod is set:</span></span>
  
```azurecli-interactive
NAME         CLUSTER-IP     EXTERNAL-IP     PORT(S)        AGE       
kubernetes   10.0.0.1       <none>          443/TCP        21h       
iis          10.0.111.25    13.64.158.233   80/TCP         22m
```

<span data-ttu-id="7d622-150">Vous pouvez utiliser un navigateur web de votre choix toosee hello par défaut IIS page d’accueil à l’adresse IP externe de hello :</span><span class="sxs-lookup"><span data-stu-id="7d622-150">You can use a web browser of your choice toosee hello default IIS welcome page at hello external IP address:</span></span>

![Image de navigation tooIIS](./media/container-service-kubernetes-windows-walkthrough/kubernetes-iis.png)  


## <a name="delete-cluster"></a><span data-ttu-id="7d622-152">Supprimer un cluster</span><span class="sxs-lookup"><span data-stu-id="7d622-152">Delete cluster</span></span>
<span data-ttu-id="7d622-153">Lorsque le cluster de hello n’est plus nécessaire, vous pouvez utiliser hello [suppression du groupe az](/cli/azure/group#delete) groupe de ressources tooremove hello, service de conteneur et toutes les ressources de la commande.</span><span class="sxs-lookup"><span data-stu-id="7d622-153">When hello cluster is no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, container service, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```


## <a name="next-steps"></a><span data-ttu-id="7d622-154">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7d622-154">Next steps</span></span>

<span data-ttu-id="7d622-155">Par le biais de ce guide de démarrage rapide, vous avez déployé un cluster Kubernetes, vous vous êtes connecté avec `kubectl` et vous avez déployé un pod avec un conteneur IIS.</span><span class="sxs-lookup"><span data-stu-id="7d622-155">In this quick start, you deployed a Kubernetes cluster, connected with `kubectl`, and deployed a pod with an IIS container.</span></span> <span data-ttu-id="7d622-156">toolearn en savoir plus sur le Service de conteneur Azure, continuer toohello Kubernetes didacticiel.</span><span class="sxs-lookup"><span data-stu-id="7d622-156">toolearn more about Azure Container Service, continue toohello Kubernetes tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7d622-157">Gérer un cluster Kubernetes ACS</span><span class="sxs-lookup"><span data-stu-id="7d622-157">Manage an ACS Kubernetes cluster</span></span>](container-service-tutorial-kubernetes-prepare-app.md)
