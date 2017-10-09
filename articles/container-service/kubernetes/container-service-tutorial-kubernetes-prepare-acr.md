---
title: "didacticiel de Service de conteneur aaaAzure - préparer un ACR | Documents Microsoft"
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
ms.openlocfilehash: 3980e5ce4eb9836f83c761a2f76c944bb3f13060
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-use-azure-container-registry"></a><span data-ttu-id="afdeb-104">Déployer et utiliser Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="afdeb-104">Deploy and use Azure Container Registry</span></span>

<span data-ttu-id="afdeb-105">Azure Container Registry (ACR) est un registre privé Azure pour les images de conteneur Docker.</span><span class="sxs-lookup"><span data-stu-id="afdeb-105">Azure Container Registry (ACR) is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="afdeb-106">Ce didacticiel, la partie deux des sept, Guide de déploiement d’une instance de Registre de conteneur Azure et l’envoi d’un tooit d’image de conteneur.</span><span class="sxs-lookup"><span data-stu-id="afdeb-106">This tutorial, part two of seven, walks through deploying an Azure Container Registry instance, and pushing a container image tooit.</span></span> <span data-ttu-id="afdeb-107">Les étapes terminées sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="afdeb-107">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="afdeb-108">Déploiement d’une instance Azure Container Registry (ACR)</span><span class="sxs-lookup"><span data-stu-id="afdeb-108">Deploying an Azure Container Registry (ACR) instance</span></span>
> * <span data-ttu-id="afdeb-109">Marquage d’une image conteneur pour ACR</span><span class="sxs-lookup"><span data-stu-id="afdeb-109">Tagging a container image for ACR</span></span>
> * <span data-ttu-id="afdeb-110">Téléchargement hello image tooACR</span><span class="sxs-lookup"><span data-stu-id="afdeb-110">Uploading hello image tooACR</span></span>

<span data-ttu-id="afdeb-111">Dans les didacticiels suivants, cette instance ACR est intégrée à un cluster Azure Container Service Kubernetes, pour l’exécution des images de conteneur en toute sécurité.</span><span class="sxs-lookup"><span data-stu-id="afdeb-111">In subsequent tutorials, this ACR instance is integrated with an Azure Container Service Kubernetes cluster, for securely running container images.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="afdeb-112">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="afdeb-112">Before you begin</span></span>

