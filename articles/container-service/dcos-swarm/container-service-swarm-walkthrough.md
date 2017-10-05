---
title: "Démarrage rapide : Cluster Azure Docker Swarm pour Linux | Microsoft Docs"
description: "Découvrez rapidement comment créer un cluster Docker Swarm pour des conteneurs Linux dans Azure Container Service, avec Azure CLI."
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service, Docker, Swarm
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/14/2017
ms.author: nepeters
ms.custom: 
ms.openlocfilehash: 1d10c347795227ed056a95d1bcd4aff82af7b876
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-docker-swarm-cluster"></a><span data-ttu-id="81115-103">Déployer le cluster Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="81115-103">Deploy Docker Swarm cluster</span></span>

<span data-ttu-id="81115-104">Dans ce guide de démarrage rapide, un cluster Docker Swarm est déployé à l’aide d’Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="81115-104">In this quick start, a Docker Swarm cluster is deployed using the Azure CLI.</span></span> <span data-ttu-id="81115-105">Une application à plusieurs conteneurs composée d’un serveur web frontal et d’une instance Redis est ensuite déployée, puis exécutée sur le cluster.</span><span class="sxs-lookup"><span data-stu-id="81115-105">A multi-container application consisting of web front end and a Redis instance is then deployed and run on the cluster.</span></span> <span data-ttu-id="81115-106">Ceci fait, l’application est accessible via internet.</span><span class="sxs-lookup"><span data-stu-id="81115-106">Once completed, the application is accessible over the internet.</span></span>

<span data-ttu-id="81115-107">Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="81115-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="81115-108">Ce guide de démarrage rapide nécessite que vous exécutiez Azure CLI version 2.0.4 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="81115-108">This quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="81115-109">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="81115-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="81115-110">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="81115-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="81115-111">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="81115-111">Create a resource group</span></span>

