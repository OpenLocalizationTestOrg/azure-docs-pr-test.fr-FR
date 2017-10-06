---
title: "Registre de conteneur de Docker privé aaaCreate - CLI d’Azure | Documents Microsoft"
description: "Commencer à créer et gérer des registres de conteneur Docker privés avec hello Azure CLI 2.0"
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: na
tags: 
keywords: 
ms.assetid: 29e20d75-bf39-4f7d-815f-a2e47209be7d
ms.service: container-registry
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: nepeters
ms.custom: na
ms.openlocfilehash: 2cadf42db0681a09c95486510f1e65c6f87c5280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-container-registry-using-hello-azure-cli"></a><span data-ttu-id="0e853-103">Créer un Registre de conteneur gérés à l’aide de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="0e853-103">Create a managed container registry using hello Azure CLI</span></span>

<span data-ttu-id="0e853-104">Azure Container Registry est un service de registre de conteneurs Docker géré utilisé pour stocker des images de conteneurs Docker privés.</span><span class="sxs-lookup"><span data-stu-id="0e853-104">Azure Container Registry is a managed Docker container registry service used for storing private Docker container images.</span></span> <span data-ttu-id="0e853-105">Ce guide décrit en détail la création d’une instance managée de Registre de conteneur Azure à l’aide de hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="0e853-105">This guide details creating a managed Azure Container Registry instance using hello Azure CLI.</span></span>

<span data-ttu-id="0e853-106">Les registres de conteneurs Azure gérés sont en préversion et non disponibles dans toutes les régions.</span><span class="sxs-lookup"><span data-stu-id="0e853-106">Managed Azure container registries are in preview and not available in all regions.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="0e853-107">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, ce démarrage rapide nécessite que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="0e853-107">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="0e853-108">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="0e853-108">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="0e853-109">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="0e853-109">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="0e853-110">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="0e853-110">Create a resource group</span></span>

