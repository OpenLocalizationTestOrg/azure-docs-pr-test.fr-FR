---
title: "aaaManage Role-Based contrôle d’accès (RBAC) avec Azure PowerShell | Documents Microsoft"
description: "Comment toomanage RBAC avec Azure PowerShell, y compris la liste des rôles, l’attribution de rôles et la suppression des attributions de rôles."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 9e225dba-9044-4b13-b573-2f30d77925a9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: fa44991113e75b345177867b0bede38de4373e04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-role-based-access-control-with-azure-powershell"></a><span data-ttu-id="fa3cd-103">Gestion du Contrôle d’accès en fonction du rôle (RBAC) avec Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="fa3cd-103">Manage Role-Based Access Control with Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fa3cd-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fa3cd-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="fa3cd-105">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="fa3cd-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="fa3cd-106">API REST</span><span class="sxs-lookup"><span data-stu-id="fa3cd-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)

<span data-ttu-id="fa3cd-107">Vous pouvez utiliser le contrôle d’accès en fonction du rôle (RBAC) dans hello portail Azure et une API de gestion des ressources Azure toomanage accès tooyour souscription à un niveau de granularité fin.</span><span class="sxs-lookup"><span data-stu-id="fa3cd-107">You can use Role-Based Access Control (RBAC) in hello Azure portal and Azure Resource Management API toomanage access tooyour subscription at a fine-grained level.</span></span> <span data-ttu-id="fa3cd-108">Avec cette fonctionnalité, vous pouvez accorder l’accès pour les utilisateurs, groupes ou principaux du service Active Directory en attribuant certains toothem de rôles à une portée particulière.</span><span class="sxs-lookup"><span data-stu-id="fa3cd-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles toothem at a particular scope.</span></span>

<span data-ttu-id="fa3cd-109">Avant de pouvoir utiliser PowerShell toomanage RBAC, vous devez hello suivant des conditions préalables :</span><span class="sxs-lookup"><span data-stu-id="fa3cd-109">Before you can use PowerShell toomanage RBAC, you need hello following prerequisites:</span></span>

* <span data-ttu-id="fa3cd-110">Azure PowerShell, version 0.8.8 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="fa3cd-110">Azure PowerShell version 0.8.8 or later.</span></span> <span data-ttu-id="fa3cd-111">version la plus récente tooinstall hello et à associer à votre abonnement Azure, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fa3cd-111">tooinstall hello latest version and associate it with your Azure subscription, see [how tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="fa3cd-112">Applets de commande Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fa3cd-112">Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="fa3cd-113">Installer hello [applets de commande Azure Resource Manager](/powershell/azure/overview) dans PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fa3cd-113">Install hello [Azure Resource Manager cmdlets](/powershell/azure/overview) in PowerShell.</span></span>

## <a name="list-roles"></a><span data-ttu-id="fa3cd-114">Répertorier les rôles</span><span class="sxs-lookup"><span data-stu-id="fa3cd-114">List roles</span></span>
### <a name="list-all-available-roles"></a><span data-ttu-id="fa3cd-115">Répertorier tous les rôles disponibles</span><span class="sxs-lookup"><span data-stu-id="fa3cd-115">List all available roles</span></span>
<span data-ttu-id="fa3cd-116">rôles RBAC toolist qui sont disponibles pour l’attribution et tooinspect hello operations toowhich leur accorder l’accès, utilisez `Get-AzureRmRoleDefinition`.</span><span class="sxs-lookup"><span data-stu-id="fa3cd-116">toolist RBAC roles that are available for assignment and tooinspect hello operations toowhich they grant access, use `Get-AzureRmRoleDefinition`.</span></span>

```
Get-AzureRmRoleDefinition | FT Name, Description
```

![RBAC PowerShell - Get-AzureRmRoleDefinition - capture d’écran](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition1.png)

