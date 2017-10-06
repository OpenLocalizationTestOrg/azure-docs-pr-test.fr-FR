---
title: "aaaManage Role-Based contrôle d’accès (RBAC) avec CLI d’Azure | Documents Microsoft"
description: "Découvrez comment toomanage Role-Based contrôle d’accès (RBAC) avec hello Azure de ligne de commande de l’interface à la liste de rôles et de rôle actions et en attribuant des rôles toohello des étendues d’abonnement et d’application."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 3483ee01-8177-49e7-b337-4d5cb14f5e32
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: 438418e5f6ee9b98908c9c264d516eb722a4e26d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-role-based-access-control-with-hello-azure-command-line-interface"></a>Gérer le contrôle d’accès basée sur les rôles avec hello interface de ligne de commande Azure
> [!div class="op_single_selector"]
> * [PowerShell](role-based-access-control-manage-access-powershell.md)
> * [Interface de ligne de commande Azure](role-based-access-control-manage-access-azure-cli.md)
> * [API REST](role-based-access-control-manage-access-rest.md)


Vous pouvez utiliser le contrôle d’accès en fonction du rôle (RBAC) dans hello portail Azure et abonnement de tooyour accès API Azure Resource Manager toomanage et ressources à un niveau de granularité fin. Avec cette fonctionnalité, vous pouvez accorder l’accès pour les utilisateurs, groupes ou principaux du service Active Directory en attribuant certains toothem de rôles à une portée particulière.

Avant de pouvoir utiliser hello Azure interface de ligne de commande (CLI) toomanage RBAC, vous devez disposer de hello suivant des conditions préalables :

* Azure CLI version 0.8.8 ou ultérieure. version la plus récente tooinstall hello et à associer à votre abonnement Azure, consultez [installer et configurer hello CLI d’Azure](../cli-install-nodejs.md).
* Azure Resource Manager dans l’interface de ligne de commande Azure. Accédez trop[Using hello CLI d’Azure avec hello Gestionnaire de ressources](../xplat-cli-azure-resource-manager.md) pour plus d’informations.

## <a name="list-roles"></a>Répertorier les rôles
### <a name="list-all-available-roles"></a>Répertorier tous les rôles disponibles
toolist tous les rôles disponibles, utilisez :

        azure role list

Hello suivant montre la liste des hello *tous les rôles disponibles*.

```
azure role list --json | jq '.[] | {"roleName":.properties.roleName, "description":.properties.description}'
```

![Ligne de commande Azure RBAC - liste des rôles azure - capture d’écran](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-list.png)

### <a name="list-actions-of-a-role"></a>Répertorier les actions d'un rôle
actions de hello toolist d’un rôle, utilisez :

    azure role show "<role name>"

Hello suivant montre les actions hello Hello *collaborateur* et *contributeur de l’ordinateur virtuel* rôles.

```
azure role show "contributor" --json | jq '.[] | {"Actions":.properties.permissions[0].actions,"NotActions":properties.permissions[0].notActions}'

azure role show "virtual machine contributor" --json | jq '.[] | .properties.permissions[0].actions'
```

![Ligne de commande Azure RBAC - affichage des rôles azure - capture d’écran](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-show.png)

## <a name="list-access"></a>Répertorier les accès
### <a name="list-role-assignments-effective-on-a-resource-group"></a>Répertorier les affectations de rôles valables dans un groupe de ressources
toolist hello attributions de rôles qui existent dans un groupe de ressources, utilisez :

    azure role assignment list --resource-group <resource group name>

Hello suivant montre les attributions de rôles hello Bonjour *PHARMACEUTIQUE-ventes-projecforcast* groupe.

```
azure role assignment list --resource-group pharma-sales-projecforcast --json | jq '.[] | {"DisplayName":.properties.aADObject.displayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![Ligne de commande Azure RBAC - liste des affectations de rôle azure par groupe - capture d’écran](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-1.png)

### <a name="list-role-assignments-for-a-user"></a>Répertorier les attributions de rôles pour un utilisateur
affectations de rôle toolist hello pour un utilisateur spécifique et hello assignés tooa groupes de l’utilisateur, utilisez :

    azure role assignment list --signInName <user email>

Vous pouvez également afficher les attributions de rôles qui sont héritées de groupes en modifiant la commande hello :

    azure role assignment list --expandPrincipalGroups --signInName <user email>

Hello suivant montre les attributions de rôles hello accordées toohello  *sameert@aaddemo.com*  utilisateur. Cela inclut les rôles qui sont attribués directement toohello utilisateur et les rôles qui sont héritées de groupes.

```
azure role assignment list --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'

azure role assignment list --expandPrincipalGroups --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![Ligne de commande Azure RBAC - liste des affectations de rôle azure par utilisateur - capture d’écran](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-2.png)

## <a name="grant-access"></a>Accorder l'accès
toogrant accès une fois que vous avez identifié le rôle hello que vous souhaitez tooassign, utilisez :

    azure role assignment create

### <a name="assign-a-role-toogroup-at-hello-subscription-scope"></a>Affecter un toogroup de rôle au niveau de l’étendue de l’abonnement hello
tooassign un groupe de tooa des rôles au niveau de l’étendue de l’abonnement hello, utilisez :

    azure role assignment create --objectId  <group object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

exemple Hello affecte hello *lecteur* rôle trop*équipe de Christine Koch* à hello *abonnement* étendue.

![Ligne de commande Azure RBAC - création des affectations de rôle azure par groupe - capture d’écran](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-1.png)

### <a name="assign-a-role-tooan-application-at-hello-subscription-scope"></a>Affecter une application tooan de rôle au niveau de l’étendue de l’abonnement hello
tooassign une application tooan de rôle au niveau de l’étendue de l’abonnement hello, utilisez :

    azure role assignment create --objectId  <applications object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

