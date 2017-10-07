---
title: "Accorder des autorisations à des utilisateurs sur des stratégies de laboratoire spécifiques | Microsoft Docs"
description: "Découvrez comment accorder des autorisations aux utilisateurs sur des stratégies de laboratoire spécifique dans DevTest Labs selon les besoins de chaque utilisateur"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 5ca829f0-eb69-40a1-ae26-03a629db1d7e
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: 0bd9f83257834d9681479ba9117c48ffd6d6e166
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="grant-user-permissions-to-specific-lab-policies"></a><span data-ttu-id="48ae5-103">Accorder des autorisations à des utilisateurs sur des stratégies de laboratoire spécifiques</span><span class="sxs-lookup"><span data-stu-id="48ae5-103">Grant user permissions to specific lab policies</span></span>
## <a name="overview"></a><span data-ttu-id="48ae5-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="48ae5-104">Overview</span></span>
<span data-ttu-id="48ae5-105">Cet article explique comment utiliser PowerShell pour accorder à des utilisateurs des autorisations sur une stratégie de laboratoire particulière.</span><span class="sxs-lookup"><span data-stu-id="48ae5-105">This article illustrates how to use PowerShell to grant users permissions to a particular lab policy.</span></span> <span data-ttu-id="48ae5-106">De cette façon, les autorisations peuvent être appliquées selon les besoins de chaque utilisateur.</span><span class="sxs-lookup"><span data-stu-id="48ae5-106">That way, permissions can be applied based on each user's needs.</span></span> <span data-ttu-id="48ae5-107">Par exemple, vous pouvez accorder à un utilisateur la possibilité de modifier les paramètres de stratégie d’une machine virtuelle, mais pas les stratégies de coût.</span><span class="sxs-lookup"><span data-stu-id="48ae5-107">For example, you might want to grant a particular user the ability to change the VM policy settings, but not the cost policies.</span></span>

## <a name="policies-as-resources"></a><span data-ttu-id="48ae5-108">Stratégies en tant que ressources</span><span class="sxs-lookup"><span data-stu-id="48ae5-108">Policies as resources</span></span>
<span data-ttu-id="48ae5-109">Comme expliqué dans l’article [Contrôle d’accès en fonction du rôle Azure](../active-directory/role-based-access-control-configure.md) , RBAC permet une gestion précise de l’accès aux ressources pour Azure.</span><span class="sxs-lookup"><span data-stu-id="48ae5-109">As discussed in the [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md) article, RBAC enables fine-grained access management of resources for Azure.</span></span> <span data-ttu-id="48ae5-110">Avec le contrôle d’accès en fonction du rôle, vous pouvez séparer les tâches au sein de votre équipe chargée des opérations de développement et accorder aux utilisateurs uniquement les accès nécessaires pour accomplir leur travail.</span><span class="sxs-lookup"><span data-stu-id="48ae5-110">Using RBAC, you can segregate duties within your DevOps team and grant only the amount of access to users that they need to perform their jobs.</span></span>

