---
title: "aaaCreate des rôles personnalisés pour Azure RBAC. | Documents Microsoft"
description: "Découvrez comment toodefine des rôles personnalisés avec du contrôle d’accès pour la gestion d’identité plus précise dans votre abonnement Azure."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: e4206ea9-52c3-47ee-af29-f6eef7566fa5
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/11/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 60df12632ef6c086d5feeb1809196d7c4ee5e021
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-custom-roles-for-azure-role-based-access-control"></a><span data-ttu-id="3c2cb-103">Créer des rôles personnalisés pour le contrôle d’accès en fonction du rôle Azure</span><span class="sxs-lookup"><span data-stu-id="3c2cb-103">Create custom roles for Azure Role-Based Access Control</span></span>
<span data-ttu-id="3c2cb-104">Créer un rôle personnalisé dans le contrôle d’accès du (RBAC) si aucun des rôles intégrés de hello répond à vos besoins spécifiques.</span><span class="sxs-lookup"><span data-stu-id="3c2cb-104">Create a custom role in Azure Role-Based Access Control (RBAC) if none of hello built-in roles meet your specific access needs.</span></span> <span data-ttu-id="3c2cb-105">Des rôles personnalisés peuvent être créés à l’aide de [Azure PowerShell](role-based-access-control-manage-access-powershell.md), [Interface de ligne de commande Azure](role-based-access-control-manage-access-azure-cli.md) (CLI) et hello [API REST](role-based-access-control-manage-access-rest.md).</span><span class="sxs-lookup"><span data-stu-id="3c2cb-105">Custom roles can be created using [Azure PowerShell](role-based-access-control-manage-access-powershell.md), [Azure Command-Line Interface](role-based-access-control-manage-access-azure-cli.md) (CLI), and hello [REST API](role-based-access-control-manage-access-rest.md).</span></span> <span data-ttu-id="3c2cb-106">Tout comme les rôles intégrés, vous pouvez affecter toousers de rôles personnalisés, des groupes et des applications au niveau d’abonnement, de groupe de ressources et de portées de ressource.</span><span class="sxs-lookup"><span data-stu-id="3c2cb-106">Just like built-in roles, you can assign custom roles toousers, groups, and applications at subscription, resource group, and resource scopes.</span></span> <span data-ttu-id="3c2cb-107">Les rôles personnalisés sont stockés dans un client Azure AD et peuvent être partagés entre les abonnements.</span><span class="sxs-lookup"><span data-stu-id="3c2cb-107">Custom roles are stored in an Azure AD tenant and can be shared across subscriptions.</span></span>

<span data-ttu-id="3c2cb-108">Chaque client peut créer des rôles personnalisés de too2000.</span><span class="sxs-lookup"><span data-stu-id="3c2cb-108">Each tenant can create up too2000 custom roles.</span></span> 

<span data-ttu-id="3c2cb-109">Hello suivant montre un rôle personnalisé pour la surveillance et le redémarrage des ordinateurs virtuels :</span><span class="sxs-lookup"><span data-stu-id="3c2cb-109">hello following example shows a custom role for monitoring and restarting virtual machines:</span></span>

```
{
  "Name": "Virtual Machine Operator",
  "Id": "cadb4a5a-4e7a-47be-84db-05cad13b6769",
  "IsCustom": true,
  "Description": "Can monitor and restart virtual machines.",
  "Actions": [
    "Microsoft.Storage/*/read",
    "Microsoft.Network/*/read",
    "Microsoft.Compute/*/read",
    "Microsoft.Compute/virtualMachines/start/action",
    "Microsoft.Compute/virtualMachines/restart/action",
    "Microsoft.Authorization/*/read",
    "Microsoft.Resources/subscriptions/resourceGroups/read",
    "Microsoft.Insights/alertRules/*",
    "Microsoft.Insights/diagnosticSettings/*",
    "Microsoft.Support/*"
  ],
  "NotActions": [

  ],
  "AssignableScopes": [
    "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624",
    "/subscriptions/34370e90-ac4a-4bf9-821f-85eeedeae1a2"
  ]
}
```
## <a name="actions"></a><span data-ttu-id="3c2cb-110">Actions</span><span class="sxs-lookup"><span data-stu-id="3c2cb-110">Actions</span></span>
<span data-ttu-id="3c2cb-111">Hello **Actions** propriété d’un rôle personnalisé spécifie hello opérations Azure toowhich hello rôle accorde un accès.</span><span class="sxs-lookup"><span data-stu-id="3c2cb-111">hello **Actions** property of a custom role specifies hello Azure operations toowhich hello role grants access.</span></span> <span data-ttu-id="3c2cb-112">Il s’agit d’un ensemble de chaînes d’opération qui identifient les opérations sécurisables des fournisseurs de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="3c2cb-112">It is a collection of operation strings that identify securable operations of Azure resource providers.</span></span> <span data-ttu-id="3c2cb-113">Chaînes d’opération suivent le format hello `Microsoft.<ProviderName>/<ChildResourceType>/<action>`.</span><span class="sxs-lookup"><span data-stu-id="3c2cb-113">Operation strings follow hello format of `Microsoft.<ProviderName>/<ChildResourceType>/<action>`.</span></span> <span data-ttu-id="3c2cb-114">Chaînes d’opération qui contiennent des caractères génériques (\*) tooall les opérations qui correspondent à la chaîne d’opération hello accorder l’accès.</span><span class="sxs-lookup"><span data-stu-id="3c2cb-114">Operation strings that contain wildcards (\*) grant access tooall operations that match hello operation string.</span></span> <span data-ttu-id="3c2cb-115">Exemple :</span><span class="sxs-lookup"><span data-stu-id="3c2cb-115">For instance:</span></span>

