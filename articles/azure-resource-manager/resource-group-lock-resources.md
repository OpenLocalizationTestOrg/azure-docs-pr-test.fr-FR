---
title: "Verrouiller les ressources Azure pour empêcher les modifications | Microsoft Docs"
description: "Empêchez les utilisateurs de mettre à jour ou de supprimer des ressources Azure critiques en appliquant un verrou à tous les utilisateurs et rôles."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 53c57e8f-741c-4026-80e0-f4c02638c98b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: tomfitz
ms.openlocfilehash: 44c87b00f4fc63dbfd45a07d9a8cddc5eaf1a65c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="lock-resources-to-prevent-unexpected-changes"></a><span data-ttu-id="fa640-103">Verrouiller les ressources pour empêcher les modifications inattendues</span><span class="sxs-lookup"><span data-stu-id="fa640-103">Lock resources to prevent unexpected changes</span></span> 
<span data-ttu-id="fa640-104">En tant qu’administrateur, vous pouvez avoir besoin de verrouiller un abonnement, une ressource ou un groupe de ressources afin d’empêcher d’autres utilisateurs de votre organisation de supprimer ou modifier de manière accidentelle des ressources critiques.</span><span class="sxs-lookup"><span data-stu-id="fa640-104">As an administrator, you may need to lock a subscription, resource group, or resource to prevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="fa640-105">Vous pouvez définir le niveau de verrouillage sur **CanNotDelete** ou **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="fa640-105">You can set the lock level to **CanNotDelete** or **ReadOnly**.</span></span> 

* <span data-ttu-id="fa640-106">**CanNotDelete** signifie que les utilisateurs autorisés peuvent lire et modifier une ressource, mais pas la supprimer.</span><span class="sxs-lookup"><span data-stu-id="fa640-106">**CanNotDelete** means authorized users can still read and modify a resource, but they can't delete the resource.</span></span> 
* <span data-ttu-id="fa640-107">**ReadOnly** signifie que les utilisateurs autorisés peuvent lire une ressource, mais pas la supprimer ni la mettre à jour.</span><span class="sxs-lookup"><span data-stu-id="fa640-107">**ReadOnly** means authorized users can read a resource, but they can't delete or update the resource.</span></span> <span data-ttu-id="fa640-108">Appliquer ce verrou revient à limiter à tous les utilisateurs autorisés les autorisations accordées par le rôle **Lecteur**.</span><span class="sxs-lookup"><span data-stu-id="fa640-108">Applying this lock is similar to restricting all authorized users to the permissions granted by the **Reader** role.</span></span> 

## <a name="how-locks-are-applied"></a><span data-ttu-id="fa640-109">Application des verrous</span><span class="sxs-lookup"><span data-stu-id="fa640-109">How locks are applied</span></span>

<span data-ttu-id="fa640-110">Lorsque vous appliquez un verrou à une étendue parente, toutes les ressources de cette étendue héritent du même verrou.</span><span class="sxs-lookup"><span data-stu-id="fa640-110">When you apply a lock at a parent scope, all resources within that scope inherit the same lock.</span></span> <span data-ttu-id="fa640-111">Même les ressources que vous ajoutez par la suite héritent du verrou du parent.</span><span class="sxs-lookup"><span data-stu-id="fa640-111">Even resources you add later inherit the lock from the parent.</span></span> <span data-ttu-id="fa640-112">Le verrou le plus restrictif de l’héritage est prioritaire.</span><span class="sxs-lookup"><span data-stu-id="fa640-112">The most restrictive lock in the inheritance takes precedence.</span></span>

<span data-ttu-id="fa640-113">Contrairement au contrôle d'accès basé sur les rôles, vous utilisez des verrous de gestion pour appliquer une restriction à tous les utilisateurs et rôles.</span><span class="sxs-lookup"><span data-stu-id="fa640-113">Unlike role-based access control, you use management locks to apply a restriction across all users and roles.</span></span> <span data-ttu-id="fa640-114">Pour en savoir plus sur la définition des autorisations pour les utilisateurs et les rôles, consultez [Contrôle d’accès en fonction du rôle Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="fa640-114">To learn about setting permissions for users and roles, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>

