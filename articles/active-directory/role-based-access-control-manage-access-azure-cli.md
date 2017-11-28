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
# <a name="manage-role-based-access-control-with-hello-azure-command-line-interface"></a><span data-ttu-id="6e2ac-103">Gérer le contrôle d’accès basée sur les rôles avec hello interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="6e2ac-103">Manage Role-Based Access Control with hello Azure command-line interface</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6e2ac-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6e2ac-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="6e2ac-105">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="6e2ac-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="6e2ac-106">API REST</span><span class="sxs-lookup"><span data-stu-id="6e2ac-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)


<span data-ttu-id="6e2ac-107">Vous pouvez utiliser le contrôle d’accès en fonction du rôle (RBAC) dans hello portail Azure et abonnement de tooyour accès API Azure Resource Manager toomanage et ressources à un niveau de granularité fin.</span><span class="sxs-lookup"><span data-stu-id="6e2ac-107">You can use Role-Based Access Control (RBAC) in hello Azure portal and Azure Resource Manager API toomanage access tooyour subscription and resources at a fine-grained level.</span></span> <span data-ttu-id="6e2ac-108">Avec cette fonctionnalité, vous pouvez accorder l’accès pour les utilisateurs, groupes ou principaux du service Active Directory en attribuant certains toothem de rôles à une portée particulière.</span><span class="sxs-lookup"><span data-stu-id="6e2ac-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles toothem at a particular scope.</span></span>

<span data-ttu-id="6e2ac-109">Avant de pouvoir utiliser hello Azure interface de ligne de commande (CLI) toomanage RBAC, vous devez disposer de hello suivant des conditions préalables :</span><span class="sxs-lookup"><span data-stu-id="6e2ac-109">Before you can use hello Azure command-line interface (CLI) toomanage RBAC, you must have hello following prerequisites:</span></span>

