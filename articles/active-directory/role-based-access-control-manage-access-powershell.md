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
# <a name="manage-role-based-access-control-with-azure-powershell"></a>Gestion du Contrôle d’accès en fonction du rôle (RBAC) avec Azure PowerShell
> [!div class="op_single_selector"]
> * [PowerShell](role-based-access-control-manage-access-powershell.md)
> * [Interface de ligne de commande Azure](role-based-access-control-manage-access-azure-cli.md)
> * [API REST](role-based-access-control-manage-access-rest.md)

Vous pouvez utiliser le contrôle d’accès en fonction du rôle (RBAC) dans hello portail Azure et une API de gestion des ressources Azure toomanage accès tooyour souscription à un niveau de granularité fin. Avec cette fonctionnalité, vous pouvez accorder l’accès pour les utilisateurs, groupes ou principaux du service Active Directory en attribuant certains toothem de rôles à une portée particulière.

Avant de pouvoir utiliser PowerShell toomanage RBAC, vous devez hello suivant des conditions préalables :

* Azure PowerShell, version 0.8.8 ou ultérieure. version la plus récente tooinstall hello et à associer à votre abonnement Azure, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).
* Applets de commande Azure Resource Manager. Installer hello [applets de commande Azure Resource Manager](/powershell/azure/overview) dans PowerShell.

## <a name="list-roles"></a>Répertorier les rôles
### <a name="list-all-available-roles"></a>Répertorier tous les rôles disponibles
rôles RBAC toolist qui sont disponibles pour l’attribution et tooinspect hello operations toowhich leur accorder l’accès, utilisez `Get-AzureRmRoleDefinition`.

```
Get-AzureRmRoleDefinition | FT Name, Description
```

![RBAC PowerShell - Get-AzureRmRoleDefinition - capture d’écran](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition1.png)

### <a name="list-actions-of-a-role"></a>Répertorier les actions d'un rôle
actions de hello toolist pour un rôle spécifique, utilisez `Get-AzureRmRoleDefinition <role name>`.

```
Get-AzureRmRoleDefinition Contributor | FL Actions, NotActions

(Get-AzureRmRoleDefinition "Virtual Machine Contributor").Actions
```

![RBAC PowerShell - Get-AzureRmRoleDefinition pour un rôle spécifique - capture d’écran](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition2.png)

## <a name="see-who-has-access"></a>Voir quel utilisateur a des autorisations d’accès
Utilisez des affectations d’accès toolist RBAC, `Get-AzureRmRoleAssignment`.

### <a name="list-role-assignments-at-a-specific-scope"></a>Répertorier les attributions de rôle dans une étendue spécifique
Vous pouvez voir toutes les affectations d’accès hello pour une ressource, un groupe de ressources ou un abonnement spécifié. Par exemple, toosee hello toutes les attributions active hello pour un groupe de ressources, utilisez `Get-AzureRmRoleAssignment -ResourceGroupName <resource group name>`.

```
Get-AzureRmRoleAssignment -ResourceGroupName Pharma-Sales-ProjectForcast | FL DisplayName, RoleDefinitionName, Scope
```

![RBAC PowerShell - Get-AzureRmRoleAssignment pour un groupe de ressource - capture d’écran](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment1.png)

### <a name="list-roles-assigned-tooa-user"></a>Liste des rôles tooa utilisateur attribués
toolist tous les rôles hello assignés tooa spécifié utilisateur et les rôles hello qui sont affectés à des groupes toohello toowhich hello utilisateur appartient, utilisez `Get-AzureRmRoleAssignment -SignInName <User email> -ExpandPrincipalGroups`.

```
Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com | FL DisplayName, RoleDefinitionName, Scope

Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com -ExpandPrincipalGroups | FL DisplayName, RoleDefinitionName, Scope
```

![RBAC PowerShell - Get-AzureRmRoleAssignment pour un utilisateur - capture d’écran](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment2.png)

### <a name="list-classic-service-administrator-and-coadmin-role-assignments"></a>Répertorier les affectations classiques des rôles Administrateur de service et Coadministrateur
les affectations d’accès toolist pour l’administrateur de l’abonnement classique hello et coadministrators, utilisez :

    Get-AzureRmRoleAssignment -IncludeClassicAdministrators

## <a name="grant-access"></a>Accorder l'accès
### <a name="search-for-object-ids"></a>Rechercher des ID d’objet
tooassign un rôle, vous devez tooidentify hello objet (utilisateur, groupe ou application) et étendue de hello.

Si vous ne connaissez pas hello ID d’abonnement, vous pouvez le trouver dans hello **abonnements** panneau sur hello portail Azure. toolearn tooquery hello ID d’abonnement, voir [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) sur MSDN.