* <span data-ttu-id="3c2cb-116">`*/read`octroie accéder à des opérations de tooread pour tous les types de ressources de tous les fournisseurs de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="3c2cb-116">`*/read` grants access tooread operations for all resource types of all Azure resource providers.</span></span>
* <span data-ttu-id="3c2cb-117">`Microsoft.Compute/*`octroie accéder à des opérations de tooall pour tous les types de ressource dans le fournisseur de ressources Microsoft.Compute hello.</span><span class="sxs-lookup"><span data-stu-id="3c2cb-117">`Microsoft.Compute/*` grants access tooall operations for all resource types in hello Microsoft.Compute resource provider.</span></span>
* <span data-ttu-id="3c2cb-118">`Microsoft.Network/*/read`octroie accéder à des opérations de tooread pour tous les types de ressource dans le fournisseur de ressources Microsoft.Network hello de Azure.</span><span class="sxs-lookup"><span data-stu-id="3c2cb-118">`Microsoft.Network/*/read` grants access tooread operations for all resource types in hello Microsoft.Network resource provider of Azure.</span></span>
* <span data-ttu-id="3c2cb-119">`Microsoft.Compute/virtualMachines/*`octroie accéder à des opérations de tooall des ordinateurs virtuels et de ses types de ressources enfants.</span><span class="sxs-lookup"><span data-stu-id="3c2cb-119">`Microsoft.Compute/virtualMachines/*` grants access tooall operations of virtual machines and its child resource types.</span></span>
* <span data-ttu-id="3c2cb-120">`Microsoft.Web/sites/restart/Action`octroie accéder aux sites Web de toorestart.</span><span class="sxs-lookup"><span data-stu-id="3c2cb-120">`Microsoft.Web/sites/restart/Action` grants access toorestart websites.</span></span>

<span data-ttu-id="3c2cb-121">Utilisez `Get-AzureRmProviderOperation` (dans PowerShell) ou `azure provider operations show` (dans Azure CLI) opérations toolist des fournisseurs de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="3c2cb-121">Use `Get-AzureRmProviderOperation` (in PowerShell) or `azure provider operations show` (in Azure CLI) toolist operations of Azure resource providers.</span></span> <span data-ttu-id="3c2cb-122">Vous pouvez également utiliser ces tooverify commandes qu’une chaîne de l’opération est valide et les chaînes d’opération tooexpand génériques.</span><span class="sxs-lookup"><span data-stu-id="3c2cb-122">You may also use these commands tooverify that an operation string is valid, and tooexpand wildcard operation strings.</span></span>

```
Get-AzureRMProviderOperation Microsoft.Compute/virtualMachines/*/action | FT Operation, OperationName

Get-AzureRMProviderOperation Microsoft.Network/*
```

![Capture d’écran PowerShell - Get-AzureRMProviderOperation](./media/role-based-access-control-configure/1-get-azurermprovideroperation-1.png)

```
azure provider operations show "Microsoft.Compute/virtualMachines/*/action" --js on | jq '.[] | .operation'

azure provider operations show "Microsoft.Network/*"
```

![<span data-ttu-id="3c2cb-124">Capture d’écran de l’interface de ligne de commande Azure ; les opérations du fournisseur azure affichent « Microsoft.Compute/virtualMachines/\*/action »</span><span class="sxs-lookup"><span data-stu-id="3c2cb-124">Azure CLI screenshot - azure provider operations show "Microsoft.Compute/virtualMachines/\*/action"</span></span> ](./media/role-based-access-control-configure/1-azure-provider-operations-show.png)