### <a name="list-actions-of-a-role"></a><span data-ttu-id="fa3cd-118">Répertorier les actions d'un rôle</span><span class="sxs-lookup"><span data-stu-id="fa3cd-118">List actions of a role</span></span>
<span data-ttu-id="fa3cd-119">actions de hello toolist pour un rôle spécifique, utilisez `Get-AzureRmRoleDefinition <role name>`.</span><span class="sxs-lookup"><span data-stu-id="fa3cd-119">toolist hello actions for a specific role, use `Get-AzureRmRoleDefinition <role name>`.</span></span>

```
Get-AzureRmRoleDefinition Contributor | FL Actions, NotActions

(Get-AzureRmRoleDefinition "Virtual Machine Contributor").Actions
```

![RBAC PowerShell - Get-AzureRmRoleDefinition pour un rôle spécifique - capture d’écran](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition2.png)

## <a name="see-who-has-access"></a><span data-ttu-id="fa3cd-121">Voir quel utilisateur a des autorisations d’accès</span><span class="sxs-lookup"><span data-stu-id="fa3cd-121">See who has access</span></span>
<span data-ttu-id="fa3cd-122">Utilisez des affectations d’accès toolist RBAC, `Get-AzureRmRoleAssignment`.</span><span class="sxs-lookup"><span data-stu-id="fa3cd-122">toolist RBAC access assignments, use `Get-AzureRmRoleAssignment`.</span></span>

### <a name="list-role-assignments-at-a-specific-scope"></a><span data-ttu-id="fa3cd-123">Répertorier les attributions de rôle dans une étendue spécifique</span><span class="sxs-lookup"><span data-stu-id="fa3cd-123">List role assignments at a specific scope</span></span>
<span data-ttu-id="fa3cd-124">Vous pouvez voir toutes les affectations d’accès hello pour une ressource, un groupe de ressources ou un abonnement spécifié.</span><span class="sxs-lookup"><span data-stu-id="fa3cd-124">You can see all hello access assignments for a specified subscription, resource group, or resource.</span></span> <span data-ttu-id="fa3cd-125">Par exemple, toosee hello toutes les attributions active hello pour un groupe de ressources, utilisez `Get-AzureRmRoleAssignment -ResourceGroupName <resource group name>`.</span><span class="sxs-lookup"><span data-stu-id="fa3cd-125">For example, toosee hello all hello active assignments for a resource group, use `Get-AzureRmRoleAssignment -ResourceGroupName <resource group name>`.</span></span>

```
Get-AzureRmRoleAssignment -ResourceGroupName Pharma-Sales-ProjectForcast | FL DisplayName, RoleDefinitionName, Scope
```

![RBAC PowerShell - Get-AzureRmRoleAssignment pour un groupe de ressource - capture d’écran](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment1.png)

### <a name="list-roles-assigned-tooa-user"></a><span data-ttu-id="fa3cd-127">Liste des rôles tooa utilisateur attribués</span><span class="sxs-lookup"><span data-stu-id="fa3cd-127">List roles assigned tooa user</span></span>
<span data-ttu-id="fa3cd-128">toolist tous les rôles hello assignés tooa spécifié utilisateur et les rôles hello qui sont affectés à des groupes toohello toowhich hello utilisateur appartient, utilisez `Get-AzureRmRoleAssignment -SignInName <User email> -ExpandPrincipalGroups`.</span><span class="sxs-lookup"><span data-stu-id="fa3cd-128">toolist all hello roles that are assigned tooa specified user and hello roles that are assigned toohello groups toowhich hello user belongs, use `Get-AzureRmRoleAssignment -SignInName <User email> -ExpandPrincipalGroups`.</span></span>

```
Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com | FL DisplayName, RoleDefinitionName, Scope

Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com -ExpandPrincipalGroups | FL DisplayName, RoleDefinitionName, Scope
```

![RBAC PowerShell - Get-AzureRmRoleAssignment pour un utilisateur - capture d’écran](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment2.png)

