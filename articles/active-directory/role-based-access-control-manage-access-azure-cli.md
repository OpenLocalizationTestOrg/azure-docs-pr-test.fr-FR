---
title: "Gestion du Contrôle d’accès en fonction du rôle avec l’interface de ligne de commande Azure | Microsoft Docs"
description: "Découvrez comment gérer le contrôle d'accès en fonction du rôle avec l'interface de ligne de commande Azure en répertoriant les rôles et les actions de rôle, et en affectant des rôles pour l'abonnement et l'application."
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
ms.openlocfilehash: ad644de6d23950e699d99042d27381336626caab
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-role-based-access-control-with-the-azure-command-line-interface"></a><span data-ttu-id="651ed-103">Gestion du contrôle d’accès en fonction du rôle avec l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="651ed-103">Manage Role-Based Access Control with the Azure command-line interface</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="651ed-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="651ed-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="651ed-105">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="651ed-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="651ed-106">API REST</span><span class="sxs-lookup"><span data-stu-id="651ed-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)


<span data-ttu-id="651ed-107">Le contrôle d’accès en fonction du rôle (RBAC) disponible dans le portail Azure et l’API Azure Resource Manager permet une gestion très fine de l’accès à votre abonnement et à vos ressources.</span><span class="sxs-lookup"><span data-stu-id="651ed-107">You can use Role-Based Access Control (RBAC) in the Azure portal and Azure Resource Manager API to manage access to your subscription and resources at a fine-grained level.</span></span> <span data-ttu-id="651ed-108">Cette fonctionnalité vous permet d’accorder l’accès aux utilisateurs, groupes et principaux du service Active Directory en leur affectant certains rôles avec une étendue spécifique.</span><span class="sxs-lookup"><span data-stu-id="651ed-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles to them at a particular scope.</span></span>

<span data-ttu-id="651ed-109">Pour pouvoir utiliser l’interface de ligne de commande (CLI) Azure afin de gérer le contrôle d’accès en fonction du rôle, vous devez disposer des composants suivants :</span><span class="sxs-lookup"><span data-stu-id="651ed-109">Before you can use the Azure command-line interface (CLI) to manage RBAC, you must have the following prerequisites:</span></span>