<span data-ttu-id="afdeb-113">Bonjour [didacticiel précédent](./container-service-tutorial-kubernetes-prepare-app.md), une image de conteneur a été créée pour une application Azure vote simple.</span><span class="sxs-lookup"><span data-stu-id="afdeb-113">In hello [previous tutorial](./container-service-tutorial-kubernetes-prepare-app.md), a container image was created for a simple Azure Voting application.</span></span> <span data-ttu-id="afdeb-114">Dans ce didacticiel, cette image est transmise tooan Registre de conteneur Azure.</span><span class="sxs-lookup"><span data-stu-id="afdeb-114">In this tutorial, this image is pushed tooan Azure Container Registry.</span></span> <span data-ttu-id="afdeb-115">Si vous n’avez pas créé image des application Azure vote hello, retourner trop[didacticiel 1 : créer des images de conteneur](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="afdeb-115">If you have not created hello Azure Voting app image, return too[Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> <span data-ttu-id="afdeb-116">Vous pouvez également hello étapes détaillées ici fonctionnent avec n’importe quelle image de conteneur.</span><span class="sxs-lookup"><span data-stu-id="afdeb-116">Alternatively, hello steps detailed here work with any container image.</span></span>

<span data-ttu-id="afdeb-117">Ce didacticiel nécessite que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="afdeb-117">This tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="afdeb-118">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="afdeb-118">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="afdeb-119">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="afdeb-119">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="afdeb-120">Déployer Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="afdeb-120">Deploy Azure Container Registry</span></span>

<span data-ttu-id="afdeb-121">Lorsque vous déployez un registre de conteneurs Azure, il vous faut tout d’abord un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="afdeb-121">When deploying an Azure Container Registry, you first need a resource group.</span></span> <span data-ttu-id="afdeb-122">Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="afdeb-122">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="afdeb-123">Créer un groupe de ressources avec hello [création de groupe de az](/cli/azure/group#create) commande.</span><span class="sxs-lookup"><span data-stu-id="afdeb-123">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="afdeb-124">Dans cet exemple, un groupe de ressources nommé *myResourceGroup* est créé dans hello *westeurope* région.</span><span class="sxs-lookup"><span data-stu-id="afdeb-124">In this example, a resource group named *myResourceGroup* is created in hello *westeurope* region.</span></span>

```azurecli
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="afdeb-125">Créer un Registre de conteneur Azure avec hello [az acr créer](/cli/azure/acr#create) commande.</span><span class="sxs-lookup"><span data-stu-id="afdeb-125">Create an Azure Container registry with hello [az acr create](/cli/azure/acr#create) command.</span></span> <span data-ttu-id="afdeb-126">nom d’un Registre de conteneur de Hello **doit être unique**.</span><span class="sxs-lookup"><span data-stu-id="afdeb-126">hello name of a Container Registry **must be unique**.</span></span>

```azurecli
az acr create --resource-group myResourceGroup --name <acrName> --sku Basic --admin-enabled true
```

<span data-ttu-id="afdeb-127">Dans l’ensemble de rest hello de ce didacticiel, nous utilisons « acrname » comme espace réservé pour le nom du Registre hello conteneur que vous avez choisi.</span><span class="sxs-lookup"><span data-stu-id="afdeb-127">Throughout hello rest of this tutorial, we use "acrname" as a placeholder for hello container registry name that you chose.</span></span>

## <a name="container-registry-login"></a><span data-ttu-id="afdeb-128">Connexion au registre de conteneurs</span><span class="sxs-lookup"><span data-stu-id="afdeb-128">Container registry login</span></span>

<span data-ttu-id="afdeb-129">Vous devez vous connecter dans l’instance ACR tooyour avant d’installer des images tooit.</span><span class="sxs-lookup"><span data-stu-id="afdeb-129">You must log in tooyour ACR instance before pushing images tooit.</span></span> <span data-ttu-id="afdeb-130">Hello d’utilisation [connexion d’acr az](https://docs.microsoft.com/en-us/cli/azure/acr#login) opération de hello toocomplete de commandes.</span><span class="sxs-lookup"><span data-stu-id="afdeb-130">Use hello [az acr login](https://docs.microsoft.com/en-us/cli/azure/acr#login) command toocomplete hello operation.</span></span> <span data-ttu-id="afdeb-131">Vous devez tooprovide hello unique nom Registre de conteneur toohello lors de sa création.</span><span class="sxs-lookup"><span data-stu-id="afdeb-131">You need tooprovide hello unique name given toohello container registry when it was created.</span></span>

```azurecli
az acr login --name <acrName>
```

<span data-ttu-id="afdeb-132">commande Hello renvoie un message de succès de la connexion une fois terminé.</span><span class="sxs-lookup"><span data-stu-id="afdeb-132">hello command returns a 'Login Succeeded’ message once completed.</span></span>

## <a name="tag-container-images"></a><span data-ttu-id="afdeb-133">Marquer les images de conteneur</span><span class="sxs-lookup"><span data-stu-id="afdeb-133">Tag container images</span></span>

<span data-ttu-id="afdeb-134">Chaque image de conteneur doit toobe balisé avec le nom de loginServer hello du Registre de hello.</span><span class="sxs-lookup"><span data-stu-id="afdeb-134">Each container image needs toobe tagged with hello loginServer name of hello registry.</span></span> <span data-ttu-id="afdeb-135">Cette balise est utilisée pour le routage lors de la distribution du Registre de conteneur images tooan image.</span><span class="sxs-lookup"><span data-stu-id="afdeb-135">This tag is used for routing when pushing container images tooan image registry.</span></span>

<span data-ttu-id="afdeb-136">toosee une liste d’images en cours, utilisez hello [images docker](https://docs.docker.com/engine/reference/commandline/images/) commande.</span><span class="sxs-lookup"><span data-stu-id="afdeb-136">toosee a list of current images, use hello [docker images](https://docs.docker.com/engine/reference/commandline/images/) command.</span></span>

```bash
docker images
```

<span data-ttu-id="afdeb-137">Output:</span><span class="sxs-lookup"><span data-stu-id="afdeb-137">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front             latest              4675398c9172        13 minutes ago      694MB
redis                        latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask               788ca94b2313        9 months ago        694MB
```

<span data-ttu-id="afdeb-138">nom de loginServer hello tooget, exécutez hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="afdeb-138">tooget hello loginServer name, run hello following command.</span></span>

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

<span data-ttu-id="afdeb-139">Maintenant, hello de balise *avant de vote d’azure* image avec loginServer hello du Registre de conteneur hello.</span><span class="sxs-lookup"><span data-stu-id="afdeb-139">Now, tag hello *azure-vote-front* image with hello loginServer of hello container registry.</span></span> <span data-ttu-id="afdeb-140">En outre, ajoutez `:redis-v1` fin toohello de nom de l’image hello.</span><span class="sxs-lookup"><span data-stu-id="afdeb-140">Also, add `:redis-v1` toohello end of hello image name.</span></span> <span data-ttu-id="afdeb-141">Cette balise indique la version de l’image hello.</span><span class="sxs-lookup"><span data-stu-id="afdeb-141">This tag indicates hello image version.</span></span>

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v1
```

<span data-ttu-id="afdeb-142">Une fois balisé, réexécutez [images docker] (https://docs.docker.com/engine/reference/commandline/images/) tooverify hello.</span><span class="sxs-lookup"><span data-stu-id="afdeb-142">Once tagged, run [docker images] (https://docs.docker.com/engine/reference/commandline/images/) tooverify hello operation.</span></span>

```bash
docker images
```

<span data-ttu-id="afdeb-143">Output:</span><span class="sxs-lookup"><span data-stu-id="afdeb-143">Output:</span></span>

```bash
REPOSITORY                                           TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front                                     latest              eaf2b9c57e5e        8 minutes ago       716 MB
mycontainerregistry082.azurecr.io/azure-vote-front   redis-v1            eaf2b9c57e5e        8 minutes ago       716 MB
redis                                                latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask                           flask               788ca94b2313        8 months ago        694 MB
```

## <a name="push-images-tooregistry"></a><span data-ttu-id="afdeb-144">Push tooregistry d’images</span><span class="sxs-lookup"><span data-stu-id="afdeb-144">Push images tooregistry</span></span>

<span data-ttu-id="afdeb-145">Push hello *avant de vote d’azure* Registre toohello d’images.</span><span class="sxs-lookup"><span data-stu-id="afdeb-145">Push hello *azure-vote-front* image toohello registry.</span></span> 

<span data-ttu-id="afdeb-146">À l’aide de hello l’exemple suivant, remplacez hello ACR loginServer par loginServer hello à partir de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="afdeb-146">Using hello following example, replace hello ACR loginServer name with hello loginServer from your environment.</span></span>

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v1
```

<span data-ttu-id="afdeb-147">Cette opération prend quelques minutes toocomplete.</span><span class="sxs-lookup"><span data-stu-id="afdeb-147">This takes a couple of minutes toocomplete.</span></span>

## <a name="list-images-in-registry"></a><span data-ttu-id="afdeb-148">Créer la liste des images du registre</span><span class="sxs-lookup"><span data-stu-id="afdeb-148">List images in registry</span></span>

<span data-ttu-id="afdeb-149">tooreturn une liste d’images qui ont été déplacées du Registre le conteneur Azure tooyour, hello d’utilisateur [liste des référentiels az acr](/cli/azure/acr/repository#list) commande.</span><span class="sxs-lookup"><span data-stu-id="afdeb-149">tooreturn a list of images that have been pushed tooyour Azure Container registry, user hello [az acr repository list](/cli/azure/acr/repository#list) command.</span></span> <span data-ttu-id="afdeb-150">Mettre à jour la commande hello avec le nom de l’instance ACR hello.</span><span class="sxs-lookup"><span data-stu-id="afdeb-150">Update hello command with hello ACR instance name.</span></span>

```azurecli
az acr repository list --name <acrName> --output table
```

<span data-ttu-id="afdeb-151">Output:</span><span class="sxs-lookup"><span data-stu-id="afdeb-151">Output:</span></span>

```azurecli
Result
----------------
azure-vote-front
```

<span data-ttu-id="afdeb-152">Puis les balises de hello toosee d’une image spécifique, utilisez hello [az acr référentiel afficher-balises](/cli/azure/acr/repository#show-tags) commande.</span><span class="sxs-lookup"><span data-stu-id="afdeb-152">And then toosee hello tags for a specific image, use hello [az acr repository show-tags](/cli/azure/acr/repository#show-tags) command.</span></span>

```azurecli
az acr repository show-tags --name <acrName> --repository azure-vote-front --output table
```

<span data-ttu-id="afdeb-153">Output:</span><span class="sxs-lookup"><span data-stu-id="afdeb-153">Output:</span></span>

```azurecli
Result
--------
redis-v1
```

<span data-ttu-id="afdeb-154">À l’achèvement de didacticiel, image de conteneur hello ayant été stockée dans une instance de Registre de conteneur Azure privée.</span><span class="sxs-lookup"><span data-stu-id="afdeb-154">At tutorial completion, hello container image has been stored in a private Azure Container Registry instance.</span></span> <span data-ttu-id="afdeb-155">Cette image est déployée à partir du cluster ACR tooa Kubernetes dans les didacticiels suivants.</span><span class="sxs-lookup"><span data-stu-id="afdeb-155">This image is deployed from ACR tooa Kubernetes cluster in subsequent tutorials.</span></span>

## <a name="next-steps"></a><span data-ttu-id="afdeb-156">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="afdeb-156">Next steps</span></span>

<span data-ttu-id="afdeb-157">Dans ce didacticiel, un registre de conteneurs Azure a été préparé pour une utilisation dans un cluster ACS Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="afdeb-157">In this tutorial, an Azure Container Registry was prepared for use in an ACS Kubernetes cluster.</span></span> <span data-ttu-id="afdeb-158">Hello suit ont été effectuée :</span><span class="sxs-lookup"><span data-stu-id="afdeb-158">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="afdeb-159">Déploiement d’une instance Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="afdeb-159">Deployed an Azure Container Registry instance</span></span>
> * <span data-ttu-id="afdeb-160">Marquage d’une image conteneur pour ACR</span><span class="sxs-lookup"><span data-stu-id="afdeb-160">Tagged a container image for ACR</span></span>
> * <span data-ttu-id="afdeb-161">Hello téléchargé image tooACR</span><span class="sxs-lookup"><span data-stu-id="afdeb-161">Uploaded hello image tooACR</span></span>

<span data-ttu-id="afdeb-162">Avance toohello toolearn de didacticiel suivant sur le déploiement d’un cluster Kubernetes dans Azure.</span><span class="sxs-lookup"><span data-stu-id="afdeb-162">Advance toohello next tutorial toolearn about deploying a Kubernetes cluster in Azure.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="afdeb-163">Déployer un cluster Kubernetes</span><span class="sxs-lookup"><span data-stu-id="afdeb-163">Deploy Kubernetes cluster</span></span>](./container-service-tutorial-kubernetes-deploy-cluster.md)