## <a name="notactions"></a><span data-ttu-id="3c2cb-125">NotActions</span><span class="sxs-lookup"><span data-stu-id="3c2cb-125">NotActions</span></span>
<span data-ttu-id="3c2cb-126">Hello d’utilisation **NotActions** propriété si hello d’opérations que vous souhaitez tooallow plus facilement définie en excluant les opérations restreintes.</span><span class="sxs-lookup"><span data-stu-id="3c2cb-126">Use hello **NotActions** property if hello set of operations that you wish tooallow is more easily defined by excluding restricted operations.</span></span> <span data-ttu-id="3c2cb-127">accès accordé par un rôle personnalisé Hello est calculé en soustrayant hello **NotActions** opérations hello **Actions** operations.</span><span class="sxs-lookup"><span data-stu-id="3c2cb-127">hello access granted by a custom role is computed by subtracting hello **NotActions** operations from hello **Actions** operations.</span></span>

> [!NOTE]
> <span data-ttu-id="3c2cb-128">Si un utilisateur est assigné à un rôle qui exclut une opération dans **NotActions**et est affectée à un second rôle qui accorde l’accès toohello même opération, utilisateur de hello est autorisée tooperform cette opération.</span><span class="sxs-lookup"><span data-stu-id="3c2cb-128">If a user is assigned a role that excludes an operation in **NotActions**, and is assigned a second role that grants access toohello same operation, hello user is allowed tooperform that operation.</span></span> <span data-ttu-id="3c2cb-129">**NotActions** n’est pas une instruction deny de règle : il est simplement un toocreate facilement un ensemble d’opérations autorisées lorsque des opérations spécifiques doivent toobe exclu.</span><span class="sxs-lookup"><span data-stu-id="3c2cb-129">**NotActions** is not a deny rule – it is simply a convenient way toocreate a set of allowed operations when specific operations need toobe excluded.</span></span>
>
>

## <a name="assignablescopes"></a><span data-ttu-id="3c2cb-130">AssignableScopes</span><span class="sxs-lookup"><span data-stu-id="3c2cb-130">AssignableScopes</span></span>
<span data-ttu-id="3c2cb-131">Hello **AssignableScopes** la propriété du rôle personnalisé de hello spécifie étendues hello (des abonnements, des groupes de ressources ou des ressources) au sein de quel hello rôle personnalisé est disponible pour l’attribution.</span><span class="sxs-lookup"><span data-stu-id="3c2cb-131">hello **AssignableScopes** property of hello custom role specifies hello scopes (subscriptions, resource groups, or resources) within which hello custom role is available for assignment.</span></span> <span data-ttu-id="3c2cb-132">Vous pouvez faire de rôle personnalisé hello disponibles pour l’assignation dans uniquement les abonnements hello ou groupes de ressources qui nécessitent et pas l’utilisateur l’encombrement de l’expérience pour rest hello d’abonnements de hello ou des groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="3c2cb-132">You can make hello custom role available for assignment in only hello subscriptions or resource groups that require it, and not clutter user experience for hello rest of hello subscriptions or resource groups.</span></span>

<span data-ttu-id="3c2cb-133">Voici des exemples d’étendues assignables valides :</span><span class="sxs-lookup"><span data-stu-id="3c2cb-133">Examples of valid assignable scopes include:</span></span>

* <span data-ttu-id="3c2cb-134">« / subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e », « / subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624 » - permet de disponible pour l’attribution de rôle de hello dans deux abonnements.</span><span class="sxs-lookup"><span data-stu-id="3c2cb-134">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e”, “/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624” - makes hello role available for assignment in two subscriptions.</span></span>
* <span data-ttu-id="3c2cb-135">« / subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e » - permet de disponible pour l’attribution de rôle de hello dans un seul abonnement.</span><span class="sxs-lookup"><span data-stu-id="3c2cb-135">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e” - makes hello role available for assignment in a single subscription.</span></span>
* <span data-ttu-id="3c2cb-136">« / abonnements/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/réseau » - rend hello rôle disponible pour l’assignation uniquement dans le groupe de ressources réseau hello.</span><span class="sxs-lookup"><span data-stu-id="3c2cb-136">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network” - makes hello role available for assignment only in hello Network resource group.</span></span>

> [!NOTE]
> <span data-ttu-id="3c2cb-137">Vous devez utiliser au moins un abonnement, groupe de ressources ou ID de ressource.</span><span class="sxs-lookup"><span data-stu-id="3c2cb-137">You must use at least one subscription, resource group, or resource ID.</span></span>
>
>

## <a name="custom-roles-access-control"></a><span data-ttu-id="3c2cb-138">Contrôle d’accès des rôles personnalisés</span><span class="sxs-lookup"><span data-stu-id="3c2cb-138">Custom roles access control</span></span>
<span data-ttu-id="3c2cb-139">Hello **AssignableScopes** la propriété du rôle personnalisé de hello contrôle également qui peut afficher, modifier et supprimer le rôle de hello.</span><span class="sxs-lookup"><span data-stu-id="3c2cb-139">hello **AssignableScopes** property of hello custom role also controls who can view, modify, and delete hello role.</span></span>