### <a name="list-classic-service-administrator-and-coadmin-role-assignments"></a><span data-ttu-id="fa3cd-130">Répertorier les affectations classiques des rôles Administrateur de service et Coadministrateur</span><span class="sxs-lookup"><span data-stu-id="fa3cd-130">List classic service administrator and coadmin role assignments</span></span>
<span data-ttu-id="fa3cd-131">les affectations d’accès toolist pour l’administrateur de l’abonnement classique hello et coadministrators, utilisez :</span><span class="sxs-lookup"><span data-stu-id="fa3cd-131">toolist access assignments for hello classic subscription administrator and coadministrators, use:</span></span>

    Get-AzureRmRoleAssignment -IncludeClassicAdministrators

## <a name="grant-access"></a><span data-ttu-id="fa3cd-132">Accorder l'accès</span><span class="sxs-lookup"><span data-stu-id="fa3cd-132">Grant access</span></span>
### <a name="search-for-object-ids"></a><span data-ttu-id="fa3cd-133">Rechercher des ID d’objet</span><span class="sxs-lookup"><span data-stu-id="fa3cd-133">Search for object IDs</span></span>
<span data-ttu-id="fa3cd-134">tooassign un rôle, vous devez tooidentify hello objet (utilisateur, groupe ou application) et étendue de hello.</span><span class="sxs-lookup"><span data-stu-id="fa3cd-134">tooassign a role, you need tooidentify both hello object (user, group, or application) and hello scope.</span></span>

<span data-ttu-id="fa3cd-135">Si vous ne connaissez pas hello ID d’abonnement, vous pouvez le trouver dans hello **abonnements** panneau sur hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="fa3cd-135">If you don't know hello subscription ID, you can find it in hello **Subscriptions** blade on hello Azure portal.</span></span> <span data-ttu-id="fa3cd-136">toolearn tooquery hello ID d’abonnement, voir [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) sur MSDN.</span><span class="sxs-lookup"><span data-stu-id="fa3cd-136">toolearn how tooquery for hello subscription ID, see [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) on MSDN.</span></span>

<span data-ttu-id="fa3cd-137">ID d’objet tooget hello pour un groupe Azure AD, utilisez :</span><span class="sxs-lookup"><span data-stu-id="fa3cd-137">tooget hello object ID for an Azure AD group, use:</span></span>

    Get-AzureRmADGroup -SearchString <group name in quotes>

<span data-ttu-id="fa3cd-138">ID d’objet tooget hello pour un principal du service Azure AD ou une application, utilisez :</span><span class="sxs-lookup"><span data-stu-id="fa3cd-138">tooget hello object ID for an Azure AD service principal or application, use:</span></span>

    Get-AzureRmADServicePrincipal -SearchString <service name in quotes>

### <a name="assign-a-role-tooan-application-at-hello-subscription-scope"></a><span data-ttu-id="fa3cd-139">Affecter une application tooan de rôle au niveau de l’étendue de l’abonnement hello</span><span class="sxs-lookup"><span data-stu-id="fa3cd-139">Assign a role tooan application at hello subscription scope</span></span>
<span data-ttu-id="fa3cd-140">application de tooan toogrant accès à l’étendue de l’abonnement hello, utilisez :</span><span class="sxs-lookup"><span data-stu-id="fa3cd-140">toogrant access tooan application at hello subscription scope, use:</span></span>

    New-AzureRmRoleAssignment -ObjectId <application id> -RoleDefinitionName <role name> -Scope <subscription id>

![RBAC PowerShell - New-AzureRmRoleAssignment - capture d’écran](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment2.png)

### <a name="assign-a-role-tooa-user-at-hello-resource-group-scope"></a><span data-ttu-id="fa3cd-142">Affecter un utilisateur tooa de rôle au niveau de l’étendue de groupe de ressources hello</span><span class="sxs-lookup"><span data-stu-id="fa3cd-142">Assign a role tooa user at hello resource group scope</span></span>
<span data-ttu-id="fa3cd-143">utilisateur de tooa toogrant accès à l’étendue de groupe de ressources hello, utilisez :</span><span class="sxs-lookup"><span data-stu-id="fa3cd-143">toogrant access tooa user at hello resource group scope, use:</span></span>

    New-AzureRmRoleAssignment -SignInName <email of user> -RoleDefinitionName <role name in quotes> -ResourceGroupName <resource group name>

