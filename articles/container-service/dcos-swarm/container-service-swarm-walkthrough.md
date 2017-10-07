---
title: aaaQuickstart - Swarm de Docker Azure de cluster pour Linux | Documents Microsoft
description: "En savoir plus rapidement les toocreate un cluster Docker Swarm pour les conteneurs Linux dans le conteneur de Service Azure avec hello CLI d’Azure."
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
ms.openlocfilehash: 3028d2d00585360ec163518bf98f69bb0dd44dec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-docker-swarm-cluster"></a><span data-ttu-id="0b2b3-103">Déployer le cluster Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="0b2b3-103">Deploy Docker Swarm cluster</span></span>

<span data-ttu-id="0b2b3-104">Dans ce guide de démarrage rapide, un cluster Docker Swarm est déployé à l’aide de hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="0b2b3-104">In this quick start, a Docker Swarm cluster is deployed using hello Azure CLI.</span></span> <span data-ttu-id="0b2b3-105">Une application conteneur multi composé d’un serveur web frontal et une instance de Redis est puis déployée et exécutée sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="0b2b3-105">A multi-container application consisting of web front end and a Redis instance is then deployed and run on hello cluster.</span></span> <span data-ttu-id="0b2b3-106">Une fois terminé, l’application hello est accessible sur internet de hello.</span><span class="sxs-lookup"><span data-stu-id="0b2b3-106">Once completed, hello application is accessible over hello internet.</span></span>

<span data-ttu-id="0b2b3-107">Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="0b2b3-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="0b2b3-108">Ce démarrage rapide nécessite que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="0b2b3-108">This quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="0b2b3-109">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="0b2b3-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="0b2b3-110">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="0b2b3-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="0b2b3-111">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="0b2b3-111">Create a resource group</span></span>