<span data-ttu-id="0e853-111">Créer un groupe de ressources avec hello [création de groupe de az](/cli/azure/group#create) commande.</span><span class="sxs-lookup"><span data-stu-id="0e853-111">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="0e853-112">Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="0e853-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="0e853-113">Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *westcentralus* emplacement.</span><span class="sxs-lookup"><span data-stu-id="0e853-113">hello following example creates a resource group named *myResourceGroup* in hello *westcentralus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location westcentralus
```

## <a name="create-a-container-registry"></a><span data-ttu-id="0e853-114">Créer un registre de conteneur</span><span class="sxs-lookup"><span data-stu-id="0e853-114">Create a container registry</span></span>

<span data-ttu-id="0e853-115">Créez une instance de l’ACR à l’aide de hello [az acr créer](/cli/azure/acr#create) commande.</span><span class="sxs-lookup"><span data-stu-id="0e853-115">Create an ACR instance using hello [az acr create](/cli/azure/acr#create) command.</span></span>

> [!NOTE]
> <span data-ttu-id="0e853-116">Lorsque vous créez un registre, spécifiez un nom de domaine global unique de niveau supérieur, contenant uniquement des chiffres et des lettres.</span><span class="sxs-lookup"><span data-stu-id="0e853-116">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span>

 <span data-ttu-id="0e853-117">nom de Registre Hello dans l’exemple de hello est *myContainerRegistry1*, remplacer par un nom unique de votre choix.</span><span class="sxs-lookup"><span data-stu-id="0e853-117">hello registry name in hello example is *myContainerRegistry1*, substitute a unique name of your own.</span></span>

```azurecli
az acr create --name myContainerRegistry1 --resource-group myResourceGroup --sku Managed_Standard
```

<span data-ttu-id="0e853-118">Lors de la création de Registre de hello, sortie de hello est similaire toohello suivantes :</span><span class="sxs-lookup"><span data-stu-id="0e853-118">When hello registry is created, hello output is similar toohello following:</span></span>

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-29T04:50:28.607134+00:00",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myContainerRegistry1",
  "location": "westcentralus",
  "loginServer": "mycontainerregistry1.azurecr.io",
  "name": "myContainerRegistry1",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "sku": {
    "name": "Managed_Standard",
    "tier": "Managed"
  },
  "storageAccount": null,
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

## <a name="log-in-tooacr-instance"></a><span data-ttu-id="0e853-119">Ouvrez une session dans l’instance de tooACR</span><span class="sxs-lookup"><span data-stu-id="0e853-119">Log in tooACR instance</span></span>

<span data-ttu-id="0e853-120">Avant de poussées et les images de conteneur, vous devez vous connecter dans l’instance ACR toohello.</span><span class="sxs-lookup"><span data-stu-id="0e853-120">Before pushing and pulling container images, you must log in toohello ACR instance.</span></span> <span data-ttu-id="0e853-121">toodo utilisez donc hello [connexion d’acr az](/cli/azure/acr#login) commande.</span><span class="sxs-lookup"><span data-stu-id="0e853-121">toodo so, use hello [az acr login](/cli/azure/acr#login) command.</span></span>

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

<span data-ttu-id="0e853-122">commande Hello renvoie un message de succès de la connexion une fois terminé.</span><span class="sxs-lookup"><span data-stu-id="0e853-122">hello command returns a 'Login Succeeded' message once completed.</span></span>

## <a name="use-azure-container-registry"></a><span data-ttu-id="0e853-123">Utilisation d’Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="0e853-123">Use Azure Container Registry</span></span>

### <a name="list-container-images"></a><span data-ttu-id="0e853-124">Répertorier les images conteneur</span><span class="sxs-lookup"><span data-stu-id="0e853-124">List container images</span></span>

<span data-ttu-id="0e853-125">Hello d’utilisation `az acr` commandes CLI de balises dans un référentiel et des images de hello tooquery.</span><span class="sxs-lookup"><span data-stu-id="0e853-125">Use hello `az acr` CLI commands tooquery hello images and tags in a repository.</span></span>

> [!NOTE]
> <span data-ttu-id="0e853-126">Actuellement, Registre de conteneur ne prend pas en charge hello `docker search` tooquery de commande pour les images et les balises.</span><span class="sxs-lookup"><span data-stu-id="0e853-126">Currently, Container Registry does not support hello `docker search` command tooquery for images and tags.</span></span>

### <a name="list-repositories"></a><span data-ttu-id="0e853-127">Répertorier les référentiels</span><span class="sxs-lookup"><span data-stu-id="0e853-127">List repositories</span></span>

<span data-ttu-id="0e853-128">Hello exemple suivant répertorie les référentiels hello dans un Registre, au format JSON (JavaScript Object Notation) :</span><span class="sxs-lookup"><span data-stu-id="0e853-128">hello following example lists hello repositories in a registry, in JSON (JavaScript Object Notation) format:</span></span>

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a><span data-ttu-id="0e853-129">Répertorier les balises</span><span class="sxs-lookup"><span data-stu-id="0e853-129">List tags</span></span>

<span data-ttu-id="0e853-130">Hello exemple suivant répertorie les balises hello sur hello **exemples/nginx** référentiel, au format JSON :</span><span class="sxs-lookup"><span data-stu-id="0e853-130">hello following example lists hello tags on hello **samples/nginx** repository, in JSON format:</span></span>

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a><span data-ttu-id="0e853-131">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0e853-131">Next steps</span></span>

<span data-ttu-id="0e853-132">Dans ce guide de démarrage rapide, vous avez créé une instance managée de Registre de conteneur Azure à l’aide de hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="0e853-132">In this quick start, you've created a managed Azure Container Registry instance using hello Azure CLI.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0e853-133">Push de votre première image à l’aide de hello Docker CLI</span><span class="sxs-lookup"><span data-stu-id="0e853-133">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
