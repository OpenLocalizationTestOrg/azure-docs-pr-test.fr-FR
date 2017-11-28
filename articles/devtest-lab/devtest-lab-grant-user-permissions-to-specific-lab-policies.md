---
title: "stratégies de laboratoire aaaGrant utilisateur autorisations toospecific | Documents Microsoft"
description: "Découvrez comment les stratégies toogrant utilisateur autorisations toospecific lab dans DevTest Labs en fonction des besoins de chaque utilisateur"
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
ms.openlocfilehash: 35647ab837243188f06566cdf365b67fe33a3865
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="grant-user-permissions-toospecific-lab-policies"></a><span data-ttu-id="4ae98-103">Accorder des autorisations utilisateur toospecific des stratégies de laboratoire</span><span class="sxs-lookup"><span data-stu-id="4ae98-103">Grant user permissions toospecific lab policies</span></span>
## <a name="overview"></a><span data-ttu-id="4ae98-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="4ae98-104">Overview</span></span>
<span data-ttu-id="4ae98-105">Cet article explique comment toouse stratégie de PowerShell toogrant utilisateurs autorisations tooa lab particulier.</span><span class="sxs-lookup"><span data-stu-id="4ae98-105">This article illustrates how toouse PowerShell toogrant users permissions tooa particular lab policy.</span></span> <span data-ttu-id="4ae98-106">De cette façon, les autorisations peuvent être appliquées selon les besoins de chaque utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4ae98-106">That way, permissions can be applied based on each user's needs.</span></span> <span data-ttu-id="4ae98-107">Par exemple, vous pourriez toogrant un paramètre de stratégie utilisateur particulier hello hello capacité toochange machine virtuelle, mais pas hello coût des stratégies.</span><span class="sxs-lookup"><span data-stu-id="4ae98-107">For example, you might want toogrant a particular user hello ability toochange hello VM policy settings, but not hello cost policies.</span></span>

## <a name="policies-as-resources"></a><span data-ttu-id="4ae98-108">Stratégies en tant que ressources</span><span class="sxs-lookup"><span data-stu-id="4ae98-108">Policies as resources</span></span>
<span data-ttu-id="4ae98-109">Comme indiqué dans hello [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md) article, RBAC permet la gestion accès affiné des ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="4ae98-109">As discussed in hello [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md) article, RBAC enables fine-grained access management of resources for Azure.</span></span> <span data-ttu-id="4ae98-110">À l’aide de RBAC, vous pouvez séparer les droits au sein de votre équipe DevOps et accorder uniquement hello quantité toousers d’accès dont ils ont besoin tooperform leur travail.</span><span class="sxs-lookup"><span data-stu-id="4ae98-110">Using RBAC, you can segregate duties within your DevOps team and grant only hello amount of access toousers that they need tooperform their jobs.</span></span>