* <span data-ttu-id="6e2ac-110">Azure CLI version 0.8.8 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="6e2ac-110">Azure CLI version 0.8.8 or later.</span></span> <span data-ttu-id="6e2ac-111">version la plus récente tooinstall hello et à associer à votre abonnement Azure, consultez [installer et configurer hello CLI d’Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="6e2ac-111">tooinstall hello latest version and associate it with your Azure subscription, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="6e2ac-112">Azure Resource Manager dans l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="6e2ac-112">Azure Resource Manager in Azure CLI.</span></span> <span data-ttu-id="6e2ac-113">Accédez trop[Using hello CLI d’Azure avec hello Gestionnaire de ressources](../xplat-cli-azure-resource-manager.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="6e2ac-113">Go too[Using hello Azure CLI with hello Resource Manager](../xplat-cli-azure-resource-manager.md) for more details.</span></span>

## <a name="list-roles"></a><span data-ttu-id="6e2ac-114">Répertorier les rôles</span><span class="sxs-lookup"><span data-stu-id="6e2ac-114">List roles</span></span>
### <a name="list-all-available-roles"></a><span data-ttu-id="6e2ac-115">Répertorier tous les rôles disponibles</span><span class="sxs-lookup"><span data-stu-id="6e2ac-115">List all available roles</span></span>
<span data-ttu-id="6e2ac-116">toolist tous les rôles disponibles, utilisez :</span><span class="sxs-lookup"><span data-stu-id="6e2ac-116">toolist all available roles, use:</span></span>

        azure role list

<span data-ttu-id="6e2ac-117">Hello suivant montre la liste des hello *tous les rôles disponibles*.</span><span class="sxs-lookup"><span data-stu-id="6e2ac-117">hello following example shows hello list of *all available roles*.</span></span>

```
azure role list --json | jq '.[] | {"roleName":.properties.roleName, "description":.properties.description}'
```

![Ligne de commande Azure RBAC - liste des rôles azure - capture d’écran](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-list.png)

### <a name="list-actions-of-a-role"></a><span data-ttu-id="6e2ac-119">Répertorier les actions d'un rôle</span><span class="sxs-lookup"><span data-stu-id="6e2ac-119">List actions of a role</span></span>
<span data-ttu-id="6e2ac-120">actions de hello toolist d’un rôle, utilisez :</span><span class="sxs-lookup"><span data-stu-id="6e2ac-120">toolist hello actions of a role, use:</span></span>

    azure role show "<role name>"

<span data-ttu-id="6e2ac-121">Hello suivant montre les actions hello Hello *collaborateur* et *contributeur de l’ordinateur virtuel* rôles.</span><span class="sxs-lookup"><span data-stu-id="6e2ac-121">hello following example shows hello actions of hello *Contributor* and *Virtual Machine Contributor* roles.</span></span>

```
azure role show "contributor" --json | jq '.[] | {"Actions":.properties.permissions[0].actions,"NotActions":properties.permissions[0].notActions}'

azure role show "virtual machine contributor" --json | jq '.[] | .properties.permissions[0].actions'
```

![Ligne de commande Azure RBAC - affichage des rôles azure - capture d’écran](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-show.png)

## <a name="list-access"></a><span data-ttu-id="6e2ac-123">Répertorier les accès</span><span class="sxs-lookup"><span data-stu-id="6e2ac-123">List access</span></span>
### <a name="list-role-assignments-effective-on-a-resource-group"></a><span data-ttu-id="6e2ac-124">Répertorier les affectations de rôles valables dans un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="6e2ac-124">List role assignments effective on a resource group</span></span>
<span data-ttu-id="6e2ac-125">toolist hello attributions de rôles qui existent dans un groupe de ressources, utilisez :</span><span class="sxs-lookup"><span data-stu-id="6e2ac-125">toolist hello role assignments that exist in a resource group, use:</span></span>

    azure role assignment list --resource-group <resource group name>

<span data-ttu-id="6e2ac-126">Hello suivant montre les attributions de rôles hello Bonjour *PHARMACEUTIQUE-ventes-projecforcast* groupe.</span><span class="sxs-lookup"><span data-stu-id="6e2ac-126">hello following example shows hello role assignments in hello *pharma-sales-projecforcast* group.</span></span>

```
azure role assignment list --resource-group pharma-sales-projecforcast --json | jq '.[] | {"DisplayName":.properties.aADObject.displayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![Ligne de commande Azure RBAC - liste des affectations de rôle azure par groupe - capture d’écran](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-1.png)

### <a name="list-role-assignments-for-a-user"></a><span data-ttu-id="6e2ac-128">Répertorier les attributions de rôles pour un utilisateur</span><span class="sxs-lookup"><span data-stu-id="6e2ac-128">List role assignments for a user</span></span>
<span data-ttu-id="6e2ac-129">affectations de rôle toolist hello pour un utilisateur spécifique et hello assignés tooa groupes de l’utilisateur, utilisez :</span><span class="sxs-lookup"><span data-stu-id="6e2ac-129">toolist hello role assignments for a specific user and hello assignments that are assigned tooa user's groups, use:</span></span>

    azure role assignment list --signInName <user email>

<span data-ttu-id="6e2ac-130">Vous pouvez également afficher les attributions de rôles qui sont héritées de groupes en modifiant la commande hello :</span><span class="sxs-lookup"><span data-stu-id="6e2ac-130">You can also see role assignments that are inherited from groups by modifying hello command:</span></span>

    azure role assignment list --expandPrincipalGroups --signInName <user email>

<span data-ttu-id="6e2ac-131">Hello suivant montre les attributions de rôles hello accordées toohello  *sameert@aaddemo.com*  utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6e2ac-131">hello following example shows hello role assignments that are granted toohello *sameert@aaddemo.com* user.</span></span> <span data-ttu-id="6e2ac-132">Cela inclut les rôles qui sont attribués directement toohello utilisateur et les rôles qui sont héritées de groupes.</span><span class="sxs-lookup"><span data-stu-id="6e2ac-132">This includes roles that are assigned directly toohello user and roles that are inherited from groups.</span></span>

```
azure role assignment list --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'

azure role assignment list --expandPrincipalGroups --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![Ligne de commande Azure RBAC - liste des affectations de rôle azure par utilisateur - capture d’écran](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-2.png)

## <a name="grant-access"></a><span data-ttu-id="6e2ac-134">Accorder l'accès</span><span class="sxs-lookup"><span data-stu-id="6e2ac-134">Grant access</span></span>
<span data-ttu-id="6e2ac-135">toogrant accès une fois que vous avez identifié le rôle hello que vous souhaitez tooassign, utilisez :</span><span class="sxs-lookup"><span data-stu-id="6e2ac-135">toogrant access after you have identified hello role that you want tooassign, use:</span></span>

    azure role assignment create

### <a name="assign-a-role-toogroup-at-hello-subscription-scope"></a><span data-ttu-id="6e2ac-136">Affecter un toogroup de rôle au niveau de l’étendue de l’abonnement hello</span><span class="sxs-lookup"><span data-stu-id="6e2ac-136">Assign a role toogroup at hello subscription scope</span></span>
<span data-ttu-id="6e2ac-137">tooassign un groupe de tooa des rôles au niveau de l’étendue de l’abonnement hello, utilisez :</span><span class="sxs-lookup"><span data-stu-id="6e2ac-137">tooassign a role tooa group at hello subscription scope, use:</span></span>

    azure role assignment create --objectId  <group object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

<span data-ttu-id="6e2ac-138">exemple Hello affecte hello *lecteur* rôle trop*équipe de Christine Koch* à hello *abonnement* étendue.</span><span class="sxs-lookup"><span data-stu-id="6e2ac-138">hello following example assigns hello *Reader* role too*Christine Koch's Team* at hello *subscription* scope.</span></span>

![Ligne de commande Azure RBAC - création des affectations de rôle azure par groupe - capture d’écran](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-1.png)

### <a name="assign-a-role-tooan-application-at-hello-subscription-scope"></a><span data-ttu-id="6e2ac-140">Affecter une application tooan de rôle au niveau de l’étendue de l’abonnement hello</span><span class="sxs-lookup"><span data-stu-id="6e2ac-140">Assign a role tooan application at hello subscription scope</span></span>
<span data-ttu-id="6e2ac-141">tooassign une application tooan de rôle au niveau de l’étendue de l’abonnement hello, utilisez :</span><span class="sxs-lookup"><span data-stu-id="6e2ac-141">tooassign a role tooan application at hello subscription scope, use:</span></span>

    azure role assignment create --objectId  <applications object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

<span data-ttu-id="6e2ac-142">Hello exemple suivant accorde hello *collaborateur* rôle tooan *AD Azure* application hello sélectionné l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="6e2ac-142">hello following example grants hello *Contributor* role tooan *Azure AD* application on hello selected subscription.</span></span>

 ![Ligne de commande Azure RBAC - création de liste des affectations de rôle azure par utilisateur](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-2.png)

### <a name="assign-a-role-tooa-user-at-hello-resource-group-scope"></a><span data-ttu-id="6e2ac-144">Affecter un utilisateur tooa de rôle au niveau de l’étendue de groupe de ressources hello</span><span class="sxs-lookup"><span data-stu-id="6e2ac-144">Assign a role tooa user at hello resource group scope</span></span>
<span data-ttu-id="6e2ac-145">tooassign un utilisateur tooa de rôle au niveau de l’étendue de groupe de ressources hello, utilisez :</span><span class="sxs-lookup"><span data-stu-id="6e2ac-145">tooassign a role tooa user at hello resource group scope, use:</span></span>

    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>

<span data-ttu-id="6e2ac-146">Hello exemple suivant accorde hello *contributeur de l’ordinateur virtuel* rôle trop *samert@aaddemo.com*  utilisateur hello *PHARMACEUTIQUE-ventes-ProjectForcast* étendue de groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="6e2ac-146">hello following example grants hello *Virtual Machine Contributor* role too*samert@aaddemo.com* user at hello *Pharma-Sales-ProjectForcast* resource group scope.</span></span>

![Ligne de commande Azure RBAC - création des affectations de rôle azure par utilisateur - capture d’écran](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-3.png)

### <a name="assign-a-role-tooa-group-at-hello-resource-scope"></a><span data-ttu-id="6e2ac-148">Affecter un groupe de tooa de rôle au niveau de la portée de la ressource hello</span><span class="sxs-lookup"><span data-stu-id="6e2ac-148">Assign a role tooa group at hello resource scope</span></span>
<span data-ttu-id="6e2ac-149">tooassign un groupe de tooa des rôles au niveau de la portée de la ressource hello, utilisez :</span><span class="sxs-lookup"><span data-stu-id="6e2ac-149">tooassign a role tooa group at hello resource scope, use:</span></span>

    azure role assignment create --objectId <group id> --role "<name of role>" --resource-name <resource group name> --resource-type <resource group type> --parent <resource group parent> --resource-group <resource group>

<span data-ttu-id="6e2ac-150">Hello exemple suivant accorde hello *contributeur de l’ordinateur virtuel* rôle tooan *Azure AD* groupe sur un *sous-réseau*.</span><span class="sxs-lookup"><span data-stu-id="6e2ac-150">hello following example grants hello *Virtual Machine Contributor* role tooan *Azure AD* group on a *subnet*.</span></span>

![Ligne de commande Azure RBAC - création des affectations de rôle azure par groupe - capture d’écran](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-4.png)

## <a name="remove-access"></a><span data-ttu-id="6e2ac-152">Suppression d'accès</span><span class="sxs-lookup"><span data-stu-id="6e2ac-152">Remove access</span></span>
<span data-ttu-id="6e2ac-153">tooremove une attribution de rôle, utilisez :</span><span class="sxs-lookup"><span data-stu-id="6e2ac-153">tooremove a role assignment, use:</span></span>

    azure role assignment delete --objectId <object id toofrom which tooremove role> --roleName "<role name>"

<span data-ttu-id="6e2ac-154">exemple Hello supprime hello *contributeur de l’ordinateur virtuel* attribution de rôle à partir de hello  *sammert@aaddemo.com*  utilisateur sur hello *PHARMACEUTIQUE-ventes-ProjectForcast* groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="6e2ac-154">hello following example removes hello *Virtual Machine Contributor* role assignment from hello *sammert@aaddemo.com* user on hello *Pharma-Sales-ProjectForcast* resource group.</span></span>
<span data-ttu-id="6e2ac-155">exemple de Hello supprime puis attribution de rôle hello d’un groupe sur l’abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="6e2ac-155">hello example then removes hello role assignment from a group on hello subscription.</span></span>

![Ligne de commande Azure RBAC - suppression d’affectation de rôle - capture d’écran](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-assignment-delete.png)

## <a name="create-a-custom-role"></a><span data-ttu-id="6e2ac-157">Créer un rôle personnalisé</span><span class="sxs-lookup"><span data-stu-id="6e2ac-157">Create a custom role</span></span>
<span data-ttu-id="6e2ac-158">toocreate un rôle personnalisé, utilisez :</span><span class="sxs-lookup"><span data-stu-id="6e2ac-158">toocreate a custom role, use:</span></span>

    azure role create --inputfile <file path>

<span data-ttu-id="6e2ac-159">Hello exemple suivant crée un rôle personnalisé appelé *opérateur de l’ordinateur virtuel*.</span><span class="sxs-lookup"><span data-stu-id="6e2ac-159">hello following example creates a custom role called *Virtual Machine Operator*.</span></span> <span data-ttu-id="6e2ac-160">Ce rôle personnalisé accorde l’accès tooall lire des opérations de *Microsoft.Compute*, *Microsoft.Storage*, et *Microsoft.Network* fournisseurs et accorde l’accès aux ressources de toostart, redémarrer et analyser des ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="6e2ac-160">This custom role grants access tooall read operations of *Microsoft.Compute*, *Microsoft.Storage*, and *Microsoft.Network* resource providers and grants access toostart, restart, and monitor virtual machines.</span></span> <span data-ttu-id="6e2ac-161">Ce rôle personnalisé peut être utilisé dans deux abonnements.</span><span class="sxs-lookup"><span data-stu-id="6e2ac-161">This custom role can be used in two subscriptions.</span></span> <span data-ttu-id="6e2ac-162">Cet exemple utilise un fichier JSON en tant qu’entrée.</span><span class="sxs-lookup"><span data-stu-id="6e2ac-162">This example uses a JSON file as an input.</span></span>

![JSON - définition de rôle personnalisé - capture d’écran](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-1.png)

![Ligne de commande Azure RBAC - création d’un rôle azure - capture d’écran](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-2.png)

## <a name="modify-a-custom-role"></a><span data-ttu-id="6e2ac-165">Modifier un rôle personnalisé</span><span class="sxs-lookup"><span data-stu-id="6e2ac-165">Modify a custom role</span></span>
<span data-ttu-id="6e2ac-166">toomodify un rôle personnalisé, utilisez d’abord hello `azure role show` définition de rôle tooretrieve des commandes.</span><span class="sxs-lookup"><span data-stu-id="6e2ac-166">toomodify a custom role, first use hello `azure role show` command tooretrieve role definition.</span></span> <span data-ttu-id="6e2ac-167">En second lieu, assurez-vous de fichier de définition de rôle toohello hello modifications souhaitées.</span><span class="sxs-lookup"><span data-stu-id="6e2ac-167">Second, make hello desired changes toohello role definition file.</span></span> <span data-ttu-id="6e2ac-168">Enfin, utilisez `azure role set` toosave hello modifié la définition de rôle.</span><span class="sxs-lookup"><span data-stu-id="6e2ac-168">Finally, use `azure role set` toosave hello modified role definition.</span></span>

    azure role set --inputfile <file path>

<span data-ttu-id="6e2ac-169">exemple Hello ajoute hello *Microsoft.Insights/diagnosticSettings/* opération toohello **Actions**et un abonnement Azure de toohello **AssignableScopes**du rôle de hello opérateur de Machine virtuelle personnalisée.</span><span class="sxs-lookup"><span data-stu-id="6e2ac-169">hello following example adds hello *Microsoft.Insights/diagnosticSettings/* operation toohello **Actions**, and an Azure subscription toohello **AssignableScopes** of hello Virtual Machine Operator custom role.</span></span>

![JSON - modifier la définition de rôle personnalisé - capture d’écran](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set-1.png)

![Ligne de commande Azure RBAC - définition d’un rôle azure - capture d’écran](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set2.png)

## <a name="delete-a-custom-role"></a><span data-ttu-id="6e2ac-172">Supprimer un rôle personnalisé</span><span class="sxs-lookup"><span data-stu-id="6e2ac-172">Delete a custom role</span></span>
<span data-ttu-id="6e2ac-173">toodelete un rôle personnalisé, utilisez d’abord hello `azure role show` commande toodetermine hello **ID** du rôle de hello.</span><span class="sxs-lookup"><span data-stu-id="6e2ac-173">toodelete a custom role, first use hello `azure role show` command toodetermine hello **ID** of hello role.</span></span> <span data-ttu-id="6e2ac-174">Ensuite, utilisez hello `azure role delete` rôle de hello toodelete de commande en spécifiant hello **ID**.</span><span class="sxs-lookup"><span data-stu-id="6e2ac-174">Then, use hello `azure role delete` command toodelete hello role by specifying hello **ID**.</span></span>

<span data-ttu-id="6e2ac-175">exemple Hello supprime hello *opérateur de Machine virtuelle* rôle personnalisé.</span><span class="sxs-lookup"><span data-stu-id="6e2ac-175">hello following example removes hello *Virtual Machine Operator* custom role.</span></span>

![Ligne de commande Azure RBAC - suppression d’un rôle azure - capture d’écran](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-delete.png)

## <a name="list-custom-roles"></a><span data-ttu-id="6e2ac-177">Répertorier les rôles personnalisés</span><span class="sxs-lookup"><span data-stu-id="6e2ac-177">List custom roles</span></span>
<span data-ttu-id="6e2ac-178">rôles hello toolist qui sont disponibles pour l’assignation dans une étendue, utilisez hello `azure role list` commande.</span><span class="sxs-lookup"><span data-stu-id="6e2ac-178">toolist hello roles that are available for assignment at a scope, use hello `azure role list` command.</span></span>

<span data-ttu-id="6e2ac-179">Hello commande suivante répertorie tous les rôles qui sont disponibles pour l’assignation dans l’abonnement de hello sélectionné.</span><span class="sxs-lookup"><span data-stu-id="6e2ac-179">hello following command lists all roles that are available for assignment in hello selected subscription.</span></span>

```
azure role list --json | jq '.[] | {"name":.properties.roleName, type:.properties.type}'
```

![Ligne de commande Azure RBAC - liste des rôles azure - capture d’écran](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list1.png)

<span data-ttu-id="6e2ac-181">Dans l’exemple suivant de hello, hello *opérateur de Machine virtuelle* rôle personnalisé n’est pas disponible dans hello *Production4* abonnement, car cet abonnement n’est pas Bonjour  **AssignableScopes** du rôle de hello.</span><span class="sxs-lookup"><span data-stu-id="6e2ac-181">In hello following example, hello *Virtual Machine Operator* custom role isn’t available in hello *Production4* subscription because that subscription isn’t in hello **AssignableScopes** of hello role.</span></span>

```
azure role list --json | jq '.[] | if .properties.type == "CustomRole" then .properties.roleName else empty end'
```

![Ligne de commande Azure RBAC - liste des rôles azure pour les rôles personnalisés - capture d’écran](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list2.png)

## <a name="next-steps"></a><span data-ttu-id="6e2ac-183">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6e2ac-183">Next steps</span></span>
[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]