![RBAC PowerShell - New-AzureRmRoleAssignment - capture d’écran](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment3.png)

### <a name="assign-a-role-tooa-group-at-hello-resource-scope"></a><span data-ttu-id="fa3cd-145">Affecter un groupe de tooa de rôle au niveau de la portée de la ressource hello</span><span class="sxs-lookup"><span data-stu-id="fa3cd-145">Assign a role tooa group at hello resource scope</span></span>
<span data-ttu-id="fa3cd-146">groupe de tooa toogrant accès à la portée de la ressource hello, utilisez :</span><span class="sxs-lookup"><span data-stu-id="fa3cd-146">toogrant access tooa group at hello resource scope, use:</span></span>

    New-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name in quotes> -ResourceName <resource name> -ResourceType <resource type> -ParentResource <parent resource> -ResourceGroupName <resource group name>

![RBAC PowerShell - New-AzureRmRoleAssignment - capture d’écran](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment4.png)

## <a name="remove-access"></a><span data-ttu-id="fa3cd-148">Suppression d'accès</span><span class="sxs-lookup"><span data-stu-id="fa3cd-148">Remove access</span></span>
<span data-ttu-id="fa3cd-149">tooremove l’accès pour les utilisateurs, des groupes et des applications, utilisez :</span><span class="sxs-lookup"><span data-stu-id="fa3cd-149">tooremove access for users, groups, and applications, use:</span></span>

    Remove-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name> -Scope <scope such as subscription id>

![RBAC PowerShell - Remove-AzureRmRoleAssignment - capture d’écran](./media/role-based-access-control-manage-access-powershell/3-remove-azure-rm-role-assignment.png)

## <a name="create-a-custom-role"></a><span data-ttu-id="fa3cd-151">Créer un rôle personnalisé</span><span class="sxs-lookup"><span data-stu-id="fa3cd-151">Create a custom role</span></span>
<span data-ttu-id="fa3cd-152">toocreate un rôle personnalisé, utilisez hello ```New-AzureRmRoleDefinition``` commande.</span><span class="sxs-lookup"><span data-stu-id="fa3cd-152">toocreate a custom role, use hello ```New-AzureRmRoleDefinition``` command.</span></span> <span data-ttu-id="fa3cd-153">Il existe deux méthodes de structuration de rôle hello, à l’aide de PSRoleDefinitionObject ou un modèle JSON.</span><span class="sxs-lookup"><span data-stu-id="fa3cd-153">There are two methods of structuring hello role, using PSRoleDefinitionObject or a JSON template.</span></span> 

## <a name="get-actions-for-a-resource-provider"></a><span data-ttu-id="fa3cd-154">Actions Get pour un fournisseur de ressources</span><span class="sxs-lookup"><span data-stu-id="fa3cd-154">Get Actions for a Resource Provider</span></span>
<span data-ttu-id="fa3cd-155">Lorsque vous créez des rôles personnalisés à partir de zéro, il est important tooknow tous hello opérations possibles, de fournisseurs de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="fa3cd-155">When You are creating custom roles from scratch, it is important tooknow all hello possible operations from hello resource providers.</span></span>
<span data-ttu-id="fa3cd-156">Hello d’utilisation ```Get-AzureRMProviderOperation``` commande tooget ces informations.</span><span class="sxs-lookup"><span data-stu-id="fa3cd-156">Use hello ```Get-AzureRMProviderOperation``` command tooget this information.</span></span>
<span data-ttu-id="fa3cd-157">Par exemple, si vous souhaitez toocheck toutes les opérations disponibles hello pour la Machine virtuelle utilisent cette commande :</span><span class="sxs-lookup"><span data-stu-id="fa3cd-157">For example, if you want toocheck all hello available operations for virtual Machine use this command:</span></span>