<span data-ttu-id="4ae98-111">Dans DevTest Labs, une stratégie est un type de ressource qui permet l’action de RBAC hello **Microsoft.DevTestLab/labs/policySets/policies/**.</span><span class="sxs-lookup"><span data-stu-id="4ae98-111">In DevTest Labs, a policy is a resource type that enables hello RBAC action **Microsoft.DevTestLab/labs/policySets/policies/**.</span></span> <span data-ttu-id="4ae98-112">Chaque stratégie lab est une ressource de type de ressource de stratégie de hello et peut être affecté comme un rôle RBAC tooan étendue.</span><span class="sxs-lookup"><span data-stu-id="4ae98-112">Each lab policy is a resource in hello Policy resource type, and can be assigned as a scope tooan RBAC role.</span></span>

<span data-ttu-id="4ae98-113">Par exemple, dans l’ordre toogrant les utilisateurs en lecture/écriture autorisation toohello **autorisé des tailles de machine virtuelle** stratégie, vous devez créer un rôle personnalisé qui fonctionne avec hello **Microsoft.DevTestLab/labs/policySets/policies/** * action et puis affecter hello utilisateurs appropriés toothis personnalisé rôle dans la portée de hello de **Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**.</span><span class="sxs-lookup"><span data-stu-id="4ae98-113">For example, in order toogrant users read/write permission toohello **Allowed VM Sizes** policy, you would create a custom role that works with hello **Microsoft.DevTestLab/labs/policySets/policies/*** action, and then assign hello appropriate users toothis custom role in hello scope of **Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**.</span></span>

<span data-ttu-id="4ae98-114">toolearn savoir plus sur les rôles personnalisés dans RBAC, consultez hello [rôles de personnaliser le contrôle d’accès](../active-directory/role-based-access-control-custom-roles.md).</span><span class="sxs-lookup"><span data-stu-id="4ae98-114">toolearn more about custom roles in RBAC, see hello [Custom roles access control](../active-directory/role-based-access-control-custom-roles.md).</span></span>

## <a name="creating-a-lab-custom-role-using-powershell"></a><span data-ttu-id="4ae98-115">Création d’un rôle personnalisé de laboratoire en utilisant PowerShell</span><span class="sxs-lookup"><span data-stu-id="4ae98-115">Creating a lab custom role using PowerShell</span></span>
<span data-ttu-id="4ae98-116">Tooget commande a démarré, vous devez hello tooread suivant l’article, qui explique comment tooinstall et configurer les applets de commande PowerShell Azure hello : [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre).</span><span class="sxs-lookup"><span data-stu-id="4ae98-116">In order tooget started, you’ll need tooread hello following article, which will explain how tooinstall and configure hello Azure PowerShell cmdlets: [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre).</span></span>

<span data-ttu-id="4ae98-117">Une fois que vous avez configuré hello applets de commande PowerShell de Azure, vous pouvez effectuer hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="4ae98-117">Once you’ve set up hello Azure PowerShell cmdlets, you can perform hello following tasks:</span></span>

* <span data-ttu-id="4ae98-118">Liste de toutes les opérations de hello/actions pour un fournisseur de ressources</span><span class="sxs-lookup"><span data-stu-id="4ae98-118">List all hello operations/actions for a resource provider</span></span>
* <span data-ttu-id="4ae98-119">Répertorier les actions d’un rôle particulier :</span><span class="sxs-lookup"><span data-stu-id="4ae98-119">List actions in a particular role:</span></span>
* <span data-ttu-id="4ae98-120">Créer un rôle personnalisé</span><span class="sxs-lookup"><span data-stu-id="4ae98-120">Create a custom role</span></span>

<span data-ttu-id="4ae98-121">Hello PowerShell script suivant illustre des exemples de tooperform ces tâches :</span><span class="sxs-lookup"><span data-stu-id="4ae98-121">hello following PowerShell script illustrates examples of how tooperform these tasks:</span></span>

    ‘List all hello operations/actions for a resource provider.
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

## <a name="assigning-permissions-tooa-user-for-a-specific-policy-using-custom-roles"></a><span data-ttu-id="4ae98-122">Affectation d’autorisations tooa utilisateur pour une stratégie spécifique à l’aide de rôles personnalisés</span><span class="sxs-lookup"><span data-stu-id="4ae98-122">Assigning permissions tooa user for a specific policy using custom roles</span></span>
<span data-ttu-id="4ae98-123">Une fois que vous avez défini vos rôles personnalisés, vous pouvez les affecter toousers.</span><span class="sxs-lookup"><span data-stu-id="4ae98-123">Once you’ve defined your custom roles, you can assign them toousers.</span></span> <span data-ttu-id="4ae98-124">Dans l’ordre tooassign un utilisateur tooa de rôle personnalisé, vous devez d’abord obtenir hello **ObjectId** représentant cet utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4ae98-124">In order tooassign a custom role tooa user, you must first obtain hello **ObjectId** representing that user.</span></span> <span data-ttu-id="4ae98-125">toodo qui, utilisez hello **Get-AzureRmADUser** applet de commande.</span><span class="sxs-lookup"><span data-stu-id="4ae98-125">toodo that, use hello **Get-AzureRmADUser** cmdlet.</span></span>

<span data-ttu-id="4ae98-126">Dans l’exemple suivant de hello, hello **ObjectId** Hello *SomeUser* utilisateur est 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3.</span><span class="sxs-lookup"><span data-stu-id="4ae98-126">In hello following example, hello **ObjectId** of hello *SomeUser* user is 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3.</span></span>

    PS C:\>Get-AzureRmADUser -SearchString "SomeUser"

    DisplayName                    Type                           ObjectId
    -----------                    ----                           --------
    someuser@hotmail.com                                          05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3

<span data-ttu-id="4ae98-127">Une fois que vous avez hello **ObjectId** pour l’utilisateur de hello et un nom de rôle personnalisé, vous pouvez l’affecter rôle toohello avec hello **New-AzureRmRoleAssignment** applet de commande :</span><span class="sxs-lookup"><span data-stu-id="4ae98-127">Once you have hello **ObjectId** for hello user and a custom role name, you can assign that role toohello user with hello **New-AzureRmRoleAssignment** cmdlet:</span></span>

    PS C:\>New-AzureRmRoleAssignment -ObjectId 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3 -RoleDefinitionName "Policy Contributor" -Scope /subscriptions/<SubscriptionID>/resourceGroups/<ResourceGroupName>/providers/Microsoft.DevTestLab/labs/<LabName>/policySets/policies/AllowedVmSizesInLab

<span data-ttu-id="4ae98-128">Dans l’exemple précédent de hello, hello **AllowedVmSizesInLab** stratégie est utilisée.</span><span class="sxs-lookup"><span data-stu-id="4ae98-128">In hello previous example, hello **AllowedVmSizesInLab** policy is used.</span></span> <span data-ttu-id="4ae98-129">Vous pouvez utiliser un des hello les stratégies suivantes :</span><span class="sxs-lookup"><span data-stu-id="4ae98-129">You can use any of hello following polices:</span></span>

* <span data-ttu-id="4ae98-130">MaxVmsAllowedPerUser</span><span class="sxs-lookup"><span data-stu-id="4ae98-130">MaxVmsAllowedPerUser</span></span>
* <span data-ttu-id="4ae98-131">MaxVmsAllowedPerLab</span><span class="sxs-lookup"><span data-stu-id="4ae98-131">MaxVmsAllowedPerLab</span></span>
* <span data-ttu-id="4ae98-132">AllowedVmSizesInLab</span><span class="sxs-lookup"><span data-stu-id="4ae98-132">AllowedVmSizesInLab</span></span>
* <span data-ttu-id="4ae98-133">LabVmsShutdown</span><span class="sxs-lookup"><span data-stu-id="4ae98-133">LabVmsShutdown</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="4ae98-134">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4ae98-134">Next steps</span></span>
<span data-ttu-id="4ae98-135">Une fois vous avez accordé des stratégies de laboratoire autorisations toospecific utilisateur, Voici certains tooconsider étapes suivant :</span><span class="sxs-lookup"><span data-stu-id="4ae98-135">Once you've granted user permissions toospecific lab policies, here are some next steps tooconsider:</span></span>

* <span data-ttu-id="4ae98-136">[Laboratoire tooa de sécuriser l’accès](devtest-lab-add-devtest-user.md).</span><span class="sxs-lookup"><span data-stu-id="4ae98-136">[Secure access tooa lab](devtest-lab-add-devtest-user.md).</span></span>
* <span data-ttu-id="4ae98-137">[Définir des stratégies de laboratoire](devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="4ae98-137">[Set lab policies](devtest-lab-set-lab-policy.md).</span></span>
* <span data-ttu-id="4ae98-138">[Créer un modèle de laboratoire](devtest-lab-create-template.md).</span><span class="sxs-lookup"><span data-stu-id="4ae98-138">[Create a lab template](devtest-lab-create-template.md).</span></span>
* <span data-ttu-id="4ae98-139">[Créer des artefacts personnalisés pour vos machines virtuelles](devtest-lab-artifact-author.md).</span><span class="sxs-lookup"><span data-stu-id="4ae98-139">[Create custom artifacts for your VMs](devtest-lab-artifact-author.md).</span></span>
* <span data-ttu-id="4ae98-140">[Ajouter une machine virtuelle avec lab de tooa artefacts](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="4ae98-140">[Add a VM with artifacts tooa lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