<span data-ttu-id="fa640-115">Les verrous Resource Manager s'appliquent uniquement aux opérations qui se produisent dans le plan de gestion, c'est-à-dire les opérations envoyées à `https://management.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="fa640-115">Resource Manager locks apply only to operations that happen in the management plane, which consists of operations sent to `https://management.azure.com`.</span></span> <span data-ttu-id="fa640-116">Les verrous ne limitent pas la manière dont les ressources exécutent leurs propres fonctions.</span><span class="sxs-lookup"><span data-stu-id="fa640-116">The locks do not restrict how resources perform their own functions.</span></span> <span data-ttu-id="fa640-117">Les modifications des ressources sont limitées, mais pas les opérations sur les ressources.</span><span class="sxs-lookup"><span data-stu-id="fa640-117">Resource changes are restricted, but resource operations are not restricted.</span></span> <span data-ttu-id="fa640-118">Par exemple, un verrou ReadOnly sur une base de données SQL vous empêche de supprimer ou de modifier cette base de données, mais il ne vous empêche pas de créer, mettre à jour ou supprimer les données qu'elle contient.</span><span class="sxs-lookup"><span data-stu-id="fa640-118">For example, a ReadOnly lock on a SQL Database prevents you from deleting or modifying the database, but it does not prevent you from creating, updating, or deleting data in the database.</span></span> <span data-ttu-id="fa640-119">Les transactions de données sont autorisées car ces opérations ne sont pas envoyées à `https://management.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="fa640-119">Data transactions are permitted because those operations are not sent to `https://management.azure.com`.</span></span>

<span data-ttu-id="fa640-120">L’application de **ReadOnly** peut produire des résultats inattendus, car certaines opérations qui ressemblent à des opérations de lecture nécessitent en fait des actions supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="fa640-120">Applying **ReadOnly** can lead to unexpected results because some operations that seem like read operations actually require additional actions.</span></span> <span data-ttu-id="fa640-121">Par exemple, le placement d’un verrou **ReadOnly** sur un compte de stockage empêche tous les utilisateurs de répertorier les clés.</span><span class="sxs-lookup"><span data-stu-id="fa640-121">For example, placing a **ReadOnly** lock on a storage account prevents all users from listing the keys.</span></span> <span data-ttu-id="fa640-122">L’opération de listage de clés est gérée via une demande POST, car les clés retournées sont disponibles pour les opérations d’écriture.</span><span class="sxs-lookup"><span data-stu-id="fa640-122">The list keys operation is handled through a POST request because the returned keys are available for write operations.</span></span> <span data-ttu-id="fa640-123">Autre exemple : le placement d’un verrou **ReadOnly** sur une ressource App Service empêche l’Explorateur de serveurs Visual Studio d’afficher les fichiers de la ressource, car cette interaction requiert un accès en écriture.</span><span class="sxs-lookup"><span data-stu-id="fa640-123">For another example, placing a **ReadOnly** lock on an App Service resource prevents Visual Studio Server Explorer from displaying files for the resource because that interaction requires write access.</span></span>

## <a name="who-can-create-or-delete-locks-in-your-organization"></a><span data-ttu-id="fa640-124">Personnes autorisées à créer ou supprimer des verrous dans votre organisation</span><span class="sxs-lookup"><span data-stu-id="fa640-124">Who can create or delete locks in your organization</span></span>
<span data-ttu-id="fa640-125">Pour créer ou supprimer des verrous de gestion, vous devez avoir accès à des actions `Microsoft.Authorization/*` ou `Microsoft.Authorization/locks/*`.</span><span class="sxs-lookup"><span data-stu-id="fa640-125">To create or delete management locks, you must have access to `Microsoft.Authorization/*` or `Microsoft.Authorization/locks/*` actions.</span></span> <span data-ttu-id="fa640-126">Parmi les rôles prédéfinis, seuls les rôles **Propriétaire** et **Administrateur de l'accès utilisateur** peuvent effectuer ces actions.</span><span class="sxs-lookup"><span data-stu-id="fa640-126">Of the built-in roles, only **Owner** and **User Access Administrator** are granted those actions.</span></span>