<span data-ttu-id="48ae5-111">Dans DevTest Labs, une stratégie est un type de ressource qui active l’action RBAC **Microsoft.DevTestLab/labs/policySets/policies/**.</span><span class="sxs-lookup"><span data-stu-id="48ae5-111">In DevTest Labs, a policy is a resource type that enables the RBAC action **Microsoft.DevTestLab/labs/policySets/policies/**.</span></span> <span data-ttu-id="48ae5-112">Chaque stratégie de laboratoire est une ressource de type stratégie et peut être affectée comme étendue à un rôle RBAC.</span><span class="sxs-lookup"><span data-stu-id="48ae5-112">Each lab policy is a resource in the Policy resource type, and can be assigned as a scope to an RBAC role.</span></span>

<span data-ttu-id="48ae5-113">Par exemple, pour accorder l’autorisation de lecture/écriture aux utilisateurs la **autorisé des tailles de machine virtuelle** stratégie, vous devez créer un rôle personnalisé qui fonctionne avec les **Microsoft.DevTestLab/labs/policySets/policies/*** action et ensuite affecter les utilisateurs appropriés à ce rôle personnalisé dans l’étendue de **Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**.</span><span class="sxs-lookup"><span data-stu-id="48ae5-113">For example, in order to grant users read/write permission to the **Allowed VM Sizes** policy, you would create a custom role that works with the **Microsoft.DevTestLab/labs/policySets/policies/*** action, and then assign the appropriate users to this custom role in the scope of **Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**.</span></span>

<span data-ttu-id="48ae5-114">Pour en savoir plus sur les rôles personnalisés dans RBAC, consultez [Contrôle d’accès des rôles personnalisés](../active-directory/role-based-access-control-custom-roles.md).</span><span class="sxs-lookup"><span data-stu-id="48ae5-114">To learn more about custom roles in RBAC, see the [Custom roles access control](../active-directory/role-based-access-control-custom-roles.md).</span></span>

## <a name="creating-a-lab-custom-role-using-powershell"></a><span data-ttu-id="48ae5-115">Création d’un rôle personnalisé de laboratoire en utilisant PowerShell</span><span class="sxs-lookup"><span data-stu-id="48ae5-115">Creating a lab custom role using PowerShell</span></span>
<span data-ttu-id="48ae5-116">Pour commencer, vous devez lire l’article suivant, qui explique comment installer et configurer les applets de commande Azure PowerShell : [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre).</span><span class="sxs-lookup"><span data-stu-id="48ae5-116">In order to get started, you’ll need to read the following article, which will explain how to install and configure the Azure PowerShell cmdlets: [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre).</span></span>

<span data-ttu-id="48ae5-117">Une fois que vous avez configuré les applets de commande Azure PowerShell, vous pouvez effectuer les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="48ae5-117">Once you’ve set up the Azure PowerShell cmdlets, you can perform the following tasks:</span></span>

* <span data-ttu-id="48ae5-118">Répertorier toutes les opérations/actions d’un fournisseur de ressources</span><span class="sxs-lookup"><span data-stu-id="48ae5-118">List all the operations/actions for a resource provider</span></span>
* <span data-ttu-id="48ae5-119">Répertorier les actions d’un rôle particulier :</span><span class="sxs-lookup"><span data-stu-id="48ae5-119">List actions in a particular role:</span></span>
* <span data-ttu-id="48ae5-120">Créer un rôle personnalisé</span><span class="sxs-lookup"><span data-stu-id="48ae5-120">Create a custom role</span></span>

<span data-ttu-id="48ae5-121">Le script PowerShell suivant montre des exemples permettant d’effectuer ces tâches :</span><span class="sxs-lookup"><span data-stu-id="48ae5-121">The following PowerShell script illustrates examples of how to perform these tasks:</span></span>

    ‘List all the operations/actions for a resource provider.
    Get-AzureRmProviderOperation -OperationSearchString "Microsoft.DevTestLab/*"

    ‘List actions in a particular role.
    (Get-AzureRmRoleDefinition "DevTest Labs User").Actions

    ‘Create custom role.
    $policyRoleDef = (Get-AzureRmRoleDefinition "DevTest Labs User")
    $policyRoleDef.Id = $null
    $policyRoleDef.Name = "Policy Contributor"
    $policyRoleDef.IsCustom = $true
    $policyRoleDef.AssignableScopes.Clear()
    $policyRoleDef.AssignableScopes.Add("/subscriptions/<SubscriptionID> ")
    $policyRoleDef.Actions.Add("Microsoft.DevTestLab/labs/policySets/policies/*")
    $policyRoleDef = (New-AzureRmRoleDefinition -Role $policyRoleDef)

## <a name="assigning-permissions-to-a-user-for-a-specific-policy-using-custom-roles"></a><span data-ttu-id="48ae5-122">Attribution d'autorisations à un utilisateur pour une stratégie spécifique à l'aide de rôles personnalisés</span><span class="sxs-lookup"><span data-stu-id="48ae5-122">Assigning permissions to a user for a specific policy using custom roles</span></span>
<span data-ttu-id="48ae5-123">Une fois que vous avez défini vos rôles personnalisés, vous pouvez les attribuer aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="48ae5-123">Once you’ve defined your custom roles, you can assign them to users.</span></span> <span data-ttu-id="48ae5-124">Pour affecter un rôle personnalisé à un utilisateur, vous devez d’abord obtenir **l’ObjectId** représentant cet utilisateur.</span><span class="sxs-lookup"><span data-stu-id="48ae5-124">In order to assign a custom role to a user, you must first obtain the **ObjectId** representing that user.</span></span> <span data-ttu-id="48ae5-125">Pour cela, utilisez l’applet de commande **Get-AzureRmADUser** .</span><span class="sxs-lookup"><span data-stu-id="48ae5-125">To do that, use the **Get-AzureRmADUser** cmdlet.</span></span>

<span data-ttu-id="48ae5-126">Dans l’exemple suivant, **l’ObjectId** de l’utilisateur *SomeUser* est 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3.</span><span class="sxs-lookup"><span data-stu-id="48ae5-126">In the following example, the **ObjectId** of the *SomeUser* user is 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3.</span></span>

    PS C:\>Get-AzureRmADUser -SearchString "SomeUser"

    DisplayName                    Type                           ObjectId
    -----------                    ----                           --------
    someuser@hotmail.com                                          05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3

<span data-ttu-id="48ae5-127">Une fois que vous disposez de **l’ObjectId** de l’utilisateur et d’un nom de rôle personnalisé, vous pouvez affecter ce rôle à l’utilisateur avec l’applet de commande **New-AzureRmRoleAssignment** :</span><span class="sxs-lookup"><span data-stu-id="48ae5-127">Once you have the **ObjectId** for the user and a custom role name, you can assign that role to the user with the **New-AzureRmRoleAssignment** cmdlet:</span></span>

    PS C:\>New-AzureRmRoleAssignment -ObjectId 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3 -RoleDefinitionName "Policy Contributor" -Scope /subscriptions/<SubscriptionID>/resourceGroups/<ResourceGroupName>/providers/Microsoft.DevTestLab/labs/<LabName>/policySets/policies/AllowedVmSizesInLab

<span data-ttu-id="48ae5-128">Dans l’exemple précédent, la stratégie **AllowedVmSizesInLab** est utilisée.</span><span class="sxs-lookup"><span data-stu-id="48ae5-128">In the previous example, the **AllowedVmSizesInLab** policy is used.</span></span> <span data-ttu-id="48ae5-129">Vous pouvez utiliser une des stratégies suivantes :</span><span class="sxs-lookup"><span data-stu-id="48ae5-129">You can use any of the following polices:</span></span>

* <span data-ttu-id="48ae5-130">MaxVmsAllowedPerUser</span><span class="sxs-lookup"><span data-stu-id="48ae5-130">MaxVmsAllowedPerUser</span></span>
* <span data-ttu-id="48ae5-131">MaxVmsAllowedPerLab</span><span class="sxs-lookup"><span data-stu-id="48ae5-131">MaxVmsAllowedPerLab</span></span>
* <span data-ttu-id="48ae5-132">AllowedVmSizesInLab</span><span class="sxs-lookup"><span data-stu-id="48ae5-132">AllowedVmSizesInLab</span></span>
* <span data-ttu-id="48ae5-133">LabVmsShutdown</span><span class="sxs-lookup"><span data-stu-id="48ae5-133">LabVmsShutdown</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="48ae5-134">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="48ae5-134">Next steps</span></span>
<span data-ttu-id="48ae5-135">Après avoir accordé aux utilisateurs des autorisations sur des stratégies de laboratoire spécifiques, voici des étapes à prendre en compte :</span><span class="sxs-lookup"><span data-stu-id="48ae5-135">Once you've granted user permissions to specific lab policies, here are some next steps to consider:</span></span>

* <span data-ttu-id="48ae5-136">[Sécuriser l’accès à un laboratoire](devtest-lab-add-devtest-user.md).</span><span class="sxs-lookup"><span data-stu-id="48ae5-136">[Secure access to a lab](devtest-lab-add-devtest-user.md).</span></span>
* <span data-ttu-id="48ae5-137">[Définir des stratégies de laboratoire](devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="48ae5-137">[Set lab policies](devtest-lab-set-lab-policy.md).</span></span>
* <span data-ttu-id="48ae5-138">[Créer un modèle de laboratoire](devtest-lab-create-template.md).</span><span class="sxs-lookup"><span data-stu-id="48ae5-138">[Create a lab template](devtest-lab-create-template.md).</span></span>
* <span data-ttu-id="48ae5-139">[Créer des artefacts personnalisés pour vos machines virtuelles](devtest-lab-artifact-author.md).</span><span class="sxs-lookup"><span data-stu-id="48ae5-139">[Create custom artifacts for your VMs](devtest-lab-artifact-author.md).</span></span>
* <span data-ttu-id="48ae5-140">[Ajouter une machine virtuelle avec des artefacts à un laboratoire](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="48ae5-140">[Add a VM with artifacts to a lab](devtest-lab-add-vm-with-artifacts.md).</span></span>