<span data-ttu-id="81115-112">Créez un groupe de ressources avec la commande [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="81115-112">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="81115-113">Un groupe de ressources Azure est un groupe logique dans lequel des ressources Azure sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="81115-113">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="81115-114">L’exemple suivant crée un groupe de ressources nommé *myResourceGroup* à l’emplacement *westus*.</span><span class="sxs-lookup"><span data-stu-id="81115-114">The following example creates a resource group named *myResourceGroup* in the *westus* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="81115-115">Output:</span><span class="sxs-lookup"><span data-stu-id="81115-115">Output:</span></span>

```json
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup",
  "location": "westcentralus",
  "managedBy": null,
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-docker-swarm-cluster"></a><span data-ttu-id="81115-116">Créer le cluster Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="81115-116">Create Docker Swarm cluster</span></span>

<span data-ttu-id="81115-117">Pour créer un cluster Docker Swarm dans Azure Container Service, utilisez la commande [az acs create](/cli/azure/acs#create).</span><span class="sxs-lookup"><span data-stu-id="81115-117">Create a Docker Swarm cluster in Azure Container Service with the [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="81115-118">L’exemple ci-après permet de créer un cluster nommé *mySwarmCluster*, qui inclut un nœud maître Linux et trois nœuds agents Linux.</span><span class="sxs-lookup"><span data-stu-id="81115-118">The following example creates a cluster named *mySwarmCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive
az acs create --name mySwarmCluster --orchestrator-type Swarm --resource-group myResourceGroup --generate-ssh-keys
```

<span data-ttu-id="81115-119">Au bout de quelques minutes, la commande se termine et retourne des informations formatées Json sur le cluster.</span><span class="sxs-lookup"><span data-stu-id="81115-119">After several minutes, the command completes and returns json formatted information about the cluster.</span></span>

## <a name="connect-to-the-cluster"></a><span data-ttu-id="81115-120">Connexion au cluster</span><span class="sxs-lookup"><span data-stu-id="81115-120">Connect to the cluster</span></span>

<span data-ttu-id="81115-121">Pour suivre ce guide de démarrage rapide, vous avez besoin de l’adresse IP du nœud maître Docker Swarm et du pool d’agents Docker.</span><span class="sxs-lookup"><span data-stu-id="81115-121">Throughout this quick start, you need the IP address of both the Docker Swarm master and the Docker agent pool.</span></span> <span data-ttu-id="81115-122">Exécutez la commande suivante pour retourner les deux adresses IP.</span><span class="sxs-lookup"><span data-stu-id="81115-122">Run the following command to return both IP addresses.</span></span>


```bash
az network public-ip list --resource-group myResourceGroup --query '[*].{Name:name,IPAddress:ipAddress}' -o table
```

<span data-ttu-id="81115-123">Output:</span><span class="sxs-lookup"><span data-stu-id="81115-123">Output:</span></span>

```bash
Name                                                                 IPAddress
-------------------------------------------------------------------  -------------
swarmm-agent-ip-myswarmcluster-myresourcegroup-d5b9d4agent-66066781  52.179.23.131
swarmm-master-ip-myswarmcluster-myresourcegroup-d5b9d4mgmt-66066781  52.141.37.199
```

<span data-ttu-id="81115-124">Créez un tunnel SSH vers le nœud maître Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="81115-124">Create an SSH tunnel to the Swarm master.</span></span> <span data-ttu-id="81115-125">Remplacez `IPAddress` par l’adresse IP du nœud maître Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="81115-125">Replace `IPAddress` with the IP address of the Swarm master.</span></span>

```bash
ssh -p 2200 -fNL 2375:localhost:2375 azureuser@IPAddress
```

<span data-ttu-id="81115-126">Définissez la variable d’environnement `DOCKER_HOST`.</span><span class="sxs-lookup"><span data-stu-id="81115-126">Set the `DOCKER_HOST` environment variable.</span></span> <span data-ttu-id="81115-127">Ceci vous permet d’exécuter des commandes docker pour le Docker Swarm sans avoir à spécifier le nom de l’hôte.</span><span class="sxs-lookup"><span data-stu-id="81115-127">This allows you to run docker commands against the Docker Swarm without having to specify the name of the host.</span></span>

```bash
export DOCKER_HOST=:2375
```

<span data-ttu-id="81115-128">Vous êtes maintenant prêt à exécuter les services Docker sur le Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="81115-128">You are now ready to run Docker services on the Docker Swarm.</span></span>


## <a name="run-the-application"></a><span data-ttu-id="81115-129">Exécution de l'application</span><span class="sxs-lookup"><span data-stu-id="81115-129">Run the application</span></span>

<span data-ttu-id="81115-130">Créez un fichier nommé `docker-compose.yaml`, puis copiez-y le contenu suivant.</span><span class="sxs-lookup"><span data-stu-id="81115-130">Create a file named `docker-compose.yaml` and copy the following content into it.</span></span>

```yaml
version: '3'
services:
  azure-vote-back:
    image: redis
    container_name: azure-vote-back
    ports:
        - "6379:6379"

  azure-vote-front:
    image: microsoft/azure-vote-front:redis-v1
    container_name: azure-vote-front
    environment:
      REDIS: azure-vote-back
    ports:
        - "80:80"
```

<span data-ttu-id="81115-131">Exécutez la commande ci-dessous pour créer le service Azure Vote.</span><span class="sxs-lookup"><span data-stu-id="81115-131">Run the following command to create the Azure Vote service.</span></span>

```bash
docker-compose up -d
```

<span data-ttu-id="81115-132">Output:</span><span class="sxs-lookup"><span data-stu-id="81115-132">Output:</span></span>

```bash
Creating network "user_default" with the default driver
Pulling azure-vote-front (microsoft/azure-vote-front:redis-v1)...
swarm-agent-EE873B23000005: Pulling microsoft/azure-vote-front:redis-v1...
swarm-agent-EE873B23000004: Pulling microsoft/azure-vote-front:redis-v1... : downloaded
Pulling azure-vote-back (redis:latest)...
swarm-agent-EE873B23000004: Pulling redis:latest... : downloaded
Creating azure-vote-front ... 
Creating azure-vote-back ... 
Creating azure-vote-front
Creating azure-vote-back ...
```

## <a name="test-the-application"></a><span data-ttu-id="81115-133">Test de l'application</span><span class="sxs-lookup"><span data-stu-id="81115-133">Test the application</span></span>

<span data-ttu-id="81115-134">Naviguez dans l’adresse IP du pool d’agents Swarm pour tester l’application Azure Vote.</span><span class="sxs-lookup"><span data-stu-id="81115-134">Browse to the IP address of the Swarm agent pool to test out the Azure Vote application.</span></span>

![Image de la navigation vers Azure Vote](media/container-service-docker-swarm-mode-walkthrough/azure-vote.png)

## <a name="delete-cluster"></a><span data-ttu-id="81115-136">Supprimer un cluster</span><span class="sxs-lookup"><span data-stu-id="81115-136">Delete cluster</span></span>
<span data-ttu-id="81115-137">Lorsque vous n’avez plus besoin du cluster, vous pouvez utiliser la commande [az group delete](/cli/azure/group#delete) pour supprimer le groupe de ressources, le service de conteneur et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="81115-137">When the cluster is no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, container service, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-the-code"></a><span data-ttu-id="81115-138">Obtenir le code</span><span class="sxs-lookup"><span data-stu-id="81115-138">Get the code</span></span>

<span data-ttu-id="81115-139">Dans ce guide de démarrage rapide, des images de conteneur créées au préalable ont été utilisées pour créer un service Docker.</span><span class="sxs-lookup"><span data-stu-id="81115-139">In this quick start, pre-created container images have been used to create a Docker service.</span></span> <span data-ttu-id="81115-140">Le code de l’application associé, Dockerfile, et le fichier Compose sont disponibles sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="81115-140">The related application code, Dockerfile, and Compose file are available on GitHub.</span></span>

[<span data-ttu-id="81115-141">https://github.com/Azure-Samples/azure-voting-app-redis</span><span class="sxs-lookup"><span data-stu-id="81115-141">https://github.com/Azure-Samples/azure-voting-app-redis</span></span>](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a><span data-ttu-id="81115-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="81115-142">Next steps</span></span>

<span data-ttu-id="81115-143">Dans ce guide de démarrage rapide, vous avez déployé un cluster Docker Swarm et vous y avez déployé une application de plusieurs conteneurs.</span><span class="sxs-lookup"><span data-stu-id="81115-143">In this quick start, you deployed a Docker Swarm cluster and deployed a multi-container application to it.</span></span>

<span data-ttu-id="81115-144">Pour en savoir plus sur l’intégration de Docker Swarm avec Visual Studio Team Services, passez à la section CI/CD avec Docker Swarm et VSTS.</span><span class="sxs-lookup"><span data-stu-id="81115-144">To learn about integrating Docker warm with Visual Studio Team Services, continue to the CI/CD with Docker Swarm and VSTS.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="81115-145">CI/CD avec Docker Swarm et VSTS</span><span class="sxs-lookup"><span data-stu-id="81115-145">CI/CD with Docker Swarm and VSTS</span></span>](./container-service-docker-swarm-setup-ci-cd.md)