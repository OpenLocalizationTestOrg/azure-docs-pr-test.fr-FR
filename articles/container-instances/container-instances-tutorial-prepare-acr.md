---
title: "Didacticiel Azure Container Instances - Préparer Azure Container Registry | Microsoft Docs"
description: "Didacticiel Azure Container Instances - Préparer Azure Container Registry"
services: container-instances
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, conteneurs, microservices, Kubernetes, DC/OS, Azure
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: cc96ba9f5abd45a7503ba3327b30e1f809391384
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-and-use-azure-container-registry"></a><span data-ttu-id="a34a6-104">Déployer et utiliser Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="a34a6-104">Deploy and use Azure Container Registry</span></span>

<span data-ttu-id="a34a6-105">Il s’agit de la deuxième partie d’un didacticiel en trois parties.</span><span class="sxs-lookup"><span data-stu-id="a34a6-105">This is part two of a three-part tutorial.</span></span> <span data-ttu-id="a34a6-106">À l’[étape précédente](./container-instances-tutorial-prepare-app.md), nous avons créé une image conteneur pour une application web simple écrite en [Node.js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="a34a6-106">In the [previous step](./container-instances-tutorial-prepare-app.md), a container image was created for a simple web application written in [Node.js](http://nodejs.org).</span></span> <span data-ttu-id="a34a6-107">Dans ce didacticiel, nous allons envoyer cette image à Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="a34a6-107">In this tutorial, this image is pushed to an Azure Container Registry.</span></span> <span data-ttu-id="a34a6-108">Si vous n’avez pas créé l’image de conteneur, retournez au [Didacticiel 1 : Créer une image conteneur](./container-instances-tutorial-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="a34a6-108">If you have not created the container image, return to [Tutorial 1 – Create container image](./container-instances-tutorial-prepare-app.md).</span></span> 

<span data-ttu-id="a34a6-109">Azure Container Registry est un registre privé Azure pour les images conteneur Docker.</span><span class="sxs-lookup"><span data-stu-id="a34a6-109">The Azure Container Registry is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="a34a6-110">Ce didacticiel explique comment déployer une instance Azure Container Registry et lui envoyer une image conteneur.</span><span class="sxs-lookup"><span data-stu-id="a34a6-110">This tutorial walks through deploying an Azure Container Registry instance, and pushing a container image to it.</span></span> <span data-ttu-id="a34a6-111">Les étapes accomplies sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="a34a6-111">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a34a6-112">Déploiement d’une instance Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="a34a6-112">Deploying an Azure Container Registry instance</span></span>
> * <span data-ttu-id="a34a6-113">Balisage d’image conteneur pour Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="a34a6-113">Tagging container image for Azure Container Registry</span></span>
> * <span data-ttu-id="a34a6-114">Chargement d’image dans Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="a34a6-114">Uploading image to Azure Container Registry</span></span>

<span data-ttu-id="a34a6-115">Dans les didacticiels suivants vous déploierez le conteneur de votre Registre privé vers Azure Container Instances.</span><span class="sxs-lookup"><span data-stu-id="a34a6-115">In subsequent tutorials, you deploy the container from your private registry to Azure Container Instances.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a34a6-116">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="a34a6-116">Before you begin</span></span>

<span data-ttu-id="a34a6-117">Ce didacticiel nécessite que vous exécutiez Azure CLI version 2.0.4 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="a34a6-117">This tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="a34a6-118">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="a34a6-118">Run `az --version` to find the version.</span></span> <span data-ttu-id="a34a6-119">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a34a6-119">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="a34a6-120">Déployer Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="a34a6-120">Deploy Azure Container Registry</span></span>

<span data-ttu-id="a34a6-121">Lorsque vous déployez un registre de conteneurs Azure, il vous faut tout d’abord un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="a34a6-121">When deploying an Azure Container Registry, you first need a resource group.</span></span> <span data-ttu-id="a34a6-122">Un groupe de ressources Azure est une collection logique dans laquelle des ressources Azure sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="a34a6-122">An Azure resource group is a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="a34a6-123">Créez un groupe de ressources avec la commande [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="a34a6-123">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="a34a6-124">Dans cet exemple, un groupe de ressources nommé *myResourceGroupVM* est créé dans la région *eastus*.</span><span class="sxs-lookup"><span data-stu-id="a34a6-124">In this example, a resource group named *myResourceGroup* is created in the *eastus* region.</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="a34a6-125">Créez un registre de conteneurs Azure à l’aide de la commande [az acr create](/cli/azure/acr#create).</span><span class="sxs-lookup"><span data-stu-id="a34a6-125">Create an Azure Container registry with the [az acr create](/cli/azure/acr#create) command.</span></span> <span data-ttu-id="a34a6-126">Le nom d’un registre de conteneurs **doit être unique**.</span><span class="sxs-lookup"><span data-stu-id="a34a6-126">The name of a Container Registry **must be unique**.</span></span> <span data-ttu-id="a34a6-127">Dans l’exemple suivant, nous utilisons le nom *mycontainerregistry082*.</span><span class="sxs-lookup"><span data-stu-id="a34a6-127">In the following example, we use the name *mycontainerregistry082*.</span></span>

```azurecli
az acr create --resource-group myResourceGroup --name mycontainerregistry082 --sku Basic --admin-enabled true
```

<span data-ttu-id="a34a6-128">Dans le reste de ce didacticiel, nous utilisons `<acrname>`. Ce nom correspond au registre de conteneurs que vous avez choisi.</span><span class="sxs-lookup"><span data-stu-id="a34a6-128">Throughout the rest of this tutorial, we use `<acrname>` as a placeholder for the container registry name that you chose.</span></span>

## <a name="container-registry-login"></a><span data-ttu-id="a34a6-129">Connexion au registre de conteneurs</span><span class="sxs-lookup"><span data-stu-id="a34a6-129">Container registry login</span></span>

<span data-ttu-id="a34a6-130">Vous devez vous connecter à votre instance ACR avant de lui envoyer des images.</span><span class="sxs-lookup"><span data-stu-id="a34a6-130">You must log in to your ACR instance before pushing images to it.</span></span> <span data-ttu-id="a34a6-131">Utilisez la commande [az acr login](https://docs.microsoft.com/en-us/cli/azure/acr#login) pour terminer l’opération.</span><span class="sxs-lookup"><span data-stu-id="a34a6-131">Use the [az acr login](https://docs.microsoft.com/en-us/cli/azure/acr#login) command to complete the operation.</span></span> <span data-ttu-id="a34a6-132">Vous devez fournir le nom unique qui a été donné au Registre de conteneurs au moment de sa création.</span><span class="sxs-lookup"><span data-stu-id="a34a6-132">You need to provide the unique name given to the container registry when it was created.</span></span>

```azurecli
az acr login --name <acrName>
```

<span data-ttu-id="a34a6-133">Après son exécution, la commande retourne le message « Connexion réussie ».</span><span class="sxs-lookup"><span data-stu-id="a34a6-133">The command returns a 'Login Succeeded’ message once completed.</span></span>

## <a name="tag-container-image"></a><span data-ttu-id="a34a6-134">Baliser l’image de conteneur</span><span class="sxs-lookup"><span data-stu-id="a34a6-134">Tag container image</span></span>

<span data-ttu-id="a34a6-135">Pour pouvoir déployer une image conteneur à partir d’un registre privé, vous devez la baliser avec le `loginServer` nom du registre.</span><span class="sxs-lookup"><span data-stu-id="a34a6-135">To deploy a container image from a private registry, the image needs to be tagged with the `loginServer` name of the registry.</span></span>

<span data-ttu-id="a34a6-136">Pour afficher une liste des images en cours, utilisez la commande `docker images`.</span><span class="sxs-lookup"><span data-stu-id="a34a6-136">To see a list of current images, use the `docker images` command.</span></span>

```bash
docker images
```

<span data-ttu-id="a34a6-137">Output:</span><span class="sxs-lookup"><span data-stu-id="a34a6-137">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

<span data-ttu-id="a34a6-138">Pour obtenir le nom de loginServer, exécutez la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="a34a6-138">To get the loginServer name, run the following command.</span></span>

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

<span data-ttu-id="a34a6-139">Balisez l’image *aci-tutorial-app* à l’aide du loginServer du registre de conteneurs.</span><span class="sxs-lookup"><span data-stu-id="a34a6-139">Tag the *aci-tutorial-app* image with the loginServer of the container registry.</span></span> <span data-ttu-id="a34a6-140">En outre, ajoutez `:v1` à la fin du nom de l’image.</span><span class="sxs-lookup"><span data-stu-id="a34a6-140">Also, add `:v1` to the end of the image name.</span></span> <span data-ttu-id="a34a6-141">Cette balise indique le numéro de version de l’image.</span><span class="sxs-lookup"><span data-stu-id="a34a6-141">This tag indicates the image version number.</span></span>

```bash
docker tag aci-tutorial-app <acrLoginServer>/aci-tutorial-app:v1
```

<span data-ttu-id="a34a6-142">Une fois marqué, exécutez `docker images` pour vérifier l’opération.</span><span class="sxs-lookup"><span data-stu-id="a34a6-142">Once tagged, run `docker images` to verify the operation.</span></span>

```bash
docker images
```

<span data-ttu-id="a34a6-143">Output:</span><span class="sxs-lookup"><span data-stu-id="a34a6-143">Output:</span></span>

```bash
REPOSITORY                                                TAG                 IMAGE ID            CREATED             SIZE
aci-tutorial-app                                          latest              5c745774dfa9        39 seconds ago      68.1 MB
mycontainerregistry082.azurecr.io/aci-tutorial-app        v1                  a9dace4e1a17        7 minutes ago       68.1 MB
```

## <a name="push-image-to-azure-container-registry"></a><span data-ttu-id="a34a6-144">Envoyer l’image à Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="a34a6-144">Push image to Azure Container Registry</span></span>

<span data-ttu-id="a34a6-145">Envoyez l’image *aci-tutorial-app* au registre.</span><span class="sxs-lookup"><span data-stu-id="a34a6-145">Push the *aci-tutorial-app* image to the registry.</span></span>

<span data-ttu-id="a34a6-146">À l’aide de l’exemple suivant, remplacez le nom loginServer du registre de conteneurs par le loginServer de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="a34a6-146">Using the following example, replace the container registry loginServer name with the loginServer from your environment.</span></span>

```bash
docker push <acrLoginServer>/aci-tutorial-app:v1
```

## <a name="list-images-in-azure-container-registry"></a><span data-ttu-id="a34a6-147">Énumérer les images dans Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="a34a6-147">List images in Azure Container Registry</span></span>

<span data-ttu-id="a34a6-148">Pour retourner une liste d’images qui ont été déplacées dans le registre de conteneurs Azure, utilisez la commande [az acr repository list](/cli/azure/acr/repository#list).</span><span class="sxs-lookup"><span data-stu-id="a34a6-148">To return a list of images that have been pushed to your Azure Container registry, user the [az acr repository list](/cli/azure/acr/repository#list) command.</span></span> <span data-ttu-id="a34a6-149">Mettez à jour la commande avec le nom du registre de conteneurs.</span><span class="sxs-lookup"><span data-stu-id="a34a6-149">Update the command with the container registry name.</span></span>

```azurecli
az acr repository list --name <acrName> --output table
```

<span data-ttu-id="a34a6-150">Output:</span><span class="sxs-lookup"><span data-stu-id="a34a6-150">Output:</span></span>

```azurecli
Result
----------------
aci-tutorial-app
```

<span data-ttu-id="a34a6-151">Puis, pour afficher les balises d’une image spécifique, utilisez la commande [az acr repository show-tags](/cli/azure/acr/repository#show-tags).</span><span class="sxs-lookup"><span data-stu-id="a34a6-151">And then to see the tags for a specific image, use the [az acr repository show-tags](/cli/azure/acr/repository#show-tags) command.</span></span>

```azurecli
az acr repository show-tags --name <acrName> --repository aci-tutorial-app --output table
```

<span data-ttu-id="a34a6-152">Output:</span><span class="sxs-lookup"><span data-stu-id="a34a6-152">Output:</span></span>

```azurecli
Result
--------
v1
```

## <a name="next-steps"></a><span data-ttu-id="a34a6-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a34a6-153">Next steps</span></span>

<span data-ttu-id="a34a6-154">Dans ce didacticiel, nous avons préparé un Azure Container Registry pour une utilisation avec Azure Container Instances, et nous avons envoyé l’image conteneur.</span><span class="sxs-lookup"><span data-stu-id="a34a6-154">In this tutorial, an Azure Container Registry was prepared for use with Azure Container Instances, and the container image was pushed.</span></span> <span data-ttu-id="a34a6-155">Les étapes suivantes ont été effectuées :</span><span class="sxs-lookup"><span data-stu-id="a34a6-155">The following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a34a6-156">Déploiement d’une instance Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="a34a6-156">Deploying an Azure Container Registry instance</span></span>
> * <span data-ttu-id="a34a6-157">Balisage d’image conteneur pour Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="a34a6-157">Tagging container image for Azure Container Registry</span></span>
> * <span data-ttu-id="a34a6-158">Chargement d’image dans Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="a34a6-158">Uploading image to Azure Container Registry</span></span>

<span data-ttu-id="a34a6-159">Passez au didacticiel suivant pour en savoir plus sur le déploiement du conteneur sur Azure à l’aide d’Azure Container Instances.</span><span class="sxs-lookup"><span data-stu-id="a34a6-159">Advance to the next tutorial to learn about deploying the container to Azure using Azure Container Instances.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a34a6-160">Déployer des conteneurs sur Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="a34a6-160">Deploy containers to Azure Container Instances</span></span>](./container-instances-tutorial-deploy-app.md)
