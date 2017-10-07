---
title: aaaQuickstart - cluster Azure Kubernetes pour Linux | Documents Microsoft
description: "En savoir plus rapidement les toocreate un cluster Kubernetes pour les conteneurs Linux dans le conteneur de Service Azure avec hello CLI d’Azure."
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 8da267e8-2aeb-4c24-9a7a-65bdca3a82d6
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/21/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 8b0d7a803148c1cbf329f4b76f2e99b4b7e14983
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-kubernetes-cluster-for-linux-containers"></a><span data-ttu-id="60b0d-103">Déployer un cluster Azure Kubernetes pour des conteneurs Linux</span><span class="sxs-lookup"><span data-stu-id="60b0d-103">Deploy Kubernetes cluster for Linux containers</span></span>

<span data-ttu-id="60b0d-104">Dans ce guide de démarrage rapide, un cluster Kubernetes est déployé à l’aide de hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="60b0d-104">In this quick start, a Kubernetes cluster is deployed using hello Azure CLI.</span></span> <span data-ttu-id="60b0d-105">Une application conteneur multi composé d’un serveur web frontal et une instance de Redis est puis déployée et exécutée sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="60b0d-105">A multi-container application consisting of web front end and a Redis instance is then deployed and run on hello cluster.</span></span> <span data-ttu-id="60b0d-106">Une fois terminé, l’application hello est accessible sur internet de hello.</span><span class="sxs-lookup"><span data-stu-id="60b0d-106">Once completed, hello application is accessible over hello internet.</span></span> 