## <a name="portal"></a><span data-ttu-id="fa640-127">Portail</span><span class="sxs-lookup"><span data-stu-id="fa640-127">Portal</span></span>
[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="template"></a><span data-ttu-id="fa640-128">Modèle</span><span class="sxs-lookup"><span data-stu-id="fa640-128">Template</span></span>
<span data-ttu-id="fa640-129">L’exemple suivant représente un modèle créant un verrou sur un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="fa640-129">The following example shows a template that creates a lock on a storage account.</span></span> <span data-ttu-id="fa640-130">Le compte de stockage auquel est appliqué le verrou est fourni en tant que paramètre.</span><span class="sxs-lookup"><span data-stu-id="fa640-130">The storage account on which to apply the lock is provided as a parameter.</span></span> <span data-ttu-id="fa640-131">Le nom du verrou résulte de la concaténation du nom de la ressource avec **/Microsoft.Authorization/** et le nom du verrou, en l’occurrence **myLock**.</span><span class="sxs-lookup"><span data-stu-id="fa640-131">The name of the lock is created by concatenating the resource name with **/Microsoft.Authorization/** and the name of the lock, in this case **myLock**.</span></span>

<span data-ttu-id="fa640-132">Le type fourni est spécifique au type de ressource.</span><span class="sxs-lookup"><span data-stu-id="fa640-132">The type provided is specific to the resource type.</span></span> <span data-ttu-id="fa640-133">Pour le stockage, définissez le type suivant : « Microsoft.Storage/storageaccounts/providers/locks ».</span><span class="sxs-lookup"><span data-stu-id="fa640-133">For storage, set the type to "Microsoft.Storage/storageaccounts/providers/locks".</span></span>

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "lockedResource": {
          "type": "string"
        }
      },
      "resources": [
        {
          "name": "[concat(parameters('lockedResource'), '/Microsoft.Authorization/myLock')]",
          "type": "Microsoft.Storage/storageAccounts/providers/locks",
          "apiVersion": "2015-01-01",
          "properties": {
            "level": "CannotDelete"
          }
        }
      ]
    }

## <a name="powershell"></a><span data-ttu-id="fa640-134">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fa640-134">PowerShell</span></span>
<span data-ttu-id="fa640-135">Vous pouvez verrouiller des ressources déployées avec Azure PowerShell en utilisant la commande [New-AzureRmResourceLock](/powershell/module/azurerm.resources/new-azurermresourcelock).</span><span class="sxs-lookup"><span data-stu-id="fa640-135">You lock deployed resources with Azure PowerShell by using the [New-AzureRmResourceLock](/powershell/module/azurerm.resources/new-azurermresourcelock) command.</span></span>

<span data-ttu-id="fa640-136">Pour verrouiller une ressource, indiquez le nom de la ressource, son type de ressource et son nom de groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="fa640-136">To lock a resource, provide the name of the resource, its resource type, and its resource group name.</span></span>

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockSite `
  -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="fa640-137">Pour verrouiller un groupe de ressources : indiquez le nom du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="fa640-137">To lock a resource group, provide the name of the resource group.</span></span>

```powershell
New-AzureRmResourceLock -LockName LockGroup -LockLevel CanNotDelete `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="fa640-138">Pour obtenir des informations sur un verrou, utilisez [Get-AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock).</span><span class="sxs-lookup"><span data-stu-id="fa640-138">To get information about a lock, use [Get-AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock).</span></span> <span data-ttu-id="fa640-139">Pour obtenir tous les verrous de votre abonnement, utilisez :</span><span class="sxs-lookup"><span data-stu-id="fa640-139">To get all the locks in your subscription, use:</span></span>

```powershell
Get-AzureRmResourceLock
```

<span data-ttu-id="fa640-140">Pour obtenir tous les verrous d’une ressource, utilisez :</span><span class="sxs-lookup"><span data-stu-id="fa640-140">To get all locks for a resource, use:</span></span>

```powershell
Get-AzureRmResourceLock -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="fa640-141">Pour obtenir tous les verrous d’un groupe de ressources, utilisez :</span><span class="sxs-lookup"><span data-stu-id="fa640-141">To get all locks for a resource group, use:</span></span>

```powershell
Get-AzureRmResourceLock -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="fa640-142">Azure PowerShell fournit d’autres commandes d’utilisation des verrous, comme [Set-AzureRmResourceLock](/powershell/module/azurerm.resources/set-azurermresourcelock), pour mettre à jour un verrou et [Remove-AzureRmResourceLock](/powershell/module/azurerm.resources/remove-azurermresourcelock) pour supprimer un verrou.</span><span class="sxs-lookup"><span data-stu-id="fa640-142">Azure PowerShell provides other commands for working locks, such as [Set-AzureRmResourceLock](/powershell/module/azurerm.resources/set-azurermresourcelock) to update a lock, and [Remove-AzureRmResourceLock](/powershell/module/azurerm.resources/remove-azurermresourcelock) to delete a lock.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="fa640-143">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="fa640-143">Azure CLI</span></span>

<span data-ttu-id="fa640-144">Verrouillez les ressources déployées avec Azure CLI à l’aide de la commande [az lock create](/cli/azure/lock#create).</span><span class="sxs-lookup"><span data-stu-id="fa640-144">You lock deployed resources with Azure CLI by using the [az lock create](/cli/azure/lock#create) command.</span></span>

<span data-ttu-id="fa640-145">Pour verrouiller une ressource, indiquez le nom de la ressource, son type de ressource et son nom de groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="fa640-145">To lock a resource, provide the name of the resource, its resource type, and its resource group name.</span></span>

```azurecli
az lock create --name LockSite --lock-type CanNotDelete \
  --resource-group exampleresourcegroup --resource-name examplesite \
  --resource-type Microsoft.Web/sites
```

<span data-ttu-id="fa640-146">Pour verrouiller un groupe de ressources : indiquez le nom du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="fa640-146">To lock a resource group, provide the name of the resource group.</span></span>

```azurecli
az lock create --name LockGroup --lock-type CanNotDelete \
  --resource-group exampleresourcegroup
```

<span data-ttu-id="fa640-147">Pour obtenir des informations sur un verrou, utilisez la commande [az lock list](/cli/azure/lock#list).</span><span class="sxs-lookup"><span data-stu-id="fa640-147">To get information about a lock, use [az lock list](/cli/azure/lock#list).</span></span> <span data-ttu-id="fa640-148">Pour obtenir tous les verrous de votre abonnement, utilisez :</span><span class="sxs-lookup"><span data-stu-id="fa640-148">To get all the locks in your subscription, use:</span></span>

```azurecli
az lock list
```

<span data-ttu-id="fa640-149">Pour obtenir tous les verrous d’une ressource, utilisez :</span><span class="sxs-lookup"><span data-stu-id="fa640-149">To get all locks for a resource, use:</span></span>

```azurecli
az lock list --resource-group exampleresourcegroup --resource-name examplesite \
  --namespace Microsoft.Web --resource-type sites --parent ""
```

<span data-ttu-id="fa640-150">Pour obtenir tous les verrous d’un groupe de ressources, utilisez :</span><span class="sxs-lookup"><span data-stu-id="fa640-150">To get all locks for a resource group, use:</span></span>

```azurecli
az lock list --resource-group exampleresourcegroup
```

<span data-ttu-id="fa640-151">Azure CLI fournit d’autres commandes d’utilisation des verrous, telles que [az lock update](/cli/azure/lock#update) pour mettre à jour un verrou, et [az lock delete](/cli/azure/lock#delete) pour supprimer un verrou.</span><span class="sxs-lookup"><span data-stu-id="fa640-151">Azure CLI provides other commands for working locks, such as [az lock update](/cli/azure/lock#update) to update a lock, and [az lock delete](/cli/azure/lock#delete) to delete a lock.</span></span>

## <a name="rest-api"></a><span data-ttu-id="fa640-152">API REST</span><span class="sxs-lookup"><span data-stu-id="fa640-152">REST API</span></span>
<span data-ttu-id="fa640-153">Vous pouvez verrouiller des ressources déployées à l’aide de l’ [API REST pour les verrous de gestion](https://docs.microsoft.com/rest/api/resources/managementlocks).</span><span class="sxs-lookup"><span data-stu-id="fa640-153">You can lock deployed resources with the [REST API for management locks](https://docs.microsoft.com/rest/api/resources/managementlocks).</span></span> <span data-ttu-id="fa640-154">L’API REST vous permet de créer et de supprimer des verrous, et de récupérer des informations relatives aux verrous existants.</span><span class="sxs-lookup"><span data-stu-id="fa640-154">The REST API enables you to create and delete locks, and retrieve information about existing locks.</span></span>

<span data-ttu-id="fa640-155">Pour créer un verrou, exécutez :</span><span class="sxs-lookup"><span data-stu-id="fa640-155">To create a lock, run:</span></span>

    PUT https://management.azure.com/{scope}/providers/Microsoft.Authorization/locks/{lock-name}?api-version={api-version}

<span data-ttu-id="fa640-156">Le verrou peut être appliqué à un abonnement, à un groupe de ressources ou à une ressource.</span><span class="sxs-lookup"><span data-stu-id="fa640-156">The scope could be a subscription, resource group, or resource.</span></span> <span data-ttu-id="fa640-157">Le nom du verrou est personnalisable.</span><span class="sxs-lookup"><span data-stu-id="fa640-157">The lock-name is whatever you want to call the lock.</span></span> <span data-ttu-id="fa640-158">Pour la version de l’API, utilisez **2015-01-01**.</span><span class="sxs-lookup"><span data-stu-id="fa640-158">For api-version, use **2015-01-01**.</span></span>

<span data-ttu-id="fa640-159">Dans la demande, incluez un objet JSON spécifiant les propriétés du verrou.</span><span class="sxs-lookup"><span data-stu-id="fa640-159">In the request, include a JSON object that specifies the properties for the lock.</span></span>

    {
      "properties": {
        "level": "CanNotDelete",
        "notes": "Optional text notes."
      }
    } 

## <a name="next-steps"></a><span data-ttu-id="fa640-160">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fa640-160">Next steps</span></span>
* <span data-ttu-id="fa640-161">Pour plus d’informations sur l’utilisation de verrous sur des ressources, consultez [Lock Down Your Azure Resources](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)</span><span class="sxs-lookup"><span data-stu-id="fa640-161">For more information about working with resource locks, see [Lock Down Your Azure Resources](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)</span></span>
* <span data-ttu-id="fa640-162">Pour en savoir plus sur l’organisation logique de vos ressources, consultez [Organisation des ressources à l’aide de balises](resource-group-using-tags.md)</span><span class="sxs-lookup"><span data-stu-id="fa640-162">To learn about logically organizing your resources, see [Using tags to organize your resources](resource-group-using-tags.md)</span></span>
* <span data-ttu-id="fa640-163">Pour changer le groupe de ressources où se trouve une ressource, consultez [Déplacer des ressources vers un nouveau groupe de ressources](resource-group-move-resources.md)</span><span class="sxs-lookup"><span data-stu-id="fa640-163">To change which resource group a resource resides in, see [Move resources to new resource group](resource-group-move-resources.md)</span></span>
* <span data-ttu-id="fa640-164">Vous pouvez appliquer des restrictions et des conventions sur votre abonnement avec des stratégies personnalisées.</span><span class="sxs-lookup"><span data-stu-id="fa640-164">You can apply restrictions and conventions across your subscription with customized policies.</span></span> <span data-ttu-id="fa640-165">Pour plus d'informations, consultez [Utiliser le service Policy pour gérer les ressources et contrôler l'accès](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="fa640-165">For more information, see [Use Policy to manage resources and control access](resource-manager-policy.md).</span></span>
* <span data-ttu-id="fa640-166">Pour obtenir des conseils sur l’utilisation de Resource Manager par les entreprises pour gérer efficacement les abonnements, voir [Structure d’Azure Enterprise - Gouvernance normative de l’abonnement](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="fa640-166">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

