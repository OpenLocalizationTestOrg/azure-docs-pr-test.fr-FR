---
title: "Démarrage rapide : Cluster Azure Kubernetes pour Linux | Microsoft Docs"
description: "Découvrez rapidement comment créer un cluster Kubernetes pour des conteneurs Linux dans Azure Container Service, avec Azure CLI."
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
ms.openlocfilehash: 5a2131659903e79b28f4d1b795d25a31d8d4ce8d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-kubernetes-cluster-for-linux-containers"></a><span data-ttu-id="bd9c9-103">Déployer un cluster Azure Kubernetes pour des conteneurs Linux</span><span class="sxs-lookup"><span data-stu-id="bd9c9-103">Deploy Kubernetes cluster for Linux containers</span></span>

<span data-ttu-id="bd9c9-104">Dans ce guide de démarrage rapide, un cluster Kubernetes est déployé à l’aide de l’interface CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="bd9c9-104">In this quick start, a Kubernetes cluster is deployed using the Azure CLI.</span></span> <span data-ttu-id="bd9c9-105">Une application à plusieurs conteneurs composée d’un serveur web frontal et d’une instance Redis est ensuite déployée, puis exécutée sur le cluster.</span><span class="sxs-lookup"><span data-stu-id="bd9c9-105">A multi-container application consisting of web front end and a Redis instance is then deployed and run on the cluster.</span></span> <span data-ttu-id="bd9c9-106">Ceci fait, l’application est accessible via internet.</span><span class="sxs-lookup"><span data-stu-id="bd9c9-106">Once completed, the application is accessible over the internet.</span></span> 

