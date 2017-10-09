---
title: "Registre Docker privé aaaCreate - portail Azure | Documents Microsoft"
description: "Commencer à créer et gérer des registres de conteneur Docker privés avec hello portail Azure"
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: na
tags: 
keywords: 
ms.assetid: 53a3b3cb-ab4b-4560-bc00-366e2759f1a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: nepeters
ms.custom: na
ms.openlocfilehash: cf3ce0dcf3036d0e9cd1eaf01721deccb00248d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-container-registry-using-hello-azure-portal"></a><span data-ttu-id="0487b-103">Créer un Registre de conteneur gérés à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="0487b-103">Create a managed container registry using hello Azure portal</span></span>

<span data-ttu-id="0487b-104">Azure Container Registry est un service de registre de conteneurs Docker géré utilisé pour stocker des images de conteneurs Docker privés.</span><span class="sxs-lookup"><span data-stu-id="0487b-104">Azure Container Registry is a managed Docker container registry service used for storing private Docker container images.</span></span> <span data-ttu-id="0487b-105">Ce guide décrit en détail création d’une instance managée de Registre de conteneur Azure à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0487b-105">This guide details creating a managed Azure Container Registry instance using hello Azure portal.</span></span>

<span data-ttu-id="0487b-106">Les registres de conteneurs Azure gérés sont en préversion et non disponibles dans toutes les régions.</span><span class="sxs-lookup"><span data-stu-id="0487b-106">Managed Azure container registries are in preview and not available in all regions.</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="0487b-107">Connectez-vous à tooAzure</span><span class="sxs-lookup"><span data-stu-id="0487b-107">Log in tooAzure</span></span>

<span data-ttu-id="0487b-108">Ouvrez une session dans toohello portail Azure à http://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="0487b-108">Log in toohello Azure portal at http://portal.azure.com.</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="0487b-109">Créer un registre de conteneur</span><span class="sxs-lookup"><span data-stu-id="0487b-109">Create a container registry</span></span>

1. <span data-ttu-id="0487b-110">Cliquez sur hello **nouveau** bouton se trouve sur le coin supérieur gauche hello Hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0487b-110">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

2. <span data-ttu-id="0487b-111">Marketplace hello de recherche pour **Registre de conteneur Azure** et sélectionnez-le.</span><span class="sxs-lookup"><span data-stu-id="0487b-111">Search hello marketplace for **Azure container registry** and select it.</span></span>

3. <span data-ttu-id="0487b-112">Cliquez sur **créer** Panneau de création de hello ACR s’affichera.</span><span class="sxs-lookup"><span data-stu-id="0487b-112">Click **Create** which will open hello ACR creation blade.</span></span>

    ![Paramètres de Container Registry](./media/container-registry-get-started-portal/managed-container-registry-settings.png)

