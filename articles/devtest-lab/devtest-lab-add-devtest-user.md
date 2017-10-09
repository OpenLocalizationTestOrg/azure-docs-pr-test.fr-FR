---
title: "aaaAdd propriétaires et les utilisateurs dans Azure DevTest Labs | Documents Microsoft"
description: "Ajouter des propriétaires et les utilisateurs dans Azure DevTest Labs, à l’aide de hello portail Azure ou PowerShell"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 4f51d9a5-2702-45f0-a2d5-a3635b58c416
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: tarcher
ms.openlocfilehash: 2a98f5fe1efbd7c23e0d97f58f47c37462aed3b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-owners-and-users-in-azure-devtest-labs"></a><span data-ttu-id="3ffd7-103">Ajouter des propriétaires et des utilisateurs dans Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="3ffd7-103">Add owners and users in Azure DevTest Labs</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/How-to-set-security-in-your-DevTest-Lab/player]
> 
> 

<span data-ttu-id="3ffd7-104">L’accès à Azure DevTest Labs est contrôlé par le [contrôle d’accès en fonction du rôle (RBAC) Azure](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="3ffd7-104">Access in Azure DevTest Labs is controlled by [Azure Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-what-is.md).</span></span> <span data-ttu-id="3ffd7-105">À l’aide de RBAC, vous pouvez séparer les droits au sein de votre équipe dans *rôles* où vous quantité d’allocation uniquement hello d’accès nécessaires toousers tooperform leur travail.</span><span class="sxs-lookup"><span data-stu-id="3ffd7-105">Using RBAC, you can segregate duties within your team into *roles* where you grant only hello amount of access necessary toousers tooperform their jobs.</span></span> <span data-ttu-id="3ffd7-106">Trois de ces rôles RBAC sont *Propriétaire*, *Utilisateur de DevTest Labs* et *Collaborateur*.</span><span class="sxs-lookup"><span data-stu-id="3ffd7-106">Three of these RBAC roles are *Owner*, *DevTest Labs User*, and *Contributor*.</span></span> <span data-ttu-id="3ffd7-107">Dans cet article, vous Découvrez quelles actions peuvent être effectuées dans chacun des trois rôles RBAC principales hello.</span><span class="sxs-lookup"><span data-stu-id="3ffd7-107">In this article, you learn what actions can be performed in each of hello three main RBAC roles.</span></span> <span data-ttu-id="3ffd7-108">À partir de là, vous apprendrez comment atelier de tooa tooadd utilisateurs : les deux via hello portail et via un script PowerShell et comment les utilisateurs tooadd à hello niveau d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="3ffd7-108">From there, you learn how tooadd users tooa lab - both via hello portal and via a PowerShell script, and how tooadd users at hello subscription level.</span></span>

## <a name="actions-that-can-be-performed-in-each-role"></a><span data-ttu-id="3ffd7-109">Actions qui peuvent être effectuées dans chaque rôle</span><span class="sxs-lookup"><span data-stu-id="3ffd7-109">Actions that can be performed in each role</span></span>
<span data-ttu-id="3ffd7-110">Il existe trois rôles principaux que vous pouvez attribuer à un utilisateur :</span><span class="sxs-lookup"><span data-stu-id="3ffd7-110">There are three main roles that you can assign a user:</span></span>

* <span data-ttu-id="3ffd7-111">Propriétaire</span><span class="sxs-lookup"><span data-stu-id="3ffd7-111">Owner</span></span>
* <span data-ttu-id="3ffd7-112">Utilisateur de DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="3ffd7-112">DevTest Labs User</span></span>
* <span data-ttu-id="3ffd7-113">Collaborateur</span><span class="sxs-lookup"><span data-stu-id="3ffd7-113">Contributor</span></span>

<span data-ttu-id="3ffd7-114">Hello tableau suivant décrit les actions hello qui peuvent être effectuées par les utilisateurs dans chacun de ces rôles :</span><span class="sxs-lookup"><span data-stu-id="3ffd7-114">hello following table illustrates hello actions that can be performed by users in each of these roles:</span></span>

| <span data-ttu-id="3ffd7-115">**Actions que les utilisateurs dans ce rôle peuvent effectuer**</span><span class="sxs-lookup"><span data-stu-id="3ffd7-115">**Actions users in this role can perform**</span></span> | <span data-ttu-id="3ffd7-116">**Utilisateur de DevTest Labs**</span><span class="sxs-lookup"><span data-stu-id="3ffd7-116">**DevTest Labs User**</span></span> | <span data-ttu-id="3ffd7-117">**Propriétaire**</span><span class="sxs-lookup"><span data-stu-id="3ffd7-117">**Owner**</span></span> | <span data-ttu-id="3ffd7-118">**Collaborateur**</span><span class="sxs-lookup"><span data-stu-id="3ffd7-118">**Contributor**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3ffd7-119">**Tâches de laboratoire**</span><span class="sxs-lookup"><span data-stu-id="3ffd7-119">**Lab tasks**</span></span> | | | |
| <span data-ttu-id="3ffd7-120">Ajouter le laboratoire de tooa utilisateurs</span><span class="sxs-lookup"><span data-stu-id="3ffd7-120">Add users tooa lab</span></span> |<span data-ttu-id="3ffd7-121">Non</span><span class="sxs-lookup"><span data-stu-id="3ffd7-121">No</span></span> |<span data-ttu-id="3ffd7-122">Oui</span><span class="sxs-lookup"><span data-stu-id="3ffd7-122">Yes</span></span> |<span data-ttu-id="3ffd7-123">Non</span><span class="sxs-lookup"><span data-stu-id="3ffd7-123">No</span></span> |
| <span data-ttu-id="3ffd7-124">Mettre à jour les paramètres de coût</span><span class="sxs-lookup"><span data-stu-id="3ffd7-124">Update cost settings</span></span> |<span data-ttu-id="3ffd7-125">Non</span><span class="sxs-lookup"><span data-stu-id="3ffd7-125">No</span></span> |<span data-ttu-id="3ffd7-126">Oui</span><span class="sxs-lookup"><span data-stu-id="3ffd7-126">Yes</span></span> |<span data-ttu-id="3ffd7-127">Oui</span><span class="sxs-lookup"><span data-stu-id="3ffd7-127">Yes</span></span> |
| <span data-ttu-id="3ffd7-128">**Tâches de base de machine virtuelle**</span><span class="sxs-lookup"><span data-stu-id="3ffd7-128">**VM base tasks**</span></span> | | | |
| <span data-ttu-id="3ffd7-129">Ajouter et supprimer des images personnalisées</span><span class="sxs-lookup"><span data-stu-id="3ffd7-129">Add and remove custom images</span></span> |<span data-ttu-id="3ffd7-130">Non</span><span class="sxs-lookup"><span data-stu-id="3ffd7-130">No</span></span> |<span data-ttu-id="3ffd7-131">Oui</span><span class="sxs-lookup"><span data-stu-id="3ffd7-131">Yes</span></span> |<span data-ttu-id="3ffd7-132">Oui</span><span class="sxs-lookup"><span data-stu-id="3ffd7-132">Yes</span></span> |
| <span data-ttu-id="3ffd7-133">Ajouter, mettre à jour et supprimer des formules</span><span class="sxs-lookup"><span data-stu-id="3ffd7-133">Add, update, and delete formulas</span></span> |<span data-ttu-id="3ffd7-134">Oui</span><span class="sxs-lookup"><span data-stu-id="3ffd7-134">Yes</span></span> |<span data-ttu-id="3ffd7-135">Oui</span><span class="sxs-lookup"><span data-stu-id="3ffd7-135">Yes</span></span> |<span data-ttu-id="3ffd7-136">Oui</span><span class="sxs-lookup"><span data-stu-id="3ffd7-136">Yes</span></span> |
| <span data-ttu-id="3ffd7-137">Images Place de marché Azure de liste blanche</span><span class="sxs-lookup"><span data-stu-id="3ffd7-137">Whitelist Azure Marketplace images</span></span> |<span data-ttu-id="3ffd7-138">Non</span><span class="sxs-lookup"><span data-stu-id="3ffd7-138">No</span></span> |<span data-ttu-id="3ffd7-139">Oui</span><span class="sxs-lookup"><span data-stu-id="3ffd7-139">Yes</span></span> |<span data-ttu-id="3ffd7-140">Oui</span><span class="sxs-lookup"><span data-stu-id="3ffd7-140">Yes</span></span> |
| <span data-ttu-id="3ffd7-141">**Tâches de machine virtuelle**</span><span class="sxs-lookup"><span data-stu-id="3ffd7-141">**VM tasks**</span></span> | | | |
| <span data-ttu-id="3ffd7-142">Créer des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="3ffd7-142">Create VMs</span></span> |<span data-ttu-id="3ffd7-143">Oui</span><span class="sxs-lookup"><span data-stu-id="3ffd7-143">Yes</span></span> |<span data-ttu-id="3ffd7-144">Oui</span><span class="sxs-lookup"><span data-stu-id="3ffd7-144">Yes</span></span> |<span data-ttu-id="3ffd7-145">Oui</span><span class="sxs-lookup"><span data-stu-id="3ffd7-145">Yes</span></span> |
| <span data-ttu-id="3ffd7-146">Démarrer, arrêter et supprimer des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="3ffd7-146">Start, stop, and delete VMs</span></span> |<span data-ttu-id="3ffd7-147">Seuls les ordinateurs virtuels créés par l’utilisateur de hello</span><span class="sxs-lookup"><span data-stu-id="3ffd7-147">Only VMs created by hello user</span></span> |<span data-ttu-id="3ffd7-148">Oui</span><span class="sxs-lookup"><span data-stu-id="3ffd7-148">Yes</span></span> |<span data-ttu-id="3ffd7-149">Oui</span><span class="sxs-lookup"><span data-stu-id="3ffd7-149">Yes</span></span> |
| <span data-ttu-id="3ffd7-150">Mettre à jour les stratégies de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="3ffd7-150">Update VM policies</span></span> |<span data-ttu-id="3ffd7-151">Non</span><span class="sxs-lookup"><span data-stu-id="3ffd7-151">No</span></span> |<span data-ttu-id="3ffd7-152">Oui</span><span class="sxs-lookup"><span data-stu-id="3ffd7-152">Yes</span></span> |<span data-ttu-id="3ffd7-153">Oui</span><span class="sxs-lookup"><span data-stu-id="3ffd7-153">Yes</span></span> |
| <span data-ttu-id="3ffd7-154">Ajouter des disques de données à des machines virtuelles ou en supprimer de celles-ci</span><span class="sxs-lookup"><span data-stu-id="3ffd7-154">Add/remove data disks to/from VMs</span></span> |<span data-ttu-id="3ffd7-155">Seuls les ordinateurs virtuels créés par l’utilisateur de hello</span><span class="sxs-lookup"><span data-stu-id="3ffd7-155">Only VMs created by hello user</span></span> |<span data-ttu-id="3ffd7-156">Oui</span><span class="sxs-lookup"><span data-stu-id="3ffd7-156">Yes</span></span> |<span data-ttu-id="3ffd7-157">Oui</span><span class="sxs-lookup"><span data-stu-id="3ffd7-157">Yes</span></span> |
| <span data-ttu-id="3ffd7-158">**Tâches d’artefact**</span><span class="sxs-lookup"><span data-stu-id="3ffd7-158">**Artifact tasks**</span></span> | | | |
| <span data-ttu-id="3ffd7-159">Ajouter et supprimer des référentiels d’artefact</span><span class="sxs-lookup"><span data-stu-id="3ffd7-159">Add and remove artifact repositories</span></span> |<span data-ttu-id="3ffd7-160">Non</span><span class="sxs-lookup"><span data-stu-id="3ffd7-160">No</span></span> |<span data-ttu-id="3ffd7-161">Oui</span><span class="sxs-lookup"><span data-stu-id="3ffd7-161">Yes</span></span> |<span data-ttu-id="3ffd7-162">Oui</span><span class="sxs-lookup"><span data-stu-id="3ffd7-162">Yes</span></span> |
| <span data-ttu-id="3ffd7-163">Appliquer des artefacts</span><span class="sxs-lookup"><span data-stu-id="3ffd7-163">Apply artifacts</span></span> |<span data-ttu-id="3ffd7-164">Oui</span><span class="sxs-lookup"><span data-stu-id="3ffd7-164">Yes</span></span> |<span data-ttu-id="3ffd7-165">Oui</span><span class="sxs-lookup"><span data-stu-id="3ffd7-165">Yes</span></span> |<span data-ttu-id="3ffd7-166">Oui</span><span class="sxs-lookup"><span data-stu-id="3ffd7-166">Yes</span></span> |

> [!NOTE]
> <span data-ttu-id="3ffd7-167">Lorsqu’un utilisateur crée une machine virtuelle, cet utilisateur est affecté automatiquement toohello **propriétaire** rôle Hello créé la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3ffd7-167">When a user creates a VM, that user is automatically assigned toohello **Owner** role of hello created VM.</span></span>
> 
> 

## <a name="add-an-owner-or-user-at-hello-lab-level"></a><span data-ttu-id="3ffd7-168">Ajouter un propriétaire ou un utilisateur au niveau de lab hello</span><span class="sxs-lookup"><span data-stu-id="3ffd7-168">Add an owner or user at hello lab level</span></span>
<span data-ttu-id="3ffd7-169">Les propriétaires et les utilisateurs peuvent être ajoutés au niveau de lab hello via hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3ffd7-169">Owners and users can be added at hello lab level via hello Azure portal.</span></span> <span data-ttu-id="3ffd7-170">Cela comprend les utilisateurs externes qui disposent d’un [compte Microsoft (MSA)](devtest-lab-faq.md#what-is-a-microsoft-account)valide.</span><span class="sxs-lookup"><span data-stu-id="3ffd7-170">This includes external users with a valid [Microsoft account (MSA)](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span>
<span data-ttu-id="3ffd7-171">Hello comme suit vous guide tout au long des processus hello d’ajout d’un laboratoire tooa propriétaire ou un utilisateur dans Azure DevTest Labs :</span><span class="sxs-lookup"><span data-stu-id="3ffd7-171">hello following steps guide you through hello process of adding an owner or user tooa lab in Azure DevTest Labs:</span></span>

1. <span data-ttu-id="3ffd7-172">Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="3ffd7-172">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="3ffd7-173">Sélectionnez **davantage de services**, puis sélectionnez **DevTest Labs** à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="3ffd7-173">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="3ffd7-174">Dans liste hello labs, sélectionnez lab souhaité de hello.</span><span class="sxs-lookup"><span data-stu-id="3ffd7-174">From hello list of labs, select hello desired lab.</span></span>
4. <span data-ttu-id="3ffd7-175">Dans le panneau de hello lab, sélectionnez **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="3ffd7-175">On hello lab's blade, select **Configuration**.</span></span> 
5. <span data-ttu-id="3ffd7-176">Sur hello **Configuration** panneau, sélectionnez **utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="3ffd7-176">On hello **Configuration** blade, select **Users**.</span></span>
6. <span data-ttu-id="3ffd7-177">Sur hello **utilisateurs** panneau, sélectionnez **+ ajouter**.</span><span class="sxs-lookup"><span data-stu-id="3ffd7-177">On hello **Users** blade, select **+Add**.</span></span>
   
    ![Ajouter un utilisateur](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
7. <span data-ttu-id="3ffd7-179">Sur hello **sélectionner un rôle** panneau, rôle souhaité de hello select.</span><span class="sxs-lookup"><span data-stu-id="3ffd7-179">On hello **Select a role** blade, select hello desired role.</span></span> <span data-ttu-id="3ffd7-180">Hello section [les Actions qui peuvent être effectuées dans chaque rôle](#actions-that-can-be-performed-in-each-role) listes hello différentes actions qui peuvent être effectuées par les utilisateurs dans des rôles propriétaire et collaborateur DevTest utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="3ffd7-180">hello section [Actions that can be performed in each role](#actions-that-can-be-performed-in-each-role) lists hello various actions that can be performed by users in hello Owner, DevTest User, and Contributor roles.</span></span>
8. <span data-ttu-id="3ffd7-181">Sur hello **ajouter des utilisateurs** panneau, entrez l’adresse de messagerie hello ou nom d’utilisateur hello tooadd rôle hello spécifié.</span><span class="sxs-lookup"><span data-stu-id="3ffd7-181">On hello **Add users** blade, enter hello email address or name of hello user you want tooadd in hello role you specified.</span></span> <span data-ttu-id="3ffd7-182">Si l’utilisateur de hello est introuvable, un message d’erreur explique problème de hello.</span><span class="sxs-lookup"><span data-stu-id="3ffd7-182">If hello user can't be found, an error message explains hello issue.</span></span> <span data-ttu-id="3ffd7-183">Si hello utilisateur est trouvé, cet utilisateur est répertorié et sélectionné.</span><span class="sxs-lookup"><span data-stu-id="3ffd7-183">If hello user is found, that user is listed and selected.</span></span> 
9. <span data-ttu-id="3ffd7-184">Sélectionnez **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="3ffd7-184">Select **Select**.</span></span>
10. <span data-ttu-id="3ffd7-185">Sélectionnez **OK** tooclose hello **ajouter un accès** panneau.</span><span class="sxs-lookup"><span data-stu-id="3ffd7-185">Select **OK** tooclose hello **Add access** blade.</span></span>
11. <span data-ttu-id="3ffd7-186">Lorsque vous retournez toohello **utilisateurs** panneau, hello utilisateur a été ajouté.</span><span class="sxs-lookup"><span data-stu-id="3ffd7-186">When you return toohello **Users** blade, hello user has been added.</span></span>  

## <a name="add-an-external-user-tooa-lab-using-powershell"></a><span data-ttu-id="3ffd7-187">Ajouter un laboratoire de tooa utilisateur externe à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="3ffd7-187">Add an external user tooa lab using PowerShell</span></span>
<span data-ttu-id="3ffd7-188">En outre les utilisateurs tooadding hello portail Azure, vous pouvez ajouter un laboratoire de tooyour utilisateur externe à l’aide d’un script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3ffd7-188">In addition tooadding users in hello Azure portal, you can add an external user tooyour lab using a PowerShell script.</span></span> <span data-ttu-id="3ffd7-189">Bonjour, l’exemple suivant simplement modifier les valeurs de paramètre hello sous hello **toochange de valeurs** commentaire.</span><span class="sxs-lookup"><span data-stu-id="3ffd7-189">In hello following example, simply modify hello parameter values under hello **Values toochange** comment.</span></span>
<span data-ttu-id="3ffd7-190">Vous pouvez récupérer hello `subscriptionId`, `labResourceGroup`, et `labName` valeurs hello lab du Panneau de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3ffd7-190">You can retrieve hello `subscriptionId`, `labResourceGroup`, and `labName` values from hello lab blade in hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="3ffd7-191">exemple de script Hello suppose que hello spécifié utilisateur a été ajouté comme un toohello invité Active Directory et échoue si ce n’est pas le cas de hello.</span><span class="sxs-lookup"><span data-stu-id="3ffd7-191">hello sample script assumes that hello specified user has been added as a guest toohello Active Directory, and will fail if that is not hello case.</span></span> <span data-ttu-id="3ffd7-192">tooadd un utilisateur n’est pas dans hello lab tooa de Active Directory, utilisez le rôle tooa utilisateur hello tooassign portail Azure hello comme illustré dans la section de hello, [ajouter un propriétaire ou un utilisateur au niveau de lab hello](#add-an-owner-or-user-at-the-lab-level).</span><span class="sxs-lookup"><span data-stu-id="3ffd7-192">tooadd a user not in hello Active Directory tooa lab, use hello Azure portal tooassign hello user tooa role as illustrated in hello section, [Add an owner or user at hello lab level](#add-an-owner-or-user-at-the-lab-level).</span></span>   
> 
> 

    # Add an external user in DevTest Labs user role tooa lab
    # Ensure that guest users can be added toohello Azure Active directory:
    # https://azure.microsoft.com/en-us/documentation/articles/active-directory-create-users/#set-guest-user-access-policies

    # Values toochange
    $subscriptionId = "<Enter Azure subscription ID here>"
    $labResourceGroup = "<Enter lab's resource name here>"
    $labName = "<Enter lab name here>"
    $userDisplayName = "<Enter user's display name here>"

    # Log into your Azure account
    Login-AzureRmAccount

    # Select hello Azure subscription that contains hello lab. 
    # This step is optional if you have only one subscription.
    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    # Retrieve hello user object
    $adObject = Get-AzureRmADUser -SearchString $userDisplayName

    # Create hello role assignment. 
    $labId = ('subscriptions/' + $subscriptionId + '/resourceGroups/' + $labResourceGroup + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    New-AzureRmRoleAssignment -ObjectId $adObject.Id -RoleDefinitionName 'DevTest Labs User' -Scope $labId

## <a name="add-an-owner-or-user-at-hello-subscription-level"></a><span data-ttu-id="3ffd7-193">Ajouter un propriétaire ou un utilisateur au niveau d’abonnement hello</span><span class="sxs-lookup"><span data-stu-id="3ffd7-193">Add an owner or user at hello subscription level</span></span>
<span data-ttu-id="3ffd7-194">Autorisations Azure sont propagées à partir de l’étendue de toochild étendue parente dans Azure.</span><span class="sxs-lookup"><span data-stu-id="3ffd7-194">Azure permissions are propagated from parent scope toochild scope in Azure.</span></span> <span data-ttu-id="3ffd7-195">Par conséquent, les propriétaires d’un abonnement Azure qui contient des laboratoires sont automatiquement les propriétaires de ces laboratoires.</span><span class="sxs-lookup"><span data-stu-id="3ffd7-195">Therefore, owners of an Azure subscription that contains labs are automatically owners of those labs.</span></span> <span data-ttu-id="3ffd7-196">Ils possèdent également des machines virtuelles de hello et autres ressources créées par les utilisateurs du laboratoire hello et hello service de Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="3ffd7-196">They also own hello VMs and other resources created by hello lab's users, and hello Azure DevTest Labs service.</span></span> 

<span data-ttu-id="3ffd7-197">Vous pouvez ajouter lab de tooa propriétaire supplémentaire via le panneau de hello lab Bonjour [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="3ffd7-197">You can add additional owners tooa lab via hello lab's blade in hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span> <span data-ttu-id="3ffd7-198">Toutefois, hello ajouté l’étendue du propriétaire de l’administration est plus étroite que la portée du propriétaire d’abonnement hello.</span><span class="sxs-lookup"><span data-stu-id="3ffd7-198">However, hello added owner's scope of administration is more narrow than hello subscription owner's scope.</span></span> <span data-ttu-id="3ffd7-199">Par exemple, hello ajoutée propriétaires n’ont pas toosome d’accès complet des ressources hello qui sont créés dans l’abonnement de hello en hello service de DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="3ffd7-199">For example, hello added owners do not have full access toosome of hello resources that are created in hello subscription by hello DevTest Labs service.</span></span> 

<span data-ttu-id="3ffd7-200">tooadd un tooan propriétaire abonnement Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="3ffd7-200">tooadd an owner tooan Azure subscription, follow these steps:</span></span>

1. <span data-ttu-id="3ffd7-201">Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="3ffd7-201">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="3ffd7-202">Sélectionnez **plus Services**, puis sélectionnez **abonnements** à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="3ffd7-202">Select **More Services**, and then select **Subscriptions** from hello list.</span></span>
3. <span data-ttu-id="3ffd7-203">Sélectionnez l’abonnement de hello souhaité.</span><span class="sxs-lookup"><span data-stu-id="3ffd7-203">Select hello desired subscription.</span></span>
4. <span data-ttu-id="3ffd7-204">Sélectionnez l’icône **Accès** .</span><span class="sxs-lookup"><span data-stu-id="3ffd7-204">Select **Access** icon.</span></span> 
   
    ![Accéder aux utilisateurs](./media/devtest-lab-add-devtest-user/access-users.png)
5. <span data-ttu-id="3ffd7-206">Sur hello **utilisateurs** panneau, sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="3ffd7-206">On hello **Users** blade, select **Add**.</span></span>
   
    ![Ajouter un utilisateur](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
6. <span data-ttu-id="3ffd7-208">Sur hello **sélectionner un rôle** panneau, sélectionnez **propriétaire**.</span><span class="sxs-lookup"><span data-stu-id="3ffd7-208">On hello **Select a role** blade, select **Owner**.</span></span>
7. <span data-ttu-id="3ffd7-209">Sur hello **ajouter des utilisateurs** panneau, entrez l’adresse de messagerie hello ou le nom d’utilisateur de hello souhaité tooadd en tant que propriétaire.</span><span class="sxs-lookup"><span data-stu-id="3ffd7-209">On hello **Add users** blade, enter hello email address or name of hello user you want tooadd as an owner.</span></span> <span data-ttu-id="3ffd7-210">Si l’utilisateur de hello est introuvable, vous obtenez un message d’erreur expliquant le problème de hello.</span><span class="sxs-lookup"><span data-stu-id="3ffd7-210">If hello user can't be found, you get an error message explaining hello issue.</span></span> <span data-ttu-id="3ffd7-211">Si l’utilisateur de hello est trouvée, cet utilisateur est répertorié sous hello **utilisateur** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="3ffd7-211">If hello user is found, that user is listed under hello **User** text box.</span></span>
8. <span data-ttu-id="3ffd7-212">Sélectionnez le nom d’utilisateur situé hello.</span><span class="sxs-lookup"><span data-stu-id="3ffd7-212">Select hello located user name.</span></span>
9. <span data-ttu-id="3ffd7-213">Sélectionnez **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="3ffd7-213">Select **Select**.</span></span>
10. <span data-ttu-id="3ffd7-214">Sélectionnez **OK** tooclose hello **ajouter un accès** panneau.</span><span class="sxs-lookup"><span data-stu-id="3ffd7-214">Select **OK** tooclose hello **Add access** blade.</span></span>
11. <span data-ttu-id="3ffd7-215">Lorsque vous retournez toohello **utilisateurs** panneau, utilisateur de hello a été ajouté en tant que propriétaire.</span><span class="sxs-lookup"><span data-stu-id="3ffd7-215">When you return toohello **Users** blade, hello user has been added as an owner.</span></span> <span data-ttu-id="3ffd7-216">Cet utilisateur est désormais un propriétaire de n’importe quel labs créées sous cet abonnement et donc en mesure de tooperform des tâches de propriétaire.</span><span class="sxs-lookup"><span data-stu-id="3ffd7-216">This user is now an owner of any labs created under this subscription, and thus be able tooperform owner tasks.</span></span> 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

