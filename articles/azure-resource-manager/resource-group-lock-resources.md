---
title: modifications de tooprevent de ressources Azure aaaLock | Documents Microsoft
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
ms.openlocfilehash: 1f0d8911b2b129069bd2f01a9a4ec0a3cf700118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="lock-resources-tooprevent-unexpected-changes"></a><span data-ttu-id="092fd-103">Verrouiller les ressources tooprevent modifications inattendues</span><span class="sxs-lookup"><span data-stu-id="092fd-103">Lock resources tooprevent unexpected changes</span></span> 
<span data-ttu-id="092fd-104">En tant qu’administrateur, vous devrez peut-être toolock un abonnement, groupe de ressources ou ressource tooprevent autres utilisateurs de votre organisation d’accidentellement supprimer ou modifier des ressources critiques.</span><span class="sxs-lookup"><span data-stu-id="092fd-104">As an administrator, you may need toolock a subscription, resource group, or resource tooprevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="092fd-105">Vous pouvez définir au niveau du verrou hello trop**CanNotDelete** ou **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="092fd-105">You can set hello lock level too**CanNotDelete** or **ReadOnly**.</span></span> 

* <span data-ttu-id="092fd-106">**CanNotDelete** signifie que les utilisateurs autorisés peuvent toujours lire et modifier une ressource, mais ils ne peuvent pas supprimer la ressource de hello.</span><span class="sxs-lookup"><span data-stu-id="092fd-106">**CanNotDelete** means authorized users can still read and modify a resource, but they can't delete hello resource.</span></span> 
* <span data-ttu-id="092fd-107">**En lecture seule** signifie que les utilisateurs autorisés peuvent lire une ressource, mais ils ne peuvent pas supprimer ou mettre à jour la ressource de hello.</span><span class="sxs-lookup"><span data-stu-id="092fd-107">**ReadOnly** means authorized users can read a resource, but they can't delete or update hello resource.</span></span> <span data-ttu-id="092fd-108">Appliquer ce verrou est similaire toorestricting tout autorisé toohello aux utilisateurs des autorisations accordées par hello **lecteur** rôle.</span><span class="sxs-lookup"><span data-stu-id="092fd-108">Applying this lock is similar toorestricting all authorized users toohello permissions granted by hello **Reader** role.</span></span> 

## <a name="how-locks-are-applied"></a><span data-ttu-id="092fd-109">Application des verrous</span><span class="sxs-lookup"><span data-stu-id="092fd-109">How locks are applied</span></span>

<span data-ttu-id="092fd-110">Lorsque vous appliquez un verrou sur une portée parent, toutes les ressources dans cette étendue héritent hello même verrou.</span><span class="sxs-lookup"><span data-stu-id="092fd-110">When you apply a lock at a parent scope, all resources within that scope inherit hello same lock.</span></span> <span data-ttu-id="092fd-111">Même les ressources que vous ajouterez ultérieurement héritent de verrou de hello parent de hello.</span><span class="sxs-lookup"><span data-stu-id="092fd-111">Even resources you add later inherit hello lock from hello parent.</span></span> <span data-ttu-id="092fd-112">verrou de Hello plus restrictif dans l’héritage hello est prioritaire.</span><span class="sxs-lookup"><span data-stu-id="092fd-112">hello most restrictive lock in hello inheritance takes precedence.</span></span>