4. <span data-ttu-id="0487b-114">Bonjour **Registre de conteneur Azure** panneau, entrez hello informations suivantes.</span><span class="sxs-lookup"><span data-stu-id="0487b-114">In hello **Azure Container Registry** blade, enter hello following information.</span></span> <span data-ttu-id="0487b-115">Une fois ces opérations effectuées, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="0487b-115">Click **Create** when you are done.</span></span>

    <span data-ttu-id="0487b-116">a.</span><span class="sxs-lookup"><span data-stu-id="0487b-116">a.</span></span> <span data-ttu-id="0487b-117">**Nom du registre** : Un nom de domaine global unique et de niveau supérieur pour votre registre spécifique.</span><span class="sxs-lookup"><span data-stu-id="0487b-117">**Registry name**: A globally unique top-level domain name for your specific registry.</span></span> <span data-ttu-id="0487b-118">Dans cet exemple, le nom de Registre hello est *myAzureContainerRegistry1*, mais remplacer par un nom unique de votre choix.</span><span class="sxs-lookup"><span data-stu-id="0487b-118">In this example, hello registry name is *myAzureContainerRegistry1*, but substitute a unique name of your own.</span></span> <span data-ttu-id="0487b-119">nom de Hello peut contenir que des lettres et des chiffres.</span><span class="sxs-lookup"><span data-stu-id="0487b-119">hello name can contain only letters and numbers.</span></span>

    <span data-ttu-id="0487b-120">b.</span><span class="sxs-lookup"><span data-stu-id="0487b-120">b.</span></span> <span data-ttu-id="0487b-121">**Groupe de ressources**: sélectionnez un existant [groupe de ressources](../azure-resource-manager/resource-group-overview.md#resource-groups) ou nom du type hello pour un nouveau.</span><span class="sxs-lookup"><span data-stu-id="0487b-121">**Resource group**: Select an existing [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) or type hello name for a new one.</span></span>

    <span data-ttu-id="0487b-122">c.</span><span class="sxs-lookup"><span data-stu-id="0487b-122">c.</span></span> <span data-ttu-id="0487b-123">**Emplacement**: sélectionnez un emplacement de centre de données Azure où le service de hello est [disponible](https://azure.microsoft.com/regions/services/), tel que **Amérique du Sud**.</span><span class="sxs-lookup"><span data-stu-id="0487b-123">**Location**: Select an Azure datacenter location where hello service is [available](https://azure.microsoft.com/regions/services/), such as **South Central US**.</span></span>

    <span data-ttu-id="0487b-124">d.</span><span class="sxs-lookup"><span data-stu-id="0487b-124">d.</span></span> <span data-ttu-id="0487b-125">**L’utilisateur Admin**: Si vous le souhaitez, activer un Registre de hello tooaccess admin utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0487b-125">**Admin user**: If you want, enable an admin user tooaccess hello registry.</span></span> <span data-ttu-id="0487b-126">Vous pouvez modifier ce paramètre après avoir créé le Registre de hello.</span><span class="sxs-lookup"><span data-stu-id="0487b-126">You can change this setting after creating hello registry.</span></span>

    <span data-ttu-id="0487b-127">e.</span><span class="sxs-lookup"><span data-stu-id="0487b-127">e.</span></span> <span data-ttu-id="0487b-128">**Registre de managé utilisation**: sélectionnez Oui toohave ACR automatiquement gérer le stockage de Registre hello, des webhooks et l’authentification AAD.</span><span class="sxs-lookup"><span data-stu-id="0487b-128">**Use managed registry**: Select yes toohave ACR automatically manage hello registry storage, use webhooks, and use AAD authentication.</span></span>

    <span data-ttu-id="0487b-129">f.</span><span class="sxs-lookup"><span data-stu-id="0487b-129">f.</span></span> <span data-ttu-id="0487b-130">**Niveau tarifaire** : sélectionnez un niveau tarifaire. Consultez ici les prix ACR pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="0487b-130">**Pricing Tier**: Select a pricing tier, see here ACR pricing for more information.</span></span>

## <a name="log-in-tooacr-instance"></a><span data-ttu-id="0487b-131">Ouvrez une session dans l’instance de tooACR</span><span class="sxs-lookup"><span data-stu-id="0487b-131">Log in tooACR instance</span></span>

<span data-ttu-id="0487b-132">Avant de poussées et les images de conteneur, vous devez vous connecter dans l’instance ACR toohello.</span><span class="sxs-lookup"><span data-stu-id="0487b-132">Before pushing and pulling container images, you must log in toohello ACR instance.</span></span> 

<span data-ttu-id="0487b-133">toodo utilisez donc hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="0487b-133">toodo so, use hello Azure CLI 2.0.</span></span> <span data-ttu-id="0487b-134">Tout d’abord, si nécessaire, ouvrez une session dans Azure à l’aide de hello [ouverture de session az](/cli/azure/#login) commande.</span><span class="sxs-lookup"><span data-stu-id="0487b-134">First, if needed, log into Azure using hello [az login](/cli/azure/#login) command.</span></span> 

```azurecli
az login
```

<span data-ttu-id="0487b-135">Ensuite, utilisez hello [connexion d’acr az](/cli/azure/acr#login) toolog de commande dans toohello Registre de conteneur Azure.</span><span class="sxs-lookup"><span data-stu-id="0487b-135">Next, use hello [az acr login](/cli/azure/acr#login) command toolog in toohello Azure Container Registry.</span></span>

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

## <a name="use-azure-container-registry"></a><span data-ttu-id="0487b-136">Utilisation d’Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="0487b-136">Use Azure Container Registry</span></span>

### <a name="list-container-images"></a><span data-ttu-id="0487b-137">Répertorier les images conteneur</span><span class="sxs-lookup"><span data-stu-id="0487b-137">List container images</span></span>

<span data-ttu-id="0487b-138">Hello d’utilisation `az acr` commandes CLI de balises dans un référentiel et des images de hello tooquery.</span><span class="sxs-lookup"><span data-stu-id="0487b-138">Use hello `az acr` CLI commands tooquery hello images and tags in a repository.</span></span>

> [!NOTE]
> <span data-ttu-id="0487b-139">Actuellement, Registre de conteneur ne prend pas en charge hello `docker search` tooquery de commande pour les images et les balises.</span><span class="sxs-lookup"><span data-stu-id="0487b-139">Currently, Container Registry does not support hello `docker search` command tooquery for images and tags.</span></span>

### <a name="list-repositories"></a><span data-ttu-id="0487b-140">Répertorier les référentiels</span><span class="sxs-lookup"><span data-stu-id="0487b-140">List repositories</span></span>

<span data-ttu-id="0487b-141">Hello exemple suivant répertorie les référentiels hello dans un Registre, au format JSON (JavaScript Object Notation) :</span><span class="sxs-lookup"><span data-stu-id="0487b-141">hello following example lists hello repositories in a registry, in JSON (JavaScript Object Notation) format:</span></span>

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a><span data-ttu-id="0487b-142">Répertorier les balises</span><span class="sxs-lookup"><span data-stu-id="0487b-142">List tags</span></span>

<span data-ttu-id="0487b-143">Hello exemple suivant répertorie les balises hello sur hello **exemples/nginx** référentiel, au format JSON :</span><span class="sxs-lookup"><span data-stu-id="0487b-143">hello following example lists hello tags on hello **samples/nginx** repository, in JSON format:</span></span>

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a><span data-ttu-id="0487b-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0487b-144">Next steps</span></span>

<span data-ttu-id="0487b-145">Dans ce guide de démarrage rapide, vous avez créé une instance managée de Registre de conteneur Azure à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0487b-145">In this quick start, you've created a managed Azure Container Registry instance using hello Azure portal.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0487b-146">Push de votre première image à l’aide de hello Docker CLI</span><span class="sxs-lookup"><span data-stu-id="0487b-146">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
