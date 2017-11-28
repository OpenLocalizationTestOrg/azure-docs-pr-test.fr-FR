---
title: "Gérer des solutions Azure avec PowerShell | Microsoft Docs"
description: "Utilisez Azure PowerShell et Resource Manager pour gérer vos ressources."
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
ms.openlocfilehash: ff42e5cb29005c5f4b97babdae58bef9382071f0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="manage-resources-with-azure-powershell-and-resource-manager"></a><span data-ttu-id="a37bf-103">Gérer les ressources avec Azure PowerShell et Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a37bf-103">Manage resources with Azure PowerShell and Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a37bf-104">Portail</span><span class="sxs-lookup"><span data-stu-id="a37bf-104">Portal</span></span>](resource-group-portal.md)
> * [<span data-ttu-id="a37bf-105">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="a37bf-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="a37bf-106">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a37bf-106">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="a37bf-107">API REST</span><span class="sxs-lookup"><span data-stu-id="a37bf-107">REST API</span></span>](resource-manager-rest-api.md)
>
>

<span data-ttu-id="a37bf-108">Dans cet article, vous allez apprendre à gérer vos solutions avec Azure PowerShell et Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a37bf-108">In this article, you learn how to manage your solutions with Azure PowerShell and Azure Resource Manager.</span></span> <span data-ttu-id="a37bf-109">Si vous n’êtes pas familiarisé avec Resource Manager, consultez la page [Vue d’ensemble de Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a37bf-109">If you are not familiar with Resource Manager, see [Resource Manager Overview](resource-group-overview.md).</span></span> <span data-ttu-id="a37bf-110">Cette rubrique se concentre sur les tâches de gestion.</span><span class="sxs-lookup"><span data-stu-id="a37bf-110">This topic focuses on management tasks.</span></span> <span data-ttu-id="a37bf-111">Vous allez :</span><span class="sxs-lookup"><span data-stu-id="a37bf-111">You will:</span></span>

1. <span data-ttu-id="a37bf-112">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="a37bf-112">Create a resource group</span></span>
2. <span data-ttu-id="a37bf-113">Ajouter une ressource au groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="a37bf-113">Add a resource to the resource group</span></span>
3. <span data-ttu-id="a37bf-114">Ajouter une balise à la ressource</span><span class="sxs-lookup"><span data-stu-id="a37bf-114">Add a tag to the resource</span></span>
4. <span data-ttu-id="a37bf-115">Interroger les ressources selon des noms ou des valeurs de balise</span><span class="sxs-lookup"><span data-stu-id="a37bf-115">Query resources based on names or tag values</span></span>
5. <span data-ttu-id="a37bf-116">Appliquer et supprimer un verrou sur la ressource</span><span class="sxs-lookup"><span data-stu-id="a37bf-116">Apply and remove a lock on the resource</span></span>
6. <span data-ttu-id="a37bf-117">Supprimer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="a37bf-117">Delete a resource group</span></span>