```
Get-AzureRMProviderOperation "Microsoft.Compute/virtualMachines/*" | FT OperationName, Operation , Description -AutoSize
```

### <a name="create-role-with-psroledefinitionobject"></a><span data-ttu-id="fa3cd-158">Création d’un rôle avec PSRoleDefinitionObject</span><span class="sxs-lookup"><span data-stu-id="fa3cd-158">Create role with PSRoleDefinitionObject</span></span>
<span data-ttu-id="fa3cd-159">Lorsque vous utilisez PowerShell toocreate un rôle personnalisé, vous pouvez démarrer à partir de zéro ou utilisez une des hello [rôles intégrés](role-based-access-built-in-roles.md) comme point de départ.</span><span class="sxs-lookup"><span data-stu-id="fa3cd-159">When you use PowerShell toocreate a custom role, you can start from scratch or use one of hello [built-in roles](role-based-access-built-in-roles.md) as a starting point.</span></span> <span data-ttu-id="fa3cd-160">exemple Hello dans cette section commence par un rôle intégré et il personnalise puis avec plus de privilèges.</span><span class="sxs-lookup"><span data-stu-id="fa3cd-160">hello example in this section starts with a built-in role and then customizes it with more privileges.</span></span> <span data-ttu-id="fa3cd-161">Modifier hello de hello attributs tooadd *Actions*, *notActions*, ou *étendues* que vous souhaitez, puis enregistrez les modifications hello sous un nouveau rôle.</span><span class="sxs-lookup"><span data-stu-id="fa3cd-161">Edit hello attributes tooadd hello *Actions*, *notActions*, or *scopes* that you want, and then save hello changes as a new role.</span></span>

<span data-ttu-id="fa3cd-162">Hello exemple suivant commence par hello *contributeur de l’ordinateur virtuel* rôle et utilise ce toocreate un rôle personnalisé appelé *opérateur de l’ordinateur virtuel*.</span><span class="sxs-lookup"><span data-stu-id="fa3cd-162">hello following example starts with hello *Virtual Machine Contributor* role and uses that toocreate a custom role called *Virtual Machine Operator*.</span></span> <span data-ttu-id="fa3cd-163">nouveau rôle de Hello accorde l’accès tooall lire des opérations de *Microsoft.Compute*, *Microsoft.Storage*, et *Microsoft.Network* fournisseurs et accorde l’accès aux ressources de toostart, redémarrer et analyser des ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="fa3cd-163">hello new role grants access tooall read operations of *Microsoft.Compute*, *Microsoft.Storage*, and *Microsoft.Network* resource providers and grants access toostart, restart, and monitor virtual machines.</span></span> <span data-ttu-id="fa3cd-164">rôle personnalisé de Hello peut être utilisé dans deux abonnements.</span><span class="sxs-lookup"><span data-stu-id="fa3cd-164">hello custom role can be used in two subscriptions.</span></span>

