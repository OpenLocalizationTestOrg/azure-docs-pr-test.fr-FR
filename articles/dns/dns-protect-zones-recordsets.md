---
title: Protection des enregistrements et zones DNS | Microsoft Docs
description: "Comment protéger les jeux d’enregistrements et de zones DNS dans le DNS Microsoft Azure."
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: 190e69eb-e820-4fc8-8e9a-baaf0b3fb74a
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/20/2016
ms.author: jonatul
ms.openlocfilehash: 0b7040d6273b3a6b85cd55850d596807226b87fc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-protect-dns-zones-and-records"></a><span data-ttu-id="71264-103">Comment protéger les enregistrements et zones DNS</span><span class="sxs-lookup"><span data-stu-id="71264-103">How to protect DNS zones and records</span></span>

<span data-ttu-id="71264-104">Les enregistrements et zones DNS sont des ressources critiques.</span><span class="sxs-lookup"><span data-stu-id="71264-104">DNS zones and records are critical resources.</span></span> <span data-ttu-id="71264-105">La suppression d’une zone DNS, voire d’un seul enregistrement DNS, peut entraîner une interruption de service totale.</span><span class="sxs-lookup"><span data-stu-id="71264-105">Deleting a DNS zone or even just a single DNS record can result in a total service outage.</span></span>  <span data-ttu-id="71264-106">Il est donc important que les zones et enregistrements DNS critiques soient protégés contre toute modification non autorisée ou accidentelle.</span><span class="sxs-lookup"><span data-stu-id="71264-106">It is therefore important that critical DNS zones and records are protected against unauthorized or accidental changes.</span></span>

