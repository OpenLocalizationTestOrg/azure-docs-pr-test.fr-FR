---
title: "Registre Docker privé aaaCreate - portail Azure | Documents Microsoft"
description: "Commencer à créer et gérer des registres de conteneur Docker privés avec hello portail Azure"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: dlepow
tags: 
keywords: 
ms.assetid: 53a3b3cb-ab4b-4560-bc00-366e2759f1a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 40f3ce44fea26e5fbeca865c9da6df55c2df9511
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-portal"></a><span data-ttu-id="4f095-103">Créer un Registre de conteneur Docker privé à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="4f095-103">Create a private Docker container registry using hello Azure portal</span></span>
<span data-ttu-id="4f095-104">Hello toocreate portail Azure un Registre de conteneur et gérer ses paramètres.</span><span class="sxs-lookup"><span data-stu-id="4f095-104">Use hello Azure portal toocreate a container registry and manage its settings.</span></span> <span data-ttu-id="4f095-105">Vous pouvez également créer et gérer des registres de conteneur à l’aide de hello [Azure CLI 2.0 commandes](container-registry-get-started-azure-cli.md), [Azure PowerShell](container-registry-get-started-powershell.md) ou par programme avec hello Registre de conteneur [l’API REST](https://go.microsoft.com/fwlink/p/?linkid=834376).</span><span class="sxs-lookup"><span data-stu-id="4f095-105">You can also create and manage container registries using hello [Azure CLI 2.0 commands](container-registry-get-started-azure-cli.md), [Azure PowerShell](container-registry-get-started-powershell.md) or programmatically with hello Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>

<span data-ttu-id="4f095-106">Pour des informations et des concepts, consultez [hello vue d’ensemble](container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="4f095-106">For background and concepts, see [hello overview](container-registry-intro.md).</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="4f095-107">Créer un registre de conteneur</span><span class="sxs-lookup"><span data-stu-id="4f095-107">Create a container registry</span></span>
1. <span data-ttu-id="4f095-108">Bonjour [portail Azure](https://portal.azure.com), cliquez sur **+ nouveau**.</span><span class="sxs-lookup"><span data-stu-id="4f095-108">In hello [Azure portal](https://portal.azure.com), click **+ New**.</span></span>
2. <span data-ttu-id="4f095-109">Marketplace hello de recherche pour **Registre de conteneur Azure**.</span><span class="sxs-lookup"><span data-stu-id="4f095-109">Search hello marketplace for **Azure container registry**.</span></span>
3. <span data-ttu-id="4f095-110">Sélectionnez **Azure Container Registry**, avec l’éditeur **Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="4f095-110">Select **Azure Container Registry**, with publisher **Microsoft**.</span></span>
    <span data-ttu-id="4f095-111">![Service Container Registry dans Azure Marketplace](./media/container-registry-get-started-portal/container-registry-marketplace.png)</span><span class="sxs-lookup"><span data-stu-id="4f095-111">![Container Registry service in Azure Marketplace](./media/container-registry-get-started-portal/container-registry-marketplace.png)</span></span>
4. <span data-ttu-id="4f095-112">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="4f095-112">Click **Create**.</span></span> <span data-ttu-id="4f095-113">Hello **Registre de conteneur Azure** panneau s’affiche.</span><span class="sxs-lookup"><span data-stu-id="4f095-113">hello **Azure Container Registry** blade appears.</span></span>

    ![Paramètres de Container Registry](./media/container-registry-get-started-portal/container-registry-settings.png)
5. <span data-ttu-id="4f095-115">Bonjour **Registre de conteneur Azure** panneau, entrez hello informations suivantes.</span><span class="sxs-lookup"><span data-stu-id="4f095-115">In hello **Azure Container Registry** blade, enter hello following information.</span></span> <span data-ttu-id="4f095-116">Une fois ces opérations effectuées, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="4f095-116">Click **Create** when you are done.</span></span>

    <span data-ttu-id="4f095-117">a.</span><span class="sxs-lookup"><span data-stu-id="4f095-117">a.</span></span> <span data-ttu-id="4f095-118">**Nom du registre** : Un nom de domaine global unique et de niveau supérieur pour votre registre spécifique.</span><span class="sxs-lookup"><span data-stu-id="4f095-118">**Registry name**: A globally unique top-level domain name for your specific registry.</span></span> <span data-ttu-id="4f095-119">Dans cet exemple, le nom de Registre hello est *myRegistry01*, mais remplacer par un nom unique de votre choix.</span><span class="sxs-lookup"><span data-stu-id="4f095-119">In this example, hello registry name is *myRegistry01*, but substitute a unique name of your own.</span></span> <span data-ttu-id="4f095-120">nom de Hello peut contenir que des lettres et des chiffres.</span><span class="sxs-lookup"><span data-stu-id="4f095-120">hello name can contain only letters and numbers.</span></span>

    <span data-ttu-id="4f095-121">b.</span><span class="sxs-lookup"><span data-stu-id="4f095-121">b.</span></span> <span data-ttu-id="4f095-122">**Groupe de ressources**: sélectionnez un existant [groupe de ressources](../azure-resource-manager/resource-group-overview.md#resource-groups) ou nom du type hello pour un nouveau.</span><span class="sxs-lookup"><span data-stu-id="4f095-122">**Resource group**: Select an existing [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) or type hello name for a new one.</span></span>

    <span data-ttu-id="4f095-123">c.</span><span class="sxs-lookup"><span data-stu-id="4f095-123">c.</span></span> <span data-ttu-id="4f095-124">**Emplacement**: sélectionnez un emplacement de centre de données Azure où le service de hello est [disponible](https://azure.microsoft.com/regions/services/), tel que **Amérique du Sud**.</span><span class="sxs-lookup"><span data-stu-id="4f095-124">**Location**: Select an Azure datacenter location where hello service is [available](https://azure.microsoft.com/regions/services/), such as **South Central US**.</span></span>

    <span data-ttu-id="4f095-125">d.</span><span class="sxs-lookup"><span data-stu-id="4f095-125">d.</span></span> <span data-ttu-id="4f095-126">**L’utilisateur Admin**: Si vous le souhaitez, activer un Registre de hello tooaccess admin utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4f095-126">**Admin user**: If you want, enable an admin user tooaccess hello registry.</span></span> <span data-ttu-id="4f095-127">Vous pouvez modifier ce paramètre après avoir créé le Registre de hello.</span><span class="sxs-lookup"><span data-stu-id="4f095-127">You can change this setting after creating hello registry.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="4f095-128">En outre tooproviding accéder via un compte d’utilisateur administrateur, les registres de conteneur prend en charge l’authentification soutenue par des principaux du service Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4f095-128">In addition tooproviding access through an admin user account, container registries support authentication backed by Azure Active Directory service principals.</span></span> <span data-ttu-id="4f095-129">Pour plus d’informations et pour connaître les éléments à prendre en considération, consultez la section relative à [l’authentification auprès d’un conteneur](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="4f095-129">For more information and considerations, see [Authenticate with a container registry](container-registry-authentication.md).</span></span>
      >

    <span data-ttu-id="4f095-130">e.</span><span class="sxs-lookup"><span data-stu-id="4f095-130">e.</span></span> <span data-ttu-id="4f095-131">**Compte de stockage**: utiliser toocreate de paramètre par défaut hello un [compte de stockage](../storage/common/storage-introduction.md), ou sélectionnez un compte de stockage existant dans hello même emplacement.</span><span class="sxs-lookup"><span data-stu-id="4f095-131">**Storage account**: Use hello default setting toocreate a [storage account](../storage/common/storage-introduction.md), or select an existing storage account in hello same location.</span></span> <span data-ttu-id="4f095-132">Pour l’instant, l’offre Stockage Premium n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="4f095-132">Currently Premium Storage is not supported.</span></span>

## <a name="manage-registry-settings"></a><span data-ttu-id="4f095-133">Gérer les paramètres du registre</span><span class="sxs-lookup"><span data-stu-id="4f095-133">Manage registry settings</span></span>
<span data-ttu-id="4f095-134">Après avoir créé le Registre de hello, recherche hello paramètres du Registre en partant de hello **conteneur registres** panneau dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="4f095-134">After creating hello registry, find hello registry settings by starting at hello **Container Registries** blade in hello portal.</span></span> <span data-ttu-id="4f095-135">Par exemple, vous devrez peut-être toolog de paramètres hello dans le Registre de tooyour, ou peut souhaité tooenable ou désactiver l’utilisateur admin hello.</span><span class="sxs-lookup"><span data-stu-id="4f095-135">For example, you might need hello settings toolog in tooyour registry, or you might want tooenable or disable hello admin user.</span></span>

1. <span data-ttu-id="4f095-136">Sur hello **conteneur registres** panneau, cliquez sur nom hello de votre Registre.</span><span class="sxs-lookup"><span data-stu-id="4f095-136">On hello **Container Registries** blade, click hello name of your registry.</span></span>

    ![Panneau Container Registry](./media/container-registry-get-started-portal/container-registry-blade.png)
2. <span data-ttu-id="4f095-138">Cliquez sur les paramètres d’accès toomanage, **clé d’accès**.</span><span class="sxs-lookup"><span data-stu-id="4f095-138">toomanage access settings, click **Access key**.</span></span>

    ![Accès à Container Registry](./media/container-registry-get-started-portal/container-registry-access.png)
3. <span data-ttu-id="4f095-140">Notez hello suivant les paramètres :</span><span class="sxs-lookup"><span data-stu-id="4f095-140">Note hello following settings:</span></span>

   * <span data-ttu-id="4f095-141">**Serveur de connexion** -nom qualifié complet de hello vous utilisez toolog dans le Registre de toohello.</span><span class="sxs-lookup"><span data-stu-id="4f095-141">**Login server** - hello fully qualified name you use toolog in toohello registry.</span></span> <span data-ttu-id="4f095-142">Dans cet exemple, il s’agit de `myregistry01.azurecr.io`.</span><span class="sxs-lookup"><span data-stu-id="4f095-142">In this example, it is `myregistry01.azurecr.io`.</span></span>
   * <span data-ttu-id="4f095-143">**L’utilisateur Admin** - activer/désactiver tooenable ou désactiver le compte d’utilisateur admin du Registre hello.</span><span class="sxs-lookup"><span data-stu-id="4f095-143">**Admin user** - Toggle tooenable or disable hello registry's admin user account.</span></span>
   * <span data-ttu-id="4f095-144">**Nom d’utilisateur** et **mot de passe** -hello les informations d’identification du compte d’utilisateur administrateur hello (si activé) vous pouvez utiliser toolog dans le Registre de toohello.</span><span class="sxs-lookup"><span data-stu-id="4f095-144">**Username** and **Password** - hello credentials of hello admin user account (if enabled) you can use toolog in toohello registry.</span></span> <span data-ttu-id="4f095-145">Vous pouvez éventuellement régénérer les mots de passe hello.</span><span class="sxs-lookup"><span data-stu-id="4f095-145">You can optionally regenerate hello passwords.</span></span> <span data-ttu-id="4f095-146">Deux mots de passe sont créés afin que vous pouvez maintenir Registre toohello de connexions à l’aide d’un mot de passe pendant la régénération de hello autre mot de passe.</span><span class="sxs-lookup"><span data-stu-id="4f095-146">Two passwords are created so that you can maintain connections toohello registry by using one password while you regenerate hello other password.</span></span> <span data-ttu-id="4f095-147">tooauthenticate avec un principal de service au lieu de cela, consultez [authentifier avec un Registre de conteneur Docker privé](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="4f095-147">tooauthenticate with a service principal instead, see [Authenticate with a private Docker container registry](container-registry-authentication.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4f095-148">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4f095-148">Next steps</span></span>
* [<span data-ttu-id="4f095-149">Push de votre première image à l’aide de hello Docker CLI</span><span class="sxs-lookup"><span data-stu-id="4f095-149">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