```
$role = Get-AzureRmRoleDefinition "Virtual Machine Contributor"
$role.Id = $null
$role.Name = "Virtual Machine Operator"
$role.Description = "Can monitor and restart virtual machines."
$role.Actions.Clear()
$role.Actions.Add("Microsoft.Storage/*/read")
$role.Actions.Add("Microsoft.Network/*/read")
$role.Actions.Add("Microsoft.Compute/*/read")
$role.Actions.Add("Microsoft.Compute/virtualMachines/start/action")
$role.Actions.Add("Microsoft.Compute/virtualMachines/restart/action")
$role.Actions.Add("Microsoft.Authorization/*/read")
$role.Actions.Add("Microsoft.Resources/subscriptions/resourceGroups/read")
$role.Actions.Add("Microsoft.Insights/alertRules/*")
$role.Actions.Add("Microsoft.Support/*")
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add("/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e")
$role.AssignableScopes.Add("/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624")
New-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell - Get-AzureRmRoleDefinition - capture d’écran](./media/role-based-access-control-manage-access-powershell/2-new-azurermroledefinition.png)

### <a name="create-role-with-json-template"></a><span data-ttu-id="fa3cd-166">Création d’un rôle avec le modèle JSON</span><span class="sxs-lookup"><span data-stu-id="fa3cd-166">Create role with JSON template</span></span>
<span data-ttu-id="fa3cd-167">Un modèle JSON peut être utilisé en tant que définition de source de hello pour les rôles personnalisés hello.</span><span class="sxs-lookup"><span data-stu-id="fa3cd-167">A JSON template can be used as hello source definition for hello custom role.</span></span> <span data-ttu-id="fa3cd-168">Hello exemple suivant crée un rôle personnalisé qui autorise l’accès en lecture toostorage et ressources de calcul, toosupport d’accès et ajoute ce rôle tootwo abonnements.</span><span class="sxs-lookup"><span data-stu-id="fa3cd-168">hello following example creates a custom role that allows read access toostorage and compute resources, access toosupport, and adds that role tootwo subscriptions.</span></span> <span data-ttu-id="fa3cd-169">Créer un nouveau fichier `C:\CustomRoles\customrole1.json` avec hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="fa3cd-169">Create a new file `C:\CustomRoles\customrole1.json` with hello following example.</span></span> <span data-ttu-id="fa3cd-170">Hello Id doit être défini trop`null` lors de la création de rôle initial en tant qu’un nouvel ID est généré automatiquement.</span><span class="sxs-lookup"><span data-stu-id="fa3cd-170">hello Id should be set too`null` on initial role creation as a new ID is generated automatically.</span></span> 

```
{
  "Name": "Custom Role 1",
  "Id": null,
  "IsCustom": true,
  "Description": "Allows for read access tooAzure storage and compute resources and access toosupport",
  "Actions": [
    "Microsoft.Compute/*/read",
    "Microsoft.Storage/*/read",
    "Microsoft.Support/*"
  ],
  "NotActions": [
  ],
  "AssignableScopes": [
    "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624"
  ]
}
```
<span data-ttu-id="fa3cd-171">tooadd hello rôle toohello abonnements, exécutez hello suivant de commande PowerShell :</span><span class="sxs-lookup"><span data-stu-id="fa3cd-171">tooadd hello role toohello subscriptions, run hello following PowerShell command:</span></span>
```
New-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="modify-a-custom-role"></a><span data-ttu-id="fa3cd-172">Modifier un rôle personnalisé</span><span class="sxs-lookup"><span data-stu-id="fa3cd-172">Modify a custom role</span></span>
<span data-ttu-id="fa3cd-173">Toocreating comme un rôle personnalisé, vous pouvez modifier un rôle personnalisé existant à l’aide de hello PSRoleDefinitionObject ou un modèle JSON.</span><span class="sxs-lookup"><span data-stu-id="fa3cd-173">Similar toocreating a custom role, you can modify an existing custom role using either hello PSRoleDefinitionObject or a JSON template.</span></span>

### <a name="modify-role-with-psroledefinitionobject"></a><span data-ttu-id="fa3cd-174">Modification d’un rôle avec PSRoleDefinitionObject</span><span class="sxs-lookup"><span data-stu-id="fa3cd-174">Modify role with PSRoleDefinitionObject</span></span>
<span data-ttu-id="fa3cd-175">toomodify un rôle personnalisé, utilisez tout d’abord, hello `Get-AzureRmRoleDefinition` tooretrieve hello rôle définition des commandes.</span><span class="sxs-lookup"><span data-stu-id="fa3cd-175">toomodify a custom role, first, use hello `Get-AzureRmRoleDefinition` command tooretrieve hello role definition.</span></span> <span data-ttu-id="fa3cd-176">Ensuite, modifiez hello souhaité définition de rôle toohello.</span><span class="sxs-lookup"><span data-stu-id="fa3cd-176">Second, make hello desired changes toohello role definition.</span></span> <span data-ttu-id="fa3cd-177">Enfin, utilisez hello `Set-AzureRmRoleDefinition` commande toosave hello modifié la définition de rôle.</span><span class="sxs-lookup"><span data-stu-id="fa3cd-177">Finally, use hello `Set-AzureRmRoleDefinition` command toosave hello modified role definition.</span></span>