<span data-ttu-id="71264-107">Cet article explique comment le DNS Azure permet de protéger vos enregistrements et zones DNS contre de telles modifications.</span><span class="sxs-lookup"><span data-stu-id="71264-107">This article explains how Azure DNS enables you to protect your DNS zones and records against such changes.</span></span>  <span data-ttu-id="71264-108">Nous appliquons deux puissantes fonctionnalités de sécurité d’Azure Resource Manager : le [contrôle d’accès en fonction du rôle (RBAC)](../active-directory/role-based-access-control-what-is.md) et les [verrous de ressources](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="71264-108">We apply two powerful security features provided by Azure Resource Manager: [role-based access control](../active-directory/role-based-access-control-what-is.md) and [resource locks](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

## <a name="role-based-access-control"></a><span data-ttu-id="71264-109">Contrôle d’accès en fonction du rôle</span><span class="sxs-lookup"><span data-stu-id="71264-109">Role-based access control</span></span>

<span data-ttu-id="71264-110">Le contrôle d’accès en fonction du rôle (RBAC) Azure permet une gestion précise de l’accès pour les clients, groupes et ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="71264-110">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure users, groups, and resources.</span></span> <span data-ttu-id="71264-111">Le RBAC permet d’accorder précisément aux utilisateurs les droits d’accès dont ils ont besoin pour effectuer leur travail.</span><span class="sxs-lookup"><span data-stu-id="71264-111">Using RBAC, you can grant precisely the amount of access that users need to perform their jobs.</span></span> <span data-ttu-id="71264-112">Pour plus d’informations sur la gestion des droits d’accès avec RBAC, voir [Qu’est-ce que le contrôle d’accès en fonction du rôle (RBAC)](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="71264-112">For more information about how RBAC helps you manage access, see [What is Role-Based Access Control](../active-directory/role-based-access-control-what-is.md).</span></span>

### <a name="the-dns-zone-contributor-role"></a><span data-ttu-id="71264-113">Rôle « Contributeur de Zone DNS »</span><span class="sxs-lookup"><span data-stu-id="71264-113">The 'DNS Zone Contributor' role</span></span>

<span data-ttu-id="71264-114">Le rôle « Contributeur de Zone DNS » est un rôle intégré fourni par Azure pour la gestion des ressources DNS.</span><span class="sxs-lookup"><span data-stu-id="71264-114">The 'DNS Zone Contributor' role is a built-in role provided by Azure for managing DNS resources.</span></span>  <span data-ttu-id="71264-115">L’attribution d’autorisations de Contributeur de Zone DNS à un utilisateur ou à un groupe permet à ceux-ci de gérer des ressources DNS, mais pas d’un autre type.</span><span class="sxs-lookup"><span data-stu-id="71264-115">Assigning DNS Zone Contributor permissions to a user or group enables that group to manage DNS resources, but not resources of any other type.</span></span>

<span data-ttu-id="71264-116">Par exemple, supposons que le groupe de ressources « meszones » contient cinq zones pour Contoso Corporation.</span><span class="sxs-lookup"><span data-stu-id="71264-116">For example, suppose the resource group 'myzones' contains five zones for Contoso Corporation.</span></span> <span data-ttu-id="71264-117">L’octroi des autorisations « Contributeur de Zone DNS » pour ce groupe de ressources à l’administrateur DNS permet à celui-ci de contrôler totalement ces zones DNS.</span><span class="sxs-lookup"><span data-stu-id="71264-117">Granting the DNS administrator 'DNS Zone Contributor' permissions to that resource group, enables full control over those DNS zones.</span></span> <span data-ttu-id="71264-118">Cela évite également d’accorder des autorisations inutiles. Par exemple, l’administrateur DNS ne peut ni créer, ni arrêter des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="71264-118">It also avoids granting unnecessary permissions, for example the DNS administrator cannot create or stop Virtual Machines.</span></span>

<span data-ttu-id="71264-119">La façon la plus simple d’attribuer des autorisations RBAC consiste à utiliser [le portail Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="71264-119">The simplest way to assign RBAC permissions is [via the Azure portal](../active-directory/role-based-access-control-configure.md).</span></span>  <span data-ttu-id="71264-120">Ouvrez le panneau « Contrôle d’accès (IAM) » pour le groupe de ressources, cliquez sur « Ajouter », choisissez le rôle « Contributeur de Zone DNS », puis sélectionnez les utilisateurs ou groupes auxquels accorder les autorisations.</span><span class="sxs-lookup"><span data-stu-id="71264-120">Open the 'Access control (IAM)' blade for the resource group, then click 'Add', then select the 'DNS Zone Contributor' role and select the required users or groups to grant permissions.</span></span>

![RBAC au niveau groupe de ressources via le portail Azure](./media/dns-protect-zones-recordsets/rbac1.png)

<span data-ttu-id="71264-122">Vous pouvez également [accorder des autorisations à l’aide d’Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md) :</span><span class="sxs-lookup"><span data-stu-id="71264-122">Permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant 'DNS Zone Contributor' permissions to all zones in a resource group
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>"
```

<span data-ttu-id="71264-123">La commande équivalente est également [disponible via l’interface de ligne de commande Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md) :</span><span class="sxs-lookup"><span data-stu-id="71264-123">The equivalent command is also [available via the Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant 'DNS Zone Contributor' permissions to all zones in a resource group
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --resourceGroup "<resource group name>"
```

### <a name="zone-level-rbac"></a><span data-ttu-id="71264-124">RBAC au niveau zone </span><span class="sxs-lookup"><span data-stu-id="71264-124">Zone level RBAC</span></span>

<span data-ttu-id="71264-125">Vous pouvez appliquer les règles RBAC d’Azure à un abonnement, à un groupe de ressources ou à une ressource.</span><span class="sxs-lookup"><span data-stu-id="71264-125">Azure RBAC rules can be applied to a subscription, a resource group or to an individual resource.</span></span> <span data-ttu-id="71264-126">Dans le cas du DNS Azure, cette ressource peut être une zone DNS ou un jeu d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="71264-126">In the case of Azure DNS, that resource can be an individual DNS zone, or even an individual record set.</span></span>

<span data-ttu-id="71264-127">Par exemple, supposons que le groupe de ressources « meszones » contient la zone « contoso.com » et une sous-zone « customers.contoso.com », dans laquelle des enregistrements CNAME sont créés pour chaque compte client.</span><span class="sxs-lookup"><span data-stu-id="71264-127">For example, suppose the resource group 'myzones' contains the zone 'contoso.com' and a subzone 'customers.contoso.com' in which CNAME records are created for each customer account.</span></span>  <span data-ttu-id="71264-128">Le compte utilisé pour gérer ces enregistrements CNAME doit disposer des autorisations nécessaires pour créer des enregistrements uniquement dans la zone « customers.contoso.com ». Il ne doit pas avoir accès à d’autres zones.</span><span class="sxs-lookup"><span data-stu-id="71264-128">The account used to manage these CNAME records should be assigned permissions to create records in the 'customers.contoso.com' zone only, it should not have access to the other zones.</span></span>

<span data-ttu-id="71264-129">Vous pouvez accorder les autorisations RBAC au niveau zone via le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="71264-129">Zone-level RBAC permissions can be granted via the Azure portal.</span></span>  <span data-ttu-id="71264-130">Ouvrez le panneau « Contrôle d’accès (IAM) » pour la zone, cliquez sur « Ajouter », choisissez le rôle « Contributeur de Zone DNS », puis sélectionnez les utilisateurs ou groupes auxquels accorder les autorisations.</span><span class="sxs-lookup"><span data-stu-id="71264-130">Open the 'Access control (IAM)' blade for the zone, then click 'Add', then select the 'DNS Zone Contributor' role and select the required users or groups to grant permissions.</span></span>

![RBAC au niveau Zone DNS via le portail Azure](./media/dns-protect-zones-recordsets/rbac2.png)

<span data-ttu-id="71264-132">Vous pouvez également [accorder des autorisations à l’aide d’Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md) :</span><span class="sxs-lookup"><span data-stu-id="71264-132">Permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant 'DNS Zone Contributor' permissions to a specific zone
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>" -ResourceName "<zone name>" -ResourceType Microsoft.Network/DNSZones
```

<span data-ttu-id="71264-133">La commande équivalente est également [disponible via l’interface de ligne de commande Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md) :</span><span class="sxs-lookup"><span data-stu-id="71264-133">The equivalent command is also [available via the Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant 'DNS Zone Contributor' permissions to a specific zone
azure role assignment create --signInName <user email address> --roleName "DNS Zone Contributor" --resource-name <zone name> --resource-type Microsoft.Network/DNSZones --resource-group <resource group name>
```

### <a name="record-set-level-rbac"></a><span data-ttu-id="71264-134">RBAC au niveau jeu d’enregistrements</span><span class="sxs-lookup"><span data-stu-id="71264-134">Record set level RBAC</span></span>

<span data-ttu-id="71264-135">Nous pouvons aller plus loin.</span><span class="sxs-lookup"><span data-stu-id="71264-135">We can go one step further.</span></span> <span data-ttu-id="71264-136">Imaginez l’administratrice de messagerie de la société Contoso Corporation. Elle doit pouvoir accéder aux enregistrements MX et TXT du sommet (apex) de la zone « contoso.com ».</span><span class="sxs-lookup"><span data-stu-id="71264-136">Consider the mail administrator for Contoso Corporation, who needs access to the MX and TXT records at the apex of the 'contoso.com' zone.</span></span>  <span data-ttu-id="71264-137">Elle n’a pas besoin d’accéder à d’autres enregistrements MX ou TXT, ou à des enregistrements d’un autre type.</span><span class="sxs-lookup"><span data-stu-id="71264-137">She doesn't need access to any other MX or TXT records, or to any records of any other type.</span></span>  <span data-ttu-id="71264-138">Le DNS Azure vous permet de lui attribuer des autorisations au niveau jeu d’enregistrements, grâce auxquelles elle accéder précisément aux enregistrements qui lui sont nécessaires.</span><span class="sxs-lookup"><span data-stu-id="71264-138">Azure DNS allows you to assign permissions at the record set level, to precisely the records that the mail administrator needs access to.</span></span>  <span data-ttu-id="71264-139">Elle dispose ainsi exactement du contrôle dont elle a besoin, sans pouvoir apporter d’autres modifications.</span><span class="sxs-lookup"><span data-stu-id="71264-139">The mail administrator is granted precisely the control she needs, and is unable to make any other changes.</span></span>

<span data-ttu-id="71264-140">Vous pouvez configurer les autorisations RBAC au niveau jeu d’enregistrements via le portail Azure à l’aide du bouton « Utilisateurs » dans le panneau du jeu d’enregistrements :</span><span class="sxs-lookup"><span data-stu-id="71264-140">Record-set level RBAC permissions can be configured via the Azure portal, using the 'Users' button in the record set blade:</span></span>

![RBAC au niveau jeu d’enregistrements via le portail Azure](./media/dns-protect-zones-recordsets/rbac3.png)

<span data-ttu-id="71264-142">Vous pouvez également accorder les autorisations RBAC au niveau jeu d’enregistrements en utilisant [Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md) :</span><span class="sxs-lookup"><span data-stu-id="71264-142">Record-set level RBAC permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant permissions to a specific record set
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -Scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

<span data-ttu-id="71264-143">La commande équivalente est également [disponible via l’interface de ligne de commande Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md) :</span><span class="sxs-lookup"><span data-stu-id="71264-143">The equivalent command is also [available via the Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant permissions to a specific record set
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

### <a name="custom-roles"></a><span data-ttu-id="71264-144">Rôles personnalisés</span><span class="sxs-lookup"><span data-stu-id="71264-144">Custom roles</span></span>

<span data-ttu-id="71264-145">Le rôle intégré « Contributeur de Zone DNS » permet de contrôler totalement une ressource DNS.</span><span class="sxs-lookup"><span data-stu-id="71264-145">The built-in 'DNS Zone Contributor' role enables full control over a DNS resource.</span></span> <span data-ttu-id="71264-146">Vous pouvez également créer vos propres rôles Azure personnalisés afin d’offrir un contrôle encore plus précis.</span><span class="sxs-lookup"><span data-stu-id="71264-146">It is also possible to build your own customer Azure roles, to provide even finer-grained control.</span></span>

<span data-ttu-id="71264-147">Reprenons l’exemple dans lequel un enregistrement CNAME dans la zone « customers.contoso.com » est créé pour chaque compte client de Contoso Corporation.</span><span class="sxs-lookup"><span data-stu-id="71264-147">Consider again the example in which a CNAME record in the zone 'customers.contoso.com' is created for each Contoso Corporation customer account.</span></span>  <span data-ttu-id="71264-148">Le compte utilisé pour gérer ces enregistrements CNAME doit être autorisé à gérer uniquement les enregistrements CNAME.</span><span class="sxs-lookup"><span data-stu-id="71264-148">The account used to manage these CNAMEs should be granted permission to manage CNAME records only.</span></span>  <span data-ttu-id="71264-149">Il est alors dans l’impossibilité de modifier des enregistrements d’autres types (par exemple, des enregistrements MX) ou d’effectuer des opérations au niveau de zone telles que supprimer une zone.</span><span class="sxs-lookup"><span data-stu-id="71264-149">It is then unable to modify records of other types (such as changing MX records) or perform zone-level operations such as zone delete.</span></span>

<span data-ttu-id="71264-150">L’exemple suivant montre une définition de rôle personnalisé pour la gestion des enregistrements CNAME uniquement :</span><span class="sxs-lookup"><span data-stu-id="71264-150">The following example shows a custom role definition for managing CNAME records only:</span></span>

```json
{
    "Name": "DNS CNAME Contributor",
    "Id": "",
    "IsCustom": true,
    "Description": "Can manage DNS CNAME records only.",
    "Actions": [
        "Microsoft.Network/dnsZones/CNAME/*",
        "Microsoft.Network/dnsZones/read",
        "Microsoft.Authorization/*/read",
        "Microsoft.Insights/alertRules/*",
        "Microsoft.ResourceHealth/availabilityStatuses/read",
        "Microsoft.Resources/deployments/*",
        "Microsoft.Resources/subscriptions/resourceGroups/read",
        "Microsoft.Support/*"
    ],
    "NotActions": [
    ],
    "AssignableScopes": [
        "/subscriptions/ c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ]
}
```

<span data-ttu-id="71264-151">La propriété Actions définit les autorisations spécifiques de DNS suivantes :</span><span class="sxs-lookup"><span data-stu-id="71264-151">The Actions property defines the following DNS-specific permissions:</span></span>

* <span data-ttu-id="71264-152">`Microsoft.Network/dnsZones/CNAME/*` accorde un contrôle total sur les enregistrements CNAME.</span><span class="sxs-lookup"><span data-stu-id="71264-152">`Microsoft.Network/dnsZones/CNAME/*` grants full control over CNAME records</span></span>
* <span data-ttu-id="71264-153">`Microsoft.Network/dnsZones/read` accorde l’autorisation de lire les zones DNS, mais ne pas de les modifier, ce qui permet de voir la zone dans laquelle l’enregistrement CNAME est créé.</span><span class="sxs-lookup"><span data-stu-id="71264-153">`Microsoft.Network/dnsZones/read` grants permission to read DNS zones, but not to modify them, enabling you to see the zone in which the CNAME is being created.</span></span>

<span data-ttu-id="71264-154">Les Actions restantes sont copiées à partir du [rôle intégré Contributeur de Zone DNS](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor).</span><span class="sxs-lookup"><span data-stu-id="71264-154">The remaining Actions are copied from the [DNS Zone Contributor built-in role](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor).</span></span>

> [!NOTE]
> <span data-ttu-id="71264-155">L’utilisation d’un rôle RBAC personnalisé pour empêcher la suppression de jeux d’enregistrements tout en autorisant leur mise à jour ne constitue pas un contrôle efficace.</span><span class="sxs-lookup"><span data-stu-id="71264-155">Using a custom RBAC role to prevent deleting record sets while still allowing them to be updated is not an effective control.</span></span> <span data-ttu-id="71264-156">Cela empêche la suppression de jeux d’enregistrements, mais pas leur modification.</span><span class="sxs-lookup"><span data-stu-id="71264-156">It prevents record sets from being deleted, but it does not prevent them from being modified.</span></span>  <span data-ttu-id="71264-157">Les modifications autorisées incluent l’ajout et la suppression d’enregistrements du jeu d’enregistrements, y compris la suppression de tous les enregistrements pour ne laisser qu’un jeu d’enregistrements « vide ».</span><span class="sxs-lookup"><span data-stu-id="71264-157">Permitted modifications include adding and removing records from the record set, including removing all records to leave an 'empty' record set.</span></span> <span data-ttu-id="71264-158">Sur le plan de la résolution DNS, cela produit le même effet que la suppression du jeu d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="71264-158">This has the same effect as deleting the record set from a DNS resolution viewpoint.</span></span>

<span data-ttu-id="71264-159">Il n’est actuellement pas possible de définir des rôles personnalisés via le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="71264-159">Custom role definitions cannot currently be defined via the Azure portal.</span></span> <span data-ttu-id="71264-160">Vous pouvez créer un rôle personnalisé basé sur cette définition de rôle en utilisant Azure PowerShell :</span><span class="sxs-lookup"><span data-stu-id="71264-160">A custom role based on this role definition can be created using Azure PowerShell:</span></span>

```powershell
# Create new role definition based on input file
New-AzureRmRoleDefinition -InputFile <file path>
```

<span data-ttu-id="71264-161">Vous pouvez également le faire via l’interface de ligne de commande Azure :</span><span class="sxs-lookup"><span data-stu-id="71264-161">It can also be created via the Azure CLI:</span></span>

```azurecli
# Create new role definition based on input file
azure role create -inputfile <file path>
```

<span data-ttu-id="71264-162">Ensuite, vous pouvez attribuer le rôle de la même façon qu’un rôle intégré, en procédant de la manière décrite précédemment dans cet article.</span><span class="sxs-lookup"><span data-stu-id="71264-162">The role can then be assigned in the same way as built-in roles, as described earlier in this article.</span></span>

<span data-ttu-id="71264-163">Pour plus d’informations sur la façon de créer, gérer et attribuer des rôles personnalisés, consultez [Rôles personnalisés dans le contrôle d’accès en fonction du rôle (RBAC) Azure](../active-directory/role-based-access-control-custom-roles.md).</span><span class="sxs-lookup"><span data-stu-id="71264-163">For more information on how to create, manage, and assign custom roles, see [Custom Roles in Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span></span>

## <a name="resource-locks"></a><span data-ttu-id="71264-164">Verrous de ressources</span><span class="sxs-lookup"><span data-stu-id="71264-164">Resource locks</span></span>

<span data-ttu-id="71264-165">En plus de RBAC, Azure Resource Manager prend en charge un autre type de contrôle de sécurité permettant de « verrouiller » des ressources.</span><span class="sxs-lookup"><span data-stu-id="71264-165">In addition to RBAC, Azure Resource Manager supports another type of security control, namely the ability to 'lock' resources.</span></span> <span data-ttu-id="71264-166">Si les règles RBAC vous permettent de contrôler les actions d’utilisateurs ou de groupes spécifiques, les verrous appliqués à des ressources valent pour l’ensemble des utilisateurs et des rôles.</span><span class="sxs-lookup"><span data-stu-id="71264-166">Where RBAC rules allow you to control the actions of specific users and groups, resource locks are applied to the resource, and are effective across all users and roles.</span></span> <span data-ttu-id="71264-167">Pour plus d’informations, consultez [Verrouiller des ressources avec Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="71264-167">For more information, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

<span data-ttu-id="71264-168">Il existe deux types de verrous de ressources : **DoNotDelete** (Ne pas supprimer) et **ReadOnly** (Lecture seule).</span><span class="sxs-lookup"><span data-stu-id="71264-168">There are two types of resource lock: **DoNotDelete** and **ReadOnly**.</span></span> <span data-ttu-id="71264-169">Vous pouvez les appliquer à une zone DNS ou à un jeu d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="71264-169">These can be applied either to a DNS zone, or to an individual record set.</span></span>  <span data-ttu-id="71264-170">Les sections suivantes décrivent quelques scénarios courants et la manière de les prendre en charge à l’aide de verrous de ressources.</span><span class="sxs-lookup"><span data-stu-id="71264-170">The following sections describe several common scenarios, and how to support them using resource locks.</span></span>

### <a name="protecting-against-all-changes"></a><span data-ttu-id="71264-171">Protection contre toute modification</span><span class="sxs-lookup"><span data-stu-id="71264-171">Protecting against all changes</span></span>

<span data-ttu-id="71264-172">Pour empêcher toute modification, appliquez à la zone un verrou ReadOnly.</span><span class="sxs-lookup"><span data-stu-id="71264-172">To prevent any changes being made, apply a ReadOnly lock to the zone.</span></span>  <span data-ttu-id="71264-173">Cela empêche toute création, modification ou suppression de jeux d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="71264-173">This prevents new record sets from being created, and existing record sets from being modified or deleted.</span></span>

<span data-ttu-id="71264-174">Vous pouvez créer des verrous de ressources au niveau zone via le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="71264-174">Zone level resource locks can be created via the Azure portal.</span></span>  <span data-ttu-id="71264-175">Dans le panneau Zone DNS, cliquez sur « Verrous », puis sur « Ajouter » :</span><span class="sxs-lookup"><span data-stu-id="71264-175">From the DNS zone blade, click 'Locks', then 'Add':</span></span>

![Verrous de ressources au niveau zone via le portail Azure](./media/dns-protect-zones-recordsets/locks1.png)

<span data-ttu-id="71264-177">Vous pouvez également créer des verrous de ressources au niveau zone via Azure PowerShell :</span><span class="sxs-lookup"><span data-stu-id="71264-177">Zone-level resource locks can also be created via Azure PowerShell:</span></span>

```powershell
# Lock a DNS zone
New-AzureRmResourceLock -LockLevel <lock level> -LockName <lock name> -ResourceName <zone name> -ResourceType Microsoft.Network/DNSZones -ResourceGroupName <resource group name>
```

<span data-ttu-id="71264-178">La configuration de verrous de ressources Azure n’est actuellement pas possible via l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="71264-178">Configuring Azure resource locks is not currently supported via the Azure CLI.</span></span>

### <a name="protecting-individual-records"></a><span data-ttu-id="71264-179">Protection d’enregistrements spécifiques</span><span class="sxs-lookup"><span data-stu-id="71264-179">Protecting individual records</span></span>

<span data-ttu-id="71264-180">Pour empêcher la modification d’un jeu d’enregistrements DNS, appliquez-lui un verrou ReadOnly.</span><span class="sxs-lookup"><span data-stu-id="71264-180">To prevent an existing DNS record set against modification, apply a ReadOnly lock to the record set.</span></span>

> [!NOTE]
> <span data-ttu-id="71264-181">L’application d’un verrou DoNotDelete à un jeu d’enregistrements ne constitue pas un contrôle efficace.</span><span class="sxs-lookup"><span data-stu-id="71264-181">Applying a DoNotDelete lock to a record set is not an effective control.</span></span> <span data-ttu-id="71264-182">Cela empêche la suppression du jeu d’enregistrements, mais pas sa modification.</span><span class="sxs-lookup"><span data-stu-id="71264-182">It prevents the record set from being deleted, but it does not prevent it from being modified.</span></span>  <span data-ttu-id="71264-183">Les modifications autorisées incluent l’ajout et la suppression d’enregistrements du jeu d’enregistrements, y compris la suppression de tous les enregistrements pour ne laisser qu’un jeu d’enregistrements « vide ».</span><span class="sxs-lookup"><span data-stu-id="71264-183">Permitted modifications include adding and removing records from the record set, including removing all records to leave an 'empty' record set.</span></span> <span data-ttu-id="71264-184">Sur le plan de la résolution DNS, cela produit le même effet que la suppression du jeu d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="71264-184">This has the same effect as deleting the record set from a DNS resolution viewpoint.</span></span>

<span data-ttu-id="71264-185">Vous pouvez actuellement configurer des verrous de ressources au niveau jeu d’enregistrements uniquement à l’aide d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="71264-185">Record set level resource locks can currently only be configured using Azure PowerShell.</span></span>  <span data-ttu-id="71264-186">Il n’est pas possible de le faire via le portail Azure ou l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="71264-186">They are not supported in the Azure portal or Azure CLI.</span></span>

```powershell
# Lock a DNS record set
New-AzureRmResourceLock -LockLevel <lock level> -LockName "<lock name>" -ResourceName "<zone name>/<record set name>" -ResourceType "Microsoft.Network/DNSZones/<record type>" -ResourceGroupName "<resource group name>"
```

### <a name="protecting-against-zone-deletion"></a><span data-ttu-id="71264-187">Protection contre la suppression de zone</span><span class="sxs-lookup"><span data-stu-id="71264-187">Protecting against zone deletion</span></span>

<span data-ttu-id="71264-188">Lors de la suppression d’une zone dans le DNS Azure, tous les jeux d’enregistrements contenus dans celle-ci sont supprimés.</span><span class="sxs-lookup"><span data-stu-id="71264-188">When a zone is deleted in Azure DNS, all record sets in the zone are also deleted.</span></span>  <span data-ttu-id="71264-189">Il est impossible d’annuler cette opération.</span><span class="sxs-lookup"><span data-stu-id="71264-189">This operation cannot be undone.</span></span>  <span data-ttu-id="71264-190">La suppression accidentelle d’une zone critique peut avoir une incidence considérable.</span><span class="sxs-lookup"><span data-stu-id="71264-190">Accidentally deleting a critical zone has the potential to have a significant business impact.</span></span>  <span data-ttu-id="71264-191">Il est donc très important de protéger les zones contre toute suppression accidentelle.</span><span class="sxs-lookup"><span data-stu-id="71264-191">It is therefore very important to protect against accidental zone deletion.</span></span>

<span data-ttu-id="71264-192">L’application d’un verrou DoNotDelete à une zone empêche la suppression de celle-ci.</span><span class="sxs-lookup"><span data-stu-id="71264-192">Applying a DoNotDelete lock to a zone prevents the zone from being deleted.</span></span>  <span data-ttu-id="71264-193">Toutefois, les ressources enfants héritant des verrous, cela empêche également la suppression de jeux d’enregistrements figurant dans la zone, ce qui peut être indésirable.</span><span class="sxs-lookup"><span data-stu-id="71264-193">However, since locks are inherited by child resources, it also prevents any record sets in the zone from being deleted, which may be undesirable.</span></span>  <span data-ttu-id="71264-194">Par ailleurs, comme décrit dans la Remarque ci-dessus, ce procédé est également inefficace dans la mesure où il reste toujours possible de supprimer des enregistrements à partir des jeux d’enregistrements existants.</span><span class="sxs-lookup"><span data-stu-id="71264-194">Furthermore, as described in the note above, it is also ineffective since records can still be removed from the existing record sets.</span></span>

<span data-ttu-id="71264-195">Une autre solution peut être d’appliquer un verrou DoNotDelete à un jeu d’enregistrements à l’intérieur de la zone, tel le jeu d’enregistrements SOA.</span><span class="sxs-lookup"><span data-stu-id="71264-195">As an alternative, consider applying a DoNotDelete lock to a record set in the zone, such as the SOA record set.</span></span>  <span data-ttu-id="71264-196">La zone ne pouvant pas être supprimée sans supprimer également les jeux d’enregistrements qu’elle contient, cela empêche de supprimer la zone, tout en permettant de modifier librement les jeux d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="71264-196">Since the zone cannot be deleted without also deleting the record sets, this protects against zone deletion, while still allowing record sets within the zone to be modified freely.</span></span> <span data-ttu-id="71264-197">En cas de tentative de suppression de la zone, Azure Resource Manager détecte que cela aurait pour effet de supprimer également le jeu d’enregistrements SOA. Celui-ci étant verrouillé, l’appel est bloqué.</span><span class="sxs-lookup"><span data-stu-id="71264-197">If an attempt is made to delete the zone, Azure Resource Manager detects this would also delete the SOA record set, and blocks the call because the SOA is locked.</span></span>  <span data-ttu-id="71264-198">Aucun jeu d’enregistrements n’est supprimé.</span><span class="sxs-lookup"><span data-stu-id="71264-198">No record sets are deleted.</span></span>

<span data-ttu-id="71264-199">La commande PowerShell suivante crée un verrou DoNotDelete sur l’enregistrement SOA de la zone donnée :</span><span class="sxs-lookup"><span data-stu-id="71264-199">The following PowerShell command creates a DoNotDelete lock against the SOA record of the given zone:</span></span>

```powershell
# Protect against zone delete with DoNotDelete lock on the record set
New-AzureRmResourceLock -LockLevel DoNotDelete -LockName "<lock name>" -ResourceName "<zone name>/@" -ResourceType" Microsoft.Network/DNSZones/SOA" -ResourceGroupName "<resource group name>"
```

<span data-ttu-id="71264-200">Un autre moyen d’empêcher la suppression accidentelle d’une zone consiste à utiliser un rôle personnalisé afin que les comptes d’opérateur et de service utilisés pour gérer vos zones ne soient pas autorisés à supprimer des zones.</span><span class="sxs-lookup"><span data-stu-id="71264-200">Another way to prevent accidental zone deletion is by using a custom role to ensure the operator and service accounts used to manage your zones do not have zone delete permissions.</span></span> <span data-ttu-id="71264-201">Si vous avez besoin de supprimer une zone, vous pouvez appliquer une suppression en deux étapes : octroyer des autorisations de suppression de zone (dans l’étendue de la zone, afin d’éviter la suppression d’une zone incorrecte), puis supprimer la zone.</span><span class="sxs-lookup"><span data-stu-id="71264-201">When you do need to delete a zone, you can enforce a two-step delete, first granting zone delete permissions (at the zone scope, to prevent deleting the wrong zone) and second to delete the zone.</span></span>

<span data-ttu-id="71264-202">Cette seconde approche présente l’avantage qu’elle fonctionne pour toutes les zones auxquelles ces comptes accèdent, sans avoir à créer de verrous.</span><span class="sxs-lookup"><span data-stu-id="71264-202">This second approach has the advantage that it works for all zones accessed by those accounts, without having to remember to create any locks.</span></span> <span data-ttu-id="71264-203">En revanche, tous les comptes avec des autorisations de suppression de zone, tels que le propriétaire de l’abonnement, peuvent toujours supprimer accidentellement une zone critique.</span><span class="sxs-lookup"><span data-stu-id="71264-203">It has the disadvantage that any accounts with zone delete permissions, such as the subscription owner, can still accidentally delete a critical zone.</span></span>

<span data-ttu-id="71264-204">Il est possible d’utiliser les deux approches (verrous de ressources et rôles personnalisés) en même temps en guise de protection en profondeur des zones DNS.</span><span class="sxs-lookup"><span data-stu-id="71264-204">It is possible to use both approaches - resource locks and custom roles - at the same time, as a defense-in-depth approach to DNS zone protection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="71264-205">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="71264-205">Next steps</span></span>

* <span data-ttu-id="71264-206">Pour plus d’informations sur l’utilisation de RBAC, voir [Prise en main de la gestion des accès dans le portail Azure](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="71264-206">For more information about working with RBAC, see [Get started with access management in the Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>
* <span data-ttu-id="71264-207">Pour plus d’informations sur l’utilisation des verrous de ressources, voir [Verrouiller des ressources avec Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="71264-207">For more information about working with resource locks, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