<span data-ttu-id="092fd-113">Contrairement au contrôle d’accès basé sur un rôle, vous utilisez Gestion des verrous tooapply une restriction sur tous les utilisateurs et les rôles.</span><span class="sxs-lookup"><span data-stu-id="092fd-113">Unlike role-based access control, you use management locks tooapply a restriction across all users and roles.</span></span> <span data-ttu-id="092fd-114">toolearn sur la définition des autorisations pour les utilisateurs et les rôles, consultez [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="092fd-114">toolearn about setting permissions for users and roles, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>

<span data-ttu-id="092fd-115">Verrous de gestionnaire de ressources s’appliquent uniquement aux toooperations qui se produisent dans le plan de gestion de hello, qui se compose d’opérations envoyées trop`https://management.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="092fd-115">Resource Manager locks apply only toooperations that happen in hello management plane, which consists of operations sent too`https://management.azure.com`.</span></span> <span data-ttu-id="092fd-116">les verrous Hello ne limitent pas la façon dont les ressources effectuent leurs propres fonctions.</span><span class="sxs-lookup"><span data-stu-id="092fd-116">hello locks do not restrict how resources perform their own functions.</span></span> <span data-ttu-id="092fd-117">Les modifications des ressources sont limitées, mais pas les opérations sur les ressources.</span><span class="sxs-lookup"><span data-stu-id="092fd-117">Resource changes are restricted, but resource operations are not restricted.</span></span> <span data-ttu-id="092fd-118">Par exemple, un verrou en lecture seule sur une base de données SQL vous empêche de supprimer ou modifier la base de données hello, mais il ne vous empêche pas de création, mise à jour ou supprimer des données dans la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="092fd-118">For example, a ReadOnly lock on a SQL Database prevents you from deleting or modifying hello database, but it does not prevent you from creating, updating, or deleting data in hello database.</span></span> <span data-ttu-id="092fd-119">Les transactions de données sont autorisées, car ces opérations ne sont pas envoyées trop`https://management.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="092fd-119">Data transactions are permitted because those operations are not sent too`https://management.azure.com`.</span></span>

<span data-ttu-id="092fd-120">Application **ReadOnly** peut entraîner des résultats de toounexpected, car certaines opérations semblent lire opérations nécessitent réellement des actions supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="092fd-120">Applying **ReadOnly** can lead toounexpected results because some operations that seem like read operations actually require additional actions.</span></span> <span data-ttu-id="092fd-121">Par exemple, placer un **ReadOnly** verrou sur un compte de stockage empêche tous les utilisateurs d’afficher la liste des clés de hello.</span><span class="sxs-lookup"><span data-stu-id="092fd-121">For example, placing a **ReadOnly** lock on a storage account prevents all users from listing hello keys.</span></span> <span data-ttu-id="092fd-122">liste Hello opération clés est gérée via une demande POST car hello retourné clés sont disponibles pour les opérations d’écriture.</span><span class="sxs-lookup"><span data-stu-id="092fd-122">hello list keys operation is handled through a POST request because hello returned keys are available for write operations.</span></span> <span data-ttu-id="092fd-123">Pour un autre exemple, placer un **ReadOnly** verrou sur une ressource de Service de l’application empêche l’Explorateur de serveurs Visual Studio à partir de l’affichage des fichiers pour la ressource de hello, car cette interaction nécessite un accès en écriture.</span><span class="sxs-lookup"><span data-stu-id="092fd-123">For another example, placing a **ReadOnly** lock on an App Service resource prevents Visual Studio Server Explorer from displaying files for hello resource because that interaction requires write access.</span></span>

## <a name="who-can-create-or-delete-locks-in-your-organization"></a><span data-ttu-id="092fd-124">Personnes autorisées à créer ou supprimer des verrous dans votre organisation</span><span class="sxs-lookup"><span data-stu-id="092fd-124">Who can create or delete locks in your organization</span></span>
<span data-ttu-id="092fd-125">toocreate ou supprimer les verrous de gestion, vous devez avoir accès trop`Microsoft.Authorization/*` ou `Microsoft.Authorization/locks/*` actions.</span><span class="sxs-lookup"><span data-stu-id="092fd-125">toocreate or delete management locks, you must have access too`Microsoft.Authorization/*` or `Microsoft.Authorization/locks/*` actions.</span></span> <span data-ttu-id="092fd-126">Hello rôles intégrés uniquement **propriétaire** et **administrateur de l’accès utilisateur** sont accordées à ces actions.</span><span class="sxs-lookup"><span data-stu-id="092fd-126">Of hello built-in roles, only **Owner** and **User Access Administrator** are granted those actions.</span></span>

## <a name="portal"></a><span data-ttu-id="092fd-127">Portail</span><span class="sxs-lookup"><span data-stu-id="092fd-127">Portal</span></span>
[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="template"></a><span data-ttu-id="092fd-128">Modèle</span><span class="sxs-lookup"><span data-stu-id="092fd-128">Template</span></span>
<span data-ttu-id="092fd-129">Hello suivant montre un modèle qui crée un verrou sur un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="092fd-129">hello following example shows a template that creates a lock on a storage account.</span></span> <span data-ttu-id="092fd-130">compte de stockage Hello sur le tooapply le verrou de hello est fourni en tant que paramètre.</span><span class="sxs-lookup"><span data-stu-id="092fd-130">hello storage account on which tooapply hello lock is provided as a parameter.</span></span> <span data-ttu-id="092fd-131">nom du verrou de hello Hello est créé en concaténant le nom de ressource hello avec **/Microsoft.Authorization/** et hello nom du verrou de hello, dans ce cas **myLock**.</span><span class="sxs-lookup"><span data-stu-id="092fd-131">hello name of hello lock is created by concatenating hello resource name with **/Microsoft.Authorization/** and hello name of hello lock, in this case **myLock**.</span></span>

<span data-ttu-id="092fd-132">type Hello fourni est type de ressource toohello spécifique.</span><span class="sxs-lookup"><span data-stu-id="092fd-132">hello type provided is specific toohello resource type.</span></span> <span data-ttu-id="092fd-133">Pour le stockage, la valeur hello type too"Microsoft.Storage/storageaccounts/providers/locks ».</span><span class="sxs-lookup"><span data-stu-id="092fd-133">For storage, set hello type too"Microsoft.Storage/storageaccounts/providers/locks".</span></span>

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

## <a name="powershell"></a><span data-ttu-id="092fd-134">PowerShell</span><span class="sxs-lookup"><span data-stu-id="092fd-134">PowerShell</span></span>
<span data-ttu-id="092fd-135">Verrou vous déployés ressources avec Azure PowerShell à l’aide de hello [New-AzureRmResourceLock](/powershell/module/azurerm.resources/new-azurermresourcelock) commande.</span><span class="sxs-lookup"><span data-stu-id="092fd-135">You lock deployed resources with Azure PowerShell by using hello [New-AzureRmResourceLock](/powershell/module/azurerm.resources/new-azurermresourcelock) command.</span></span>

<span data-ttu-id="092fd-136">toolock une ressource, fournissez hello nom hello, son type de ressource et son nom de groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="092fd-136">toolock a resource, provide hello name of hello resource, its resource type, and its resource group name.</span></span>

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockSite `
  -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="092fd-137">toolock un groupe de ressources, fournir un nom hello hello du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="092fd-137">toolock a resource group, provide hello name of hello resource group.</span></span>

```powershell
New-AzureRmResourceLock -LockName LockGroup -LockLevel CanNotDelete `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="092fd-138">informations de tooget sur un verrou, utilisez [Get-AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock).</span><span class="sxs-lookup"><span data-stu-id="092fd-138">tooget information about a lock, use [Get-AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock).</span></span> <span data-ttu-id="092fd-139">tooget tous les verrous hello dans votre abonnement, utilisez :</span><span class="sxs-lookup"><span data-stu-id="092fd-139">tooget all hello locks in your subscription, use:</span></span>

```powershell
Get-AzureRmResourceLock
```

<span data-ttu-id="092fd-140">tooget tous les verrous d’une ressource, utilisez :</span><span class="sxs-lookup"><span data-stu-id="092fd-140">tooget all locks for a resource, use:</span></span>

```powershell
Get-AzureRmResourceLock -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="092fd-141">tooget tous les verrous d’un groupe de ressources, utilisez :</span><span class="sxs-lookup"><span data-stu-id="092fd-141">tooget all locks for a resource group, use:</span></span>

```powershell
Get-AzureRmResourceLock -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="092fd-142">Azure PowerShell fournit des autres commandes pour les verrous de travail, tels que [Set-AzureRmResourceLock](/powershell/module/azurerm.resources/set-azurermresourcelock) tooupdate un verrou, et [Remove-AzureRmResourceLock](/powershell/module/azurerm.resources/remove-azurermresourcelock) toodelete un verrou.</span><span class="sxs-lookup"><span data-stu-id="092fd-142">Azure PowerShell provides other commands for working locks, such as [Set-AzureRmResourceLock](/powershell/module/azurerm.resources/set-azurermresourcelock) tooupdate a lock, and [Remove-AzureRmResourceLock](/powershell/module/azurerm.resources/remove-azurermresourcelock) toodelete a lock.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="092fd-143">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="092fd-143">Azure CLI</span></span>

<span data-ttu-id="092fd-144">Verrou vous déployés ressources avec CLI d’Azure à l’aide de hello [créer de verrou de az](/cli/azure/lock#create) commande.</span><span class="sxs-lookup"><span data-stu-id="092fd-144">You lock deployed resources with Azure CLI by using hello [az lock create](/cli/azure/lock#create) command.</span></span>

<span data-ttu-id="092fd-145">toolock une ressource, fournissez hello nom hello, son type de ressource et son nom de groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="092fd-145">toolock a resource, provide hello name of hello resource, its resource type, and its resource group name.</span></span>

```azurecli
az lock create --name LockSite --lock-type CanNotDelete \
  --resource-group exampleresourcegroup --resource-name examplesite \
  --resource-type Microsoft.Web/sites
```

<span data-ttu-id="092fd-146">toolock un groupe de ressources, fournir un nom hello hello du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="092fd-146">toolock a resource group, provide hello name of hello resource group.</span></span>

```azurecli
az lock create --name LockGroup --lock-type CanNotDelete \
  --resource-group exampleresourcegroup
```

<span data-ttu-id="092fd-147">informations de tooget sur un verrou, utilisez [liste des verrous az](/cli/azure/lock#list).</span><span class="sxs-lookup"><span data-stu-id="092fd-147">tooget information about a lock, use [az lock list](/cli/azure/lock#list).</span></span> <span data-ttu-id="092fd-148">tooget tous les verrous hello dans votre abonnement, utilisez :</span><span class="sxs-lookup"><span data-stu-id="092fd-148">tooget all hello locks in your subscription, use:</span></span>

```azurecli
az lock list
```

<span data-ttu-id="092fd-149">tooget tous les verrous d’une ressource, utilisez :</span><span class="sxs-lookup"><span data-stu-id="092fd-149">tooget all locks for a resource, use:</span></span>

```azurecli
az lock list --resource-group exampleresourcegroup --resource-name examplesite \
  --namespace Microsoft.Web --resource-type sites --parent ""
```

<span data-ttu-id="092fd-150">tooget tous les verrous d’un groupe de ressources, utilisez :</span><span class="sxs-lookup"><span data-stu-id="092fd-150">tooget all locks for a resource group, use:</span></span>

```azurecli
az lock list --resource-group exampleresourcegroup
```

<span data-ttu-id="092fd-151">CLI Azure fournit des autres commandes pour les verrous de travail, tels que [mise à jour du verrou az](/cli/azure/lock#update) tooupdate un verrou, et [supprimer de verrou de az](/cli/azure/lock#delete) toodelete un verrou.</span><span class="sxs-lookup"><span data-stu-id="092fd-151">Azure CLI provides other commands for working locks, such as [az lock update](/cli/azure/lock#update) tooupdate a lock, and [az lock delete](/cli/azure/lock#delete) toodelete a lock.</span></span>

## <a name="rest-api"></a><span data-ttu-id="092fd-152">API REST</span><span class="sxs-lookup"><span data-stu-id="092fd-152">REST API</span></span>
<span data-ttu-id="092fd-153">Vous pouvez verrouiller les ressources déployées par hello [API REST pour les verrous de gestion](https://docs.microsoft.com/rest/api/resources/managementlocks).</span><span class="sxs-lookup"><span data-stu-id="092fd-153">You can lock deployed resources with hello [REST API for management locks](https://docs.microsoft.com/rest/api/resources/managementlocks).</span></span> <span data-ttu-id="092fd-154">Hello API REST vous toocreate et supprimer les verrous et récupérer des informations sur les verrous existants.</span><span class="sxs-lookup"><span data-stu-id="092fd-154">hello REST API enables you toocreate and delete locks, and retrieve information about existing locks.</span></span>

<span data-ttu-id="092fd-155">toocreate un verrou, exécutez :</span><span class="sxs-lookup"><span data-stu-id="092fd-155">toocreate a lock, run:</span></span>

    PUT https://management.azure.com/{scope}/providers/Microsoft.Authorization/locks/{lock-name}?api-version={api-version}

<span data-ttu-id="092fd-156">étendue de Hello peut être un abonnement, le groupe de ressources ou la ressource.</span><span class="sxs-lookup"><span data-stu-id="092fd-156">hello scope could be a subscription, resource group, or resource.</span></span> <span data-ttu-id="092fd-157">Hello-nom du verrou est tout ce que vous voulez verrouiller de hello toocall.</span><span class="sxs-lookup"><span data-stu-id="092fd-157">hello lock-name is whatever you want toocall hello lock.</span></span> <span data-ttu-id="092fd-158">Pour la version de l’API, utilisez **2015-01-01**.</span><span class="sxs-lookup"><span data-stu-id="092fd-158">For api-version, use **2015-01-01**.</span></span>

<span data-ttu-id="092fd-159">Dans la demande de hello, inclure un objet JSON qui spécifie les propriétés hello pour les verrous hello.</span><span class="sxs-lookup"><span data-stu-id="092fd-159">In hello request, include a JSON object that specifies hello properties for hello lock.</span></span>

    {
      "properties": {
        "level": "CanNotDelete",
        "notes": "Optional text notes."
      }
    } 

## <a name="next-steps"></a><span data-ttu-id="092fd-160">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="092fd-160">Next steps</span></span>
* <span data-ttu-id="092fd-161">Pour plus d’informations sur l’utilisation de verrous sur des ressources, consultez [Lock Down Your Azure Resources](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)</span><span class="sxs-lookup"><span data-stu-id="092fd-161">For more information about working with resource locks, see [Lock Down Your Azure Resources](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)</span></span>
* <span data-ttu-id="092fd-162">toolearn sur l’organisation logique de vos ressources, consultez [à l’aide des balises tooorganize vos ressources](resource-group-using-tags.md)</span><span class="sxs-lookup"><span data-stu-id="092fd-162">toolearn about logically organizing your resources, see [Using tags tooorganize your resources](resource-group-using-tags.md)</span></span>
* <span data-ttu-id="092fd-163">toochange groupe de ressources auquel une ressource se trouve dans, consultez [déplacer le groupe ressource toonew ressources](resource-group-move-resources.md)</span><span class="sxs-lookup"><span data-stu-id="092fd-163">toochange which resource group a resource resides in, see [Move resources toonew resource group](resource-group-move-resources.md)</span></span>
* <span data-ttu-id="092fd-164">Vous pouvez appliquer des restrictions et des conventions sur votre abonnement avec des stratégies personnalisées.</span><span class="sxs-lookup"><span data-stu-id="092fd-164">You can apply restrictions and conventions across your subscription with customized policies.</span></span> <span data-ttu-id="092fd-165">Pour plus d’informations, consultez [ressources toomanage de stratégie d’utilisation et de contrôler l’accès](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="092fd-165">For more information, see [Use Policy toomanage resources and control access](resource-manager-policy.md).</span></span>
* <span data-ttu-id="092fd-166">Pour obtenir des conseils comment les entreprises peuvent utiliser le Gestionnaire de ressources tooeffectively gérer les abonnements, consultez [une vue de structure Azure enterprise - gouvernance de l’abonnement normative](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="092fd-166">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