<span data-ttu-id="fa3cd-178">exemple Hello ajoute hello `Microsoft.Insights/diagnosticSettings/*` opération toohello *opérateur de Machine virtuelle* rôle personnalisé.</span><span class="sxs-lookup"><span data-stu-id="fa3cd-178">hello following example adds hello `Microsoft.Insights/diagnosticSettings/*` operation toohello *Virtual Machine Operator* custom role.</span></span>

```
$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.Actions.Add("Microsoft.Insights/diagnosticSettings/*")
Set-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell - Set-AzureRmRoleDefinition - capture d’écran](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-1.png)

<span data-ttu-id="fa3cd-180">Hello exemple suivant ajoute un abonnement Azure toohello assignable les étendues de hello *opérateur de Machine virtuelle* rôle personnalisé.</span><span class="sxs-lookup"><span data-stu-id="fa3cd-180">hello following example adds an Azure subscription toohello assignable scopes of hello *Virtual Machine Operator* custom role.</span></span>

```
Get-AzureRmSubscription - SubscriptionName Production3

$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.AssignableScopes.Add("/subscriptions/34370e90-ac4a-4bf9-821f-85eeedead1a2")
Set-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell - Set-AzureRmRoleDefinition - capture d’écran](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-2.png)

### <a name="modify-role-with-json-template"></a><span data-ttu-id="fa3cd-182">Modification d’un rôle avec le modèle JSON</span><span class="sxs-lookup"><span data-stu-id="fa3cd-182">Modify role with JSON template</span></span>
<span data-ttu-id="fa3cd-183">À l’aide du modèle JSON de la précédente hello, vous pouvez facilement modifier une tooadd rôle personnalisé existant ou supprimer des Actions.</span><span class="sxs-lookup"><span data-stu-id="fa3cd-183">Using hello previous JSON template, you can easily modify an existing custom role tooadd or remove Actions.</span></span> <span data-ttu-id="fa3cd-184">Mettre à jour le modèle JSON hello et ajouter des actions de lecture hello de mise en réseau comme indiqué dans hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="fa3cd-184">Update hello JSON template and add hello read action for networking as shown in hello following example.</span></span> <span data-ttu-id="fa3cd-185">définitions Hello répertoriées dans le modèle de hello ne sont pas appliqués de manière cumulative tooan définition existante, ce qui signifie que ce rôle hello s’affiche exactement comme vous le spécifiez dans le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="fa3cd-185">hello definitions listed in hello template are not cumulatively applied tooan existing definition, meaning that hello role appears exactly as you specify in hello template.</span></span> <span data-ttu-id="fa3cd-186">Vous devez également le champ de code hello tooupdate avec l’ID de hello du rôle de hello.</span><span class="sxs-lookup"><span data-stu-id="fa3cd-186">You also need tooupdate hello Id field with hello ID of hello role.</span></span> <span data-ttu-id="fa3cd-187">Si vous ne savez pas quelle est cette valeur, vous pouvez utiliser hello `Get-AzureRmRoleDefinition` tooget de l’applet de commande ces informations.</span><span class="sxs-lookup"><span data-stu-id="fa3cd-187">If you aren't sure what this value is, you can use hello `Get-AzureRmRoleDefinition` cmdlet tooget this information.</span></span>

```
{
  "Name": "Custom Role 1",
  "Id": "acce7ded-2559-449d-bcd5-e9604e50bad1",
  "IsCustom": true,
  "Description": "Allows for read access tooAzure storage and compute resources and access toosupport",
  "Actions": [
    "Microsoft.Compute/*/read",
    "Microsoft.Storage/*/read",
    "Microsoft.Network/*/read",
    "Microsoft.Support/*"
  ],
  "NotActions": [
  ],
  "AssignableScopes": [
    "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624"
  ]
}
```

