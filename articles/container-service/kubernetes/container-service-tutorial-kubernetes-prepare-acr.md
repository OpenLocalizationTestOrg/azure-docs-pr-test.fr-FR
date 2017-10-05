---
title: "Didacticiel Azure Container Service - Préparer l’ACR | Microsoft Docs"
description: "Didacticiel Azure Container Service - Préparer l’ACR"
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
ms.openlocfilehash: 3e1f7617bf2fc52ee4c15598f51a46276f4dc57d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-and-use-azure-container-registry"></a><span data-ttu-id="6d54e-104">Déployer et utiliser Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="6d54e-104">Deploy and use Azure Container Registry</span></span>

<span data-ttu-id="6d54e-105">Azure Container Registry (ACR) est un registre privé Azure pour les images de conteneur Docker.</span><span class="sxs-lookup"><span data-stu-id="6d54e-105">Azure Container Registry (ACR) is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="6d54e-106">Ce didacticiel (le deuxième d’une série de sept) vous aide à déployer une instance Azure Container Registry et à envoyer une image conteneur à ce dernier.</span><span class="sxs-lookup"><span data-stu-id="6d54e-106">This tutorial, part two of seven, walks through deploying an Azure Container Registry instance, and pushing a container image to it.</span></span> <span data-ttu-id="6d54e-107">Les étapes terminées sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="6d54e-107">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6d54e-108">Déploiement d’une instance Azure Container Registry (ACR)</span><span class="sxs-lookup"><span data-stu-id="6d54e-108">Deploying an Azure Container Registry (ACR) instance</span></span>
> * <span data-ttu-id="6d54e-109">Marquage d’une image conteneur pour ACR</span><span class="sxs-lookup"><span data-stu-id="6d54e-109">Tagging a container image for ACR</span></span>
> * <span data-ttu-id="6d54e-110">Chargement de l’image dans ACR</span><span class="sxs-lookup"><span data-stu-id="6d54e-110">Uploading the image to ACR</span></span>

<span data-ttu-id="6d54e-111">Dans les didacticiels suivants, cette instance ACR est intégrée à un cluster Azure Container Service Kubernetes, pour l’exécution des images de conteneur en toute sécurité.</span><span class="sxs-lookup"><span data-stu-id="6d54e-111">In subsequent tutorials, this ACR instance is integrated with an Azure Container Service Kubernetes cluster, for securely running container images.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="6d54e-112">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="6d54e-112">Before you begin</span></span>