<span data-ttu-id="bd9c9-107">L’exemple d’application utilisé dans ce document est écrit en Python.</span><span class="sxs-lookup"><span data-stu-id="bd9c9-107">The example application used in this document is written in Python.</span></span> <span data-ttu-id="bd9c9-108">Les concepts et étapes décrits dans cet article sont utilisables pour le déploiement de toute image conteneur dans un cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="bd9c9-108">The concepts and steps detailed here can be used to deploy any container image into a Kubernetes cluster.</span></span> <span data-ttu-id="bd9c9-109">Le code, le fichier Dockerfile et les fichiers manifestes Kubernetes préalablement créés qui sont associés à ce projet sont disponibles sur [GitHub](https://github.com/Azure-Samples/azure-voting-app-redis.git).</span><span class="sxs-lookup"><span data-stu-id="bd9c9-109">The code, Dockerfile, and pre-created Kubernetes manifest files related to this project are available on [GitHub](https://github.com/Azure-Samples/azure-voting-app-redis.git).</span></span>

![Image de la navigation vers Azure Vote](media/container-service-kubernetes-walkthrough/azure-vote.png)

<span data-ttu-id="bd9c9-111">Ce guide de démarrage rapide suppose une compréhension élémentaire des concepts de Kubernetes. Pour en savoir plus, consultez la [documentation Kubernetes ]( https://kubernetes.io/docs/home/).</span><span class="sxs-lookup"><span data-stu-id="bd9c9-111">This quick start assumes a basic understanding of Kubernetes concepts, for detailed information on Kubernetes see the [Kubernetes documentation]( https://kubernetes.io/docs/home/).</span></span>

<span data-ttu-id="bd9c9-112">Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="bd9c9-112">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="bd9c9-113">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0.4 ou une version ultérieure pour poursuivre la procédure décrite dans ce guide de démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="bd9c9-113">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="bd9c9-114">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="bd9c9-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="bd9c9-115">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="bd9c9-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="bd9c9-116">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="bd9c9-116">Create a resource group</span></span>

<span data-ttu-id="bd9c9-117">Créez un groupe de ressources avec la commande [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="bd9c9-117">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="bd9c9-118">Un groupe de ressources Azure est un groupe logique dans lequel des ressources Azure sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="bd9c9-118">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="bd9c9-119">L’exemple suivant crée un groupe de ressources nommé *myResourceGroup* à l’emplacement *westeurope*.</span><span class="sxs-lookup"><span data-stu-id="bd9c9-119">The following example creates a resource group named *myResourceGroup* in the *westeurope* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="bd9c9-120">Output:</span><span class="sxs-lookup"><span data-stu-id="bd9c9-120">Output:</span></span>

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

## <a name="create-kubernetes-cluster"></a><span data-ttu-id="bd9c9-121">Créer un cluster Kubernetes</span><span class="sxs-lookup"><span data-stu-id="bd9c9-121">Create Kubernetes cluster</span></span>

<span data-ttu-id="bd9c9-122">Pour créer un cluster Kubernetes dans Azure Container Service, utilisez la commande [az acs create](/cli/azure/acs#create).</span><span class="sxs-lookup"><span data-stu-id="bd9c9-122">Create a Kubernetes cluster in Azure Container Service with the [az acs create](/cli/azure/acs#create) command.</span></span> <span data-ttu-id="bd9c9-123">L’exemple ci-après permet de créer un cluster nommé *myK8sCluster*, qui inclut un nœud maître Linux et trois nœuds agents Linux.</span><span class="sxs-lookup"><span data-stu-id="bd9c9-123">The following example creates a cluster named *myK8sCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive 
az acs create --orchestrator-type kubernetes --resource-group myResourceGroup --name myK8sCluster --generate-ssh-keys 
```

<span data-ttu-id="bd9c9-124">Au bout de quelques minutes, la commande se termine et retourne des informations formatées Json sur le cluster.</span><span class="sxs-lookup"><span data-stu-id="bd9c9-124">After several minutes, the command completes and returns json formatted information about the cluster.</span></span> 

## <a name="connect-to-the-cluster"></a><span data-ttu-id="bd9c9-125">Connexion au cluster</span><span class="sxs-lookup"><span data-stu-id="bd9c9-125">Connect to the cluster</span></span>

<span data-ttu-id="bd9c9-126">Pour gérer un cluster Kubernetes, utilisez [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), le client de ligne de commande Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="bd9c9-126">To manage a Kubernetes cluster, use [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), the Kubernetes command-line client.</span></span> 

<span data-ttu-id="bd9c9-127">Si vous utilisez Azure CloudShell, l’outil kubectl est déjà installé.</span><span class="sxs-lookup"><span data-stu-id="bd9c9-127">If you're using Azure CloudShell, kubectl is already installed.</span></span> <span data-ttu-id="bd9c9-128">Si vous souhaitez l’installer en local, vous pouvez utiliser la commande [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli).</span><span class="sxs-lookup"><span data-stu-id="bd9c9-128">If you want to install it locally, you can use the [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span></span>

<span data-ttu-id="bd9c9-129">Pour configurer kubectl afin qu’il se connecte à votre cluster Kubernetes, exécutez la commande [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials).</span><span class="sxs-lookup"><span data-stu-id="bd9c9-129">To configure kubectl to connect to your Kubernetes cluster, run the [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span> <span data-ttu-id="bd9c9-130">Cette étape télécharge les informations d’identification et configure l’interface de ligne de commande Kubernetes pour leur utilisation.</span><span class="sxs-lookup"><span data-stu-id="bd9c9-130">This step downloads credentials and configures the Kubernetes CLI to use them.</span></span>

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

<span data-ttu-id="bd9c9-131">Pour vérifier la connexion à votre cluster, utilisez la commande [kubectl get](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) pour retourner une liste des nœuds du cluster.</span><span class="sxs-lookup"><span data-stu-id="bd9c9-131">To verify the connection to your cluster, use the [kubectl get](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command to return a list of the cluster nodes.</span></span>

```azurecli-interactive
kubectl get nodes
```

<span data-ttu-id="bd9c9-132">Output:</span><span class="sxs-lookup"><span data-stu-id="bd9c9-132">Output:</span></span>

```bash
NAME                    STATUS                     AGE       VERSION
k8s-agent-14ad53a1-0    Ready                      10m       v1.6.6
k8s-agent-14ad53a1-1    Ready                      10m       v1.6.6
k8s-agent-14ad53a1-2    Ready                      10m       v1.6.6
k8s-master-14ad53a1-0   Ready,SchedulingDisabled   10m       v1.6.6
```

## <a name="run-the-application"></a><span data-ttu-id="bd9c9-133">Exécution de l'application</span><span class="sxs-lookup"><span data-stu-id="bd9c9-133">Run the application</span></span>

<span data-ttu-id="bd9c9-134">Un fichier manifeste Kubernetes définit un état souhaité pour le cluster, incluant les images conteneur à exécuter.</span><span class="sxs-lookup"><span data-stu-id="bd9c9-134">A Kubernetes manifest file defines a desired state for the cluster, including what container images should be running.</span></span> <span data-ttu-id="bd9c9-135">Dans cet exemple, un manifeste est utilisé afin de créer tous les objets nécessaires pour l’exécution de l’application Azure Vote.</span><span class="sxs-lookup"><span data-stu-id="bd9c9-135">For this example, a manifest is used to create all objects needed to run the Azure Vote application.</span></span> 

<span data-ttu-id="bd9c9-136">Créez un fichier nommé `azure-vote.yml` et copiez-y le YAML suivant.</span><span class="sxs-lookup"><span data-stu-id="bd9c9-136">Create a file named `azure-vote.yml` and copy into it the following YAML.</span></span> <span data-ttu-id="bd9c9-137">Si vous travaillez dans Azure Cloud Shell, vous pouvez créer ce fichier à l’aide de vi ou de Nano comme si vous travailliez sur un système virtuel ou physique.</span><span class="sxs-lookup"><span data-stu-id="bd9c9-137">If you are working in Azure Cloud Shell, this file can be created using vi or Nano as if working on a virtual or physical system.</span></span>

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

<span data-ttu-id="bd9c9-138">Utilisez la commande [kubectl create](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) pour exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="bd9c9-138">Use the [kubectl create](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) command to run the application.</span></span>

```azurecli-interactive
kubectl create -f azure-vote.yml
```

<span data-ttu-id="bd9c9-139">Output:</span><span class="sxs-lookup"><span data-stu-id="bd9c9-139">Output:</span></span>

```bash
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-the-application"></a><span data-ttu-id="bd9c9-140">Test de l'application</span><span class="sxs-lookup"><span data-stu-id="bd9c9-140">Test the application</span></span>

<span data-ttu-id="bd9c9-141">Lorsque l’application est exécutée, un [service Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/) est créé, qui expose le serveur frontal de l’application à internet.</span><span class="sxs-lookup"><span data-stu-id="bd9c9-141">As the application is run, a [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) is created that exposes the application front end to the internet.</span></span> <span data-ttu-id="bd9c9-142">L’exécution de ce processus peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="bd9c9-142">This process can take a few minutes to complete.</span></span> 

<span data-ttu-id="bd9c9-143">Pour surveiller la progression, utilisez la commande [kubectl get service](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) avec l’argument `--watch`.</span><span class="sxs-lookup"><span data-stu-id="bd9c9-143">To monitor progress, use the [kubectl get service](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command with the `--watch` argument.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front --watch
```

<span data-ttu-id="bd9c9-144">Au début, **EXTERNAL-IP** pour le service *azure-vote-front* apparaît *En attente*.</span><span class="sxs-lookup"><span data-stu-id="bd9c9-144">Initially the **EXTERNAL-IP** for the *azure-vote-front* service appears as *pending*.</span></span> <span data-ttu-id="bd9c9-145">Une fois que l’adresse IP externe est passée du statut *En attente* à *Adresse IP*, utilisez `CTRL-C` pour arrêter le processus de surveillance kubectl.</span><span class="sxs-lookup"><span data-stu-id="bd9c9-145">Once the EXTERNAL-IP address has changed from *pending* to an *IP address*, use `CTRL-C` to stop the kubectl watch process.</span></span> 
  
```bash
azure-vote-front   10.0.34.242   <pending>     80:30676/TCP   7s
azure-vote-front   10.0.34.242   52.179.23.131   80:30676/TCP   2m
```

<span data-ttu-id="bd9c9-146">Vous pouvez désormais accéder à l’adresse IP externe pour voir l’application Azure Vote.</span><span class="sxs-lookup"><span data-stu-id="bd9c9-146">You can now browse to the external IP address to see the Azure Vote App.</span></span>

![Image de la navigation vers Azure Vote](media/container-service-kubernetes-walkthrough/azure-vote.png)  

## <a name="delete-cluster"></a><span data-ttu-id="bd9c9-148">Supprimer un cluster</span><span class="sxs-lookup"><span data-stu-id="bd9c9-148">Delete cluster</span></span>
<span data-ttu-id="bd9c9-149">Lorsque vous n’avez plus besoin du cluster, vous pouvez utiliser la commande [az group delete](/cli/azure/group#delete) pour supprimer le groupe de ressources, le service de conteneur et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="bd9c9-149">When the cluster is no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, container service, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-the-code"></a><span data-ttu-id="bd9c9-150">Obtenir le code</span><span class="sxs-lookup"><span data-stu-id="bd9c9-150">Get the code</span></span>

<span data-ttu-id="bd9c9-151">Dans ce guide de démarrage rapide, les images de conteneur, créées au préalable, ont été utilisées pour créer un déploiement Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="bd9c9-151">In this quick start, pre-created container images have been used to create a Kubernetes deployment.</span></span> <span data-ttu-id="bd9c9-152">Le code de l’application associé, Dockerfile, et le fichier manifeste Kubernetes sont disponibles sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="bd9c9-152">The related application code, Dockerfile, and Kubernetes manifest file are available on GitHub.</span></span>

[<span data-ttu-id="bd9c9-153">https://github.com/Azure-Samples/azure-voting-app-redis</span><span class="sxs-lookup"><span data-stu-id="bd9c9-153">https://github.com/Azure-Samples/azure-voting-app-redis</span></span>](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a><span data-ttu-id="bd9c9-154">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bd9c9-154">Next steps</span></span>

<span data-ttu-id="bd9c9-155">Dans ce guide de démarrage rapide, vous avez déployé un cluster Kubernetes et vous y avez déployé une application de plusieurs conteneurs.</span><span class="sxs-lookup"><span data-stu-id="bd9c9-155">In this quick start, you deployed a Kubernetes cluster and deployed a multi-container application to it.</span></span> 

<span data-ttu-id="bd9c9-156">Pour en savoir plus sur Azure Container Service et parcourir le code complet de l’exemple de déploiement, passez au didacticiel sur le cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="bd9c9-156">To learn more about Azure Container Service, and walk through a complete code to deployment example, continue to the Kubernetes cluster tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bd9c9-157">Gérer un cluster Kubernetes ACS</span><span class="sxs-lookup"><span data-stu-id="bd9c9-157">Manage an ACS Kubernetes cluster</span></span>](./container-service-tutorial-kubernetes-prepare-app.md)