<span data-ttu-id="60b0d-107">exemple d’application Hello utilisé dans ce document est écrit dans Python.</span><span class="sxs-lookup"><span data-stu-id="60b0d-107">hello example application used in this document is written in Python.</span></span> <span data-ttu-id="60b0d-108">concepts de Hello et les étapes décrites ici peuvent être utilisé toodeploy n’importe quel conteneur de l’image dans un cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="60b0d-108">hello concepts and steps detailed here can be used toodeploy any container image into a Kubernetes cluster.</span></span> <span data-ttu-id="60b0d-109">Hello code, fichier Dockerfile et le projet de toothis connexes précréé Kubernetes fichiers manifeste sont disponibles sur [GitHub](https://github.com/Azure-Samples/azure-voting-app-redis.git).</span><span class="sxs-lookup"><span data-stu-id="60b0d-109">hello code, Dockerfile, and pre-created Kubernetes manifest files related toothis project are available on [GitHub](https://github.com/Azure-Samples/azure-voting-app-redis.git).</span></span>

![Image de navigation tooAzure Vote](media/container-service-kubernetes-walkthrough/azure-vote.png)

<span data-ttu-id="60b0d-111">Ce démarrage rapide suppose une compréhension élémentaire des concepts de Kubernetes, pour plus d’informations sur Kubernetes voir hello [Kubernetes documentation]( https://kubernetes.io/docs/home/).</span><span class="sxs-lookup"><span data-stu-id="60b0d-111">This quick start assumes a basic understanding of Kubernetes concepts, for detailed information on Kubernetes see hello [Kubernetes documentation]( https://kubernetes.io/docs/home/).</span></span>

<span data-ttu-id="60b0d-112">Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="60b0d-112">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="60b0d-113">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, ce démarrage rapide nécessite que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="60b0d-113">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="60b0d-114">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="60b0d-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="60b0d-115">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="60b0d-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="60b0d-116">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="60b0d-116">Create a resource group</span></span>

<span data-ttu-id="60b0d-117">Créer un groupe de ressources avec hello [création de groupe de az](/cli/azure/group#create) commande.</span><span class="sxs-lookup"><span data-stu-id="60b0d-117">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="60b0d-118">Un groupe de ressources Azure est un groupe logique dans lequel des ressources Azure sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="60b0d-118">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="60b0d-119">Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *westeurope* emplacement.</span><span class="sxs-lookup"><span data-stu-id="60b0d-119">hello following example creates a resource group named *myResourceGroup* in hello *westeurope* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="60b0d-120">Output:</span><span class="sxs-lookup"><span data-stu-id="60b0d-120">Output:</span></span>

```json
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup",
  "location": "westeurope",
  "managedBy": null,
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-kubernetes-cluster"></a><span data-ttu-id="60b0d-121">Créer un cluster Kubernetes</span><span class="sxs-lookup"><span data-stu-id="60b0d-121">Create Kubernetes cluster</span></span>

<span data-ttu-id="60b0d-122">Créer un cluster Kubernetes dans le Service de conteneur Azure avec hello [az acs créer](/cli/azure/acs#create) commande.</span><span class="sxs-lookup"><span data-stu-id="60b0d-122">Create a Kubernetes cluster in Azure Container Service with hello [az acs create](/cli/azure/acs#create) command.</span></span> <span data-ttu-id="60b0d-123">Hello exemple suivant crée un cluster nommé *myK8sCluster* avec un Linux maître nœud et trois nœuds de l’agent Linux.</span><span class="sxs-lookup"><span data-stu-id="60b0d-123">hello following example creates a cluster named *myK8sCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive 
az acs create --orchestrator-type kubernetes --resource-group myResourceGroup --name myK8sCluster --generate-ssh-keys 
```

<span data-ttu-id="60b0d-124">Après quelques minutes, commande hello se termine et retourne des informations au format json sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="60b0d-124">After several minutes, hello command completes and returns json formatted information about hello cluster.</span></span> 

## <a name="connect-toohello-cluster"></a><span data-ttu-id="60b0d-125">Se connecter toohello cluster</span><span class="sxs-lookup"><span data-stu-id="60b0d-125">Connect toohello cluster</span></span>

<span data-ttu-id="60b0d-126">toomanage un cluster Kubernetes, utilisez [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), client de ligne de commande Kubernetes hello.</span><span class="sxs-lookup"><span data-stu-id="60b0d-126">toomanage a Kubernetes cluster, use [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), hello Kubernetes command-line client.</span></span> 

<span data-ttu-id="60b0d-127">Si vous utilisez Azure CloudShell, l’outil kubectl est déjà installé.</span><span class="sxs-lookup"><span data-stu-id="60b0d-127">If you're using Azure CloudShell, kubectl is already installed.</span></span> <span data-ttu-id="60b0d-128">Si vous souhaitez tooinstall elle, vous pouvez utiliser localement hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) commande.</span><span class="sxs-lookup"><span data-stu-id="60b0d-128">If you want tooinstall it locally, you can use hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span></span>

<span data-ttu-id="60b0d-129">tooconfigure kubectl tooconnect tooyour Kubernetes cluster, exécutez hello [az acs kubernetes get-informations d’identification](/cli/azure/acs/kubernetes#get-credentials) commande.</span><span class="sxs-lookup"><span data-stu-id="60b0d-129">tooconfigure kubectl tooconnect tooyour Kubernetes cluster, run hello [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span> <span data-ttu-id="60b0d-130">Cette étape télécharge les informations d’identification et configure hello Kubernetes CLI toouse les.</span><span class="sxs-lookup"><span data-stu-id="60b0d-130">This step downloads credentials and configures hello Kubernetes CLI toouse them.</span></span>

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

<span data-ttu-id="60b0d-131">cluster de tooyour connexion tooverify hello, utilisez hello [kubectl obtenir](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) commande tooreturn une liste de nœuds de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="60b0d-131">tooverify hello connection tooyour cluster, use hello [kubectl get](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command tooreturn a list of hello cluster nodes.</span></span>

```azurecli-interactive
kubectl get nodes
```

<span data-ttu-id="60b0d-132">Output:</span><span class="sxs-lookup"><span data-stu-id="60b0d-132">Output:</span></span>

```bash
NAME                    STATUS                     AGE       VERSION
k8s-agent-14ad53a1-0    Ready                      10m       v1.6.6
k8s-agent-14ad53a1-1    Ready                      10m       v1.6.6
k8s-agent-14ad53a1-2    Ready                      10m       v1.6.6
k8s-master-14ad53a1-0   Ready,SchedulingDisabled   10m       v1.6.6
```

## <a name="run-hello-application"></a><span data-ttu-id="60b0d-133">Exécutez l’application hello</span><span class="sxs-lookup"><span data-stu-id="60b0d-133">Run hello application</span></span>

<span data-ttu-id="60b0d-134">Un fichier manifeste Kubernetes définit un état souhaité pour le cluster de hello, y compris les images de conteneur doivent s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="60b0d-134">A Kubernetes manifest file defines a desired state for hello cluster, including what container images should be running.</span></span> <span data-ttu-id="60b0d-135">Pour cet exemple, un manifeste est utilisé toocreate tous les objets nécessaires toorun hello application de Vote de Azure.</span><span class="sxs-lookup"><span data-stu-id="60b0d-135">For this example, a manifest is used toocreate all objects needed toorun hello Azure Vote application.</span></span> 

<span data-ttu-id="60b0d-136">Créez un fichier nommé `azure-vote.yml` et copient il hello suivant YAML.</span><span class="sxs-lookup"><span data-stu-id="60b0d-136">Create a file named `azure-vote.yml` and copy into it hello following YAML.</span></span> <span data-ttu-id="60b0d-137">Si vous travaillez dans Azure Cloud Shell, vous pouvez créer ce fichier à l’aide de vi ou de Nano comme si vous travailliez sur un système virtuel ou physique.</span><span class="sxs-lookup"><span data-stu-id="60b0d-137">If you are working in Azure Cloud Shell, this file can be created using vi or Nano as if working on a virtual or physical system.</span></span>

```yaml
apiVersion: apps/v1beta1
kind: Deployment
metadata:
  name: azure-vote-back
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: azure-vote-back
    spec:
      containers:
      - name: azure-vote-back
        image: redis
        ports:
        - containerPort: 6379
          name: redis
---
apiVersion: v1
kind: Service
metadata:
  name: azure-vote-back
spec:
  ports:
  - port: 6379
  selector:
    app: azure-vote-back
---
apiVersion: apps/v1beta1
kind: Deployment
metadata:
  name: azure-vote-front
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: azure-vote-front
    spec:
      containers:
      - name: azure-vote-front
        image: microsoft/azure-vote-front:redis-v1
        ports:
        - containerPort: 80
        env:
        - name: REDIS
          value: "azure-vote-back"
---
apiVersion: v1
kind: Service
metadata:
  name: azure-vote-front
spec:
  type: LoadBalancer
  ports:
  - port: 80
  selector:
    app: azure-vote-front
```

<span data-ttu-id="60b0d-138">Hello d’utilisation [kubectl créer](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) application hello de toorun de commande.</span><span class="sxs-lookup"><span data-stu-id="60b0d-138">Use hello [kubectl create](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) command toorun hello application.</span></span>

```azurecli-interactive
kubectl create -f azure-vote.yml
```

<span data-ttu-id="60b0d-139">Output:</span><span class="sxs-lookup"><span data-stu-id="60b0d-139">Output:</span></span>

```bash
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-hello-application"></a><span data-ttu-id="60b0d-140">Tester l’application hello</span><span class="sxs-lookup"><span data-stu-id="60b0d-140">Test hello application</span></span>

<span data-ttu-id="60b0d-141">Comme l’application hello est exécutée, un [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) est créé qu’expose hello application frontale toohello internet.</span><span class="sxs-lookup"><span data-stu-id="60b0d-141">As hello application is run, a [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) is created that exposes hello application front end toohello internet.</span></span> <span data-ttu-id="60b0d-142">Ce processus peut prendre quelques minutes toocomplete.</span><span class="sxs-lookup"><span data-stu-id="60b0d-142">This process can take a few minutes toocomplete.</span></span> 

<span data-ttu-id="60b0d-143">cours toomonitor, utilisez hello [kubectl obtenir service](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) avec hello `--watch` argument.</span><span class="sxs-lookup"><span data-stu-id="60b0d-143">toomonitor progress, use hello [kubectl get service](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command with hello `--watch` argument.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front --watch
```

<span data-ttu-id="60b0d-144">Initialement hello **IP externe** pour hello *avant de vote d’azure* service apparaît sous la forme *en attente*.</span><span class="sxs-lookup"><span data-stu-id="60b0d-144">Initially hello **EXTERNAL-IP** for hello *azure-vote-front* service appears as *pending*.</span></span> <span data-ttu-id="60b0d-145">Une fois que l’adresse de hello IP externe a été modifiée à partir de *en attente* tooan *adresse IP*, utilisez `CTRL-C` processus d’observation kubectl toostop hello.</span><span class="sxs-lookup"><span data-stu-id="60b0d-145">Once hello EXTERNAL-IP address has changed from *pending* tooan *IP address*, use `CTRL-C` toostop hello kubectl watch process.</span></span> 
  
```bash
azure-vote-front   10.0.34.242   <pending>     80:30676/TCP   7s
azure-vote-front   10.0.34.242   52.179.23.131   80:30676/TCP   2m
```

<span data-ttu-id="60b0d-146">Vous pouvez maintenant rechercher le hello Azure Vote application pour toohello externe IP adresse toosee.</span><span class="sxs-lookup"><span data-stu-id="60b0d-146">You can now browse toohello external IP address toosee hello Azure Vote App.</span></span>

![Image de navigation tooAzure Vote](media/container-service-kubernetes-walkthrough/azure-vote.png)  

## <a name="delete-cluster"></a><span data-ttu-id="60b0d-148">Supprimer un cluster</span><span class="sxs-lookup"><span data-stu-id="60b0d-148">Delete cluster</span></span>
<span data-ttu-id="60b0d-149">Lorsque le cluster de hello n’est plus nécessaire, vous pouvez utiliser hello [suppression du groupe az](/cli/azure/group#delete) groupe de ressources tooremove hello, service de conteneur et toutes les ressources de la commande.</span><span class="sxs-lookup"><span data-stu-id="60b0d-149">When hello cluster is no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, container service, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-hello-code"></a><span data-ttu-id="60b0d-150">Obtenir le code de hello</span><span class="sxs-lookup"><span data-stu-id="60b0d-150">Get hello code</span></span>

<span data-ttu-id="60b0d-151">Dans ce démarrage rapide, les images de conteneur créés au préalable ont été toocreate utilisé un déploiement Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="60b0d-151">In this quick start, pre-created container images have been used toocreate a Kubernetes deployment.</span></span> <span data-ttu-id="60b0d-152">Hello liées code d’application, fichier Dockerfile, et les fichiers manifeste Kubernetes sont disponibles sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="60b0d-152">hello related application code, Dockerfile, and Kubernetes manifest file are available on GitHub.</span></span>

[<span data-ttu-id="60b0d-153">https://github.com/Azure-Samples/azure-voting-app-redis</span><span class="sxs-lookup"><span data-stu-id="60b0d-153">https://github.com/Azure-Samples/azure-voting-app-redis</span></span>](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a><span data-ttu-id="60b0d-154">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="60b0d-154">Next steps</span></span>

<span data-ttu-id="60b0d-155">Dans ce guide de démarrage rapide, vous déployé un cluster Kubernetes et déployé une application conteneur multiples de tooit.</span><span class="sxs-lookup"><span data-stu-id="60b0d-155">In this quick start, you deployed a Kubernetes cluster and deployed a multi-container application tooit.</span></span> 

<span data-ttu-id="60b0d-156">toolearn en savoir plus sur le Service de conteneur Azure et parcourir un exemple de toodeployment de code complet, continuer le didacticiel de cluster toohello Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="60b0d-156">toolearn more about Azure Container Service, and walk through a complete code toodeployment example, continue toohello Kubernetes cluster tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="60b0d-157">Gérer un cluster Kubernetes ACS</span><span class="sxs-lookup"><span data-stu-id="60b0d-157">Manage an ACS Kubernetes cluster</span></span>](./container-service-tutorial-kubernetes-prepare-app.md)