<span data-ttu-id="6d54e-113">Dans le [didacticiel précédent](./container-service-tutorial-kubernetes-prepare-app.md), une image conteneur a été créée pour une application Azure Vote.</span><span class="sxs-lookup"><span data-stu-id="6d54e-113">In the [previous tutorial](./container-service-tutorial-kubernetes-prepare-app.md), a container image was created for a simple Azure Voting application.</span></span> <span data-ttu-id="6d54e-114">Dans ce didacticiel, cette image est envoyée à Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="6d54e-114">In this tutorial, this image is pushed to an Azure Container Registry.</span></span> <span data-ttu-id="6d54e-115">Si vous n’avez pas créé l’image de l’application Azure Vote, retournez au [Didacticiel 1 : Créer des images conteneur](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="6d54e-115">If you have not created the Azure Voting app image, return to [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> <span data-ttu-id="6d54e-116">Sinon, les étapes présentées en détail ici fonctionnent avec n’importe quelle image de conteneur.</span><span class="sxs-lookup"><span data-stu-id="6d54e-116">Alternatively, the steps detailed here work with any container image.</span></span>

<span data-ttu-id="6d54e-117">Ce didacticiel nécessite que vous exécutiez Azure CLI version 2.0.4 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="6d54e-117">This tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="6d54e-118">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="6d54e-118">Run `az --version` to find the version.</span></span> <span data-ttu-id="6d54e-119">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6d54e-119">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="6d54e-120">Déployer Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="6d54e-120">Deploy Azure Container Registry</span></span>

<span data-ttu-id="6d54e-121">Lorsque vous déployez un registre de conteneurs Azure, il vous faut tout d’abord un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="6d54e-121">When deploying an Azure Container Registry, you first need a resource group.</span></span> <span data-ttu-id="6d54e-122">Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="6d54e-122">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="6d54e-123">Créez un groupe de ressources avec la commande [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="6d54e-123">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="6d54e-124">Dans cet exemple, un groupe de ressources nommé *myResourceGroupVM* est créé dans la région *westeurope*.</span><span class="sxs-lookup"><span data-stu-id="6d54e-124">In this example, a resource group named *myResourceGroup* is created in the *westeurope* region.</span></span>

```azurecli
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="6d54e-125">Créez un registre de conteneurs Azure à l’aide de la commande [az acr create](/cli/azure/acr#create).</span><span class="sxs-lookup"><span data-stu-id="6d54e-125">Create an Azure Container registry with the [az acr create](/cli/azure/acr#create) command.</span></span> <span data-ttu-id="6d54e-126">Le nom d’un registre de conteneurs **doit être unique**.</span><span class="sxs-lookup"><span data-stu-id="6d54e-126">The name of a Container Registry **must be unique**.</span></span>

```azurecli
az acr create --resource-group myResourceGroup --name <acrName> --sku Basic --admin-enabled true
```

<span data-ttu-id="6d54e-127">Dans le reste de ce didacticiel, nous utilisons « acrname ». Ce nom correspond au registre de conteneurs que vous avez choisi.</span><span class="sxs-lookup"><span data-stu-id="6d54e-127">Throughout the rest of this tutorial, we use "acrname" as a placeholder for the container registry name that you chose.</span></span>

## <a name="container-registry-login"></a><span data-ttu-id="6d54e-128">Connexion au registre de conteneurs</span><span class="sxs-lookup"><span data-stu-id="6d54e-128">Container registry login</span></span>

<span data-ttu-id="6d54e-129">Vous devez vous connecter à votre instance ACR avant de lui envoyer des images.</span><span class="sxs-lookup"><span data-stu-id="6d54e-129">You must log in to your ACR instance before pushing images to it.</span></span> <span data-ttu-id="6d54e-130">Utilisez la commande [az acr login](https://docs.microsoft.com/en-us/cli/azure/acr#login) pour terminer l’opération.</span><span class="sxs-lookup"><span data-stu-id="6d54e-130">Use the [az acr login](https://docs.microsoft.com/en-us/cli/azure/acr#login) command to complete the operation.</span></span> <span data-ttu-id="6d54e-131">Vous devez fournir le nom unique qui a été donné au Registre de conteneurs au moment de sa création.</span><span class="sxs-lookup"><span data-stu-id="6d54e-131">You need to provide the unique name given to the container registry when it was created.</span></span>

```azurecli
az acr login --name <acrName>
```

<span data-ttu-id="6d54e-132">Après son exécution, la commande retourne le message « Connexion réussie ».</span><span class="sxs-lookup"><span data-stu-id="6d54e-132">The command returns a 'Login Succeeded’ message once completed.</span></span>

## <a name="tag-container-images"></a><span data-ttu-id="6d54e-133">Marquer les images de conteneur</span><span class="sxs-lookup"><span data-stu-id="6d54e-133">Tag container images</span></span>

<span data-ttu-id="6d54e-134">Chaque image conteneur doit être marquée avec le nom de serveur de connexion du registre.</span><span class="sxs-lookup"><span data-stu-id="6d54e-134">Each container image needs to be tagged with the loginServer name of the registry.</span></span> <span data-ttu-id="6d54e-135">Cette balise est utilisée pour l’acheminement lors de l’envoi des images de conteneur dans un registre d’images.</span><span class="sxs-lookup"><span data-stu-id="6d54e-135">This tag is used for routing when pushing container images to an image registry.</span></span>

<span data-ttu-id="6d54e-136">Pour afficher la liste des images actuelles, utilisez la commande [docker images](https://docs.docker.com/engine/reference/commandline/images/).</span><span class="sxs-lookup"><span data-stu-id="6d54e-136">To see a list of current images, use the [docker images](https://docs.docker.com/engine/reference/commandline/images/) command.</span></span>

```bash
docker images
```

<span data-ttu-id="6d54e-137">Output:</span><span class="sxs-lookup"><span data-stu-id="6d54e-137">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front             latest              4675398c9172        13 minutes ago      694MB
redis                        latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask               788ca94b2313        9 months ago        694MB
```

<span data-ttu-id="6d54e-138">Pour obtenir le nom de loginServer, exécutez la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="6d54e-138">To get the loginServer name, run the following command.</span></span>

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

<span data-ttu-id="6d54e-139">Maintenant, marquez l’image *azure-vote-front* avec le loginServer du Registre de conteneurs.</span><span class="sxs-lookup"><span data-stu-id="6d54e-139">Now, tag the *azure-vote-front* image with the loginServer of the container registry.</span></span> <span data-ttu-id="6d54e-140">En outre, ajoutez `:redis-v1` à la fin du nom de l’image.</span><span class="sxs-lookup"><span data-stu-id="6d54e-140">Also, add `:redis-v1` to the end of the image name.</span></span> <span data-ttu-id="6d54e-141">Cette balise indique la version de l’image.</span><span class="sxs-lookup"><span data-stu-id="6d54e-141">This tag indicates the image version.</span></span>

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v1
```

<span data-ttu-id="6d54e-142">Une fois l’image marquée, exécutez [docker images] (https://docs.docker.com/engine/reference/commandline/images/) pour vérifier l’opération.</span><span class="sxs-lookup"><span data-stu-id="6d54e-142">Once tagged, run [docker images] (https://docs.docker.com/engine/reference/commandline/images/) to verify the operation.</span></span>

```bash
docker images
```

<span data-ttu-id="6d54e-143">Output:</span><span class="sxs-lookup"><span data-stu-id="6d54e-143">Output:</span></span>

```bash
REPOSITORY                                           TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front                                     latest              eaf2b9c57e5e        8 minutes ago       716 MB
mycontainerregistry082.azurecr.io/azure-vote-front   redis-v1            eaf2b9c57e5e        8 minutes ago       716 MB
redis                                                latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask                           flask               788ca94b2313        8 months ago        694 MB
```

## <a name="push-images-to-registry"></a><span data-ttu-id="6d54e-144">Envoyer des images au registre</span><span class="sxs-lookup"><span data-stu-id="6d54e-144">Push images to registry</span></span>

<span data-ttu-id="6d54e-145">Envoyez l’image *azure-vote-front* au registre.</span><span class="sxs-lookup"><span data-stu-id="6d54e-145">Push the *azure-vote-front* image to the registry.</span></span> 

<span data-ttu-id="6d54e-146">À l’aide de l’exemple suivant, remplacez le nom d’ACR loginServer par le loginServer à partir de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="6d54e-146">Using the following example, replace the ACR loginServer name with the loginServer from your environment.</span></span>

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v1
```

<span data-ttu-id="6d54e-147">Quelques minutes sont nécessaires pour achever l’opération.</span><span class="sxs-lookup"><span data-stu-id="6d54e-147">This takes a couple of minutes to complete.</span></span>

## <a name="list-images-in-registry"></a><span data-ttu-id="6d54e-148">Créer la liste des images du registre</span><span class="sxs-lookup"><span data-stu-id="6d54e-148">List images in registry</span></span>

<span data-ttu-id="6d54e-149">Pour retourner une liste d’images qui ont été déplacées dans le registre de conteneurs Azure, utilisez la commande [az acr repository list](/cli/azure/acr/repository#list).</span><span class="sxs-lookup"><span data-stu-id="6d54e-149">To return a list of images that have been pushed to your Azure Container registry, user the [az acr repository list](/cli/azure/acr/repository#list) command.</span></span> <span data-ttu-id="6d54e-150">Mettez à jour la commande avec le nom d’instance ACR.</span><span class="sxs-lookup"><span data-stu-id="6d54e-150">Update the command with the ACR instance name.</span></span>

```azurecli
az acr repository list --name <acrName> --output table
```

<span data-ttu-id="6d54e-151">Output:</span><span class="sxs-lookup"><span data-stu-id="6d54e-151">Output:</span></span>

```azurecli
Result
----------------
azure-vote-front
```

<span data-ttu-id="6d54e-152">Puis, pour afficher les balises d’une image spécifique, utilisez la commande [az acr repository show-tags](/cli/azure/acr/repository#show-tags).</span><span class="sxs-lookup"><span data-stu-id="6d54e-152">And then to see the tags for a specific image, use the [az acr repository show-tags](/cli/azure/acr/repository#show-tags) command.</span></span>

```azurecli
az acr repository show-tags --name <acrName> --repository azure-vote-front --output table
```

<span data-ttu-id="6d54e-153">Output:</span><span class="sxs-lookup"><span data-stu-id="6d54e-153">Output:</span></span>

```azurecli
Result
--------
redis-v1
```

<span data-ttu-id="6d54e-154">Au terme de ce didacticiel, l’image conteneur est stockée dans une instance privée Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="6d54e-154">At tutorial completion, the container image has been stored in a private Azure Container Registry instance.</span></span> <span data-ttu-id="6d54e-155">Dans les didacticiels suivants, cette image est déployée à partir d’ACR vers un cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="6d54e-155">This image is deployed from ACR to a Kubernetes cluster in subsequent tutorials.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d54e-156">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6d54e-156">Next steps</span></span>

<span data-ttu-id="6d54e-157">Dans ce didacticiel, un registre de conteneurs Azure a été préparé pour une utilisation dans un cluster ACS Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="6d54e-157">In this tutorial, an Azure Container Registry was prepared for use in an ACS Kubernetes cluster.</span></span> <span data-ttu-id="6d54e-158">Les étapes suivantes ont été effectuées :</span><span class="sxs-lookup"><span data-stu-id="6d54e-158">The following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6d54e-159">Déploiement d’une instance Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="6d54e-159">Deployed an Azure Container Registry instance</span></span>
> * <span data-ttu-id="6d54e-160">Marquage d’une image conteneur pour ACR</span><span class="sxs-lookup"><span data-stu-id="6d54e-160">Tagged a container image for ACR</span></span>
> * <span data-ttu-id="6d54e-161">Chargement de l’image dans ACR</span><span class="sxs-lookup"><span data-stu-id="6d54e-161">Uploaded the image to ACR</span></span>

<span data-ttu-id="6d54e-162">Passer à l’étape suivante du didacticiel pour en savoir plus sur le déploiement d’un cluster Kubernetes dans Azure.</span><span class="sxs-lookup"><span data-stu-id="6d54e-162">Advance to the next tutorial to learn about deploying a Kubernetes cluster in Azure.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6d54e-163">Déployer un cluster Kubernetes</span><span class="sxs-lookup"><span data-stu-id="6d54e-163">Deploy Kubernetes cluster</span></span>](./container-service-tutorial-kubernetes-deploy-cluster.md)