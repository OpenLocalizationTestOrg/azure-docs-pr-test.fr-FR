---
title: aaaManage Azure solutions avec PowerShell | Documents Microsoft
description: Utiliser Azure PowerShell et le Gestionnaire de ressources toomanage vos ressources.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: b33b7303-3330-4af8-8329-c80ac7e9bc7f
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: powershell
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: tomfitz
ms.openlocfilehash: 47a91af8d7eb59585bcfd43571ce76b90a0d7971
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-resources-with-azure-powershell-and-resource-manager"></a><span data-ttu-id="fcc07-103">Gérer les ressources avec Azure PowerShell et Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fcc07-103">Manage resources with Azure PowerShell and Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fcc07-104">Portail</span><span class="sxs-lookup"><span data-stu-id="fcc07-104">Portal</span></span>](resource-group-portal.md)
> * [<span data-ttu-id="fcc07-105">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="fcc07-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="fcc07-106">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="fcc07-106">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="fcc07-107">API REST</span><span class="sxs-lookup"><span data-stu-id="fcc07-107">REST API</span></span>](resource-manager-rest-api.md)
>
>

<span data-ttu-id="fcc07-108">Dans cet article, vous apprendrez comment toomanage vos solutions avec Azure PowerShell et le Gestionnaire de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="fcc07-108">In this article, you learn how toomanage your solutions with Azure PowerShell and Azure Resource Manager.</span></span> <span data-ttu-id="fcc07-109">Si vous n’êtes pas familiarisé avec Resource Manager, consultez la page [Vue d’ensemble de Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fcc07-109">If you are not familiar with Resource Manager, see [Resource Manager Overview](resource-group-overview.md).</span></span> <span data-ttu-id="fcc07-110">Cette rubrique se concentre sur les tâches de gestion.</span><span class="sxs-lookup"><span data-stu-id="fcc07-110">This topic focuses on management tasks.</span></span> <span data-ttu-id="fcc07-111">Vous allez :</span><span class="sxs-lookup"><span data-stu-id="fcc07-111">You will:</span></span>

1. <span data-ttu-id="fcc07-112">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="fcc07-112">Create a resource group</span></span>
2. <span data-ttu-id="fcc07-113">Ajouter un groupe de ressources toohello</span><span class="sxs-lookup"><span data-stu-id="fcc07-113">Add a resource toohello resource group</span></span>
3. <span data-ttu-id="fcc07-114">Ajouter une ressource de toohello de balise</span><span class="sxs-lookup"><span data-stu-id="fcc07-114">Add a tag toohello resource</span></span>
4. <span data-ttu-id="fcc07-115">Interroger les ressources selon des noms ou des valeurs de balise</span><span class="sxs-lookup"><span data-stu-id="fcc07-115">Query resources based on names or tag values</span></span>
5. <span data-ttu-id="fcc07-116">Appliquer et supprimer un verrou sur une ressource de hello</span><span class="sxs-lookup"><span data-stu-id="fcc07-116">Apply and remove a lock on hello resource</span></span>
6. <span data-ttu-id="fcc07-117">Supprimer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="fcc07-117">Delete a resource group</span></span>

<span data-ttu-id="fcc07-118">Cet article ne montre pas comment toodeploy un abonnement de tooyour de modèle de gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="fcc07-118">This article does not show how toodeploy a Resource Manager template tooyour subscription.</span></span> <span data-ttu-id="fcc07-119">Pour plus d’informations, voir [Déployer des ressources à l’aide de modèles Resource Manager et d’Azure PowerShell](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="fcc07-119">For that information, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span></span>

## <a name="get-started-with-azure-powershell"></a><span data-ttu-id="fcc07-120">Prise en main de Microsoft Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="fcc07-120">Get started with Azure PowerShell</span></span>

<span data-ttu-id="fcc07-121">Si vous n’avez pas installé Azure PowerShell, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fcc07-121">If you have not installed Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="fcc07-122">Si vous avez installé Azure PowerShell Bonjour cours mais que vous n'avez pas mis à jour récemment, envisagez d’installer la version la plus récente hello.</span><span class="sxs-lookup"><span data-stu-id="fcc07-122">If you have installed Azure PowerShell in hello past but have not updated it recently, consider installing hello latest version.</span></span> <span data-ttu-id="fcc07-123">Vous pouvez mettre à jour la version hello via hello même méthode que vous avez utilisé tooinstall il.</span><span class="sxs-lookup"><span data-stu-id="fcc07-123">You can update hello version through hello same method you used tooinstall it.</span></span> <span data-ttu-id="fcc07-124">Par exemple, si vous avez utilisé hello Web Platform Installer, relancer et recherchez une mise à jour.</span><span class="sxs-lookup"><span data-stu-id="fcc07-124">For example, if you used hello Web Platform Installer, launch it again and look for an update.</span></span>

<span data-ttu-id="fcc07-125">utilisation de votre version de module de ressources Azure, de hello toocheck hello suivant l’applet de commande :</span><span class="sxs-lookup"><span data-stu-id="fcc07-125">toocheck your version of hello Azure Resources module, use hello following cmdlet:</span></span>

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

<span data-ttu-id="fcc07-126">Cette rubrique a été mise à jour pour la version 3.3.0.</span><span class="sxs-lookup"><span data-stu-id="fcc07-126">This topic was updated for version 3.3.0.</span></span> <span data-ttu-id="fcc07-127">Si vous avez une version antérieure, votre expérience peut ne pas correspond hello décrite dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="fcc07-127">If you have an earlier version, your experience might not match hello steps shown in this topic.</span></span> <span data-ttu-id="fcc07-128">Pour plus d’informations sur les applets de commande hello dans cette version, consultez [AzureRM.Resources Module](/powershell/module/azurerm.resources).</span><span class="sxs-lookup"><span data-stu-id="fcc07-128">For documentation about hello cmdlets in this version, see [AzureRM.Resources Module](/powershell/module/azurerm.resources).</span></span>

## <a name="log-in-tooyour-azure-account"></a><span data-ttu-id="fcc07-129">Ouvrez une session dans tooyour compte Azure</span><span class="sxs-lookup"><span data-stu-id="fcc07-129">Log in tooyour Azure account</span></span>
<span data-ttu-id="fcc07-130">Avant d’utiliser votre solution, vous devez vous connecter tooyour compte.</span><span class="sxs-lookup"><span data-stu-id="fcc07-130">Before working on your solution, you must log in tooyour account.</span></span>

<span data-ttu-id="fcc07-131">toolog dans tooyour compte Azure, utilisez hello **AzureRmAccount de connexion** applet de commande.</span><span class="sxs-lookup"><span data-stu-id="fcc07-131">toolog in tooyour Azure account, use hello **Login-AzureRmAccount** cmdlet.</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="fcc07-132">applet de commande Hello vous demande des informations d’identification de connexion hello pour votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="fcc07-132">hello cmdlet prompts you for hello login credentials for your Azure account.</span></span> <span data-ttu-id="fcc07-133">Une fois connecté, il télécharge les paramètres de votre compte afin qu’ils soient disponible tooAzure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fcc07-133">After logging in, it downloads your account settings so they are available tooAzure PowerShell.</span></span>

<span data-ttu-id="fcc07-134">applet de commande Hello retourne des informations sur votre toouse d’abonnement de compte et hello pour les tâches de hello.</span><span class="sxs-lookup"><span data-stu-id="fcc07-134">hello cmdlet returns information about your account and hello subscription toouse for hello tasks.</span></span>

```powershell
Environment           : AzureCloud
Account               : example@contoso.com
TenantId              : {guid}
SubscriptionId        : {guid}
SubscriptionName      : Example Subscription One
CurrentStorageAccount :

```

<span data-ttu-id="fcc07-135">Si vous avez plusieurs abonnements, vous pouvez basculer tooa autre abonnement.</span><span class="sxs-lookup"><span data-stu-id="fcc07-135">If you have more than one subscription, you can switch tooa different subscription.</span></span> <span data-ttu-id="fcc07-136">Tout d’abord, nous allons voir tous les abonnements hello pour votre compte.</span><span class="sxs-lookup"><span data-stu-id="fcc07-136">First, let's see all hello subscriptions for your account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="fcc07-137">Les abonnements activés et désactivés sont retournés.</span><span class="sxs-lookup"><span data-stu-id="fcc07-137">It returns enabled and disabled subscriptions.</span></span>

```powershell
SubscriptionName : Example Subscription One
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Enabled

SubscriptionName : Example Subscription Two
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Enabled

SubscriptionName : Example Subscription Three
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Disabled
```

<span data-ttu-id="fcc07-138">tooswitch tooa autre abonnement, fournissez le nom d’abonnement de hello avec hello **Set-AzureRmContext** applet de commande.</span><span class="sxs-lookup"><span data-stu-id="fcc07-138">tooswitch tooa different subscription, provide hello subscription name with hello **Set-AzureRmContext** cmdlet.</span></span>

```powershell
Set-AzureRmContext -SubscriptionName "Example Subscription Two"
```

## <a name="create-a-resource-group"></a><span data-ttu-id="fcc07-139">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="fcc07-139">Create a resource group</span></span>
<span data-ttu-id="fcc07-140">Avant de déployer n’importe quel abonnement tooyour de ressources, vous devez créer un groupe de ressources qui contient des ressources hello.</span><span class="sxs-lookup"><span data-stu-id="fcc07-140">Before deploying any resources tooyour subscription, you must create a resource group that will contain hello resources.</span></span>

<span data-ttu-id="fcc07-141">toocreate un groupe de ressources, utilisez hello **New-AzureRmResourceGroup** applet de commande.</span><span class="sxs-lookup"><span data-stu-id="fcc07-141">toocreate a resource group, use hello **New-AzureRmResourceGroup** cmdlet.</span></span> <span data-ttu-id="fcc07-142">commande Hello utilise hello **nom** toospecify de paramètre un nom pour le groupe de ressources hello et hello **emplacement** paramètre toospecify son emplacement.</span><span class="sxs-lookup"><span data-stu-id="fcc07-142">hello command uses hello **Name** parameter toospecify a name for hello resource group and hello **Location** parameter toospecify its location.</span></span>

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location "South Central US"
```

<span data-ttu-id="fcc07-143">sortie de Hello est Bonjour suivant le format :</span><span class="sxs-lookup"><span data-stu-id="fcc07-143">hello output is in hello following format:</span></span>

```powershell
ResourceGroupName : TestRG1
Location          : southcentralus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/{guid}/resourceGroups/TestRG1
```

<span data-ttu-id="fcc07-144">Si vous avez besoin de groupe de ressources tooretrieve hello plus tard, utilisez hello suivant l’applet de commande :</span><span class="sxs-lookup"><span data-stu-id="fcc07-144">If you need tooretrieve hello resource group later, use hello following cmdlet:</span></span>

```powershell
Get-AzureRmResourceGroup -ResourceGroupName TestRG1
```

<span data-ttu-id="fcc07-145">tooget tous hello des groupes de ressources dans votre abonnement, ne spécifiez pas un nom :</span><span class="sxs-lookup"><span data-stu-id="fcc07-145">tooget all hello resource groups in your subscription, do not specify a name:</span></span>

```powershell
Get-AzureRmResourceGroup
```

## <a name="add-resources-tooa-resource-group"></a><span data-ttu-id="fcc07-146">Ajouter le groupe de ressources tooa de ressources</span><span class="sxs-lookup"><span data-stu-id="fcc07-146">Add resources tooa resource group</span></span>
<span data-ttu-id="fcc07-147">tooadd un groupe de ressources toohello, vous pouvez utiliser hello **New-AzureRmResource** applet de commande ou une applet de commande est de type toohello spécifique de ressource que vous créez (comme **New-AzureRmStorageAccount**).</span><span class="sxs-lookup"><span data-stu-id="fcc07-147">tooadd a resource toohello resource group, you can use hello **New-AzureRmResource** cmdlet or a cmdlet that is specific toohello type of resource you are creating (like **New-AzureRmStorageAccount**).</span></span> <span data-ttu-id="fcc07-148">Il peut s’avérer plus facile toouse une applet de commande qui est le type de ressource tooa spécifique, car il inclut des paramètres pour les propriétés hello qui sont nécessaires pour la ressource hello.</span><span class="sxs-lookup"><span data-stu-id="fcc07-148">You might find it easier toouse a cmdlet that is specific tooa resource type because it includes parameters for hello properties that are needed for hello new resource.</span></span> <span data-ttu-id="fcc07-149">toouse **New-AzureRmResource**, vous devez connaître tous les tooset de propriétés hello sans être invité à les entrer.</span><span class="sxs-lookup"><span data-stu-id="fcc07-149">toouse **New-AzureRmResource**, you must know all hello properties tooset without being prompted for them.</span></span>

<span data-ttu-id="fcc07-150">Toutefois, l’ajout d’une ressource via les applets de commande peut entraîner futures toute confusion, car la ressource hello n’existe pas dans un modèle de gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="fcc07-150">However, adding a resource through cmdlets might cause future confusion because hello new resource does not exist in a Resource Manager template.</span></span> <span data-ttu-id="fcc07-151">Microsoft vous recommande de définir l’infrastructure hello pour votre solution Windows Azure dans un modèle de gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="fcc07-151">Microsoft recommends defining hello infrastructure for your Azure solution in a Resource Manager template.</span></span> <span data-ttu-id="fcc07-152">Les modèles permettent de tooreliably et à plusieurs reprises de déployer votre solution.</span><span class="sxs-lookup"><span data-stu-id="fcc07-152">Templates enable you tooreliably and repeatedly deploy your solution.</span></span> <span data-ttu-id="fcc07-153">Dans le cadre de cette rubrique, vous créez un compte de stockage avec une applet de commande PowerShell et générerez plus tard un modèle à partir de votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="fcc07-153">For this topic, you create a storage account with a PowerShell cmdlet, but later you generate a template from your resource group.</span></span>

<span data-ttu-id="fcc07-154">Hello suivant l’applet de commande crée un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="fcc07-154">hello following cmdlet creates a storage account.</span></span> <span data-ttu-id="fcc07-155">Au lieu d’utiliser le nom hello hello illustré, fournissez un nom unique pour le compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="fcc07-155">Instead of using hello name shown in hello example, provide a unique name for hello storage account.</span></span> <span data-ttu-id="fcc07-156">nom de Hello doit être comprise entre 3 et 24 caractères et utiliser uniquement des chiffres et des lettres minuscules.</span><span class="sxs-lookup"><span data-stu-id="fcc07-156">hello name must be between 3 and 24 characters in length, and use only numbers and lower-case letters.</span></span> <span data-ttu-id="fcc07-157">Si vous utilisez le nom hello hello illustré, vous recevez une erreur, car ce nom est déjà en cours d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="fcc07-157">If you use hello name shown in hello example, you receive an error because that name is already in use.</span></span>

```powershell
New-AzureRmStorageAccount -ResourceGroupName TestRG1 -AccountName mystoragename -Type "Standard_LRS" -Location "South Central US"
```

<span data-ttu-id="fcc07-158">Si vous devez tooretrieve cette ressource ultérieurement, utilisez hello suivant l’applet de commande :</span><span class="sxs-lookup"><span data-stu-id="fcc07-158">If you need tooretrieve this resource later, use hello following cmdlet:</span></span>

```powershell
Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1
```

## <a name="add-a-tag"></a><span data-ttu-id="fcc07-159">Ajouter une balise</span><span class="sxs-lookup"><span data-stu-id="fcc07-159">Add a tag</span></span>

<span data-ttu-id="fcc07-160">Balises permettent tooorganize vos ressources en fonction des propriétés de toodifferent.</span><span class="sxs-lookup"><span data-stu-id="fcc07-160">Tags enable you tooorganize your resources according toodifferent properties.</span></span> <span data-ttu-id="fcc07-161">Par exemple, peut avoir plusieurs ressources dans différents groupes de ressources qui appartiennent toohello même service.</span><span class="sxs-lookup"><span data-stu-id="fcc07-161">For example, you may have several resources in different resource groups that belong toohello same department.</span></span> <span data-ttu-id="fcc07-162">Vous pouvez appliquer une toomark de ressources de toothose balise et la valeur service en tant qu’appartenant toohello même catégorie.</span><span class="sxs-lookup"><span data-stu-id="fcc07-162">You can apply a department tag and value toothose resources toomark them as belonging toohello same category.</span></span> <span data-ttu-id="fcc07-163">Vous pouvez également indiquer si une ressource est utilisée dans un environnement de production ou de test.</span><span class="sxs-lookup"><span data-stu-id="fcc07-163">Or, you can mark whether a resource is used in a production or test environment.</span></span> <span data-ttu-id="fcc07-164">Dans cette rubrique, vous appliquez des balises tooonly une ressource, mais dans votre environnement n’est plus probablement sens tooapply balises tooall vos ressources.</span><span class="sxs-lookup"><span data-stu-id="fcc07-164">In this topic, you apply tags tooonly one resource, but in your environment it most likely makes sense tooapply tags tooall your resources.</span></span>

<span data-ttu-id="fcc07-165">Hello suivant l’applet de commande applique le compte de stockage de deux balises tooyour :</span><span class="sxs-lookup"><span data-stu-id="fcc07-165">hello following cmdlet applies two tags tooyour storage account:</span></span>

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
 ```

<span data-ttu-id="fcc07-166">Les balises sont mises à jour en tant qu’objet unique.</span><span class="sxs-lookup"><span data-stu-id="fcc07-166">Tags are updated as a single object.</span></span> <span data-ttu-id="fcc07-167">tout d’abord, tooadd une ressource tooa balise qui contient déjà des balises, extraire les balises existantes hello.</span><span class="sxs-lookup"><span data-stu-id="fcc07-167">tooadd a tag tooa resource that already includes tags, first retrieve hello existing tags.</span></span> <span data-ttu-id="fcc07-168">Ajouter hello nouvelle balise toohello objet qui contient les balises existantes hello et appliquer toutes les ressources de toohello balises hello.</span><span class="sxs-lookup"><span data-stu-id="fcc07-168">Add hello new tag toohello object that contains hello existing tags, and reapply all hello tags toohello resource.</span></span>

```powershell
$tags = (Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
```

## <a name="search-for-resources"></a><span data-ttu-id="fcc07-169">Rechercher des ressources</span><span class="sxs-lookup"><span data-stu-id="fcc07-169">Search for resources</span></span>

<span data-ttu-id="fcc07-170">Hello d’utilisation **recherche-AzureRmResource** ressources tooretrieve d’applet de commande pour les conditions de recherche différente.</span><span class="sxs-lookup"><span data-stu-id="fcc07-170">Use hello **Find-AzureRmResource** cmdlet tooretrieve resources for different search conditions.</span></span>

* <span data-ttu-id="fcc07-171">tooget une ressource par son nom, fournissez hello **ResourceNameContains** paramètre :</span><span class="sxs-lookup"><span data-stu-id="fcc07-171">tooget a resource by name, provide hello **ResourceNameContains** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceNameContains mystoragename
  ```

* <span data-ttu-id="fcc07-172">tooget toutes les ressources hello dans un groupe de ressources, fournir hello **ResourceGroupNameContains** paramètre :</span><span class="sxs-lookup"><span data-stu-id="fcc07-172">tooget all hello resources in a resource group, provide hello **ResourceGroupNameContains** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceGroupNameContains TestRG1
  ```

* <span data-ttu-id="fcc07-173">tooget toutes les ressources hello avec un nom de balise et la valeur fournir hello **TagName** et **TagValue** paramètres :</span><span class="sxs-lookup"><span data-stu-id="fcc07-173">tooget all hello resources with a tag name and value, provide hello **TagName** and **TagValue** parameters:</span></span>

  ```powershell
  Find-AzureRmResource -TagName Dept -TagValue IT
  ```

* <span data-ttu-id="fcc07-174">ressources de hello tooall avec un type particulier, fournissent des hello **ResourceType** paramètre :</span><span class="sxs-lookup"><span data-stu-id="fcc07-174">tooall hello resources with a particular resource type, provide hello **ResourceType** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceType Microsoft.Storage/storageAccounts
  ```

## <a name="lock-a-resource"></a><span data-ttu-id="fcc07-175">Verrouiller une ressource</span><span class="sxs-lookup"><span data-stu-id="fcc07-175">Lock a resource</span></span>

<span data-ttu-id="fcc07-176">Lorsque vous devez toomake vraiment une ressource critique n’est pas accidentellement supprimée ou modifiée, appliquer une ressource de toohello de verrou.</span><span class="sxs-lookup"><span data-stu-id="fcc07-176">When you need toomake sure a critical resource is not accidentally deleted or modified, apply a lock toohello resource.</span></span> <span data-ttu-id="fcc07-177">Vous pouvez spécifier le niveau **CanNotDelete** ou **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="fcc07-177">You can specify either a **CanNotDelete** or **ReadOnly**.</span></span>

<span data-ttu-id="fcc07-178">toocreate ou supprimer les verrous de gestion, vous devez avoir accès trop`Microsoft.Authorization/*` ou `Microsoft.Authorization/locks/*` actions.</span><span class="sxs-lookup"><span data-stu-id="fcc07-178">toocreate or delete management locks, you must have access too`Microsoft.Authorization/*` or `Microsoft.Authorization/locks/*` actions.</span></span> <span data-ttu-id="fcc07-179">Rôles intégrés hello uniquement propriétaire et administrateur de l’accès utilisateur sont accordées à ces actions.</span><span class="sxs-lookup"><span data-stu-id="fcc07-179">Of hello built-in roles, only Owner and User Access Administrator are granted those actions.</span></span>

<span data-ttu-id="fcc07-180">tooapply un verrou, utilisez hello suivant l’applet de commande :</span><span class="sxs-lookup"><span data-stu-id="fcc07-180">tooapply a lock, use hello following cmdlet:</span></span>

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

<span data-ttu-id="fcc07-181">Hello ressource verrouillée Bonjour précédent exemple ne peut pas être supprimé tant que hello verrou soit supprimé.</span><span class="sxs-lookup"><span data-stu-id="fcc07-181">hello locked resource in hello preceding example cannot be deleted until hello lock is removed.</span></span> <span data-ttu-id="fcc07-182">tooremove un verrou, utilisez :</span><span class="sxs-lookup"><span data-stu-id="fcc07-182">tooremove a lock, use:</span></span>

```powershell
Remove-AzureRmResourceLock -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

<span data-ttu-id="fcc07-183">Pour plus d’informations sur la définition des verrous, consultez [Verrouiller des ressources avec Azure Resource Manager](resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="fcc07-183">For more information about setting locks, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

## <a name="remove-resources-or-resource-group"></a><span data-ttu-id="fcc07-184">Supprimer des ressources ou un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="fcc07-184">Remove resources or resource group</span></span>
<span data-ttu-id="fcc07-185">Vous pouvez supprimer une ressource ou un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="fcc07-185">You can remove a resource or resource group.</span></span> <span data-ttu-id="fcc07-186">Lorsque vous supprimez un groupe de ressources, vous supprimez également toutes les ressources de hello dans ce groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="fcc07-186">When you remove a resource group, you also remove all hello resources within that resource group.</span></span>

* <span data-ttu-id="fcc07-187">toodelete une ressource du groupe de ressources hello, utilisez hello **Remove-AzureRmResource** applet de commande.</span><span class="sxs-lookup"><span data-stu-id="fcc07-187">toodelete a resource from hello resource group, use hello **Remove-AzureRmResource** cmdlet.</span></span> <span data-ttu-id="fcc07-188">Cette applet de commande supprime la ressource de hello, mais ne supprime pas le groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="fcc07-188">This cmdlet deletes hello resource, but does not delete hello resource group.</span></span>

  ```powershell
  Remove-AzureRmResource -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
  ```

* <span data-ttu-id="fcc07-189">toodelete un groupe de ressources et toutes ses ressources, utilisez hello **Remove-AzureRmResourceGroup** applet de commande.</span><span class="sxs-lookup"><span data-stu-id="fcc07-189">toodelete a resource group and all its resources, use hello **Remove-AzureRmResourceGroup** cmdlet.</span></span>

  ```powershell
  Remove-AzureRmResourceGroup -Name TestRG1
  ```

<span data-ttu-id="fcc07-190">Pour les deux applets de commande, vous êtes invité tooconfirm que vous souhaitez tooremove hello ressource ou un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="fcc07-190">For both cmdlets, you are asked tooconfirm that you wish tooremove hello resource or resource group.</span></span> <span data-ttu-id="fcc07-191">Si les opération hello supprime correctement hello ressource ou un groupe de ressources, elle retourne **True**.</span><span class="sxs-lookup"><span data-stu-id="fcc07-191">If hello operation successfully deletes hello resource or resource group, it returns **True**.</span></span>

## <a name="run-resource-manager-scripts-with-azure-automation"></a><span data-ttu-id="fcc07-192">Exécuter des scripts Resource Manager avec Azure Automation</span><span class="sxs-lookup"><span data-stu-id="fcc07-192">Run Resource Manager scripts with Azure Automation</span></span>

<span data-ttu-id="fcc07-193">Cette rubrique vous montre comment les opérations de base tooperform sur vos ressources Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fcc07-193">This topic shows you how tooperform basic operations on your resources with Azure PowerShell.</span></span> <span data-ttu-id="fcc07-194">Pour les scénarios de gestion plus avancées, vous généralement souhaitez toocreate un script et réutilisez ce script en fonction des besoins, ou selon une planification.</span><span class="sxs-lookup"><span data-stu-id="fcc07-194">For more advanced management scenarios, you typically want toocreate a script, and reuse that script as needed or on a schedule.</span></span> <span data-ttu-id="fcc07-195">[Azure Automation](../automation/automation-intro.md) offre un moyen pour vous des scripts de tooautomate fréquemment utilisé pour gérer vos solutions Azure.</span><span class="sxs-lookup"><span data-stu-id="fcc07-195">[Azure Automation](../automation/automation-intro.md) provides a way for you tooautomate frequently used scripts that manage your Azure solutions.</span></span>

<span data-ttu-id="fcc07-196">Hello rubriques suivantes vous montrent comment toouse Azure Automation, Gestionnaire de ressources et PowerShell tooeffectively effectuent des tâches de gestion :</span><span class="sxs-lookup"><span data-stu-id="fcc07-196">hello following topics show you how toouse Azure Automation, Resource Manager, and PowerShell tooeffectively perform management tasks:</span></span>

- <span data-ttu-id="fcc07-197">Pour plus d’informations sur la création d’un runbook, consultez [Mon premier Runbook PowerShell](../automation/automation-first-runbook-textual-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="fcc07-197">For information about creating a runbook, see [My first PowerShell runbook](../automation/automation-first-runbook-textual-powershell.md).</span></span>
- <span data-ttu-id="fcc07-198">Pour plus d’informations sur l’utilisation des galeries de scripts, consultez [Galeries de runbooks et de modules pour Azure Automation](../automation/automation-runbook-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="fcc07-198">For information about working with galleries of scripts, see [Runbook and module galleries for Azure Automation](../automation/automation-runbook-gallery.md).</span></span>
- <span data-ttu-id="fcc07-199">Pour les procédures opérationnelles démarrer et arrêter les machines virtuelles, consultez [scénario d’Azure Automation : au format JSON d’à l’aide de balises toocreate une planification pour le démarrage de la machine virtuelle Azure et d’arrêt](../automation/automation-scenario-start-stop-vm-wjson-tags.md).</span><span class="sxs-lookup"><span data-stu-id="fcc07-199">For runbooks that start and stop virtual machines, see [Azure Automation scenario: Using JSON-formatted tags toocreate a schedule for Azure VM startup and shutdown](../automation/automation-scenario-start-stop-vm-wjson-tags.md).</span></span>
- <span data-ttu-id="fcc07-200">Pour les runbooks qui démarrent et arrêtent des machines virtuelles durant les heures creuses, consultez [Solution Start/Stop VMs during off-hours (Démarrer/arrêter des machines virtuelles durant les heures creuses) dans Automation](../automation/automation-solution-vm-management.md).</span><span class="sxs-lookup"><span data-stu-id="fcc07-200">For runbooks that start and stop virtual machines off-hours, see [Start/Stop VMs during off-hours solution in Automation](../automation/automation-solution-vm-management.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fcc07-201">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fcc07-201">Next steps</span></span>
* <span data-ttu-id="fcc07-202">toolearn sur la création de modèles du Gestionnaire de ressources, consultez [de création de modèles de gestionnaire de ressources Azure](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="fcc07-202">toolearn about creating Resource Manager templates, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="fcc07-203">toolearn sur le déploiement de modèles, consultez [déployer une application avec le modèle de gestionnaire de ressources Azure](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="fcc07-203">toolearn about deploying templates, see [Deploy an application with Azure Resource Manager Template](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="fcc07-204">Vous pouvez déplacer existant ressources tooa nouveau groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="fcc07-204">You can move existing resources tooa new resource group.</span></span> <span data-ttu-id="fcc07-205">Pour obtenir des exemples, consultez [tooNew de déplacement de ressources groupe de ressources ou d’un abonnement](resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="fcc07-205">For examples, see [Move Resources tooNew Resource Group or Subscription](resource-group-move-resources.md).</span></span>
* <span data-ttu-id="fcc07-206">Pour obtenir des conseils comment les entreprises peuvent utiliser le Gestionnaire de ressources tooeffectively gérer les abonnements, consultez [une vue de structure Azure enterprise - gouvernance de l’abonnement normative](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="fcc07-206">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