<span data-ttu-id="fa3cd-188">tooupdate hello rôle d’existant, exécutez hello suivant de commande PowerShell :</span><span class="sxs-lookup"><span data-stu-id="fa3cd-188">tooupdate hello existing role, run hello following PowerShell command:</span></span>
```
Set-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="delete-a-custom-role"></a><span data-ttu-id="fa3cd-189">Supprimer un rôle personnalisé</span><span class="sxs-lookup"><span data-stu-id="fa3cd-189">Delete a custom role</span></span>
<span data-ttu-id="fa3cd-190">toodelete un rôle personnalisé, utilisez hello `Remove-AzureRmRoleDefinition` commande.</span><span class="sxs-lookup"><span data-stu-id="fa3cd-190">toodelete a custom role, use hello `Remove-AzureRmRoleDefinition` command.</span></span>

<span data-ttu-id="fa3cd-191">exemple Hello supprime hello *opérateur de Machine virtuelle* rôle personnalisé.</span><span class="sxs-lookup"><span data-stu-id="fa3cd-191">hello following example removes hello *Virtual Machine Operator* custom role.</span></span>

```
Get-AzureRmRoleDefinition "Virtual Machine Operator"

Get-AzureRmRoleDefinition "Virtual Machine Operator" | Remove-AzureRmRoleDefinition
```

![RBAC PowerShell - Remove-AzureRmRoleDefinition - capture d’écran](./media/role-based-access-control-manage-access-powershell/4-remove-azurermroledefinition.png)

## <a name="list-custom-roles"></a><span data-ttu-id="fa3cd-193">Répertorier les rôles personnalisés</span><span class="sxs-lookup"><span data-stu-id="fa3cd-193">List custom roles</span></span>
<span data-ttu-id="fa3cd-194">rôles hello toolist qui sont disponibles pour l’assignation dans une étendue, utilisez hello `Get-AzureRmRoleDefinition` commande.</span><span class="sxs-lookup"><span data-stu-id="fa3cd-194">toolist hello roles that are available for assignment at a scope, use hello `Get-AzureRmRoleDefinition` command.</span></span>

<span data-ttu-id="fa3cd-195">Bonjour à l’exemple suivant répertorie tous les rôles qui sont disponibles pour l’assignation dans l’abonnement de hello sélectionné.</span><span class="sxs-lookup"><span data-stu-id="fa3cd-195">hello following example lists all roles that are available for assignment in hello selected subscription.</span></span>

```
Get-AzureRmRoleDefinition | FT Name, IsCustom
```

![RBAC PowerShell - Get-AzureRmRoleDefinition - capture d’écran](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition-1.png)

<span data-ttu-id="fa3cd-197">Dans l’exemple suivant de hello, hello *opérateur de Machine virtuelle* rôle personnalisé n’est pas disponible dans hello *Production4* abonnement, car cet abonnement n’est pas Bonjour  **AssignableScopes** du rôle de hello.</span><span class="sxs-lookup"><span data-stu-id="fa3cd-197">In hello following example, hello *Virtual Machine Operator* custom role isn’t available in hello *Production4* subscription because that subscription isn’t in hello **AssignableScopes** of hello role.</span></span>

![RBAC PowerShell - Get-AzureRmRoleDefinition - capture d’écran](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition2.png)

## <a name="see-also"></a><span data-ttu-id="fa3cd-199">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="fa3cd-199">See also</span></span>
* <span data-ttu-id="fa3cd-200">[Utilisation d’Azure PowerShell avec Azure Resource Manager](../powershell-azure-resource-manager.md)
  [!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]</span><span class="sxs-lookup"><span data-stu-id="fa3cd-200">[Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md)
[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]</span></span>

