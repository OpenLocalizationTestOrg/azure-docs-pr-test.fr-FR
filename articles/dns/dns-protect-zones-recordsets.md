---
title: aaaProtecting Zones et enregistrements DNS | Documents Microsoft
description: "Comment les zones DNS tooprotect et enregistrement définit dans le système DNS de Microsoft Azure."
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
ms.openlocfilehash: 7945f6240feeed3d79a11d340f9f845e083026ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprotect-dns-zones-and-records"></a><span data-ttu-id="8031c-103">Comment tooprotect DNS zones et enregistrements</span><span class="sxs-lookup"><span data-stu-id="8031c-103">How tooprotect DNS zones and records</span></span>

<span data-ttu-id="8031c-104">Les enregistrements et zones DNS sont des ressources critiques.</span><span class="sxs-lookup"><span data-stu-id="8031c-104">DNS zones and records are critical resources.</span></span> <span data-ttu-id="8031c-105">La suppression d’une zone DNS, voire d’un seul enregistrement DNS, peut entraîner une interruption de service totale.</span><span class="sxs-lookup"><span data-stu-id="8031c-105">Deleting a DNS zone or even just a single DNS record can result in a total service outage.</span></span>  <span data-ttu-id="8031c-106">Il est donc important que les zones et enregistrements DNS critiques soient protégés contre toute modification non autorisée ou accidentelle.</span><span class="sxs-lookup"><span data-stu-id="8031c-106">It is therefore important that critical DNS zones and records are protected against unauthorized or accidental changes.</span></span>