<span data-ttu-id="0b2b3-112">Créer un groupe de ressources avec hello [création de groupe de az](/cli/azure/group#create) commande.</span><span class="sxs-lookup"><span data-stu-id="0b2b3-112">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="0b2b3-113">Un groupe de ressources Azure est un groupe logique dans lequel des ressources Azure sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="0b2b3-113">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="0b2b3-114">Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *westus* emplacement.</span><span class="sxs-lookup"><span data-stu-id="0b2b3-114">hello following example creates a resource group named *myResourceGroup* in hello *westus* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="0b2b3-115">Output:</span><span class="sxs-lookup"><span data-stu-id="0b2b3-115">Output:</span></span>

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

## <a name="create-docker-swarm-cluster"></a><span data-ttu-id="0b2b3-116">Créer le cluster Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="0b2b3-116">Create Docker Swarm cluster</span></span>

<span data-ttu-id="0b2b3-117">Créer un cluster de Docker Swarm dans le Service de conteneur Azure avec hello [az acs créer](/cli/azure/acs#create) commande.</span><span class="sxs-lookup"><span data-stu-id="0b2b3-117">Create a Docker Swarm cluster in Azure Container Service with hello [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="0b2b3-118">Hello exemple suivant crée un cluster nommé *mySwarmCluster* avec un Linux maître nœud et trois nœuds de l’agent Linux.</span><span class="sxs-lookup"><span data-stu-id="0b2b3-118">hello following example creates a cluster named *mySwarmCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive
az acs create --name mySwarmCluster --orchestrator-type Swarm --resource-group myResourceGroup --generate-ssh-keys
```

<span data-ttu-id="0b2b3-119">Après quelques minutes, commande hello se termine et retourne des informations au format json sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="0b2b3-119">After several minutes, hello command completes and returns json formatted information about hello cluster.</span></span>

## <a name="connect-toohello-cluster"></a><span data-ttu-id="0b2b3-120">Se connecter toohello cluster</span><span class="sxs-lookup"><span data-stu-id="0b2b3-120">Connect toohello cluster</span></span>

<span data-ttu-id="0b2b3-121">Tout au long de ce guide de démarrage rapide, vous avez besoin de l’adresse IP hello principale de Docker Swarm hello et pool d’agents hello Docker.</span><span class="sxs-lookup"><span data-stu-id="0b2b3-121">Throughout this quick start, you need hello IP address of both hello Docker Swarm master and hello Docker agent pool.</span></span> <span data-ttu-id="0b2b3-122">La commande suivante d’exécution hello tooreturn les deux adresses IP.</span><span class="sxs-lookup"><span data-stu-id="0b2b3-122">Run hello following command tooreturn both IP addresses.</span></span>


```bash
az network public-ip list --resource-group myResourceGroup --query '[*].{Name:name,IPAddress:ipAddress}' -o table
```

<span data-ttu-id="0b2b3-123">Output:</span><span class="sxs-lookup"><span data-stu-id="0b2b3-123">Output:</span></span>

```bash
Name                                                                 IPAddress
-------------------------------------------------------------------  -------------
swarmm-agent-ip-myswarmcluster-myresourcegroup-d5b9d4agent-66066781  52.179.23.131
swarmm-master-ip-myswarmcluster-myresourcegroup-d5b9d4mgmt-66066781  52.141.37.199
```

<span data-ttu-id="0b2b3-124">Créer un SSH maître de tunnel toohello essaim.</span><span class="sxs-lookup"><span data-stu-id="0b2b3-124">Create an SSH tunnel toohello Swarm master.</span></span> <span data-ttu-id="0b2b3-125">Remplacez `IPAddress` avec adresse IP principale d’essaim hello hello.</span><span class="sxs-lookup"><span data-stu-id="0b2b3-125">Replace `IPAddress` with hello IP address of hello Swarm master.</span></span>

```bash
ssh -p 2200 -fNL 2375:localhost:2375 azureuser@IPAddress
```

<span data-ttu-id="0b2b3-126">Ensemble hello `DOCKER_HOST` variable d’environnement.</span><span class="sxs-lookup"><span data-stu-id="0b2b3-126">Set hello `DOCKER_HOST` environment variable.</span></span> <span data-ttu-id="0b2b3-127">Ainsi, vous toorun les commandes docker sur hello Docker Swarm sans avoir le nom de hello toospecify d’hôte de hello.</span><span class="sxs-lookup"><span data-stu-id="0b2b3-127">This allows you toorun docker commands against hello Docker Swarm without having toospecify hello name of hello host.</span></span>

```bash
export DOCKER_HOST=:2375
```

<span data-ttu-id="0b2b3-128">Vous êtes maintenant prêt toorun des services de Docker sur hello Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="0b2b3-128">You are now ready toorun Docker services on hello Docker Swarm.</span></span>


## <a name="run-hello-application"></a><span data-ttu-id="0b2b3-129">Exécutez l’application hello</span><span class="sxs-lookup"><span data-stu-id="0b2b3-129">Run hello application</span></span>

<span data-ttu-id="0b2b3-130">Créez un fichier nommé `docker-compose.yaml` et hello de copie suivant contenu dans celui-ci.</span><span class="sxs-lookup"><span data-stu-id="0b2b3-130">Create a file named `docker-compose.yaml` and copy hello following content into it.</span></span>

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

<span data-ttu-id="0b2b3-131">Exécutez hello après commande toocreate hello Azure Vote service.</span><span class="sxs-lookup"><span data-stu-id="0b2b3-131">Run hello following command toocreate hello Azure Vote service.</span></span>

```bash
docker-compose up -d
```

<span data-ttu-id="0b2b3-132">Output:</span><span class="sxs-lookup"><span data-stu-id="0b2b3-132">Output:</span></span>

```bash
Creating network "user_default" with hello default driver
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

## <a name="test-hello-application"></a><span data-ttu-id="0b2b3-133">Tester l’application hello</span><span class="sxs-lookup"><span data-stu-id="0b2b3-133">Test hello application</span></span>

<span data-ttu-id="0b2b3-134">Parcourir l’adresse IP toohello hello essaim agent pool tootest d’application Azure Vote hello.</span><span class="sxs-lookup"><span data-stu-id="0b2b3-134">Browse toohello IP address of hello Swarm agent pool tootest out hello Azure Vote application.</span></span>

![Image de navigation tooAzure Vote](media/container-service-docker-swarm-mode-walkthrough/azure-vote.png)

## <a name="delete-cluster"></a><span data-ttu-id="0b2b3-136">Supprimer un cluster</span><span class="sxs-lookup"><span data-stu-id="0b2b3-136">Delete cluster</span></span>
<span data-ttu-id="0b2b3-137">Lorsque le cluster de hello n’est plus nécessaire, vous pouvez utiliser hello [suppression du groupe az](/cli/azure/group#delete) groupe de ressources tooremove hello, service de conteneur et toutes les ressources de la commande.</span><span class="sxs-lookup"><span data-stu-id="0b2b3-137">When hello cluster is no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, container service, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-hello-code"></a><span data-ttu-id="0b2b3-138">Obtenir le code de hello</span><span class="sxs-lookup"><span data-stu-id="0b2b3-138">Get hello code</span></span>

<span data-ttu-id="0b2b3-139">Dans ce guide de démarrage rapide, les images de conteneur précréés ont été toocreate utilisé un service de Docker.</span><span class="sxs-lookup"><span data-stu-id="0b2b3-139">In this quick start, pre-created container images have been used toocreate a Docker service.</span></span> <span data-ttu-id="0b2b3-140">Hello liés le code d’application, fichier Dockerfile, et le fichier de message sont disponibles sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="0b2b3-140">hello related application code, Dockerfile, and Compose file are available on GitHub.</span></span>

[<span data-ttu-id="0b2b3-141">https://github.com/Azure-Samples/azure-voting-app-redis</span><span class="sxs-lookup"><span data-stu-id="0b2b3-141">https://github.com/Azure-Samples/azure-voting-app-redis</span></span>](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a><span data-ttu-id="0b2b3-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0b2b3-142">Next steps</span></span>

<span data-ttu-id="0b2b3-143">Dans ce guide de démarrage rapide, vous déployé un cluster Docker Swarm et déployé une application conteneur multiples de tooit.</span><span class="sxs-lookup"><span data-stu-id="0b2b3-143">In this quick start, you deployed a Docker Swarm cluster and deployed a multi-container application tooit.</span></span>

<span data-ttu-id="0b2b3-144">toolearn sur l’intégration de Docker à chaud avec Visual Studio Team Services, continuer toohello CI/CD avec Docker Swarm et VSTS.</span><span class="sxs-lookup"><span data-stu-id="0b2b3-144">toolearn about integrating Docker warm with Visual Studio Team Services, continue toohello CI/CD with Docker Swarm and VSTS.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0b2b3-145">CI/CD avec Docker Swarm et VSTS</span><span class="sxs-lookup"><span data-stu-id="0b2b3-145">CI/CD with Docker Swarm and VSTS</span></span>](./container-service-docker-swarm-setup-ci-cd.md)