ID d’objet tooget hello pour un groupe Azure AD, utilisez :

    Get-AzureRmADGroup -SearchString <group name in quotes>

ID d’objet tooget hello pour un principal du service Azure AD ou une application, utilisez :

    Get-AzureRmADServicePrincipal -SearchString <service name in quotes>

### <a name="assign-a-role-tooan-application-at-hello-subscription-scope"></a>Affecter une application tooan de rôle au niveau de l’étendue de l’abonnement hello
application de tooan toogrant accès à l’étendue de l’abonnement hello, utilisez :

    New-AzureRmRoleAssignment -ObjectId <application id> -RoleDefinitionName <role name> -Scope <subscription id>

![RBAC PowerShell - New-AzureRmRoleAssignment - capture d’écran](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment2.png)

### <a name="assign-a-role-tooa-user-at-hello-resource-group-scope"></a>Affecter un utilisateur tooa de rôle au niveau de l’étendue de groupe de ressources hello
utilisateur de tooa toogrant accès à l’étendue de groupe de ressources hello, utilisez :

    New-AzureRmRoleAssignment -SignInName <email of user> -RoleDefinitionName <role name in quotes> -ResourceGroupName <resource group name>

![RBAC PowerShell - New-AzureRmRoleAssignment - capture d’écran](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment3.png)

### <a name="assign-a-role-tooa-group-at-hello-resource-scope"></a>Affecter un groupe de tooa de rôle au niveau de la portée de la ressource hello
groupe de tooa toogrant accès à la portée de la ressource hello, utilisez :

    New-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name in quotes> -ResourceName <resource name> -ResourceType <resource type> -ParentResource <parent resource> -ResourceGroupName <resource group name>

![RBAC PowerShell - New-AzureRmRoleAssignment - capture d’écran](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment4.png)

## <a name="remove-access"></a>Suppression d'accès
tooremove l’accès pour les utilisateurs, des groupes et des applications, utilisez :

    Remove-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name> -Scope <scope such as subscription id>

![RBAC PowerShell - Remove-AzureRmRoleAssignment - capture d’écran](./media/role-based-access-control-manage-access-powershell/3-remove-azure-rm-role-assignment.png)

## <a name="create-a-custom-role"></a>Créer un rôle personnalisé
toocreate un rôle personnalisé, utilisez hello ```New-AzureRmRoleDefinition``` commande. Il existe deux méthodes de structuration de rôle hello, à l’aide de PSRoleDefinitionObject ou un modèle JSON. 

## <a name="get-actions-for-a-resource-provider"></a>Actions Get pour un fournisseur de ressources
Lorsque vous créez des rôles personnalisés à partir de zéro, il est important tooknow tous hello opérations possibles, de fournisseurs de ressources hello.
Hello d’utilisation ```Get-AzureRMProviderOperation``` commande tooget ces informations.
Par exemple, si vous souhaitez toocheck toutes les opérations disponibles hello pour la Machine virtuelle utilisent cette commande :

```
Get-AzureRMProviderOperation "Microsoft.Compute/virtualMachines/*" | FT OperationName, Operation , Description -AutoSize
```

### <a name="create-role-with-psroledefinitionobject"></a>Création d’un rôle avec PSRoleDefinitionObject
Lorsque vous utilisez PowerShell toocreate un rôle personnalisé, vous pouvez démarrer à partir de zéro ou utilisez une des hello [rôles intégrés](role-based-access-built-in-roles.md) comme point de départ. exemple Hello dans cette section commence par un rôle intégré et il personnalise puis avec plus de privilèges. Modifier hello de hello attributs tooadd *Actions*, *notActions*, ou *étendues* que vous souhaitez, puis enregistrez les modifications hello sous un nouveau rôle.

Hello exemple suivant commence par hello *contributeur de l’ordinateur virtuel* rôle et utilise ce toocreate un rôle personnalisé appelé *opérateur de l’ordinateur virtuel*. nouveau rôle de Hello accorde l’accès tooall lire des opérations de *Microsoft.Compute*, *Microsoft.Storage*, et *Microsoft.Network* fournisseurs et accorde l’accès aux ressources de toostart, redémarrer et analyser des ordinateurs virtuels. rôle personnalisé de Hello peut être utilisé dans deux abonnements.

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