Hello exemple suivant accorde hello *collaborateur* rôle tooan *AD Azure* application hello sélectionné l’abonnement.

 ![Ligne de commande Azure RBAC - création de liste des affectations de rôle azure par utilisateur](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-2.png)

### <a name="assign-a-role-tooa-user-at-hello-resource-group-scope"></a>Affecter un utilisateur tooa de rôle au niveau de l’étendue de groupe de ressources hello
tooassign un utilisateur tooa de rôle au niveau de l’étendue de groupe de ressources hello, utilisez :

    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>

Hello exemple suivant accorde hello *contributeur de l’ordinateur virtuel* rôle trop *samert@aaddemo.com*  utilisateur hello *PHARMACEUTIQUE-ventes-ProjectForcast* étendue de groupe de ressources.

![Ligne de commande Azure RBAC - création des affectations de rôle azure par utilisateur - capture d’écran](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-3.png)

### <a name="assign-a-role-tooa-group-at-hello-resource-scope"></a>Affecter un groupe de tooa de rôle au niveau de la portée de la ressource hello
tooassign un groupe de tooa des rôles au niveau de la portée de la ressource hello, utilisez :

    azure role assignment create --objectId <group id> --role "<name of role>" --resource-name <resource group name> --resource-type <resource group type> --parent <resource group parent> --resource-group <resource group>

Hello exemple suivant accorde hello *contributeur de l’ordinateur virtuel* rôle tooan *Azure AD* groupe sur un *sous-réseau*.

![Ligne de commande Azure RBAC - création des affectations de rôle azure par groupe - capture d’écran](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-4.png)

## <a name="remove-access"></a>Suppression d'accès
tooremove une attribution de rôle, utilisez :

    azure role assignment delete --objectId <object id toofrom which tooremove role> --roleName "<role name>"

exemple Hello supprime hello *contributeur de l’ordinateur virtuel* attribution de rôle à partir de hello  *sammert@aaddemo.com*  utilisateur sur hello *PHARMACEUTIQUE-ventes-ProjectForcast* groupe de ressources.
exemple de Hello supprime puis attribution de rôle hello d’un groupe sur l’abonnement de hello.

![Ligne de commande Azure RBAC - suppression d’affectation de rôle - capture d’écran](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-assignment-delete.png)

## <a name="create-a-custom-role"></a>Créer un rôle personnalisé
toocreate un rôle personnalisé, utilisez :

    azure role create --inputfile <file path>

Hello exemple suivant crée un rôle personnalisé appelé *opérateur de l’ordinateur virtuel*. Ce rôle personnalisé accorde l’accès tooall lire des opérations de *Microsoft.Compute*, *Microsoft.Storage*, et *Microsoft.Network* fournisseurs et accorde l’accès aux ressources de toostart, redémarrer et analyser des ordinateurs virtuels. Ce rôle personnalisé peut être utilisé dans deux abonnements. Cet exemple utilise un fichier JSON en tant qu’entrée.

![JSON - définition de rôle personnalisé - capture d’écran](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-1.png)

![Ligne de commande Azure RBAC - création d’un rôle azure - capture d’écran](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-2.png)

## <a name="modify-a-custom-role"></a>Modifier un rôle personnalisé
toomodify un rôle personnalisé, utilisez d’abord hello `azure role show` définition de rôle tooretrieve des commandes. En second lieu, assurez-vous de fichier de définition de rôle toohello hello modifications souhaitées. Enfin, utilisez `azure role set` toosave hello modifié la définition de rôle.

    azure role set --inputfile <file path>

exemple Hello ajoute hello *Microsoft.Insights/diagnosticSettings/* opération toohello **Actions**et un abonnement Azure de toohello **AssignableScopes**du rôle de hello opérateur de Machine virtuelle personnalisée.

![JSON - modifier la définition de rôle personnalisé - capture d’écran](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set-1.png)

![Ligne de commande Azure RBAC - définition d’un rôle azure - capture d’écran](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set2.png)

## <a name="delete-a-custom-role"></a>Supprimer un rôle personnalisé
toodelete un rôle personnalisé, utilisez d’abord hello `azure role show` commande toodetermine hello **ID** du rôle de hello. Ensuite, utilisez hello `azure role delete` rôle de hello toodelete de commande en spécifiant hello **ID**.

exemple Hello supprime hello *opérateur de Machine virtuelle* rôle personnalisé.

![Ligne de commande Azure RBAC - suppression d’un rôle azure - capture d’écran](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-delete.png)

## <a name="list-custom-roles"></a>Répertorier les rôles personnalisés
rôles hello toolist qui sont disponibles pour l’assignation dans une étendue, utilisez hello `azure role list` commande.

Hello commande suivante répertorie tous les rôles qui sont disponibles pour l’assignation dans l’abonnement de hello sélectionné.

```
azure role list --json | jq '.[] | {"name":.properties.roleName, type:.properties.type}'
```

![Ligne de commande Azure RBAC - liste des rôles azure - capture d’écran](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list1.png)

Dans l’exemple suivant de hello, hello *opérateur de Machine virtuelle* rôle personnalisé n’est pas disponible dans hello *Production4* abonnement, car cet abonnement n’est pas Bonjour  **AssignableScopes** du rôle de hello.

```
azure role list --json | jq '.[] | if .properties.type == "CustomRole" then .properties.roleName else empty end'
```

![Ligne de commande Azure RBAC - liste des rôles azure pour les rôles personnalisés - capture d’écran](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list2.png)

## <a name="next-steps"></a>Étapes suivantes
[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]