* <span data-ttu-id="651ed-110">Azure CLI version 0.8.8 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="651ed-110">Azure CLI version 0.8.8 or later.</span></span> <span data-ttu-id="651ed-111">Pour installer la dernière version et l’associer à votre abonnement Azure, consultez [Installer et configurer Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="651ed-111">To install the latest version and associate it with your Azure subscription, see [Install and Configure the Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="651ed-112">Azure Resource Manager dans l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="651ed-112">Azure Resource Manager in Azure CLI.</span></span> <span data-ttu-id="651ed-113">Pour plus d’informations, consultez [Utilisation de l’interface de ligne de commande Azure avec Azure Resource Manager](../xplat-cli-azure-resource-manager.md) .</span><span class="sxs-lookup"><span data-stu-id="651ed-113">Go to [Using the Azure CLI with the Resource Manager](../xplat-cli-azure-resource-manager.md) for more details.</span></span>

## <a name="list-roles"></a><span data-ttu-id="651ed-114">Répertorier les rôles</span><span class="sxs-lookup"><span data-stu-id="651ed-114">List roles</span></span>
### <a name="list-all-available-roles"></a><span data-ttu-id="651ed-115">Répertorier tous les rôles disponibles</span><span class="sxs-lookup"><span data-stu-id="651ed-115">List all available roles</span></span>
<span data-ttu-id="651ed-116">Pour répertorier tous les rôles, utilisez :</span><span class="sxs-lookup"><span data-stu-id="651ed-116">To list all available roles, use:</span></span>

        azure role list

<span data-ttu-id="651ed-117">L'exemple suivant affiche la liste de *tous les rôles disponibles*.</span><span class="sxs-lookup"><span data-stu-id="651ed-117">The following example shows the list of *all available roles*.</span></span>

```
azure role list --json | jq '.[] | {"roleName":.properties.roleName, "description":.properties.description}'
```

![Ligne de commande Azure RBAC - liste des rôles azure - capture d’écran](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-list.png)

### <a name="list-actions-of-a-role"></a><span data-ttu-id="651ed-119">Répertorier les actions d'un rôle</span><span class="sxs-lookup"><span data-stu-id="651ed-119">List actions of a role</span></span>
<span data-ttu-id="651ed-120">Pour répertorier les actions d'un rôle, utilisez :</span><span class="sxs-lookup"><span data-stu-id="651ed-120">To list the actions of a role, use:</span></span>

    azure role show "<role name>"

<span data-ttu-id="651ed-121">L’exemple suivant montre les actions des rôles *Collaborateur* et *Collaborateur de machine virtuelle*.</span><span class="sxs-lookup"><span data-stu-id="651ed-121">The following example shows the actions of the *Contributor* and *Virtual Machine Contributor* roles.</span></span>

```
azure role show "contributor" --json | jq '.[] | {"Actions":.properties.permissions[0].actions,"NotActions":properties.permissions[0].notActions}'

azure role show "virtual machine contributor" --json | jq '.[] | .properties.permissions[0].actions'
```

![Ligne de commande Azure RBAC - affichage des rôles azure - capture d’écran](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-show.png)

## <a name="list-access"></a><span data-ttu-id="651ed-123">Répertorier les accès</span><span class="sxs-lookup"><span data-stu-id="651ed-123">List access</span></span>
### <a name="list-role-assignments-effective-on-a-resource-group"></a><span data-ttu-id="651ed-124">Répertorier les affectations de rôles valables dans un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="651ed-124">List role assignments effective on a resource group</span></span>
<span data-ttu-id="651ed-125">Pour répertorier les attributions de rôles qui existent dans un groupe de ressources, utilisez :</span><span class="sxs-lookup"><span data-stu-id="651ed-125">To list the role assignments that exist in a resource group, use:</span></span>

    azure role assignment list --resource-group <resource group name>

<span data-ttu-id="651ed-126">L’exemple suivant illustre les attributions de rôle dans le groupe *pharma-sales-projecforcast* .</span><span class="sxs-lookup"><span data-stu-id="651ed-126">The following example shows the role assignments in the *pharma-sales-projecforcast* group.</span></span>

```
azure role assignment list --resource-group pharma-sales-projecforcast --json | jq '.[] | {"DisplayName":.properties.aADObject.displayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![Ligne de commande Azure RBAC - liste des affectations de rôle azure par groupe - capture d’écran](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-1.png)

### <a name="list-role-assignments-for-a-user"></a><span data-ttu-id="651ed-128">Répertorier les attributions de rôles pour un utilisateur</span><span class="sxs-lookup"><span data-stu-id="651ed-128">List role assignments for a user</span></span>
<span data-ttu-id="651ed-129">Pour répertorier les attributions de rôle pour un utilisateur spécifique et les attributions affectées aux groupes d’un utilisateur, utilisez :</span><span class="sxs-lookup"><span data-stu-id="651ed-129">To list the role assignments for a specific user and the assignments that are assigned to a user's groups, use:</span></span>

    azure role assignment list --signInName <user email>

<span data-ttu-id="651ed-130">Vous pouvez également afficher les affectations de rôles héritées de groupes en modifiant la commande :</span><span class="sxs-lookup"><span data-stu-id="651ed-130">You can also see role assignments that are inherited from groups by modifying the command:</span></span>

    azure role assignment list --expandPrincipalGroups --signInName <user email>

<span data-ttu-id="651ed-131">L’exemple suivant montre les attributions de rôles octroyées à l’utilisateur *sameert@aaddemo.com* .</span><span class="sxs-lookup"><span data-stu-id="651ed-131">The following example shows the role assignments that are granted to the *sameert@aaddemo.com* user.</span></span> <span data-ttu-id="651ed-132">Cela inclut les rôles attribués directement à l’utilisateur et ceux hérités des groupes.</span><span class="sxs-lookup"><span data-stu-id="651ed-132">This includes roles that are assigned directly to the user and roles that are inherited from groups.</span></span>

```
azure role assignment list --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'

azure role assignment list --expandPrincipalGroups --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![Ligne de commande Azure RBAC - liste des affectations de rôle azure par utilisateur - capture d’écran](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-2.png)

## <a name="grant-access"></a><span data-ttu-id="651ed-134">Accorder l'accès</span><span class="sxs-lookup"><span data-stu-id="651ed-134">Grant access</span></span>
<span data-ttu-id="651ed-135">Pour accorder l'accès après avoir identifié le rôle que vous souhaitez affecter, utilisez :</span><span class="sxs-lookup"><span data-stu-id="651ed-135">To grant access after you have identified the role that you want to assign, use:</span></span>

    azure role assignment create

### <a name="assign-a-role-to-group-at-the-subscription-scope"></a><span data-ttu-id="651ed-136">Affecter un rôle à un groupe pour l'abonnement</span><span class="sxs-lookup"><span data-stu-id="651ed-136">Assign a role to group at the subscription scope</span></span>
<span data-ttu-id="651ed-137">Pour affecter un rôle à un groupe pour l'abonnement, utilisez :</span><span class="sxs-lookup"><span data-stu-id="651ed-137">To assign a role to a group at the subscription scope, use:</span></span>

    azure role assignment create --objectId  <group object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

<span data-ttu-id="651ed-138">L’exemple suivant affecte le rôle *Lecteur* à *l’équipe de Christine Koch* pour *l’abonnement*.</span><span class="sxs-lookup"><span data-stu-id="651ed-138">The following example assigns the *Reader* role to *Christine Koch's Team* at the *subscription* scope.</span></span>

![Ligne de commande Azure RBAC - création des affectations de rôle azure par groupe - capture d’écran](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-1.png)

### <a name="assign-a-role-to-an-application-at-the-subscription-scope"></a><span data-ttu-id="651ed-140">Affectation d'un rôle à une application pour l'abonnement</span><span class="sxs-lookup"><span data-stu-id="651ed-140">Assign a role to an application at the subscription scope</span></span>
<span data-ttu-id="651ed-141">Pour affecter un rôle à une application pour l'abonnement, utilisez :</span><span class="sxs-lookup"><span data-stu-id="651ed-141">To assign a role to an application at the subscription scope, use:</span></span>

    azure role assignment create --objectId  <applications object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

<span data-ttu-id="651ed-142">L’exemple suivant affecte le rôle *Collaborateur* à une application *Azure AD* pour l’abonnement sélectionné.</span><span class="sxs-lookup"><span data-stu-id="651ed-142">The following example grants the *Contributor* role to an *Azure AD* application on the selected subscription.</span></span>

 ![Ligne de commande Azure RBAC - création de liste des affectations de rôle azure par utilisateur](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-2.png)

### <a name="assign-a-role-to-a-user-at-the-resource-group-scope"></a><span data-ttu-id="651ed-144">Affectation d'un rôle à un utilisateur pour le groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="651ed-144">Assign a role to a user at the resource group scope</span></span>
<span data-ttu-id="651ed-145">Pour affecter un rôle à un utilisateur pour le groupe de ressources, utilisez :</span><span class="sxs-lookup"><span data-stu-id="651ed-145">To assign a role to a user at the resource group scope, use:</span></span>

    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>

<span data-ttu-id="651ed-146">L’exemple suivant affecte le rôle *Collaborateur de machine virtuelle* à l’utilisateur *samert@aaddemo.com* au groupe de ressources *Pharma-Sales-ProjectForcast*.</span><span class="sxs-lookup"><span data-stu-id="651ed-146">The following example grants the *Virtual Machine Contributor* role to *samert@aaddemo.com* user at the *Pharma-Sales-ProjectForcast* resource group scope.</span></span>

![Ligne de commande Azure RBAC - création des affectations de rôle azure par utilisateur - capture d’écran](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-3.png)

### <a name="assign-a-role-to-a-group-at-the-resource-scope"></a><span data-ttu-id="651ed-148">Affectation d'un rôle à un utilisateur pour des ressources</span><span class="sxs-lookup"><span data-stu-id="651ed-148">Assign a role to a group at the resource scope</span></span>
<span data-ttu-id="651ed-149">Pour affecter un rôle à un groupe au niveau des ressources, utilisez :</span><span class="sxs-lookup"><span data-stu-id="651ed-149">To assign a role to a group at the resource scope, use:</span></span>

    azure role assignment create --objectId <group id> --role "<name of role>" --resource-name <resource group name> --resource-type <resource group type> --parent <resource group parent> --resource-group <resource group>

<span data-ttu-id="651ed-150">L’exemple suivant affecte le rôle *Collaborateur de machine virtuelle* à un groupe *Azure AD* dans un *sous-réseau*.</span><span class="sxs-lookup"><span data-stu-id="651ed-150">The following example grants the *Virtual Machine Contributor* role to an *Azure AD* group on a *subnet*.</span></span>

![Ligne de commande Azure RBAC - création des affectations de rôle azure par groupe - capture d’écran](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-4.png)

## <a name="remove-access"></a><span data-ttu-id="651ed-152">Suppression d'accès</span><span class="sxs-lookup"><span data-stu-id="651ed-152">Remove access</span></span>
<span data-ttu-id="651ed-153">Pour supprimer une affectation de rôle</span><span class="sxs-lookup"><span data-stu-id="651ed-153">To remove a role assignment, use:</span></span>

    azure role assignment delete --objectId <object id to from which to remove role> --roleName "<role name>"

<span data-ttu-id="651ed-154">L’exemple suivant supprime l’affectation du rôle *Collaborateur de machine virtuelle* de l’utilisateur *sammert@aaddemo.com* pour le groupe de ressources *Pharma-Sales-ProjectForcast*.</span><span class="sxs-lookup"><span data-stu-id="651ed-154">The following example removes the *Virtual Machine Contributor* role assignment from the *sammert@aaddemo.com* user on the *Pharma-Sales-ProjectForcast* resource group.</span></span>
<span data-ttu-id="651ed-155">L'exemple supprime ensuite l'affectation de rôle du groupe pour l'abonnement.</span><span class="sxs-lookup"><span data-stu-id="651ed-155">The example then removes the role assignment from a group on the subscription.</span></span>

![Ligne de commande Azure RBAC - suppression d’affectation de rôle - capture d’écran](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-assignment-delete.png)

## <a name="create-a-custom-role"></a><span data-ttu-id="651ed-157">Créer un rôle personnalisé</span><span class="sxs-lookup"><span data-stu-id="651ed-157">Create a custom role</span></span>
<span data-ttu-id="651ed-158">Pour créer un rôle personnalisé, utilisez :</span><span class="sxs-lookup"><span data-stu-id="651ed-158">To create a custom role, use:</span></span>

    azure role create --inputfile <file path>

<span data-ttu-id="651ed-159">L’exemple suivant crée un rôle personnalisé appelé *Opérateur de machine virtuelle*.</span><span class="sxs-lookup"><span data-stu-id="651ed-159">The following example creates a custom role called *Virtual Machine Operator*.</span></span> <span data-ttu-id="651ed-160">Ce rôle personnalisé accorde l’accès à toutes les opérations des fournisseurs de ressources *Microsoft.Compute*, *Microsoft.Storage* et *Microsoft.Network* ainsi que l’accès nécessaire pour démarrer, redémarrer et surveiller des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="651ed-160">This custom role grants access to all read operations of *Microsoft.Compute*, *Microsoft.Storage*, and *Microsoft.Network* resource providers and grants access to start, restart, and monitor virtual machines.</span></span> <span data-ttu-id="651ed-161">Ce rôle personnalisé peut être utilisé dans deux abonnements.</span><span class="sxs-lookup"><span data-stu-id="651ed-161">This custom role can be used in two subscriptions.</span></span> <span data-ttu-id="651ed-162">Cet exemple utilise un fichier JSON en tant qu’entrée.</span><span class="sxs-lookup"><span data-stu-id="651ed-162">This example uses a JSON file as an input.</span></span>

![JSON - définition de rôle personnalisé - capture d’écran](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-1.png)

![Ligne de commande Azure RBAC - création d’un rôle azure - capture d’écran](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-2.png)

## <a name="modify-a-custom-role"></a><span data-ttu-id="651ed-165">Modifier un rôle personnalisé</span><span class="sxs-lookup"><span data-stu-id="651ed-165">Modify a custom role</span></span>
<span data-ttu-id="651ed-166">Pour modifier un rôle personnalisé, utilisez d’abord la commande `azure role show` pour récupérer la définition de rôle.</span><span class="sxs-lookup"><span data-stu-id="651ed-166">To modify a custom role, first use the `azure role show` command to retrieve role definition.</span></span> <span data-ttu-id="651ed-167">Apportez ensuite les modifications souhaitées au fichier de définition de rôle.</span><span class="sxs-lookup"><span data-stu-id="651ed-167">Second, make the desired changes to the role definition file.</span></span> <span data-ttu-id="651ed-168">Enfin, utilisez `azure role set` pour enregistrer la définition de rôle modifiée.</span><span class="sxs-lookup"><span data-stu-id="651ed-168">Finally, use `azure role set` to save the modified role definition.</span></span>

    azure role set --inputfile <file path>

<span data-ttu-id="651ed-169">L’exemple suivant ajoute l’opération *Microsoft.Insights/diagnosticSettings/* à **Actions** et un abonnement Azure à **AssignableScopes** du rôle personnalisé Opérateur de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="651ed-169">The following example adds the *Microsoft.Insights/diagnosticSettings/* operation to the **Actions**, and an Azure subscription to the **AssignableScopes** of the Virtual Machine Operator custom role.</span></span>

![JSON - modifier la définition de rôle personnalisé - capture d’écran](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set-1.png)

![Ligne de commande Azure RBAC - définition d’un rôle azure - capture d’écran](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set2.png)

## <a name="delete-a-custom-role"></a><span data-ttu-id="651ed-172">Supprimer un rôle personnalisé</span><span class="sxs-lookup"><span data-stu-id="651ed-172">Delete a custom role</span></span>
<span data-ttu-id="651ed-173">Pour supprimer un rôle personnalisé, utilisez tout d’abord la commande `azure role show` afin de déterminer la propriété **ID** du rôle.</span><span class="sxs-lookup"><span data-stu-id="651ed-173">To delete a custom role, first use the `azure role show` command to determine the **ID** of the role.</span></span> <span data-ttu-id="651ed-174">Ensuite, utilisez la commande `azure role delete` pour supprimer le rôle en spécifiant la propriété **ID**.</span><span class="sxs-lookup"><span data-stu-id="651ed-174">Then, use the `azure role delete` command to delete the role by specifying the **ID**.</span></span>

<span data-ttu-id="651ed-175">L’exemple suivant supprime le rôle personnalisé *Opérateur de machine virtuelle* .</span><span class="sxs-lookup"><span data-stu-id="651ed-175">The following example removes the *Virtual Machine Operator* custom role.</span></span>

![Ligne de commande Azure RBAC - suppression d’un rôle azure - capture d’écran](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-delete.png)

## <a name="list-custom-roles"></a><span data-ttu-id="651ed-177">Répertorier les rôles personnalisés</span><span class="sxs-lookup"><span data-stu-id="651ed-177">List custom roles</span></span>
<span data-ttu-id="651ed-178">Pour répertorier les rôles pouvant être affectés dans une étendue, utilisez la commande `azure role list` .</span><span class="sxs-lookup"><span data-stu-id="651ed-178">To list the roles that are available for assignment at a scope, use the `azure role list` command.</span></span>

<span data-ttu-id="651ed-179">La commande suivante répertorie tous les rôles pouvant être affectés à l’abonnement sélectionné.</span><span class="sxs-lookup"><span data-stu-id="651ed-179">The following command lists all roles that are available for assignment in the selected subscription.</span></span>

```
azure role list --json | jq '.[] | {"name":.properties.roleName, type:.properties.type}'
```

![Ligne de commande Azure RBAC - liste des rôles azure - capture d’écran](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list1.png)

<span data-ttu-id="651ed-181">Dans l’exemple suivant, le rôle personnalisé *Opérateur de machine virtuelle* n’est pas disponible dans l’abonnement *Production4*, car cet abonnement ne figure pas dans l’élément **AssignableScopes** du rôle.</span><span class="sxs-lookup"><span data-stu-id="651ed-181">In the following example, the *Virtual Machine Operator* custom role isn’t available in the *Production4* subscription because that subscription isn’t in the **AssignableScopes** of the role.</span></span>

```
azure role list --json | jq '.[] | if .properties.type == "CustomRole" then .properties.roleName else empty end'
```

![Ligne de commande Azure RBAC - liste des rôles azure pour les rôles personnalisés - capture d’écran](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list2.png)

## <a name="next-steps"></a><span data-ttu-id="651ed-183">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="651ed-183">Next steps</span></span>
[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]