<span data-ttu-id="a37bf-118">Cet article n’indique pas comment déployer un modèle Resource Manager sur votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="a37bf-118">This article does not show how to deploy a Resource Manager template to your subscription.</span></span> <span data-ttu-id="a37bf-119">Pour plus d’informations, voir [Déployer des ressources à l’aide de modèles Resource Manager et d’Azure PowerShell](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="a37bf-119">For that information, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span></span>

## <a name="get-started-with-azure-powershell"></a><span data-ttu-id="a37bf-120">Prise en main de Microsoft Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a37bf-120">Get started with Azure PowerShell</span></span>

<span data-ttu-id="a37bf-121">Si Azure PowerShell n’est pas installé sur votre système, consultez la page [Installation et configuration d’Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a37bf-121">If you have not installed Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="a37bf-122">Si vous avez déjà installé Azure PowerShell mais ne l’avez pas mis à jour récemment, envisagez d’installer la version la plus récente.</span><span class="sxs-lookup"><span data-stu-id="a37bf-122">If you have installed Azure PowerShell in the past but have not updated it recently, consider installing the latest version.</span></span> <span data-ttu-id="a37bf-123">Vous pouvez mettre à jour la version en appliquant la même méthode que lors de l’installation.</span><span class="sxs-lookup"><span data-stu-id="a37bf-123">You can update the version through the same method you used to install it.</span></span> <span data-ttu-id="a37bf-124">Par exemple, si vous avez utilisé le programme Web Platform Installer, relancez-le et recherchez si une mise à jour est disponible.</span><span class="sxs-lookup"><span data-stu-id="a37bf-124">For example, if you used the Web Platform Installer, launch it again and look for an update.</span></span>

<span data-ttu-id="a37bf-125">Pour vérifier votre version du module de ressources Azure, utilisez l’applet de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a37bf-125">To check your version of the Azure Resources module, use the following cmdlet:</span></span>

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

<span data-ttu-id="a37bf-126">Cette rubrique a été mise à jour pour la version 3.3.0.</span><span class="sxs-lookup"><span data-stu-id="a37bf-126">This topic was updated for version 3.3.0.</span></span> <span data-ttu-id="a37bf-127">Si vous possédez une version antérieure, les étapes présentées dans cette rubrique ne correspondront peut-être pas à votre situation.</span><span class="sxs-lookup"><span data-stu-id="a37bf-127">If you have an earlier version, your experience might not match the steps shown in this topic.</span></span> <span data-ttu-id="a37bf-128">Pour plus d’informations sur les applets de commande pour cette version, consultez [AzureRM.Resources Module](/powershell/module/azurerm.resources) (Module AzureRM.Resources).</span><span class="sxs-lookup"><span data-stu-id="a37bf-128">For documentation about the cmdlets in this version, see [AzureRM.Resources Module](/powershell/module/azurerm.resources).</span></span>

## <a name="log-in-to-your-azure-account"></a><span data-ttu-id="a37bf-129">Connexion à votre compte Azure</span><span class="sxs-lookup"><span data-stu-id="a37bf-129">Log in to your Azure account</span></span>
<span data-ttu-id="a37bf-130">Avant de travailler sur votre solution, vous devez vous connecter à votre compte.</span><span class="sxs-lookup"><span data-stu-id="a37bf-130">Before working on your solution, you must log in to your account.</span></span>

<span data-ttu-id="a37bf-131">Pour vous connecter à votre compte Azure, utilisez l’applet de commande **Login-AzureRmAccount**.</span><span class="sxs-lookup"><span data-stu-id="a37bf-131">To log in to your Azure account, use the **Login-AzureRmAccount** cmdlet.</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="a37bf-132">Les applets de commande vous invitent à entrer les informations d’identification de connexion pour votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="a37bf-132">The cmdlet prompts you for the login credentials for your Azure account.</span></span> <span data-ttu-id="a37bf-133">Une fois que vous êtes connecté, l’applet de commande télécharge vos paramètres de compte pour qu’ils soient reconnus par Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a37bf-133">After logging in, it downloads your account settings so they are available to Azure PowerShell.</span></span>

<span data-ttu-id="a37bf-134">L’applet de commande retourne des informations sur votre compte et l’abonnement à utiliser pour les tâches.</span><span class="sxs-lookup"><span data-stu-id="a37bf-134">The cmdlet returns information about your account and the subscription to use for the tasks.</span></span>

```powershell
Environment           : AzureCloud
Account               : example@contoso.com
TenantId              : {guid}
SubscriptionId        : {guid}
SubscriptionName      : Example Subscription One
CurrentStorageAccount :

```

<span data-ttu-id="a37bf-135">Si vous avez plusieurs abonnements, vous pouvez en choisir un autre.</span><span class="sxs-lookup"><span data-stu-id="a37bf-135">If you have more than one subscription, you can switch to a different subscription.</span></span> <span data-ttu-id="a37bf-136">Tout d’abord, nous allons voir tous les abonnements de votre compte.</span><span class="sxs-lookup"><span data-stu-id="a37bf-136">First, let's see all the subscriptions for your account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="a37bf-137">Les abonnements activés et désactivés sont retournés.</span><span class="sxs-lookup"><span data-stu-id="a37bf-137">It returns enabled and disabled subscriptions.</span></span>

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

<span data-ttu-id="a37bf-138">Pour choisir un autre abonnement, indiquez le nom de l’abonnement avec l’applet de commande **Set-AzureRmContext**.</span><span class="sxs-lookup"><span data-stu-id="a37bf-138">To switch to a different subscription, provide the subscription name with the **Set-AzureRmContext** cmdlet.</span></span>

```powershell
Set-AzureRmContext -SubscriptionName "Example Subscription Two"
```

## <a name="create-a-resource-group"></a><span data-ttu-id="a37bf-139">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="a37bf-139">Create a resource group</span></span>
<span data-ttu-id="a37bf-140">Avant de déployer des ressources dans votre abonnement, vous devez créer un groupe de ressources qui contiendra ces ressources.</span><span class="sxs-lookup"><span data-stu-id="a37bf-140">Before deploying any resources to your subscription, you must create a resource group that will contain the resources.</span></span>

<span data-ttu-id="a37bf-141">Pour créer un groupe de ressources, utilisez l’applet de commande **New-AzureRmResourceGroup** .</span><span class="sxs-lookup"><span data-stu-id="a37bf-141">To create a resource group, use the **New-AzureRmResourceGroup** cmdlet.</span></span> <span data-ttu-id="a37bf-142">La commande utilise le paramètre **Name** pour attribuer un nom au groupe de ressources et le paramètre **Location** pour indiquer son emplacement.</span><span class="sxs-lookup"><span data-stu-id="a37bf-142">The command uses the **Name** parameter to specify a name for the resource group and the **Location** parameter to specify its location.</span></span>

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location "South Central US"
```

<span data-ttu-id="a37bf-143">La sortie est au format suivant :</span><span class="sxs-lookup"><span data-stu-id="a37bf-143">The output is in the following format:</span></span>

```powershell
ResourceGroupName : TestRG1
Location          : southcentralus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/{guid}/resourceGroups/TestRG1
```

<span data-ttu-id="a37bf-144">Si vous avez besoin de récupérer le groupe de ressources ultérieurement, utilisez l’applet de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a37bf-144">If you need to retrieve the resource group later, use the following cmdlet:</span></span>

```powershell
Get-AzureRmResourceGroup -ResourceGroupName TestRG1
```

<span data-ttu-id="a37bf-145">Pour obtenir tous les groupes de ressources de votre abonnement, n’indiquez aucun nom :</span><span class="sxs-lookup"><span data-stu-id="a37bf-145">To get all the resource groups in your subscription, do not specify a name:</span></span>

```powershell
Get-AzureRmResourceGroup
```

## <a name="add-resources-to-a-resource-group"></a><span data-ttu-id="a37bf-146">Ajouter des ressources à un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="a37bf-146">Add resources to a resource group</span></span>
<span data-ttu-id="a37bf-147">Pour ajouter une ressource au groupe de ressources, vous pouvez utiliser l’applet de commande **New-AzureRmResource** ou une applet de commande spécifique au type de ressource que vous créez (comme **New-AzureRmStorageAccount**).</span><span class="sxs-lookup"><span data-stu-id="a37bf-147">To add a resource to the resource group, you can use the **New-AzureRmResource** cmdlet or a cmdlet that is specific to the type of resource you are creating (like **New-AzureRmStorageAccount**).</span></span> <span data-ttu-id="a37bf-148">Il est peut-être plus facile d’utiliser une applet de commande spécifique à un type de ressource, car elle inclut les paramètres relatifs aux propriétés requises pour la nouvelle ressource.</span><span class="sxs-lookup"><span data-stu-id="a37bf-148">You might find it easier to use a cmdlet that is specific to a resource type because it includes parameters for the properties that are needed for the new resource.</span></span> <span data-ttu-id="a37bf-149">Pour utiliser **New-AzureRmResource**, vous devez connaître toutes les propriétés à définir, même si vous n’êtes pas invité à les entrer.</span><span class="sxs-lookup"><span data-stu-id="a37bf-149">To use **New-AzureRmResource**, you must know all the properties to set without being prompted for them.</span></span>

<span data-ttu-id="a37bf-150">Cependant, l’ajout d’une ressource à l’aide d’applets de commande risque de créer une confusion par la suite, car la nouvelle ressource n’existe pas dans un modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a37bf-150">However, adding a resource through cmdlets might cause future confusion because the new resource does not exist in a Resource Manager template.</span></span> <span data-ttu-id="a37bf-151">Microsoft recommande de définir l’infrastructure de votre solution Azure dans un modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a37bf-151">Microsoft recommends defining the infrastructure for your Azure solution in a Resource Manager template.</span></span> <span data-ttu-id="a37bf-152">Les modèles vous permettent de déployer votre solution plusieurs fois de manière fiable.</span><span class="sxs-lookup"><span data-stu-id="a37bf-152">Templates enable you to reliably and repeatedly deploy your solution.</span></span> <span data-ttu-id="a37bf-153">Dans le cadre de cette rubrique, vous créez un compte de stockage avec une applet de commande PowerShell et générerez plus tard un modèle à partir de votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="a37bf-153">For this topic, you create a storage account with a PowerShell cmdlet, but later you generate a template from your resource group.</span></span>

<span data-ttu-id="a37bf-154">L’applet de commande suivante permet de créer un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="a37bf-154">The following cmdlet creates a storage account.</span></span> <span data-ttu-id="a37bf-155">Au lieu d’utiliser le nom indiqué dans l’exemple, entrez un nom unique pour le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="a37bf-155">Instead of using the name shown in the example, provide a unique name for the storage account.</span></span> <span data-ttu-id="a37bf-156">Le nom doit comprendre entre 3 et 24 caractères et comporter uniquement des lettres en minuscules et des nombres.</span><span class="sxs-lookup"><span data-stu-id="a37bf-156">The name must be between 3 and 24 characters in length, and use only numbers and lower-case letters.</span></span> <span data-ttu-id="a37bf-157">Si vous utilisez le nom indiqué dans l’exemple, vous recevez une erreur, car ce nom est déjà en cours d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="a37bf-157">If you use the name shown in the example, you receive an error because that name is already in use.</span></span>

```powershell
New-AzureRmStorageAccount -ResourceGroupName TestRG1 -AccountName mystoragename -Type "Standard_LRS" -Location "South Central US"
```

<span data-ttu-id="a37bf-158">Si vous avez besoin de récupérer cette ressource ultérieurement, utilisez l’applet de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a37bf-158">If you need to retrieve this resource later, use the following cmdlet:</span></span>

```powershell
Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1
```

## <a name="add-a-tag"></a><span data-ttu-id="a37bf-159">Ajouter une balise</span><span class="sxs-lookup"><span data-stu-id="a37bf-159">Add a tag</span></span>

<span data-ttu-id="a37bf-160">Les balises vous permettent d’organiser vos ressources en fonction de différentes propriétés.</span><span class="sxs-lookup"><span data-stu-id="a37bf-160">Tags enable you to organize your resources according to different properties.</span></span> <span data-ttu-id="a37bf-161">Par exemple, vous pouvez disposer de plusieurs ressources incluses dans différents groupes de ressources appartenant au même service.</span><span class="sxs-lookup"><span data-stu-id="a37bf-161">For example, you may have several resources in different resource groups that belong to the same department.</span></span> <span data-ttu-id="a37bf-162">Vous pouvez appliquer une valeur et une balise de service à ces ressources pour les marquer comme appartenant à la même catégorie.</span><span class="sxs-lookup"><span data-stu-id="a37bf-162">You can apply a department tag and value to those resources to mark them as belonging to the same category.</span></span> <span data-ttu-id="a37bf-163">Vous pouvez également indiquer si une ressource est utilisée dans un environnement de production ou de test.</span><span class="sxs-lookup"><span data-stu-id="a37bf-163">Or, you can mark whether a resource is used in a production or test environment.</span></span> <span data-ttu-id="a37bf-164">Dans le cadre de cette rubrique, vous appliquez des balises à une seule ressource, mais il conviendra probablement d’appliquer des balises à toutes vos ressources dans votre environnement.</span><span class="sxs-lookup"><span data-stu-id="a37bf-164">In this topic, you apply tags to only one resource, but in your environment it most likely makes sense to apply tags to all your resources.</span></span>

<span data-ttu-id="a37bf-165">L’applet de commande suivante applique deux balises à votre compte de stockage :</span><span class="sxs-lookup"><span data-stu-id="a37bf-165">The following cmdlet applies two tags to your storage account:</span></span>

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
 ```

<span data-ttu-id="a37bf-166">Les balises sont mises à jour en tant qu’objet unique.</span><span class="sxs-lookup"><span data-stu-id="a37bf-166">Tags are updated as a single object.</span></span> <span data-ttu-id="a37bf-167">Pour ajouter une balise à une ressource qui inclut déjà des balises, commencez par récupérer les balises existantes.</span><span class="sxs-lookup"><span data-stu-id="a37bf-167">To add a tag to a resource that already includes tags, first retrieve the existing tags.</span></span> <span data-ttu-id="a37bf-168">Ajoutez la nouvelle balise à l’objet qui contient les balises existantes et appliquez de nouveau toutes les balises à la ressource.</span><span class="sxs-lookup"><span data-stu-id="a37bf-168">Add the new tag to the object that contains the existing tags, and reapply all the tags to the resource.</span></span>

```powershell
$tags = (Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
```

## <a name="search-for-resources"></a><span data-ttu-id="a37bf-169">Rechercher des ressources</span><span class="sxs-lookup"><span data-stu-id="a37bf-169">Search for resources</span></span>

<span data-ttu-id="a37bf-170">Utilisez l’applet de commande **Find-AzureRmResource** pour récupérer les ressources selon différentes conditions de recherche.</span><span class="sxs-lookup"><span data-stu-id="a37bf-170">Use the **Find-AzureRmResource** cmdlet to retrieve resources for different search conditions.</span></span>

* <span data-ttu-id="a37bf-171">Pour obtenir une ressource par son nom, indiquez le paramètre **ResourceNameContains** :</span><span class="sxs-lookup"><span data-stu-id="a37bf-171">To get a resource by name, provide the **ResourceNameContains** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceNameContains mystoragename
  ```

* <span data-ttu-id="a37bf-172">Pour obtenir toutes les ressources d’un groupe de ressources, indiquez le paramètre **ResourceGroupNameContains** :</span><span class="sxs-lookup"><span data-stu-id="a37bf-172">To get all the resources in a resource group, provide the **ResourceGroupNameContains** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceGroupNameContains TestRG1
  ```

* <span data-ttu-id="a37bf-173">Pour obtenir toutes les ressources ayant une valeur et un nom de balise, indiquez les paramètres **TagName** et **TagValue** :</span><span class="sxs-lookup"><span data-stu-id="a37bf-173">To get all the resources with a tag name and value, provide the **TagName** and **TagValue** parameters:</span></span>

  ```powershell
  Find-AzureRmResource -TagName Dept -TagValue IT
  ```

* <span data-ttu-id="a37bf-174">Pour obtenir toutes les ressources d’un type particulier, indiquez le paramètre **ResourceType** :</span><span class="sxs-lookup"><span data-stu-id="a37bf-174">To all the resources with a particular resource type, provide the **ResourceType** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceType Microsoft.Storage/storageAccounts
  ```

## <a name="lock-a-resource"></a><span data-ttu-id="a37bf-175">Verrouiller une ressource</span><span class="sxs-lookup"><span data-stu-id="a37bf-175">Lock a resource</span></span>

<span data-ttu-id="a37bf-176">Pour vous assurer qu’une ressource critique ne sera pas accidentellement supprimée ou modifiée, appliquez un verrou à la ressource.</span><span class="sxs-lookup"><span data-stu-id="a37bf-176">When you need to make sure a critical resource is not accidentally deleted or modified, apply a lock to the resource.</span></span> <span data-ttu-id="a37bf-177">Vous pouvez spécifier le niveau **CanNotDelete** ou **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="a37bf-177">You can specify either a **CanNotDelete** or **ReadOnly**.</span></span>

<span data-ttu-id="a37bf-178">Pour créer ou supprimer des verrous de gestion, vous devez avoir accès à des actions `Microsoft.Authorization/*` ou `Microsoft.Authorization/locks/*`.</span><span class="sxs-lookup"><span data-stu-id="a37bf-178">To create or delete management locks, you must have access to `Microsoft.Authorization/*` or `Microsoft.Authorization/locks/*` actions.</span></span> <span data-ttu-id="a37bf-179">Parmi les rôles prédéfinis, seuls les rôles Propriétaire et Administrateur de l'accès utilisateur peuvent effectuer ces actions.</span><span class="sxs-lookup"><span data-stu-id="a37bf-179">Of the built-in roles, only Owner and User Access Administrator are granted those actions.</span></span>

<span data-ttu-id="a37bf-180">Pour appliquer un verrou, utilisez l’applet de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a37bf-180">To apply a lock, use the following cmdlet:</span></span>

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

<span data-ttu-id="a37bf-181">La ressource verrouillée de l’exemple précédent ne peut pas être effacée tant que le verrou n’est pas supprimé.</span><span class="sxs-lookup"><span data-stu-id="a37bf-181">The locked resource in the preceding example cannot be deleted until the lock is removed.</span></span> <span data-ttu-id="a37bf-182">Pour supprimer un verrou, utilisez :</span><span class="sxs-lookup"><span data-stu-id="a37bf-182">To remove a lock, use:</span></span>

```powershell
Remove-AzureRmResourceLock -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

<span data-ttu-id="a37bf-183">Pour plus d’informations sur la définition des verrous, consultez [Verrouiller des ressources avec Azure Resource Manager](resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="a37bf-183">For more information about setting locks, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

## <a name="remove-resources-or-resource-group"></a><span data-ttu-id="a37bf-184">Supprimer des ressources ou un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="a37bf-184">Remove resources or resource group</span></span>
<span data-ttu-id="a37bf-185">Vous pouvez supprimer une ressource ou un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="a37bf-185">You can remove a resource or resource group.</span></span> <span data-ttu-id="a37bf-186">Lorsque vous supprimez un groupe de ressources, vous supprimez également toutes les ressources qu’il contient.</span><span class="sxs-lookup"><span data-stu-id="a37bf-186">When you remove a resource group, you also remove all the resources within that resource group.</span></span>

* <span data-ttu-id="a37bf-187">Pour supprimer une ressource du groupe de ressources, utilisez l’applet de commande **Remove-AzureRmResource** .</span><span class="sxs-lookup"><span data-stu-id="a37bf-187">To delete a resource from the resource group, use the **Remove-AzureRmResource** cmdlet.</span></span> <span data-ttu-id="a37bf-188">Cette applet de commande supprime la ressource, mais pas le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="a37bf-188">This cmdlet deletes the resource, but does not delete the resource group.</span></span>

  ```powershell
  Remove-AzureRmResource -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
  ```

* <span data-ttu-id="a37bf-189">Pour supprimer un groupe de ressources et toutes les ressources qu’il contient, utilisez l’applet de commande **Remove-AzureRmResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="a37bf-189">To delete a resource group and all its resources, use the **Remove-AzureRmResourceGroup** cmdlet.</span></span>

  ```powershell
  Remove-AzureRmResourceGroup -Name TestRG1
  ```

<span data-ttu-id="a37bf-190">Pour les deux applets de commande, vous êtes invité à confirmer que vous souhaitez supprimer la ressource ou le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="a37bf-190">For both cmdlets, you are asked to confirm that you wish to remove the resource or resource group.</span></span> <span data-ttu-id="a37bf-191">Si l’opération supprime avec succès la ressource ou le groupe de ressources, elle retourne la valeur **True**.</span><span class="sxs-lookup"><span data-stu-id="a37bf-191">If the operation successfully deletes the resource or resource group, it returns **True**.</span></span>

## <a name="run-resource-manager-scripts-with-azure-automation"></a><span data-ttu-id="a37bf-192">Exécuter des scripts Resource Manager avec Azure Automation</span><span class="sxs-lookup"><span data-stu-id="a37bf-192">Run Resource Manager scripts with Azure Automation</span></span>

<span data-ttu-id="a37bf-193">Cette rubrique montre comment effectuer des opérations de base sur vos ressources avec Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a37bf-193">This topic shows you how to perform basic operations on your resources with Azure PowerShell.</span></span> <span data-ttu-id="a37bf-194">Pour les scénarios de gestion plus avancés, vous souhaiterez généralement créer un script et le réutiliser en fonction de vos besoins ou selon une planification.</span><span class="sxs-lookup"><span data-stu-id="a37bf-194">For more advanced management scenarios, you typically want to create a script, and reuse that script as needed or on a schedule.</span></span> <span data-ttu-id="a37bf-195">[Azure Automation](../automation/automation-intro.md) vous offre un moyen d’automatiser les scripts fréquemment utilisés, qui gèrent vos solutions Azure.</span><span class="sxs-lookup"><span data-stu-id="a37bf-195">[Azure Automation](../automation/automation-intro.md) provides a way for you to automate frequently used scripts that manage your Azure solutions.</span></span>

<span data-ttu-id="a37bf-196">Les rubriques suivantes vous montrent comment utiliser Azure Automation, Resource Manager et PowerShell pour exécuter efficacement des tâches de gestion :</span><span class="sxs-lookup"><span data-stu-id="a37bf-196">The following topics show you how to use Azure Automation, Resource Manager, and PowerShell to effectively perform management tasks:</span></span>

- <span data-ttu-id="a37bf-197">Pour plus d’informations sur la création d’un runbook, consultez [Mon premier Runbook PowerShell](../automation/automation-first-runbook-textual-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="a37bf-197">For information about creating a runbook, see [My first PowerShell runbook](../automation/automation-first-runbook-textual-powershell.md).</span></span>
- <span data-ttu-id="a37bf-198">Pour plus d’informations sur l’utilisation des galeries de scripts, consultez [Galeries de runbooks et de modules pour Azure Automation](../automation/automation-runbook-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="a37bf-198">For information about working with galleries of scripts, see [Runbook and module galleries for Azure Automation](../automation/automation-runbook-gallery.md).</span></span>
- <span data-ttu-id="a37bf-199">Pour les runbooks qui démarrent et arrêtent des machines virtuelles, consultez [Scénario Azure Automation : utilisation de balises au format JSON afin de créer une planification pour le démarrage et l’arrêt de machines virtuelles Azure](../automation/automation-scenario-start-stop-vm-wjson-tags.md).</span><span class="sxs-lookup"><span data-stu-id="a37bf-199">For runbooks that start and stop virtual machines, see [Azure Automation scenario: Using JSON-formatted tags to create a schedule for Azure VM startup and shutdown](../automation/automation-scenario-start-stop-vm-wjson-tags.md).</span></span>
- <span data-ttu-id="a37bf-200">Pour les runbooks qui démarrent et arrêtent des machines virtuelles durant les heures creuses, consultez [Solution Start/Stop VMs during off-hours (Démarrer/arrêter des machines virtuelles durant les heures creuses) dans Automation](../automation/automation-solution-vm-management.md).</span><span class="sxs-lookup"><span data-stu-id="a37bf-200">For runbooks that start and stop virtual machines off-hours, see [Start/Stop VMs during off-hours solution in Automation](../automation/automation-solution-vm-management.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a37bf-201">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a37bf-201">Next steps</span></span>
* <span data-ttu-id="a37bf-202">Pour en savoir plus sur la création de modèles Resource Manager, consultez [Création de modèles Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a37bf-202">To learn about creating Resource Manager templates, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="a37bf-203">Pour savoir comment déployer des modèles, consultez [Déployer une application avec un modèle Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="a37bf-203">To learn about deploying templates, see [Deploy an application with Azure Resource Manager Template](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="a37bf-204">Vous pouvez déplacer des ressources existantes vers un nouveau groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="a37bf-204">You can move existing resources to a new resource group.</span></span> <span data-ttu-id="a37bf-205">Pour obtenir des exemples, consultez [Déplacer des ressources vers un nouveau groupe de ressources ou un nouvel abonnement](resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="a37bf-205">For examples, see [Move Resources to New Resource Group or Subscription](resource-group-move-resources.md).</span></span>
* <span data-ttu-id="a37bf-206">Pour obtenir des conseils sur l’utilisation de Resource Manager par les entreprises pour gérer efficacement les abonnements, voir [Structure d’Azure Enterprise - Gouvernance normative de l’abonnement](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="a37bf-206">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