### <a name="create-role-with-json-template"></a>Création d’un rôle avec le modèle JSON
Un modèle JSON peut être utilisé en tant que définition de source de hello pour les rôles personnalisés hello. Hello exemple suivant crée un rôle personnalisé qui autorise l’accès en lecture toostorage et ressources de calcul, toosupport d’accès et ajoute ce rôle tootwo abonnements. Créer un nouveau fichier `C:\CustomRoles\customrole1.json` avec hello l’exemple suivant. Hello Id doit être défini trop`null` lors de la création de rôle initial en tant qu’un nouvel ID est généré automatiquement. 

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
tooadd hello rôle toohello abonnements, exécutez hello suivant de commande PowerShell :
```
New-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="modify-a-custom-role"></a>Modifier un rôle personnalisé
Toocreating comme un rôle personnalisé, vous pouvez modifier un rôle personnalisé existant à l’aide de hello PSRoleDefinitionObject ou un modèle JSON.

### <a name="modify-role-with-psroledefinitionobject"></a>Modification d’un rôle avec PSRoleDefinitionObject
toomodify un rôle personnalisé, utilisez tout d’abord, hello `Get-AzureRmRoleDefinition` tooretrieve hello rôle définition des commandes. Ensuite, modifiez hello souhaité définition de rôle toohello. Enfin, utilisez hello `Set-AzureRmRoleDefinition` commande toosave hello modifié la définition de rôle.

exemple Hello ajoute hello `Microsoft.Insights/diagnosticSettings/*` opération toohello *opérateur de Machine virtuelle* rôle personnalisé.

```
$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.Actions.Add("Microsoft.Insights/diagnosticSettings/*")
Set-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell - Set-AzureRmRoleDefinition - capture d’écran](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-1.png)

Hello exemple suivant ajoute un abonnement Azure toohello assignable les étendues de hello *opérateur de Machine virtuelle* rôle personnalisé.

```
Get-AzureRmSubscription - SubscriptionName Production3

$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.AssignableScopes.Add("/subscriptions/34370e90-ac4a-4bf9-821f-85eeedead1a2")
Set-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell - Set-AzureRmRoleDefinition - capture d’écran](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-2.png)

### <a name="modify-role-with-json-template"></a>Modification d’un rôle avec le modèle JSON
À l’aide du modèle JSON de la précédente hello, vous pouvez facilement modifier une tooadd rôle personnalisé existant ou supprimer des Actions. Mettre à jour le modèle JSON hello et ajouter des actions de lecture hello de mise en réseau comme indiqué dans hello l’exemple suivant. définitions Hello répertoriées dans le modèle de hello ne sont pas appliqués de manière cumulative tooan définition existante, ce qui signifie que ce rôle hello s’affiche exactement comme vous le spécifiez dans le modèle de hello. Vous devez également le champ de code hello tooupdate avec l’ID de hello du rôle de hello. Si vous ne savez pas quelle est cette valeur, vous pouvez utiliser hello `Get-AzureRmRoleDefinition` tooget de l’applet de commande ces informations.

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

tooupdate hello rôle d’existant, exécutez hello suivant de commande PowerShell :
```
Set-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="delete-a-custom-role"></a>Supprimer un rôle personnalisé
toodelete un rôle personnalisé, utilisez hello `Remove-AzureRmRoleDefinition` commande.

exemple Hello supprime hello *opérateur de Machine virtuelle* rôle personnalisé.

```
Get-AzureRmRoleDefinition "Virtual Machine Operator"

Get-AzureRmRoleDefinition "Virtual Machine Operator" | Remove-AzureRmRoleDefinition
```

![RBAC PowerShell - Remove-AzureRmRoleDefinition - capture d’écran](./media/role-based-access-control-manage-access-powershell/4-remove-azurermroledefinition.png)

## <a name="list-custom-roles"></a>Répertorier les rôles personnalisés
rôles hello toolist qui sont disponibles pour l’assignation dans une étendue, utilisez hello `Get-AzureRmRoleDefinition` commande.

Bonjour à l’exemple suivant répertorie tous les rôles qui sont disponibles pour l’assignation dans l’abonnement de hello sélectionné.

```
Get-AzureRmRoleDefinition | FT Name, IsCustom
```

![RBAC PowerShell - Get-AzureRmRoleDefinition - capture d’écran](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition-1.png)

Dans l’exemple suivant de hello, hello *opérateur de Machine virtuelle* rôle personnalisé n’est pas disponible dans hello *Production4* abonnement, car cet abonnement n’est pas Bonjour  **AssignableScopes** du rôle de hello.

![RBAC PowerShell - Get-AzureRmRoleDefinition - capture d’écran](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition2.png)

## <a name="see-also"></a>Voir aussi
* [Utilisation d’Azure PowerShell avec Azure Resource Manager](../powershell-azure-resource-manager.md)
  [!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]

