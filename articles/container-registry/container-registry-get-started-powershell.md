---
title: "Créer des référentiels Azure Container Registry | Microsoft Docs"
description: "Utiliser des référentiels Azure Container Registry pour gérer des images Docker"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: cristyg
ms.openlocfilehash: 1e5d5ea5b1ec121fe008abc48178b1d58f540ce1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-private-docker-container-registry-using-the-azure-powershell"></a><span data-ttu-id="66501-103">Créer un registre de conteneurs Docker privé à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="66501-103">Create a private Docker container registry using the Azure PowerShell</span></span>
<span data-ttu-id="66501-104">Utilisez les commandes dans [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) pour créer un registre de conteneurs et gérer ses paramètres à partir de votre ordinateur Windows.</span><span class="sxs-lookup"><span data-stu-id="66501-104">Use commands in [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) to create a container registry and manage its settings from your Windows computer.</span></span> <span data-ttu-id="66501-105">Vous pouvez également créer et gérer des registres de conteneurs à l’aide du [portail Azure](container-registry-get-started-portal.md), d’[Azure CLI](container-registry-get-started-azure-cli.md) ou par programmation avec [l’API REST](https://go.microsoft.com/fwlink/p/?linkid=834376) de registre de conteneurs.</span><span class="sxs-lookup"><span data-stu-id="66501-105">You can also create and manage container registries using the [Azure portal](container-registry-get-started-portal.md), the [Azure CLI](container-registry-get-started-azure-cli.md), or programmatically with the Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>


* <span data-ttu-id="66501-106">Pour plus d’informations, notamment sur les concepts, consultez la [page de présentation](container-registry-intro.md)</span><span class="sxs-lookup"><span data-stu-id="66501-106">For background and concepts, see [the overview](container-registry-intro.md)</span></span>
* <span data-ttu-id="66501-107">Pour obtenir une liste complète des applets de commande pris en charge, consultez [Applets de commande de gestion d’Azure Container Registry](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/).</span><span class="sxs-lookup"><span data-stu-id="66501-107">For a full list of supported cmdlets, see [Azure Container Registry Management Cmdlets](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="66501-108">Prérequis</span><span class="sxs-lookup"><span data-stu-id="66501-108">Prerequisites</span></span>
* <span data-ttu-id="66501-109">**Azure PowerShell** : pour installer et découvrir Azure PowerShell, consultez les [instructions d’installation](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="66501-109">**Azure PowerShell**: To install and get started with Azure PowerShell, see the [installation instructions](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="66501-110">Connectez-vous à votre abonnement Azure en exécutant `Login-AzureRMAccount`.</span><span class="sxs-lookup"><span data-stu-id="66501-110">Log in to your Azure subscription by running `Login-AzureRMAccount`.</span></span> <span data-ttu-id="66501-111">Pour plus d’informations, consultez [Bien démarrer avec Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep).</span><span class="sxs-lookup"><span data-stu-id="66501-111">For more information, see [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep).</span></span>
* <span data-ttu-id="66501-112">**Groupe de ressources** : créez un [groupe de ressources](../azure-resource-manager/resource-group-overview.md#resource-groups) avant de créer un registre de conteneur, ou utilisez un groupe de ressources existant.</span><span class="sxs-lookup"><span data-stu-id="66501-112">**Resource group**: Create a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) before creating a container registry, or use an existing resource group.</span></span> <span data-ttu-id="66501-113">Assurez-vous que le groupe de ressources est dans un emplacement où le service Container Registry est [disponible](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="66501-113">Make sure the resource group is in a location where the Container Registry service is [available](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="66501-114">Pour créer un groupe de ressources à l’aide d’Azure PowerShell, consultez [la documentation de référence de Powershell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group).</span><span class="sxs-lookup"><span data-stu-id="66501-114">To create a resource group using Azure PowerShell, see [the PowerShell reference](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group).</span></span>
* <span data-ttu-id="66501-115">**Compte de stockage** (facultatif) : créez un [compte de stockage](../storage/common/storage-introduction.md) Azure standard pour prendre en charge le registre de conteneur dans le même emplacement.</span><span class="sxs-lookup"><span data-stu-id="66501-115">**Storage account** (optional): Create a standard Azure [storage account](../storage/common/storage-introduction.md) to back the container registry in the same location.</span></span> <span data-ttu-id="66501-116">Si vous ne spécifiez pas de compte de stockage lors de la création d’un registre avec `New-AzureRMContainerRegistry`, la commande en crée un pour vous.</span><span class="sxs-lookup"><span data-stu-id="66501-116">If you don't specify a storage account when creating a registry with `New-AzureRMContainerRegistry`, the command creates one for you.</span></span> <span data-ttu-id="66501-117">Pour créer un compte de stockage à l’aide de PowerShell, consultez [la documentation de référence de PowerShell](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount).</span><span class="sxs-lookup"><span data-stu-id="66501-117">To create a storage account using PowerShell, see [the PowerShell reference](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount).</span></span> <span data-ttu-id="66501-118">Pour l’instant, l’offre Stockage Premium n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="66501-118">Currently Premium Storage is not supported.</span></span>
* <span data-ttu-id="66501-119">**Principal de service** (facultatif) : lorsque vous créez un registre avec PowerShell, par défaut son accès n’est pas configuré.</span><span class="sxs-lookup"><span data-stu-id="66501-119">**Service principal** (optional): When you create a registry with PowerShell, by default it is not set up for access.</span></span> <span data-ttu-id="66501-120">Selon vos besoins, vous pouvez assigner un principal de service Azure Active Directory existant à un registre, ou en créer un et l’y affecter.</span><span class="sxs-lookup"><span data-stu-id="66501-120">Depending on your needs, you can assign an existing Azure Active Directory service principal to a registry or create and assign a new one.</span></span> <span data-ttu-id="66501-121">Vous pouvez également activer le compte de l’utilisateur administrateur du registre.</span><span class="sxs-lookup"><span data-stu-id="66501-121">Alternatively, you can enable the registry's admin user account.</span></span> <span data-ttu-id="66501-122">Consultez les sections disponibles plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="66501-122">See the sections later in this article.</span></span> <span data-ttu-id="66501-123">Pour plus d’informations sur l’accès au registre, consultez la section relative à [l’authentification auprès d’un conteneur](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="66501-123">For more information about registry access, see [Authenticate with the container registry](container-registry-authentication.md).</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="66501-124">Créer un registre de conteneur</span><span class="sxs-lookup"><span data-stu-id="66501-124">Create a container registry</span></span>
<span data-ttu-id="66501-125">Exécutez la commande `New-AzureRMContainerRegistry` pour créer un registre de conteneur.</span><span class="sxs-lookup"><span data-stu-id="66501-125">Run the `New-AzureRMContainerRegistry` command to create a container registry.</span></span>

> [!TIP]
> <span data-ttu-id="66501-126">Lorsque vous créez un registre, spécifiez un nom de domaine global unique de niveau supérieur, contenant uniquement des chiffres et des lettres.</span><span class="sxs-lookup"><span data-stu-id="66501-126">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span> <span data-ttu-id="66501-127">Dans cet exemple, le nom de registre est `MyRegistry`, mais vous pouvez le remplacer par un nom unique de votre choix.</span><span class="sxs-lookup"><span data-stu-id="66501-127">The registry name in the examples is `MyRegistry`, but substitute a unique name of your own.</span></span>
>
>

<span data-ttu-id="66501-128">La commande suivante utilise les paramètres minimum pour créer le registre de conteneur `MyRegistry` dans le groupe de ressources `MyResourceGroup` à l’emplacement Sud du centre des États-Unis :</span><span class="sxs-lookup"><span data-stu-id="66501-128">The following command uses the minimal parameters to create container registry `MyRegistry` in the resource group `MyResourceGroup` in the South Central US location:</span></span>

```PowerShell
$Registry = New-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

* <span data-ttu-id="66501-129">`-StorageAccountName` est facultatif.</span><span class="sxs-lookup"><span data-stu-id="66501-129">`-StorageAccountName` is optional.</span></span> <span data-ttu-id="66501-130">S’il n’est pas spécifié, un compte de stockage est créé avec un nom comprenant le nom de Registre et un horodatage dans le groupe de ressources spécifié.</span><span class="sxs-lookup"><span data-stu-id="66501-130">If not specified, a storage account is created with a name consisting of the registry name and a timestamp in the specified resource group.</span></span>

## <a name="assign-a-service-principal"></a><span data-ttu-id="66501-131">Affecter un principal de service</span><span class="sxs-lookup"><span data-stu-id="66501-131">Assign a service principal</span></span>
<span data-ttu-id="66501-132">Utilisez les commandes PowerShell pour affecter un [principal de service](../azure-resource-manager/resource-group-authenticate-service-principal.md) Azure Active Directory à un registre.</span><span class="sxs-lookup"><span data-stu-id="66501-132">Use PowerShell commands to assign an Azure Active Directory [service principal](../azure-resource-manager/resource-group-authenticate-service-principal.md) to a registry.</span></span> <span data-ttu-id="66501-133">Le principal du service dans ces exemples est affecté au rôle de propriétaire, mais vous pouvez attribuer [d’autres rôles](../active-directory/role-based-access-control-configure.md) si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="66501-133">The service principal in these examples is assigned the Owner role, but you can assign [other roles](../active-directory/role-based-access-control-configure.md) if you want.</span></span>

### <a name="create-a-service-principal"></a><span data-ttu-id="66501-134">Créer un principal du service</span><span class="sxs-lookup"><span data-stu-id="66501-134">Create a service principal</span></span>
<span data-ttu-id="66501-135">Dans la commande suivante, un principal de service est créé.</span><span class="sxs-lookup"><span data-stu-id="66501-135">In the following command, a new service principal is created.</span></span> <span data-ttu-id="66501-136">Spécifiez un mot de passe fort avec le paramètre `-Password`.</span><span class="sxs-lookup"><span data-stu-id="66501-136">Specify a strong password with the `-Password` parameter.</span></span>

```PowerShell
$ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName ApplicationDisplayName -Password "MyPassword"
```

### <a name="assign-a-new-or-existing-service-principal"></a><span data-ttu-id="66501-137">Affecter un principal de service existant ou nouveau</span><span class="sxs-lookup"><span data-stu-id="66501-137">Assign a new or existing service principal</span></span>
<span data-ttu-id="66501-138">Vous pouvez affecter un principal de service nouveau ou existant à un registre.</span><span class="sxs-lookup"><span data-stu-id="66501-138">You can assign a new or an existing service principal to a registry.</span></span> <span data-ttu-id="66501-139">Pour attribuer l’accès du rôle Propriétaire au registre, exécutez une commande similaire à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="66501-139">To assign it Owner role access to the registry, run a command similar to the following example:</span></span>

```PowerShell
New-AzureRMRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Registry.Id
```

##<a name="sign-in-to-the-registry-with-the-service-principal"></a><span data-ttu-id="66501-140">Se connecter au registre avec le principal de service</span><span class="sxs-lookup"><span data-stu-id="66501-140">Sign in to the registry with the service principal</span></span>
<span data-ttu-id="66501-141">Après avoir affecté le principal de service au registre, vous pouvez vous connecter à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="66501-141">After assigning the service principal to the registry, you can sign in using the following command:</span></span>

```PowerShell
docker login -u $ServicePrincipal.ApplicationId -p myPassword
```

## <a name="manage-admin-credentials"></a><span data-ttu-id="66501-142">Gérer les informations d’identification de l’administrateur</span><span class="sxs-lookup"><span data-stu-id="66501-142">Manage admin credentials</span></span>
<span data-ttu-id="66501-143">Un compte d’administrateur est automatiquement créé pour chaque registre de conteneur et est désactivé par défaut.</span><span class="sxs-lookup"><span data-stu-id="66501-143">An admin account is automatically created for each container registry and is disabled by default.</span></span> <span data-ttu-id="66501-144">Les exemples suivants montrent les commandes PowerShell permettant de gérer les informations d’identification d’administrateur pour votre registre de conteneurs.</span><span class="sxs-lookup"><span data-stu-id="66501-144">The following examples show PowerShell commands to manage the admin credentials for your container registry.</span></span>

### <a name="obtain-admin-user-credentials"></a><span data-ttu-id="66501-145">Obtenir les informations d’identification de l’utilisateur Admin</span><span class="sxs-lookup"><span data-stu-id="66501-145">Obtain admin user credentials</span></span>
```PowerShell
Get-AzureRMContainerRegistryCredential -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

### <a name="enable-admin-user-for-an-existing-registry"></a><span data-ttu-id="66501-146">Activer l’utilisateur Admin pour un registre existant</span><span class="sxs-lookup"><span data-stu-id="66501-146">Enable admin user for an existing registry</span></span>
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -EnableAdminUser
```

### <a name="disable-admin-user-for-an-existing-registry"></a><span data-ttu-id="66501-147">Désactiver l’utilisateur Admin pour un registre existant</span><span class="sxs-lookup"><span data-stu-id="66501-147">Disable admin user for an existing registry</span></span>
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -DisableAdminUser
```

## <a name="next-steps"></a><span data-ttu-id="66501-148">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="66501-148">Next steps</span></span>
* [<span data-ttu-id="66501-149">Effectuer un push de votre première image à l’aide de l’interface CLI Docker</span><span class="sxs-lookup"><span data-stu-id="66501-149">Push your first image using the Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
