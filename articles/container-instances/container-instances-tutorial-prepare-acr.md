---
title: "didacticiel d’Instances de conteneurs aaaAzure - préparer un Registre de conteneur Azure | Documents Microsoft"
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
ms.openlocfilehash: 2525626125740c3c861fad36aad207d0b587ff54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-use-azure-container-registry"></a><span data-ttu-id="d21dc-104">Déployer et utiliser Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="d21dc-104">Deploy and use Azure Container Registry</span></span>

<span data-ttu-id="d21dc-105">Il s’agit de la deuxième partie d’un didacticiel en trois parties.</span><span class="sxs-lookup"><span data-stu-id="d21dc-105">This is part two of a three-part tutorial.</span></span> <span data-ttu-id="d21dc-106">Bonjour [précédemment](./container-instances-tutorial-prepare-app.md), une image de conteneur a été créée pour une application web simple écrite [Node.js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="d21dc-106">In hello [previous step](./container-instances-tutorial-prepare-app.md), a container image was created for a simple web application written in [Node.js](http://nodejs.org).</span></span> <span data-ttu-id="d21dc-107">Dans ce didacticiel, cette image est transmise tooan Registre de conteneur Azure.</span><span class="sxs-lookup"><span data-stu-id="d21dc-107">In this tutorial, this image is pushed tooan Azure Container Registry.</span></span> <span data-ttu-id="d21dc-108">Si vous n’avez pas créé image de conteneur hello, retourner trop[didacticiel 1 : créer une image de conteneur](./container-instances-tutorial-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="d21dc-108">If you have not created hello container image, return too[Tutorial 1 – Create container image](./container-instances-tutorial-prepare-app.md).</span></span> 

<span data-ttu-id="d21dc-109">Hello Registre de conteneur Azure est un registre basé sur Azure, privé, pour les images de conteneur Docker.</span><span class="sxs-lookup"><span data-stu-id="d21dc-109">hello Azure Container Registry is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="d21dc-110">Ce didacticiel Guide de déploiement d’une instance de Registre de conteneur Azure et l’envoi d’un tooit d’image de conteneur.</span><span class="sxs-lookup"><span data-stu-id="d21dc-110">This tutorial walks through deploying an Azure Container Registry instance, and pushing a container image tooit.</span></span> <span data-ttu-id="d21dc-111">Les étapes terminées sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="d21dc-111">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d21dc-112">Déploiement d’une instance Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="d21dc-112">Deploying an Azure Container Registry instance</span></span>
> * <span data-ttu-id="d21dc-113">Balisage d’image conteneur pour Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="d21dc-113">Tagging container image for Azure Container Registry</span></span>
> * <span data-ttu-id="d21dc-114">Télécharger l’image tooAzure Registre de conteneur</span><span class="sxs-lookup"><span data-stu-id="d21dc-114">Uploading image tooAzure Container Registry</span></span>

<span data-ttu-id="d21dc-115">Dans les didacticiels suivants vous déployez le conteneur de hello à partir de votre tooAzure Registre privé les Instances du conteneur.</span><span class="sxs-lookup"><span data-stu-id="d21dc-115">In subsequent tutorials, you deploy hello container from your private registry tooAzure Container Instances.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d21dc-116">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="d21dc-116">Before you begin</span></span>

<span data-ttu-id="d21dc-117">Ce didacticiel nécessite que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="d21dc-117">This tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="d21dc-118">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="d21dc-118">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="d21dc-119">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d21dc-119">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="d21dc-120">Déployer Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="d21dc-120">Deploy Azure Container Registry</span></span>

<span data-ttu-id="d21dc-121">Lorsque vous déployez un registre de conteneurs Azure, il vous faut tout d’abord un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="d21dc-121">When deploying an Azure Container Registry, you first need a resource group.</span></span> <span data-ttu-id="d21dc-122">Un groupe de ressources Azure est une collection logique dans laquelle des ressources Azure sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="d21dc-122">An Azure resource group is a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="d21dc-123">Créer un groupe de ressources avec hello [création de groupe de az](/cli/azure/group#create) commande.</span><span class="sxs-lookup"><span data-stu-id="d21dc-123">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="d21dc-124">Dans cet exemple, un groupe de ressources nommé *myResourceGroup* est créé dans hello *eastus* région.</span><span class="sxs-lookup"><span data-stu-id="d21dc-124">In this example, a resource group named *myResourceGroup* is created in hello *eastus* region.</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="d21dc-125">Créer un Registre de conteneur Azure avec hello [az acr créer](/cli/azure/acr#create) commande.</span><span class="sxs-lookup"><span data-stu-id="d21dc-125">Create an Azure Container registry with hello [az acr create](/cli/azure/acr#create) command.</span></span> <span data-ttu-id="d21dc-126">nom d’un Registre de conteneur de Hello **doit être unique**.</span><span class="sxs-lookup"><span data-stu-id="d21dc-126">hello name of a Container Registry **must be unique**.</span></span> <span data-ttu-id="d21dc-127">Bonjour l’exemple suivant, nous utilisons le nom de hello *mycontainerregistry082*.</span><span class="sxs-lookup"><span data-stu-id="d21dc-127">In hello following example, we use hello name *mycontainerregistry082*.</span></span>

```azurecli
az acr create --resource-group myResourceGroup --name mycontainerregistry082 --sku Basic --admin-enabled true
```

<span data-ttu-id="d21dc-128">Dans l’ensemble de rest hello de ce didacticiel, nous utilisons `<acrname>` comme espace réservé pour le nom du Registre hello conteneur que vous avez choisi.</span><span class="sxs-lookup"><span data-stu-id="d21dc-128">Throughout hello rest of this tutorial, we use `<acrname>` as a placeholder for hello container registry name that you chose.</span></span>

## <a name="container-registry-login"></a><span data-ttu-id="d21dc-129">Connexion au registre de conteneurs</span><span class="sxs-lookup"><span data-stu-id="d21dc-129">Container registry login</span></span>

<span data-ttu-id="d21dc-130">Vous devez vous connecter dans l’instance ACR tooyour avant d’installer des images tooit.</span><span class="sxs-lookup"><span data-stu-id="d21dc-130">You must log in tooyour ACR instance before pushing images tooit.</span></span> <span data-ttu-id="d21dc-131">Hello d’utilisation [connexion d’acr az](https://docs.microsoft.com/en-us/cli/azure/acr#login) opération de hello toocomplete de commandes.</span><span class="sxs-lookup"><span data-stu-id="d21dc-131">Use hello [az acr login](https://docs.microsoft.com/en-us/cli/azure/acr#login) command toocomplete hello operation.</span></span> <span data-ttu-id="d21dc-132">Vous devez tooprovide hello unique nom Registre de conteneur toohello lors de sa création.</span><span class="sxs-lookup"><span data-stu-id="d21dc-132">You need tooprovide hello unique name given toohello container registry when it was created.</span></span>

```azurecli
az acr login --name <acrName>
```

<span data-ttu-id="d21dc-133">commande Hello renvoie un message de succès de la connexion une fois terminé.</span><span class="sxs-lookup"><span data-stu-id="d21dc-133">hello command returns a 'Login Succeeded’ message once completed.</span></span>

## <a name="tag-container-image"></a><span data-ttu-id="d21dc-134">Baliser l’image de conteneur</span><span class="sxs-lookup"><span data-stu-id="d21dc-134">Tag container image</span></span>

<span data-ttu-id="d21dc-135">toodeploy une image de conteneur à partir d’un Registre privé, image de hello doit toobe balisé avec hello `loginServer` nom du Registre de hello.</span><span class="sxs-lookup"><span data-stu-id="d21dc-135">toodeploy a container image from a private registry, hello image needs toobe tagged with hello `loginServer` name of hello registry.</span></span>

<span data-ttu-id="d21dc-136">toosee une liste d’images en cours, utilisez hello `docker images` commande.</span><span class="sxs-lookup"><span data-stu-id="d21dc-136">toosee a list of current images, use hello `docker images` command.</span></span>

```bash
docker images
```

<span data-ttu-id="d21dc-137">Output:</span><span class="sxs-lookup"><span data-stu-id="d21dc-137">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

<span data-ttu-id="d21dc-138">nom de loginServer hello tooget, exécutez hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="d21dc-138">tooget hello loginServer name, run hello following command.</span></span>

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

<span data-ttu-id="d21dc-139">Hello de balise *aci-didacticiel-app* image avec loginServer hello du Registre de conteneur hello.</span><span class="sxs-lookup"><span data-stu-id="d21dc-139">Tag hello *aci-tutorial-app* image with hello loginServer of hello container registry.</span></span> <span data-ttu-id="d21dc-140">En outre, ajoutez `:v1` fin toohello de nom de l’image hello.</span><span class="sxs-lookup"><span data-stu-id="d21dc-140">Also, add `:v1` toohello end of hello image name.</span></span> <span data-ttu-id="d21dc-141">Cette balise indique le numéro de version d’image hello.</span><span class="sxs-lookup"><span data-stu-id="d21dc-141">This tag indicates hello image version number.</span></span>

```bash
docker tag aci-tutorial-app <acrLoginServer>/aci-tutorial-app:v1
```

<span data-ttu-id="d21dc-142">Une fois que balisé, exécutez `docker images` opération hello de tooverify.</span><span class="sxs-lookup"><span data-stu-id="d21dc-142">Once tagged, run `docker images` tooverify hello operation.</span></span>

```bash
docker images
```

<span data-ttu-id="d21dc-143">Output:</span><span class="sxs-lookup"><span data-stu-id="d21dc-143">Output:</span></span>

```bash
REPOSITORY                                                TAG                 IMAGE ID            CREATED             SIZE
aci-tutorial-app                                          latest              5c745774dfa9        39 seconds ago      68.1 MB
mycontainerregistry082.azurecr.io/aci-tutorial-app        v1                  a9dace4e1a17        7 minutes ago       68.1 MB
```

## <a name="push-image-tooazure-container-registry"></a><span data-ttu-id="d21dc-144">Push image tooAzure Registre de conteneur</span><span class="sxs-lookup"><span data-stu-id="d21dc-144">Push image tooAzure Container Registry</span></span>

<span data-ttu-id="d21dc-145">Push hello *aci-didacticiel-app* Registre toohello d’images.</span><span class="sxs-lookup"><span data-stu-id="d21dc-145">Push hello *aci-tutorial-app* image toohello registry.</span></span>

<span data-ttu-id="d21dc-146">À l’aide de hello l’exemple suivant, remplacez hello conteneur Registre loginServer par loginServer hello à partir de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="d21dc-146">Using hello following example, replace hello container registry loginServer name with hello loginServer from your environment.</span></span>

```bash
docker push <acrLoginServer>/aci-tutorial-app:v1
```

## <a name="list-images-in-azure-container-registry"></a><span data-ttu-id="d21dc-147">Énumérer les images dans Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="d21dc-147">List images in Azure Container Registry</span></span>

<span data-ttu-id="d21dc-148">tooreturn une liste d’images qui ont été déplacées du Registre le conteneur Azure tooyour, hello d’utilisateur [liste des référentiels az acr](/cli/azure/acr/repository#list) commande.</span><span class="sxs-lookup"><span data-stu-id="d21dc-148">tooreturn a list of images that have been pushed tooyour Azure Container registry, user hello [az acr repository list](/cli/azure/acr/repository#list) command.</span></span> <span data-ttu-id="d21dc-149">Mettre à jour la commande hello par le nom de Registre de conteneur hello.</span><span class="sxs-lookup"><span data-stu-id="d21dc-149">Update hello command with hello container registry name.</span></span>

```azurecli
az acr repository list --name <acrName> --output table
```

<span data-ttu-id="d21dc-150">Output:</span><span class="sxs-lookup"><span data-stu-id="d21dc-150">Output:</span></span>

```azurecli
Result
----------------
aci-tutorial-app
```

<span data-ttu-id="d21dc-151">Puis les balises de hello toosee d’une image spécifique, utilisez hello [az acr référentiel afficher-balises](/cli/azure/acr/repository#show-tags) commande.</span><span class="sxs-lookup"><span data-stu-id="d21dc-151">And then toosee hello tags for a specific image, use hello [az acr repository show-tags](/cli/azure/acr/repository#show-tags) command.</span></span>

```azurecli
az acr repository show-tags --name <acrName> --repository aci-tutorial-app --output table
```

<span data-ttu-id="d21dc-152">Output:</span><span class="sxs-lookup"><span data-stu-id="d21dc-152">Output:</span></span>

```azurecli
Result
--------
v1
```

## <a name="next-steps"></a><span data-ttu-id="d21dc-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d21dc-153">Next steps</span></span>

<span data-ttu-id="d21dc-154">Dans ce didacticiel, un Registre de conteneur Azure a été préparé pour une utilisation avec les Instances du conteneur Azure et image de conteneur hello a été envoyée.</span><span class="sxs-lookup"><span data-stu-id="d21dc-154">In this tutorial, an Azure Container Registry was prepared for use with Azure Container Instances, and hello container image was pushed.</span></span> <span data-ttu-id="d21dc-155">Hello suit ont été effectuée :</span><span class="sxs-lookup"><span data-stu-id="d21dc-155">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d21dc-156">Déploiement d’une instance Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="d21dc-156">Deploying an Azure Container Registry instance</span></span>
> * <span data-ttu-id="d21dc-157">Balisage d’image conteneur pour Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="d21dc-157">Tagging container image for Azure Container Registry</span></span>
> * <span data-ttu-id="d21dc-158">Télécharger l’image tooAzure Registre de conteneur</span><span class="sxs-lookup"><span data-stu-id="d21dc-158">Uploading image tooAzure Container Registry</span></span>

<span data-ttu-id="d21dc-159">Avance toohello toolearn de didacticiel suivant sur le déploiement de hello tooAzure de conteneur à l’aide d’Instances de conteneurs Azure.</span><span class="sxs-lookup"><span data-stu-id="d21dc-159">Advance toohello next tutorial toolearn about deploying hello container tooAzure using Azure Container Instances.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d21dc-160">Déployer des conteneurs tooAzure Instances de conteneurs</span><span class="sxs-lookup"><span data-stu-id="d21dc-160">Deploy containers tooAzure Container Instances</span></span>](./container-instances-tutorial-deploy-app.md)