* <span data-ttu-id="3c2cb-140">Qui peut créer un rôle personnalisé ?</span><span class="sxs-lookup"><span data-stu-id="3c2cb-140">Who can create a custom role?</span></span>
    <span data-ttu-id="3c2cb-141">Les propriétaires (et les administrateurs de l’accès utilisateur) d’abonnements, de groupes de ressources et de ressources peuvent créer des rôles personnalisés utilisables au sein de ces étendues.</span><span class="sxs-lookup"><span data-stu-id="3c2cb-141">Owners (and User Access Administrators) of subscriptions, resource groups, and resources can create custom roles for use in those scopes.</span></span>
    <span data-ttu-id="3c2cb-142">utilisateur qui crée le rôle de hello Hello doit tooperform en mesure de toobe `Microsoft.Authorization/roleDefinition/write` opération sur tous les hello **AssignableScopes** du rôle de hello.</span><span class="sxs-lookup"><span data-stu-id="3c2cb-142">hello user creating hello role needs toobe able tooperform `Microsoft.Authorization/roleDefinition/write` operation on all hello **AssignableScopes** of hello role.</span></span>
* <span data-ttu-id="3c2cb-143">Qui peut modifier un rôle personnalisé ?</span><span class="sxs-lookup"><span data-stu-id="3c2cb-143">Who can modify a custom role?</span></span>
    <span data-ttu-id="3c2cb-144">Les propriétaires (et les administrateurs de l’accès utilisateur) d’abonnements, de groupes de ressources et de ressources peuvent modifier des rôles personnalisés au sein de ces étendues.</span><span class="sxs-lookup"><span data-stu-id="3c2cb-144">Owners (and User Access Administrators) of subscriptions, resource groups, and resources can modify custom roles in those scopes.</span></span> <span data-ttu-id="3c2cb-145">Les utilisateurs doivent toobe tooperform en mesure de hello `Microsoft.Authorization/roleDefinition/write` opération sur tous les hello **AssignableScopes** d’un rôle personnalisé.</span><span class="sxs-lookup"><span data-stu-id="3c2cb-145">Users need toobe able tooperform hello `Microsoft.Authorization/roleDefinition/write` operation on all hello **AssignableScopes** of a custom role.</span></span>
* <span data-ttu-id="3c2cb-146">Qui peut afficher des rôles personnalisés ?</span><span class="sxs-lookup"><span data-stu-id="3c2cb-146">Who can view custom roles?</span></span>
    <span data-ttu-id="3c2cb-147">Tous les rôles intégrés dans le contrôle d’accès en fonction du rôle Azure permettent d’afficher les rôles pouvant être affectés.</span><span class="sxs-lookup"><span data-stu-id="3c2cb-147">All built-in roles in Azure RBAC allow viewing of roles that are available for assignment.</span></span> <span data-ttu-id="3c2cb-148">Les utilisateurs qui peuvent effectuer hello `Microsoft.Authorization/roleDefinition/read` opération sur une étendue peut afficher rôles RBAC hello qui sont disponibles pour l’assignation dans cette portée.</span><span class="sxs-lookup"><span data-stu-id="3c2cb-148">Users who can perform hello `Microsoft.Authorization/roleDefinition/read` operation at a scope can view hello RBAC roles that are available for assignment at that scope.</span></span>

## <a name="see-also"></a><span data-ttu-id="3c2cb-149">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="3c2cb-149">See also</span></span>
* <span data-ttu-id="3c2cb-150">[Contrôle d’accès basé sur rôle](role-based-access-control-configure.md): prise en main RBAC Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3c2cb-150">[Role Based Access Control](role-based-access-control-configure.md): Get started with RBAC in hello Azure portal.</span></span>
* <span data-ttu-id="3c2cb-151">Découvrez comment accéder à toomanage avec :</span><span class="sxs-lookup"><span data-stu-id="3c2cb-151">Learn how toomanage access with:</span></span>
  * [<span data-ttu-id="3c2cb-152">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3c2cb-152">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
  * [<span data-ttu-id="3c2cb-153">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="3c2cb-153">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
  * [<span data-ttu-id="3c2cb-154">API REST</span><span class="sxs-lookup"><span data-stu-id="3c2cb-154">REST API</span></span>](role-based-access-control-manage-access-rest.md)
* <span data-ttu-id="3c2cb-155">[Rôles intégrés](role-based-access-built-in-roles.md): obtenir des informations sur les rôles hello livrés dans RBAC.</span><span class="sxs-lookup"><span data-stu-id="3c2cb-155">[Built-in roles](role-based-access-built-in-roles.md): Get details about hello roles that come standard in RBAC.</span></span>