<span data-ttu-id="8031c-107">Cet article explique comment Azure DNS permet de vous tooprotect vos zones et enregistrements DNS contre de telles modifications.</span><span class="sxs-lookup"><span data-stu-id="8031c-107">This article explains how Azure DNS enables you tooprotect your DNS zones and records against such changes.</span></span>  <span data-ttu-id="8031c-108">Nous appliquons deux puissantes fonctionnalités de sécurité d’Azure Resource Manager : le [contrôle d’accès en fonction du rôle (RBAC)](../active-directory/role-based-access-control-what-is.md) et les [verrous de ressources](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="8031c-108">We apply two powerful security features provided by Azure Resource Manager: [role-based access control](../active-directory/role-based-access-control-what-is.md) and [resource locks](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

## <a name="role-based-access-control"></a><span data-ttu-id="8031c-109">Contrôle d’accès en fonction du rôle</span><span class="sxs-lookup"><span data-stu-id="8031c-109">Role-based access control</span></span>

<span data-ttu-id="8031c-110">Le contrôle d’accès en fonction du rôle (RBAC) Azure permet une gestion précise de l’accès pour les clients, groupes et ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="8031c-110">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure users, groups, and resources.</span></span> <span data-ttu-id="8031c-111">À l’aide de RBAC, vous pouvez accorder précisément hello quantité accès que les utilisateurs doivent tooperform leur travail.</span><span class="sxs-lookup"><span data-stu-id="8031c-111">Using RBAC, you can grant precisely hello amount of access that users need tooperform their jobs.</span></span> <span data-ttu-id="8031c-112">Pour plus d’informations sur la gestion des droits d’accès avec RBAC, voir [Qu’est-ce que le contrôle d’accès en fonction du rôle (RBAC)](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="8031c-112">For more information about how RBAC helps you manage access, see [What is Role-Based Access Control](../active-directory/role-based-access-control-what-is.md).</span></span>

### <a name="hello-dns-zone-contributor-role"></a><span data-ttu-id="8031c-113">rôle de « Collaborateur de Zone DNS » Hello</span><span class="sxs-lookup"><span data-stu-id="8031c-113">hello 'DNS Zone Contributor' role</span></span>

<span data-ttu-id="8031c-114">rôle de « Collaborateur de Zone DNS » Hello est un rôle intégré fourni par Azure pour la gestion des ressources DNS.</span><span class="sxs-lookup"><span data-stu-id="8031c-114">hello 'DNS Zone Contributor' role is a built-in role provided by Azure for managing DNS resources.</span></span>  <span data-ttu-id="8031c-115">Affectation de collaborateur de Zone DNS autorisations tooa utilisateur ou un groupe permet de ce regroupement des ressources DNS toomanage, mais pas les ressources d’un autre type.</span><span class="sxs-lookup"><span data-stu-id="8031c-115">Assigning DNS Zone Contributor permissions tooa user or group enables that group toomanage DNS resources, but not resources of any other type.</span></span>

<span data-ttu-id="8031c-116">Par exemple, groupe de ressources hello 'myzones' contient les cinq zones de Contoso Corporation.</span><span class="sxs-lookup"><span data-stu-id="8031c-116">For example, suppose hello resource group 'myzones' contains five zones for Contoso Corporation.</span></span> <span data-ttu-id="8031c-117">Accorder hello DNS administrateur « Collaborateur de Zone DNS » autorisations toothat groupe de ressources, permet un contrôle total sur les zones DNS.</span><span class="sxs-lookup"><span data-stu-id="8031c-117">Granting hello DNS administrator 'DNS Zone Contributor' permissions toothat resource group, enables full control over those DNS zones.</span></span> <span data-ttu-id="8031c-118">Il permet également d’éviter l’octroi d’autorisations inutiles, par exemple l’administrateur DNS hello ne peut pas créer ou arrêter les Machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="8031c-118">It also avoids granting unnecessary permissions, for example hello DNS administrator cannot create or stop Virtual Machines.</span></span>

<span data-ttu-id="8031c-119">autorisations de RBAC Hello la plus simple façon tooassign est [via le portail Azure de hello](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="8031c-119">hello simplest way tooassign RBAC permissions is [via hello Azure portal](../active-directory/role-based-access-control-configure.md).</span></span>  <span data-ttu-id="8031c-120">Ouvrez le panneau hello « contrôle d’accès (IAM) » pour le groupe de ressources hello, puis 'Add', puis sur rôle de « Collaborateur de Zone DNS » hello et les utilisateurs de sélectionner hello requis ou groupes des autorisations toogrant.</span><span class="sxs-lookup"><span data-stu-id="8031c-120">Open hello 'Access control (IAM)' blade for hello resource group, then click 'Add', then select hello 'DNS Zone Contributor' role and select hello required users or groups toogrant permissions.</span></span>

![Niveau de groupe de ressources RBAC via hello portail Azure](./media/dns-protect-zones-recordsets/rbac1.png)

<span data-ttu-id="8031c-122">Vous pouvez également [accorder des autorisations à l’aide d’Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md) :</span><span class="sxs-lookup"><span data-stu-id="8031c-122">Permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant 'DNS Zone Contributor' permissions tooall zones in a resource group
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>"
```

<span data-ttu-id="8031c-123">commande équivalent Hello est également [disponible via hello CLI d’Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="8031c-123">hello equivalent command is also [available via hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant 'DNS Zone Contributor' permissions tooall zones in a resource group
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --resourceGroup "<resource group name>"
```

### <a name="zone-level-rbac"></a><span data-ttu-id="8031c-124">RBAC au niveau zone </span><span class="sxs-lookup"><span data-stu-id="8031c-124">Zone level RBAC</span></span>

<span data-ttu-id="8031c-125">Les règles RBAC Azure peuvent être appliqués tooa abonnement, un groupe ou tooan individuelle ressource.</span><span class="sxs-lookup"><span data-stu-id="8031c-125">Azure RBAC rules can be applied tooa subscription, a resource group or tooan individual resource.</span></span> <span data-ttu-id="8031c-126">Dans les cas de hello de Azure DNS, cette ressource peut être une zone DNS individuelle, ou même un jeu d’enregistrements individuel.</span><span class="sxs-lookup"><span data-stu-id="8031c-126">In hello case of Azure DNS, that resource can be an individual DNS zone, or even an individual record set.</span></span>

<span data-ttu-id="8031c-127">Par exemple, groupe de ressources hello 'myzones' contient hello zone « contoso.com » et sous-zone 'customers.contoso.com' dans lequel les enregistrements CNAME sont créés pour chaque compte client.</span><span class="sxs-lookup"><span data-stu-id="8031c-127">For example, suppose hello resource group 'myzones' contains hello zone 'contoso.com' and a subzone 'customers.contoso.com' in which CNAME records are created for each customer account.</span></span>  <span data-ttu-id="8031c-128">Hello compte utilisé toomanage ces enregistrements CNAME doivent être attribués autorisations toocreate enregistrements dans la zone « customers.contoso.com » hello, il ne doit comporter accès toohello autres zones.</span><span class="sxs-lookup"><span data-stu-id="8031c-128">hello account used toomanage these CNAME records should be assigned permissions toocreate records in hello 'customers.contoso.com' zone only, it should not have access toohello other zones.</span></span>

<span data-ttu-id="8031c-129">Les autorisations de niveau zone RBAC peuvent être accordées via hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8031c-129">Zone-level RBAC permissions can be granted via hello Azure portal.</span></span>  <span data-ttu-id="8031c-130">Pour ouvrir Panneau de 'Contrôle d’accès (IAM)' hello pour la zone de hello, puis 'Add', puis sur rôle de « Collaborateur de Zone DNS » hello et les utilisateurs de sélectionner hello requis ou groupes des autorisations toogrant.</span><span class="sxs-lookup"><span data-stu-id="8031c-130">Open hello 'Access control (IAM)' blade for hello zone, then click 'Add', then select hello 'DNS Zone Contributor' role and select hello required users or groups toogrant permissions.</span></span>

![Zone DNS de niveau RBAC via hello portail Azure](./media/dns-protect-zones-recordsets/rbac2.png)

<span data-ttu-id="8031c-132">Vous pouvez également [accorder des autorisations à l’aide d’Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md) :</span><span class="sxs-lookup"><span data-stu-id="8031c-132">Permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant 'DNS Zone Contributor' permissions tooa specific zone
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>" -ResourceName "<zone name>" -ResourceType Microsoft.Network/DNSZones
```

<span data-ttu-id="8031c-133">commande équivalent Hello est également [disponible via hello CLI d’Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="8031c-133">hello equivalent command is also [available via hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant 'DNS Zone Contributor' permissions tooa specific zone
azure role assignment create --signInName <user email address> --roleName "DNS Zone Contributor" --resource-name <zone name> --resource-type Microsoft.Network/DNSZones --resource-group <resource group name>
```

### <a name="record-set-level-rbac"></a><span data-ttu-id="8031c-134">RBAC au niveau jeu d’enregistrements</span><span class="sxs-lookup"><span data-stu-id="8031c-134">Record set level RBAC</span></span>

<span data-ttu-id="8031c-135">Nous pouvons aller plus loin.</span><span class="sxs-lookup"><span data-stu-id="8031c-135">We can go one step further.</span></span> <span data-ttu-id="8031c-136">Envisagez d’administrateur de messagerie hello pour Contoso Corporation, qui a besoin d’accès toohello MX et les enregistrements TXT au sommet de hello de zone de « contoso.com » hello.</span><span class="sxs-lookup"><span data-stu-id="8031c-136">Consider hello mail administrator for Contoso Corporation, who needs access toohello MX and TXT records at hello apex of hello 'contoso.com' zone.</span></span>  <span data-ttu-id="8031c-137">Elle ne doivent accéder à tooany autres enregistrements MX ou TXT ou tooany les enregistrements d’un autre type.</span><span class="sxs-lookup"><span data-stu-id="8031c-137">She doesn't need access tooany other MX or TXT records, or tooany records of any other type.</span></span>  <span data-ttu-id="8031c-138">DNS Azure permet de vous tooassign des autorisations à hello jeu d’enregistrements niveau tooprecisely hello enregistrements hello administrateur de messagerie a besoin d’accéder à.</span><span class="sxs-lookup"><span data-stu-id="8031c-138">Azure DNS allows you tooassign permissions at hello record set level, tooprecisely hello records that hello mail administrator needs access to.</span></span>  <span data-ttu-id="8031c-139">Hello administrateur de messagerie est accordé avec précision les contrôle hello elle a besoin et est toomake Impossible de toutes les autres modifications.</span><span class="sxs-lookup"><span data-stu-id="8031c-139">hello mail administrator is granted precisely hello control she needs, and is unable toomake any other changes.</span></span>

<span data-ttu-id="8031c-140">Autorisations de RBAC de niveau de jeu d’enregistrements peuvent être configurées via hello portail Azure, à l’aide du bouton de hello « utilisateurs » dans le panneau de jeu d’enregistrements hello :</span><span class="sxs-lookup"><span data-stu-id="8031c-140">Record-set level RBAC permissions can be configured via hello Azure portal, using hello 'Users' button in hello record set blade:</span></span>

![Jeu d’enregistrements au niveau RBAC via hello portail Azure](./media/dns-protect-zones-recordsets/rbac3.png)

<span data-ttu-id="8031c-142">Vous pouvez également accorder les autorisations RBAC au niveau jeu d’enregistrements en utilisant [Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md) :</span><span class="sxs-lookup"><span data-stu-id="8031c-142">Record-set level RBAC permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant permissions tooa specific record set
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -Scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

<span data-ttu-id="8031c-143">commande équivalent Hello est également [disponible via hello CLI d’Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="8031c-143">hello equivalent command is also [available via hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant permissions tooa specific record set
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

### <a name="custom-roles"></a><span data-ttu-id="8031c-144">Rôles personnalisés</span><span class="sxs-lookup"><span data-stu-id="8031c-144">Custom roles</span></span>

<span data-ttu-id="8031c-145">Hello intégré « Collaborateur de Zone DNS » rôle permet d’un contrôle total sur une ressource DNS.</span><span class="sxs-lookup"><span data-stu-id="8031c-145">hello built-in 'DNS Zone Contributor' role enables full control over a DNS resource.</span></span> <span data-ttu-id="8031c-146">Il est également possible de toobuild votre propre client Azure rôles, contrôle de tooprovide même plus précise.</span><span class="sxs-lookup"><span data-stu-id="8031c-146">It is also possible toobuild your own customer Azure roles, tooprovide even finer-grained control.</span></span>

<span data-ttu-id="8031c-147">Prenez de nouveau exemple hello dans laquelle un enregistrement CNAME dans la zone hello 'customers.contoso.com' est créé pour chaque compte client de Contoso Corporation.</span><span class="sxs-lookup"><span data-stu-id="8031c-147">Consider again hello example in which a CNAME record in hello zone 'customers.contoso.com' is created for each Contoso Corporation customer account.</span></span>  <span data-ttu-id="8031c-148">Hello compte utilisé toomanage ces enregistrements CNAME doit être accordées autorisation toomanage enregistrements CNAME du uniquement.</span><span class="sxs-lookup"><span data-stu-id="8031c-148">hello account used toomanage these CNAMEs should be granted permission toomanage CNAME records only.</span></span>  <span data-ttu-id="8031c-149">Il est impossible toomodify des enregistrements d’autres types (telles que la modification des enregistrements MX) ou effectuer des opérations de niveau zone telles que supprimer de la zone.</span><span class="sxs-lookup"><span data-stu-id="8031c-149">It is then unable toomodify records of other types (such as changing MX records) or perform zone-level operations such as zone delete.</span></span>

<span data-ttu-id="8031c-150">Bonjour à l’exemple suivant montre une définition de rôle personnalisé pour la gestion des enregistrements CNAME uniquement :</span><span class="sxs-lookup"><span data-stu-id="8031c-150">hello following example shows a custom role definition for managing CNAME records only:</span></span>

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

<span data-ttu-id="8031c-151">Hello propriété Actions définit hello les autorisations spécifiques à DNS suivantes :</span><span class="sxs-lookup"><span data-stu-id="8031c-151">hello Actions property defines hello following DNS-specific permissions:</span></span>

* <span data-ttu-id="8031c-152">`Microsoft.Network/dnsZones/CNAME/*` accorde un contrôle total sur les enregistrements CNAME.</span><span class="sxs-lookup"><span data-stu-id="8031c-152">`Microsoft.Network/dnsZones/CNAME/*` grants full control over CNAME records</span></span>
* <span data-ttu-id="8031c-153">`Microsoft.Network/dnsZones/read`accorde les zones DNS tooread autorisation, mais pas les toomodify les, l’activation de toosee vous hello zone dans quel hello CNAME est créée.</span><span class="sxs-lookup"><span data-stu-id="8031c-153">`Microsoft.Network/dnsZones/read` grants permission tooread DNS zones, but not toomodify them, enabling you toosee hello zone in which hello CNAME is being created.</span></span>

<span data-ttu-id="8031c-154">Hello Actions restantes sont copiées à partir de hello [rôle intégré du collaborateur de Zone DNS](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor).</span><span class="sxs-lookup"><span data-stu-id="8031c-154">hello remaining Actions are copied from hello [DNS Zone Contributor built-in role](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor).</span></span>

> [!NOTE]
> <span data-ttu-id="8031c-155">À l’aide d’un tooprevent de rôle RBAC personnalisé, suppression de l’enregistrement définit alors qu’en autorisant toobe mis à jour n’est pas un contrôle efficace.</span><span class="sxs-lookup"><span data-stu-id="8031c-155">Using a custom RBAC role tooprevent deleting record sets while still allowing them toobe updated is not an effective control.</span></span> <span data-ttu-id="8031c-156">Cela empêche la suppression de jeux d’enregistrements, mais pas leur modification.</span><span class="sxs-lookup"><span data-stu-id="8031c-156">It prevents record sets from being deleted, but it does not prevent them from being modified.</span></span>  <span data-ttu-id="8031c-157">Modifications autorisées incluent l’ajout et suppression d’enregistrements de jeu d’enregistrements hello, notamment la suppression de tous les enregistrements tooleave un jeu d’enregistrements 'empty'.</span><span class="sxs-lookup"><span data-stu-id="8031c-157">Permitted modifications include adding and removing records from hello record set, including removing all records tooleave an 'empty' record set.</span></span> <span data-ttu-id="8031c-158">Cela a hello même effet que la suppression de l’enregistrement hello définie à partir d’un point de vue de la résolution DNS.</span><span class="sxs-lookup"><span data-stu-id="8031c-158">This has hello same effect as deleting hello record set from a DNS resolution viewpoint.</span></span>

<span data-ttu-id="8031c-159">Les définitions de rôle personnalisé ne peut actuellement être définies via hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8031c-159">Custom role definitions cannot currently be defined via hello Azure portal.</span></span> <span data-ttu-id="8031c-160">Vous pouvez créer un rôle personnalisé basé sur cette définition de rôle en utilisant Azure PowerShell :</span><span class="sxs-lookup"><span data-stu-id="8031c-160">A custom role based on this role definition can be created using Azure PowerShell:</span></span>

```powershell
# Create new role definition based on input file
New-AzureRmRoleDefinition -InputFile <file path>
```

<span data-ttu-id="8031c-161">Il peut également être créé via hello CLI d’Azure :</span><span class="sxs-lookup"><span data-stu-id="8031c-161">It can also be created via hello Azure CLI:</span></span>

```azurecli
# Create new role definition based on input file
azure role create -inputfile <file path>
```

<span data-ttu-id="8031c-162">Hello rôle peut ensuite être attribué Bonjour même façon que les rôles intégrés, comme décrit précédemment dans cet article.</span><span class="sxs-lookup"><span data-stu-id="8031c-162">hello role can then be assigned in hello same way as built-in roles, as described earlier in this article.</span></span>

<span data-ttu-id="8031c-163">Pour plus d’informations sur la façon dont toocreate, gérer et attribuer des rôles personnalisés, consultez [des rôles personnalisés dans Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span><span class="sxs-lookup"><span data-stu-id="8031c-163">For more information on how toocreate, manage, and assign custom roles, see [Custom Roles in Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span></span>

## <a name="resource-locks"></a><span data-ttu-id="8031c-164">Verrous de ressources</span><span class="sxs-lookup"><span data-stu-id="8031c-164">Resource locks</span></span>

<span data-ttu-id="8031c-165">Ajout tooRBAC, Azure Resource Manager prend en charge un autre type de contrôle de sécurité, à savoir les too'lock possibilité hello' ressources.</span><span class="sxs-lookup"><span data-stu-id="8031c-165">In addition tooRBAC, Azure Resource Manager supports another type of security control, namely hello ability too'lock' resources.</span></span> <span data-ttu-id="8031c-166">Lorsque les règles RBAC vous toocontrol hello les actions d’autorisation des utilisateurs et groupes spécifiques, verrous des ressources toohello appliqué des ressources et sont en vigueur dans tous les utilisateurs et les rôles.</span><span class="sxs-lookup"><span data-stu-id="8031c-166">Where RBAC rules allow you toocontrol hello actions of specific users and groups, resource locks are applied toohello resource, and are effective across all users and roles.</span></span> <span data-ttu-id="8031c-167">Pour plus d’informations, consultez [Verrouiller des ressources avec Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="8031c-167">For more information, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

<span data-ttu-id="8031c-168">Il existe deux types de verrous de ressources : **DoNotDelete** (Ne pas supprimer) et **ReadOnly** (Lecture seule).</span><span class="sxs-lookup"><span data-stu-id="8031c-168">There are two types of resource lock: **DoNotDelete** and **ReadOnly**.</span></span> <span data-ttu-id="8031c-169">Ils peuvent être appliqués zone DNS de tooa ou de jeu d’enregistrements individuels tooan.</span><span class="sxs-lookup"><span data-stu-id="8031c-169">These can be applied either tooa DNS zone, or tooan individual record set.</span></span>  <span data-ttu-id="8031c-170">Hello sections suivantes décrivent plusieurs scénarios courants et comment toosupport les à l’aide de verrous de ressources.</span><span class="sxs-lookup"><span data-stu-id="8031c-170">hello following sections describe several common scenarios, and how toosupport them using resource locks.</span></span>

### <a name="protecting-against-all-changes"></a><span data-ttu-id="8031c-171">Protection contre toute modification</span><span class="sxs-lookup"><span data-stu-id="8031c-171">Protecting against all changes</span></span>

<span data-ttu-id="8031c-172">tooprevent toutes les modifications apportées, appliquez une zone toohello de verrou en lecture seule.</span><span class="sxs-lookup"><span data-stu-id="8031c-172">tooprevent any changes being made, apply a ReadOnly lock toohello zone.</span></span>  <span data-ttu-id="8031c-173">Cela empêche toute création, modification ou suppression de jeux d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="8031c-173">This prevents new record sets from being created, and existing record sets from being modified or deleted.</span></span>

<span data-ttu-id="8031c-174">Verrous de ressources de niveau zone peuvent être créés via hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8031c-174">Zone level resource locks can be created via hello Azure portal.</span></span>  <span data-ttu-id="8031c-175">À partir du Panneau de zone DNS hello, cliquez sur « Verrous », puis 'Add' :</span><span class="sxs-lookup"><span data-stu-id="8031c-175">From hello DNS zone blade, click 'Locks', then 'Add':</span></span>

![Verrous de ressources de niveau zone via hello portail Azure](./media/dns-protect-zones-recordsets/locks1.png)

<span data-ttu-id="8031c-177">Vous pouvez également créer des verrous de ressources au niveau zone via Azure PowerShell :</span><span class="sxs-lookup"><span data-stu-id="8031c-177">Zone-level resource locks can also be created via Azure PowerShell:</span></span>

```powershell
# Lock a DNS zone
New-AzureRmResourceLock -LockLevel <lock level> -LockName <lock name> -ResourceName <zone name> -ResourceType Microsoft.Network/DNSZones -ResourceGroupName <resource group name>
```

<span data-ttu-id="8031c-178">Configuration des verrous de ressources Azure n’est actuellement pas pris en charge via hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="8031c-178">Configuring Azure resource locks is not currently supported via hello Azure CLI.</span></span>

### <a name="protecting-individual-records"></a><span data-ttu-id="8031c-179">Protection d’enregistrements spécifiques</span><span class="sxs-lookup"><span data-stu-id="8031c-179">Protecting individual records</span></span>

<span data-ttu-id="8031c-180">tooprevent un enregistrement DNS existant défini contre la modification, appliquer un jeu d’enregistrements toohello verrou en lecture seule.</span><span class="sxs-lookup"><span data-stu-id="8031c-180">tooprevent an existing DNS record set against modification, apply a ReadOnly lock toohello record set.</span></span>

> [!NOTE]
> <span data-ttu-id="8031c-181">Application d’un tooa de verrou DoNotDelete jeu d’enregistrements n’est pas un contrôle efficace.</span><span class="sxs-lookup"><span data-stu-id="8031c-181">Applying a DoNotDelete lock tooa record set is not an effective control.</span></span> <span data-ttu-id="8031c-182">Il empêche hello jeu d’enregistrements d’être supprimé, mais il ne l’empêche pas d’être modifiées.</span><span class="sxs-lookup"><span data-stu-id="8031c-182">It prevents hello record set from being deleted, but it does not prevent it from being modified.</span></span>  <span data-ttu-id="8031c-183">Modifications autorisées incluent l’ajout et suppression d’enregistrements de jeu d’enregistrements hello, notamment la suppression de tous les enregistrements tooleave un jeu d’enregistrements 'empty'.</span><span class="sxs-lookup"><span data-stu-id="8031c-183">Permitted modifications include adding and removing records from hello record set, including removing all records tooleave an 'empty' record set.</span></span> <span data-ttu-id="8031c-184">Cela a hello même effet que la suppression de l’enregistrement hello définie à partir d’un point de vue de la résolution DNS.</span><span class="sxs-lookup"><span data-stu-id="8031c-184">This has hello same effect as deleting hello record set from a DNS resolution viewpoint.</span></span>

<span data-ttu-id="8031c-185">Vous pouvez actuellement configurer des verrous de ressources au niveau jeu d’enregistrements uniquement à l’aide d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8031c-185">Record set level resource locks can currently only be configured using Azure PowerShell.</span></span>  <span data-ttu-id="8031c-186">Elles ne sont pas prises en charge dans hello portail Azure ou CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="8031c-186">They are not supported in hello Azure portal or Azure CLI.</span></span>

```powershell
# Lock a DNS record set
New-AzureRmResourceLock -LockLevel <lock level> -LockName "<lock name>" -ResourceName "<zone name>/<record set name>" -ResourceType "Microsoft.Network/DNSZones/<record type>" -ResourceGroupName "<resource group name>"
```

### <a name="protecting-against-zone-deletion"></a><span data-ttu-id="8031c-187">Protection contre la suppression de zone</span><span class="sxs-lookup"><span data-stu-id="8031c-187">Protecting against zone deletion</span></span>

<span data-ttu-id="8031c-188">Lorsqu’une zone est supprimée dans le système DNS Azure, tous les jeux d’enregistrements dans la zone de hello sont également supprimés.</span><span class="sxs-lookup"><span data-stu-id="8031c-188">When a zone is deleted in Azure DNS, all record sets in hello zone are also deleted.</span></span>  <span data-ttu-id="8031c-189">Il est impossible d’annuler cette opération.</span><span class="sxs-lookup"><span data-stu-id="8031c-189">This operation cannot be undone.</span></span>  <span data-ttu-id="8031c-190">Suppression accidentelle d’une zone critique a toohave potentielle de hello un impact significatif pour l’entreprise.</span><span class="sxs-lookup"><span data-stu-id="8031c-190">Accidentally deleting a critical zone has hello potential toohave a significant business impact.</span></span>  <span data-ttu-id="8031c-191">Il est donc très important tooprotect contre la suppression accidentelle de zone.</span><span class="sxs-lookup"><span data-stu-id="8031c-191">It is therefore very important tooprotect against accidental zone deletion.</span></span>

<span data-ttu-id="8031c-192">Une zone de tooa DoNotDelete verrou empêche les zone hello d’être supprimé.</span><span class="sxs-lookup"><span data-stu-id="8031c-192">Applying a DoNotDelete lock tooa zone prevents hello zone from being deleted.</span></span>  <span data-ttu-id="8031c-193">Toutefois, étant donné que les verrous sont héritées par les ressources enfants, elle évite également les jeux d’enregistrements dans la zone hello d’être supprimé, ce qui peut être indésirable.</span><span class="sxs-lookup"><span data-stu-id="8031c-193">However, since locks are inherited by child resources, it also prevents any record sets in hello zone from being deleted, which may be undesirable.</span></span>  <span data-ttu-id="8031c-194">En outre, comme décrit dans la Remarque hello ci-dessus, il est également inefficace, car les enregistrements peuvent toujours être supprimés à partir de jeux d’enregistrements existants hello.</span><span class="sxs-lookup"><span data-stu-id="8031c-194">Furthermore, as described in hello note above, it is also ineffective since records can still be removed from hello existing record sets.</span></span>

<span data-ttu-id="8031c-195">En guise d’alternative, envisagez d’appliquer un enregistrement tooa de verrou DoNotDelete définie dans la zone hello, par exemple de jeu d’enregistrements hello SOA.</span><span class="sxs-lookup"><span data-stu-id="8031c-195">As an alternative, consider applying a DoNotDelete lock tooa record set in hello zone, such as hello SOA record set.</span></span>  <span data-ttu-id="8031c-196">Étant donné que la zone de hello ne peut pas être supprimée sans supprimer également les jeux d’enregistrements hello, cela protège contre la suppression de zone, tout en permettant aux jeux d’enregistrements dans toobe de zone hello modifiées librement.</span><span class="sxs-lookup"><span data-stu-id="8031c-196">Since hello zone cannot be deleted without also deleting hello record sets, this protects against zone deletion, while still allowing record sets within hello zone toobe modified freely.</span></span> <span data-ttu-id="8031c-197">Si une tentative est faite de zone de hello toodelete, Azure Resource Manager détecte cela serait également supprimer le jeu d’enregistrements hello SOA et blocs hello appel car hello SOA est verrouillé.</span><span class="sxs-lookup"><span data-stu-id="8031c-197">If an attempt is made toodelete hello zone, Azure Resource Manager detects this would also delete hello SOA record set, and blocks hello call because hello SOA is locked.</span></span>  <span data-ttu-id="8031c-198">Aucun jeu d’enregistrements n’est supprimé.</span><span class="sxs-lookup"><span data-stu-id="8031c-198">No record sets are deleted.</span></span>

<span data-ttu-id="8031c-199">Hello suivant de commande PowerShell crée un verrou DoNotDelete par rapport à l’enregistrement SOA de hello Hello donné zone :</span><span class="sxs-lookup"><span data-stu-id="8031c-199">hello following PowerShell command creates a DoNotDelete lock against hello SOA record of hello given zone:</span></span>

```powershell
# Protect against zone delete with DoNotDelete lock on hello record set
New-AzureRmResourceLock -LockLevel DoNotDelete -LockName "<lock name>" -ResourceName "<zone name>/@" -ResourceType" Microsoft.Network/DNSZones/SOA" -ResourceGroupName "<resource group name>"
```

<span data-ttu-id="8031c-200">Une autre façon tooprevent la suppression accidentelle de zone est en utilisant un opérateur de rôle personnalisé tooensure hello et toomanage des comptes de service que vos zones ne pas avoir de zone supprimer des autorisations.</span><span class="sxs-lookup"><span data-stu-id="8031c-200">Another way tooprevent accidental zone deletion is by using a custom role tooensure hello operator and service accounts used toomanage your zones do not have zone delete permissions.</span></span> <span data-ttu-id="8031c-201">Lorsque vous avez besoin d’une zone de toodelete, vous pouvez appliquer une suppression en deux étapes, autorisations de suppression de zone accorder premier (à l’étendue de la zone hello, tooprevent suppression d’une zone de hello) et la deuxième zone de hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="8031c-201">When you do need toodelete a zone, you can enforce a two-step delete, first granting zone delete permissions (at hello zone scope, tooprevent deleting hello wrong zone) and second toodelete hello zone.</span></span>

<span data-ttu-id="8031c-202">Cette seconde approche a l’avantage hello qu’il fonctionne pour toutes les zones accessibles par ces comptes, sans avoir à tooremember toocreate tous les verrous.</span><span class="sxs-lookup"><span data-stu-id="8031c-202">This second approach has hello advantage that it works for all zones accessed by those accounts, without having tooremember toocreate any locks.</span></span> <span data-ttu-id="8031c-203">Il a inconvénient hello que tous les comptes avec des autorisations de suppression de zone, telles que le propriétaire d’abonnement hello, toujours accidentellement à supprimer une zone critique.</span><span class="sxs-lookup"><span data-stu-id="8031c-203">It has hello disadvantage that any accounts with zone delete permissions, such as hello subscription owner, can still accidentally delete a critical zone.</span></span>

<span data-ttu-id="8031c-204">Il est possible de toouse les deux approches, verrous des ressources et des rôles personnalisés, à hello même moment, la protection de zone tooDNS une approche de défense en profondeur.</span><span class="sxs-lookup"><span data-stu-id="8031c-204">It is possible toouse both approaches - resource locks and custom roles - at hello same time, as a defense-in-depth approach tooDNS zone protection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8031c-205">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8031c-205">Next steps</span></span>

* <span data-ttu-id="8031c-206">Pour plus d’informations sur l’utilisation de RBAC, consultez [commencer avec la gestion des accès Bonjour Azure portal](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="8031c-206">For more information about working with RBAC, see [Get started with access management in hello Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>
* <span data-ttu-id="8031c-207">Pour plus d’informations sur l’utilisation des verrous de ressources, voir [Verrouiller des ressources avec Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="8031c-207">For more information about working with resource locks, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

