---
title: "référentiels de Registre de conteneur aaaAzure | Documents Microsoft"
description: "Comment toouse les référentiels de Registre de conteneur Azure pour les images de Docker"
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
ms.openlocfilehash: 448fb812f537c9502041ce5fb372b0681a9dac4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-powershell"></a><span data-ttu-id="fc958-103">Créer un Registre de conteneur Docker privé à l’aide de hello Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="fc958-103">Create a private Docker container registry using hello Azure PowerShell</span></span>
<span data-ttu-id="fc958-104">Utiliser les commandes dans [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) toocreate un Registre de conteneur et de gérer ses paramètres de votre ordinateur Windows.</span><span class="sxs-lookup"><span data-stu-id="fc958-104">Use commands in [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) toocreate a container registry and manage its settings from your Windows computer.</span></span> <span data-ttu-id="fc958-105">Vous pouvez également créer et gérer des registres de conteneur à l’aide de hello [portail Azure](container-registry-get-started-portal.md), hello [CLI d’Azure](container-registry-get-started-azure-cli.md), ou par programme avec hello Registre de conteneur [API REST](https://go.microsoft.com/fwlink/p/?linkid=834376).</span><span class="sxs-lookup"><span data-stu-id="fc958-105">You can also create and manage container registries using hello [Azure portal](container-registry-get-started-portal.md), hello [Azure CLI](container-registry-get-started-azure-cli.md), or programmatically with hello Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>


* <span data-ttu-id="fc958-106">Pour des informations et des concepts, consultez [hello vue d’ensemble](container-registry-intro.md)</span><span class="sxs-lookup"><span data-stu-id="fc958-106">For background and concepts, see [hello overview](container-registry-intro.md)</span></span>
* <span data-ttu-id="fc958-107">Pour obtenir une liste complète des applets de commande pris en charge, consultez [Applets de commande de gestion d’Azure Container Registry](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/).</span><span class="sxs-lookup"><span data-stu-id="fc958-107">For a full list of supported cmdlets, see [Azure Container Registry Management Cmdlets](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="fc958-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="fc958-108">Prerequisites</span></span>
* <span data-ttu-id="fc958-109">**Azure PowerShell**: tooinstall et prise en main Azure PowerShell, consultez hello [des instructions d’installation](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="fc958-109">**Azure PowerShell**: tooinstall and get started with Azure PowerShell, see hello [installation instructions](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="fc958-110">Connectez-vous à tooyour abonnement Azure en exécutant `Login-AzureRMAccount`.</span><span class="sxs-lookup"><span data-stu-id="fc958-110">Log in tooyour Azure subscription by running `Login-AzureRMAccount`.</span></span> <span data-ttu-id="fc958-111">Pour plus d’informations, consultez [Bien démarrer avec Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep).</span><span class="sxs-lookup"><span data-stu-id="fc958-111">For more information, see [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep).</span></span>
* <span data-ttu-id="fc958-112">**Groupe de ressources** : créez un [groupe de ressources](../azure-resource-manager/resource-group-overview.md#resource-groups) avant de créer un registre de conteneur, ou utilisez un groupe de ressources existant.</span><span class="sxs-lookup"><span data-stu-id="fc958-112">**Resource group**: Create a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) before creating a container registry, or use an existing resource group.</span></span> <span data-ttu-id="fc958-113">Assurez-vous que le groupe de ressources hello est dans un emplacement où le service de Registre de conteneur de hello est [disponible](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="fc958-113">Make sure hello resource group is in a location where hello Container Registry service is [available](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="fc958-114">toocreate un groupe de ressources à l’aide d’Azure PowerShell, consultez [hello référence PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group).</span><span class="sxs-lookup"><span data-stu-id="fc958-114">toocreate a resource group using Azure PowerShell, see [hello PowerShell reference](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group).</span></span>
* <span data-ttu-id="fc958-115">**Compte de stockage** (facultatif) : créez un Azure standard [compte de stockage](../storage/common/storage-introduction.md) tooback Registre de conteneur hello Bonjour même emplacement.</span><span class="sxs-lookup"><span data-stu-id="fc958-115">**Storage account** (optional): Create a standard Azure [storage account](../storage/common/storage-introduction.md) tooback hello container registry in hello same location.</span></span> <span data-ttu-id="fc958-116">Si vous ne spécifiez pas un compte de stockage lors de la création d’un Registre avec `New-AzureRMContainerRegistry`, commande hello crée une pour vous.</span><span class="sxs-lookup"><span data-stu-id="fc958-116">If you don't specify a storage account when creating a registry with `New-AzureRMContainerRegistry`, hello command creates one for you.</span></span> <span data-ttu-id="fc958-117">toocreate un stockage compte à l’aide de PowerShell, consultez [hello référence PowerShell](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount).</span><span class="sxs-lookup"><span data-stu-id="fc958-117">toocreate a storage account using PowerShell, see [hello PowerShell reference](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount).</span></span> <span data-ttu-id="fc958-118">Pour l’instant, l’offre Stockage Premium n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="fc958-118">Currently Premium Storage is not supported.</span></span>
* <span data-ttu-id="fc958-119">**Principal de service** (facultatif) : lorsque vous créez un registre avec PowerShell, par défaut son accès n’est pas configuré.</span><span class="sxs-lookup"><span data-stu-id="fc958-119">**Service principal** (optional): When you create a registry with PowerShell, by default it is not set up for access.</span></span> <span data-ttu-id="fc958-120">Selon vos besoins, vous pouvez affecter un Registre tooa principal de service Azure Active Directory existant ou créer et affecter un nouveau.</span><span class="sxs-lookup"><span data-stu-id="fc958-120">Depending on your needs, you can assign an existing Azure Active Directory service principal tooa registry or create and assign a new one.</span></span> <span data-ttu-id="fc958-121">Vous pouvez également activer compte d’utilisateur admin du Registre hello.</span><span class="sxs-lookup"><span data-stu-id="fc958-121">Alternatively, you can enable hello registry's admin user account.</span></span> <span data-ttu-id="fc958-122">Consultez les sections hello plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="fc958-122">See hello sections later in this article.</span></span> <span data-ttu-id="fc958-123">Pour plus d’informations sur l’accès au Registre, consultez [authentifier avec le Registre de conteneur hello](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="fc958-123">For more information about registry access, see [Authenticate with hello container registry](container-registry-authentication.md).</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="fc958-124">Créer un registre de conteneur</span><span class="sxs-lookup"><span data-stu-id="fc958-124">Create a container registry</span></span>
<span data-ttu-id="fc958-125">Exécutez hello `New-AzureRMContainerRegistry` commande toocreate un Registre de conteneur.</span><span class="sxs-lookup"><span data-stu-id="fc958-125">Run hello `New-AzureRMContainerRegistry` command toocreate a container registry.</span></span>

> [!TIP]
> <span data-ttu-id="fc958-126">Lorsque vous créez un registre, spécifiez un nom de domaine global unique de niveau supérieur, contenant uniquement des chiffres et des lettres.</span><span class="sxs-lookup"><span data-stu-id="fc958-126">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span> <span data-ttu-id="fc958-127">nom de Registre Hello dans les exemples hello est `MyRegistry`, mais remplacer par un nom unique de votre choix.</span><span class="sxs-lookup"><span data-stu-id="fc958-127">hello registry name in hello examples is `MyRegistry`, but substitute a unique name of your own.</span></span>
>
>

<span data-ttu-id="fc958-128">Hello utilise hello Registre de conteneur toocreate minimal de paramètres de commande suivante `MyRegistry` dans le groupe de ressources hello `MyResourceGroup` Bonjour emplacement Amérique du Sud :</span><span class="sxs-lookup"><span data-stu-id="fc958-128">hello following command uses hello minimal parameters toocreate container registry `MyRegistry` in hello resource group `MyResourceGroup` in hello South Central US location:</span></span>

```PowerShell
$Registry = New-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

* <span data-ttu-id="fc958-129">`-StorageAccountName` est facultatif.</span><span class="sxs-lookup"><span data-stu-id="fc958-129">`-StorageAccountName` is optional.</span></span> <span data-ttu-id="fc958-130">Si ce n’est pas spécifié, un compte de stockage est créé avec un nom composé du nom de Registre hello et un horodatage dans hello spécifié le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="fc958-130">If not specified, a storage account is created with a name consisting of hello registry name and a timestamp in hello specified resource group.</span></span>

## <a name="assign-a-service-principal"></a><span data-ttu-id="fc958-131">Affecter un principal de service</span><span class="sxs-lookup"><span data-stu-id="fc958-131">Assign a service principal</span></span>
<span data-ttu-id="fc958-132">Utilisez tooassign de commandes PowerShell Azure Active Directory [principal du service](../azure-resource-manager/resource-group-authenticate-service-principal.md) tooa Registre.</span><span class="sxs-lookup"><span data-stu-id="fc958-132">Use PowerShell commands tooassign an Azure Active Directory [service principal](../azure-resource-manager/resource-group-authenticate-service-principal.md) tooa registry.</span></span> <span data-ttu-id="fc958-133">Hello principal du service dans ces exemples se voit attribuer hello propriétaire du rôle, mais vous pouvez affecter [autres rôles](../active-directory/role-based-access-control-configure.md) si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="fc958-133">hello service principal in these examples is assigned hello Owner role, but you can assign [other roles](../active-directory/role-based-access-control-configure.md) if you want.</span></span>

### <a name="create-a-service-principal"></a><span data-ttu-id="fc958-134">Créer un principal du service</span><span class="sxs-lookup"><span data-stu-id="fc958-134">Create a service principal</span></span>
<span data-ttu-id="fc958-135">Bonjour la commande suivante, un principal de service est créé.</span><span class="sxs-lookup"><span data-stu-id="fc958-135">In hello following command, a new service principal is created.</span></span> <span data-ttu-id="fc958-136">Spécifiez un mot de passe fort avec hello `-Password` paramètre.</span><span class="sxs-lookup"><span data-stu-id="fc958-136">Specify a strong password with hello `-Password` parameter.</span></span>

```PowerShell
$ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName ApplicationDisplayName -Password "MyPassword"
```

### <a name="assign-a-new-or-existing-service-principal"></a><span data-ttu-id="fc958-137">Affecter un principal de service existant ou nouveau</span><span class="sxs-lookup"><span data-stu-id="fc958-137">Assign a new or existing service principal</span></span>
<span data-ttu-id="fc958-138">Vous pouvez affecter un nouveau paramètre ou un Registre tooa principal de service existant.</span><span class="sxs-lookup"><span data-stu-id="fc958-138">You can assign a new or an existing service principal tooa registry.</span></span> <span data-ttu-id="fc958-139">tooassign il propriétaire du rôle accès toohello exécution de Registre, un toohello similaire commande l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="fc958-139">tooassign it Owner role access toohello registry, run a command similar toohello following example:</span></span>

```PowerShell
New-AzureRMRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Registry.Id
```

##<a name="sign-in-toohello-registry-with-hello-service-principal"></a><span data-ttu-id="fc958-140">Connectez-vous au Registre toohello avec principal du service hello</span><span class="sxs-lookup"><span data-stu-id="fc958-140">Sign in toohello registry with hello service principal</span></span>
<span data-ttu-id="fc958-141">Après avoir affecté Registre toohello principal du service hello, vous pouvez vous connecter avec hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="fc958-141">After assigning hello service principal toohello registry, you can sign in using hello following command:</span></span>

```PowerShell
docker login -u $ServicePrincipal.ApplicationId -p myPassword
```

## <a name="manage-admin-credentials"></a><span data-ttu-id="fc958-142">Gérer les informations d’identification de l’administrateur</span><span class="sxs-lookup"><span data-stu-id="fc958-142">Manage admin credentials</span></span>
<span data-ttu-id="fc958-143">Un compte d’administrateur est automatiquement créé pour chaque registre de conteneur et est désactivé par défaut.</span><span class="sxs-lookup"><span data-stu-id="fc958-143">An admin account is automatically created for each container registry and is disabled by default.</span></span> <span data-ttu-id="fc958-144">Hello exemples suivants illustrent les commandes PowerShell toomanage hello admin informations d’identification pour votre Registre de conteneur.</span><span class="sxs-lookup"><span data-stu-id="fc958-144">hello following examples show PowerShell commands toomanage hello admin credentials for your container registry.</span></span>

### <a name="obtain-admin-user-credentials"></a><span data-ttu-id="fc958-145">Obtenir les informations d’identification de l’utilisateur Admin</span><span class="sxs-lookup"><span data-stu-id="fc958-145">Obtain admin user credentials</span></span>
```PowerShell
Get-AzureRMContainerRegistryCredential -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

### <a name="enable-admin-user-for-an-existing-registry"></a><span data-ttu-id="fc958-146">Activer l’utilisateur Admin pour un registre existant</span><span class="sxs-lookup"><span data-stu-id="fc958-146">Enable admin user for an existing registry</span></span>
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -EnableAdminUser
```

### <a name="disable-admin-user-for-an-existing-registry"></a><span data-ttu-id="fc958-147">Désactiver l’utilisateur Admin pour un registre existant</span><span class="sxs-lookup"><span data-stu-id="fc958-147">Disable admin user for an existing registry</span></span>
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -DisableAdminUser
```

## <a name="next-steps"></a><span data-ttu-id="fc958-148">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fc958-148">Next steps</span></span>
* [<span data-ttu-id="fc958-149">Push de votre première image à l’aide de hello Docker CLI</span><span class="sxs-lookup"><span data-stu-id="fc958-149">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
