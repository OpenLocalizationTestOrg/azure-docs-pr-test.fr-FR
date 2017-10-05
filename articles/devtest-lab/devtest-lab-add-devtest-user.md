---
title: "Ajouter des propriétaires et des utilisateurs dans Azure DevTest Labs | Microsoft Docs"
description: "Ajouter des propriétaires et des utilisateurs dans Azure DevTest Labs à l’aide du portail Azure ou de PowerShell"
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
ms.openlocfilehash: d67fa257574d6cb4ad4b18521900374fb51da290
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="add-owners-and-users-in-azure-devtest-labs"></a><span data-ttu-id="a881a-103">Ajouter des propriétaires et des utilisateurs dans Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="a881a-103">Add owners and users in Azure DevTest Labs</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/How-to-set-security-in-your-DevTest-Lab/player]
> 
> 

<span data-ttu-id="a881a-104">L’accès à Azure DevTest Labs est contrôlé par le [contrôle d’accès en fonction du rôle (RBAC) Azure](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="a881a-104">Access in Azure DevTest Labs is controlled by [Azure Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-what-is.md).</span></span> <span data-ttu-id="a881a-105">Avec le contrôle d’accès en fonction du rôle, vous pouvez séparer les tâches au sein de votre équipe en *rôles* dans lesquels vous accordez aux utilisateurs uniquement les accès nécessaires pour accomplir leur travail.</span><span class="sxs-lookup"><span data-stu-id="a881a-105">Using RBAC, you can segregate duties within your team into *roles* where you grant only the amount of access necessary to users to perform their jobs.</span></span> <span data-ttu-id="a881a-106">Trois de ces rôles RBAC sont *Propriétaire*, *Utilisateur de DevTest Labs* et *Collaborateur*.</span><span class="sxs-lookup"><span data-stu-id="a881a-106">Three of these RBAC roles are *Owner*, *DevTest Labs User*, and *Contributor*.</span></span> <span data-ttu-id="a881a-107">Dans cet article, vous allez découvrir quelles actions peuvent être effectuées dans chacun des trois rôles RBAC principaux.</span><span class="sxs-lookup"><span data-stu-id="a881a-107">In this article, you learn what actions can be performed in each of the three main RBAC roles.</span></span> <span data-ttu-id="a881a-108">À partir de là, vous allez apprendre à ajouter des utilisateurs à un laboratoire, à la fois via le portail et via un script PowerShell, et à ajouter des utilisateurs au niveau de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="a881a-108">From there, you learn how to add users to a lab - both via the portal and via a PowerShell script, and how to add users at the subscription level.</span></span>

## <a name="actions-that-can-be-performed-in-each-role"></a><span data-ttu-id="a881a-109">Actions qui peuvent être effectuées dans chaque rôle</span><span class="sxs-lookup"><span data-stu-id="a881a-109">Actions that can be performed in each role</span></span>
<span data-ttu-id="a881a-110">Il existe trois rôles principaux que vous pouvez attribuer à un utilisateur :</span><span class="sxs-lookup"><span data-stu-id="a881a-110">There are three main roles that you can assign a user:</span></span>

* <span data-ttu-id="a881a-111">Propriétaire</span><span class="sxs-lookup"><span data-stu-id="a881a-111">Owner</span></span>
* <span data-ttu-id="a881a-112">Utilisateur de DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="a881a-112">DevTest Labs User</span></span>
* <span data-ttu-id="a881a-113">Collaborateur</span><span class="sxs-lookup"><span data-stu-id="a881a-113">Contributor</span></span>

<span data-ttu-id="a881a-114">Le tableau suivant décrit les actions pouvant être effectuées par les utilisateurs dans chacun de ces rôles :</span><span class="sxs-lookup"><span data-stu-id="a881a-114">The following table illustrates the actions that can be performed by users in each of these roles:</span></span>

| <span data-ttu-id="a881a-115">**Actions que les utilisateurs dans ce rôle peuvent effectuer**</span><span class="sxs-lookup"><span data-stu-id="a881a-115">**Actions users in this role can perform**</span></span> | <span data-ttu-id="a881a-116">**Utilisateur de DevTest Labs**</span><span class="sxs-lookup"><span data-stu-id="a881a-116">**DevTest Labs User**</span></span> | <span data-ttu-id="a881a-117">**Propriétaire**</span><span class="sxs-lookup"><span data-stu-id="a881a-117">**Owner**</span></span> | <span data-ttu-id="a881a-118">**Collaborateur**</span><span class="sxs-lookup"><span data-stu-id="a881a-118">**Contributor**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a881a-119">**Tâches de laboratoire**</span><span class="sxs-lookup"><span data-stu-id="a881a-119">**Lab tasks**</span></span> | | | |
| <span data-ttu-id="a881a-120">Ajouter des utilisateurs à un laboratoire</span><span class="sxs-lookup"><span data-stu-id="a881a-120">Add users to a lab</span></span> |<span data-ttu-id="a881a-121">Non</span><span class="sxs-lookup"><span data-stu-id="a881a-121">No</span></span> |<span data-ttu-id="a881a-122">Oui</span><span class="sxs-lookup"><span data-stu-id="a881a-122">Yes</span></span> |<span data-ttu-id="a881a-123">Non</span><span class="sxs-lookup"><span data-stu-id="a881a-123">No</span></span> |
| <span data-ttu-id="a881a-124">Mettre à jour les paramètres de coût</span><span class="sxs-lookup"><span data-stu-id="a881a-124">Update cost settings</span></span> |<span data-ttu-id="a881a-125">Non</span><span class="sxs-lookup"><span data-stu-id="a881a-125">No</span></span> |<span data-ttu-id="a881a-126">Oui</span><span class="sxs-lookup"><span data-stu-id="a881a-126">Yes</span></span> |<span data-ttu-id="a881a-127">Oui</span><span class="sxs-lookup"><span data-stu-id="a881a-127">Yes</span></span> |
| <span data-ttu-id="a881a-128">**Tâches de base de machine virtuelle**</span><span class="sxs-lookup"><span data-stu-id="a881a-128">**VM base tasks**</span></span> | | | |
| <span data-ttu-id="a881a-129">Ajouter et supprimer des images personnalisées</span><span class="sxs-lookup"><span data-stu-id="a881a-129">Add and remove custom images</span></span> |<span data-ttu-id="a881a-130">Non</span><span class="sxs-lookup"><span data-stu-id="a881a-130">No</span></span> |<span data-ttu-id="a881a-131">Oui</span><span class="sxs-lookup"><span data-stu-id="a881a-131">Yes</span></span> |<span data-ttu-id="a881a-132">Oui</span><span class="sxs-lookup"><span data-stu-id="a881a-132">Yes</span></span> |
| <span data-ttu-id="a881a-133">Ajouter, mettre à jour et supprimer des formules</span><span class="sxs-lookup"><span data-stu-id="a881a-133">Add, update, and delete formulas</span></span> |<span data-ttu-id="a881a-134">Oui</span><span class="sxs-lookup"><span data-stu-id="a881a-134">Yes</span></span> |<span data-ttu-id="a881a-135">Oui</span><span class="sxs-lookup"><span data-stu-id="a881a-135">Yes</span></span> |<span data-ttu-id="a881a-136">Oui</span><span class="sxs-lookup"><span data-stu-id="a881a-136">Yes</span></span> |
| <span data-ttu-id="a881a-137">Images Place de marché Azure de liste blanche</span><span class="sxs-lookup"><span data-stu-id="a881a-137">Whitelist Azure Marketplace images</span></span> |<span data-ttu-id="a881a-138">Non</span><span class="sxs-lookup"><span data-stu-id="a881a-138">No</span></span> |<span data-ttu-id="a881a-139">Oui</span><span class="sxs-lookup"><span data-stu-id="a881a-139">Yes</span></span> |<span data-ttu-id="a881a-140">Oui</span><span class="sxs-lookup"><span data-stu-id="a881a-140">Yes</span></span> |
| <span data-ttu-id="a881a-141">**Tâches de machine virtuelle**</span><span class="sxs-lookup"><span data-stu-id="a881a-141">**VM tasks**</span></span> | | | |
| <span data-ttu-id="a881a-142">Créer des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="a881a-142">Create VMs</span></span> |<span data-ttu-id="a881a-143">Oui</span><span class="sxs-lookup"><span data-stu-id="a881a-143">Yes</span></span> |<span data-ttu-id="a881a-144">Oui</span><span class="sxs-lookup"><span data-stu-id="a881a-144">Yes</span></span> |<span data-ttu-id="a881a-145">Oui</span><span class="sxs-lookup"><span data-stu-id="a881a-145">Yes</span></span> |
| <span data-ttu-id="a881a-146">Démarrer, arrêter et supprimer des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="a881a-146">Start, stop, and delete VMs</span></span> |<span data-ttu-id="a881a-147">Seules les machines virtuelles créées par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="a881a-147">Only VMs created by the user</span></span> |<span data-ttu-id="a881a-148">Oui</span><span class="sxs-lookup"><span data-stu-id="a881a-148">Yes</span></span> |<span data-ttu-id="a881a-149">Oui</span><span class="sxs-lookup"><span data-stu-id="a881a-149">Yes</span></span> |
| <span data-ttu-id="a881a-150">Mettre à jour les stratégies de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="a881a-150">Update VM policies</span></span> |<span data-ttu-id="a881a-151">Non</span><span class="sxs-lookup"><span data-stu-id="a881a-151">No</span></span> |<span data-ttu-id="a881a-152">Oui</span><span class="sxs-lookup"><span data-stu-id="a881a-152">Yes</span></span> |<span data-ttu-id="a881a-153">Oui</span><span class="sxs-lookup"><span data-stu-id="a881a-153">Yes</span></span> |
| <span data-ttu-id="a881a-154">Ajouter des disques de données à des machines virtuelles ou en supprimer de celles-ci</span><span class="sxs-lookup"><span data-stu-id="a881a-154">Add/remove data disks to/from VMs</span></span> |<span data-ttu-id="a881a-155">Seules les machines virtuelles créées par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="a881a-155">Only VMs created by the user</span></span> |<span data-ttu-id="a881a-156">Oui</span><span class="sxs-lookup"><span data-stu-id="a881a-156">Yes</span></span> |<span data-ttu-id="a881a-157">Oui</span><span class="sxs-lookup"><span data-stu-id="a881a-157">Yes</span></span> |
| <span data-ttu-id="a881a-158">**Tâches d’artefact**</span><span class="sxs-lookup"><span data-stu-id="a881a-158">**Artifact tasks**</span></span> | | | |
| <span data-ttu-id="a881a-159">Ajouter et supprimer des référentiels d’artefact</span><span class="sxs-lookup"><span data-stu-id="a881a-159">Add and remove artifact repositories</span></span> |<span data-ttu-id="a881a-160">Non</span><span class="sxs-lookup"><span data-stu-id="a881a-160">No</span></span> |<span data-ttu-id="a881a-161">Oui</span><span class="sxs-lookup"><span data-stu-id="a881a-161">Yes</span></span> |<span data-ttu-id="a881a-162">Oui</span><span class="sxs-lookup"><span data-stu-id="a881a-162">Yes</span></span> |
| <span data-ttu-id="a881a-163">Appliquer des artefacts</span><span class="sxs-lookup"><span data-stu-id="a881a-163">Apply artifacts</span></span> |<span data-ttu-id="a881a-164">Oui</span><span class="sxs-lookup"><span data-stu-id="a881a-164">Yes</span></span> |<span data-ttu-id="a881a-165">Oui</span><span class="sxs-lookup"><span data-stu-id="a881a-165">Yes</span></span> |<span data-ttu-id="a881a-166">Oui</span><span class="sxs-lookup"><span data-stu-id="a881a-166">Yes</span></span> |

> [!NOTE]
> <span data-ttu-id="a881a-167">Lorsqu’un utilisateur crée une machine virtuelle, le rôle **Propriétaire** de la machine virtuelle créée est automatiquement attribué à cet utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a881a-167">When a user creates a VM, that user is automatically assigned to the **Owner** role of the created VM.</span></span>
> 
> 

## <a name="add-an-owner-or-user-at-the-lab-level"></a><span data-ttu-id="a881a-168">Ajouter un utilisateur ou un propriétaire au niveau du laboratoire</span><span class="sxs-lookup"><span data-stu-id="a881a-168">Add an owner or user at the lab level</span></span>
<span data-ttu-id="a881a-169">Les propriétaires et les utilisateurs peuvent être ajoutés au niveau du laboratoire via le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a881a-169">Owners and users can be added at the lab level via the Azure portal.</span></span> <span data-ttu-id="a881a-170">Cela comprend les utilisateurs externes qui disposent d’un [compte Microsoft (MSA)](devtest-lab-faq.md#what-is-a-microsoft-account)valide.</span><span class="sxs-lookup"><span data-stu-id="a881a-170">This includes external users with a valid [Microsoft account (MSA)](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span>
<span data-ttu-id="a881a-171">Les étapes suivantes vous guident dans le processus d’ajout d’un propriétaire ou d’un utilisateur à un laboratoire dans Azure DevTest Labs :</span><span class="sxs-lookup"><span data-stu-id="a881a-171">The following steps guide you through the process of adding an owner or user to a lab in Azure DevTest Labs:</span></span>

1. <span data-ttu-id="a881a-172">Connectez-vous au [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="a881a-172">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="a881a-173">Sélectionnez **Plus de services**, puis **DevTest Labs** dans la liste.</span><span class="sxs-lookup"><span data-stu-id="a881a-173">Select **More services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="a881a-174">Sélectionnez le laboratoire souhaité dans la liste des laboratoires.</span><span class="sxs-lookup"><span data-stu-id="a881a-174">From the list of labs, select the desired lab.</span></span>
4. <span data-ttu-id="a881a-175">Dans le panneau du laboratoire, sélectionnez **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="a881a-175">On the lab's blade, select **Configuration**.</span></span> 
5. <span data-ttu-id="a881a-176">Dans le panneau **Configuration**, sélectionnez **Utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="a881a-176">On the **Configuration** blade, select **Users**.</span></span>
6. <span data-ttu-id="a881a-177">Dans le panneau **Utilisateurs**, sélectionnez **+Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="a881a-177">On the **Users** blade, select **+Add**.</span></span>
   
    ![Ajouter un utilisateur](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
7. <span data-ttu-id="a881a-179">Dans le panneau **Sélectionner un rôle** , sélectionnez le rôle souhaité.</span><span class="sxs-lookup"><span data-stu-id="a881a-179">On the **Select a role** blade, select the desired role.</span></span> <span data-ttu-id="a881a-180">La section [Actions qui peuvent être effectuées dans chaque rôle](#actions-that-can-be-performed-in-each-role) répertorie les différentes actions qui peuvent être effectuées par les utilisateurs dans les rôles Propriétaire, Utilisateur de DevTest Labs et Collaborateur.</span><span class="sxs-lookup"><span data-stu-id="a881a-180">The section [Actions that can be performed in each role](#actions-that-can-be-performed-in-each-role) lists the various actions that can be performed by users in the Owner, DevTest User, and Contributor roles.</span></span>
8. <span data-ttu-id="a881a-181">Dans le panneau **Ajouter des utilisateurs** , entrez l’adresse de messagerie ou le nom de l’utilisateur que vous souhaitez ajouter dans le rôle spécifié.</span><span class="sxs-lookup"><span data-stu-id="a881a-181">On the **Add users** blade, enter the email address or name of the user you want to add in the role you specified.</span></span> <span data-ttu-id="a881a-182">Si l’utilisateur n’est pas trouvé, un message d’erreur expliquant le problème s’affiche.</span><span class="sxs-lookup"><span data-stu-id="a881a-182">If the user can't be found, an error message explains the issue.</span></span> <span data-ttu-id="a881a-183">Si l’utilisateur est trouvé, il est répertorié et sélectionné.</span><span class="sxs-lookup"><span data-stu-id="a881a-183">If the user is found, that user is listed and selected.</span></span> 
9. <span data-ttu-id="a881a-184">Sélectionnez **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="a881a-184">Select **Select**.</span></span>
10. <span data-ttu-id="a881a-185">Cliquez sur **OK** pour fermer le panneau **Ajouter un accès**.</span><span class="sxs-lookup"><span data-stu-id="a881a-185">Select **OK** to close the **Add access** blade.</span></span>
11. <span data-ttu-id="a881a-186">Lorsque vous revenez sur le panneau **Utilisateurs** , l’utilisateur a été ajouté.</span><span class="sxs-lookup"><span data-stu-id="a881a-186">When you return to the **Users** blade, the user has been added.</span></span>  

## <a name="add-an-external-user-to-a-lab-using-powershell"></a><span data-ttu-id="a881a-187">Ajouter un utilisateur externe à un laboratoire à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="a881a-187">Add an external user to a lab using PowerShell</span></span>
<span data-ttu-id="a881a-188">Outre l’ajout d’utilisateurs dans le portail Azure, vous pouvez ajouter un utilisateur externe à votre laboratoire à l’aide d’un script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a881a-188">In addition to adding users in the Azure portal, you can add an external user to your lab using a PowerShell script.</span></span> <span data-ttu-id="a881a-189">Dans l’exemple suivant, modifiez simplement les valeurs des paramètres sous le commentaire **Valeurs à modifier** .</span><span class="sxs-lookup"><span data-stu-id="a881a-189">In the following example, simply modify the parameter values under the **Values to change** comment.</span></span>
<span data-ttu-id="a881a-190">Vous pouvez récupérer les valeurs `subscriptionId`, `labResourceGroup` et `labName` à partir du panneau de laboratoire dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a881a-190">You can retrieve the `subscriptionId`, `labResourceGroup`, and `labName` values from the lab blade in the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="a881a-191">L’exemple de script suppose que l’utilisateur spécifié a été ajouté en tant qu’invité à Active Directory et échoue si ce n’est pas le cas.</span><span class="sxs-lookup"><span data-stu-id="a881a-191">The sample script assumes that the specified user has been added as a guest to the Active Directory, and will fail if that is not the case.</span></span> <span data-ttu-id="a881a-192">Pour ajouter un utilisateur qui ne se trouve pas dans Active Directory à un laboratoire, utilisez le portail Azure pour attribuer un rôle à l’utilisateur, comme illustré dans la section [Ajouter un utilisateur ou un propriétaire au niveau du laboratoire](#add-an-owner-or-user-at-the-lab-level).</span><span class="sxs-lookup"><span data-stu-id="a881a-192">To add a user not in the Active Directory to a lab, use the Azure portal to assign the user to a role as illustrated in the section, [Add an owner or user at the lab level](#add-an-owner-or-user-at-the-lab-level).</span></span>   
> 
> 

    # Add an external user in DevTest Labs user role to a lab
    # Ensure that guest users can be added to the Azure Active directory:
    # https://azure.microsoft.com/en-us/documentation/articles/active-directory-create-users/#set-guest-user-access-policies

    # Values to change
    $subscriptionId = "<Enter Azure subscription ID here>"
    $labResourceGroup = "<Enter lab's resource name here>"
    $labName = "<Enter lab name here>"
    $userDisplayName = "<Enter user's display name here>"

    # Log into your Azure account
    Login-AzureRmAccount

    # Select the Azure subscription that contains the lab. 
    # This step is optional if you have only one subscription.
    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    # Retrieve the user object
    $adObject = Get-AzureRmADUser -SearchString $userDisplayName

    # Create the role assignment. 
    $labId = ('subscriptions/' + $subscriptionId + '/resourceGroups/' + $labResourceGroup + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    New-AzureRmRoleAssignment -ObjectId $adObject.Id -RoleDefinitionName 'DevTest Labs User' -Scope $labId

## <a name="add-an-owner-or-user-at-the-subscription-level"></a><span data-ttu-id="a881a-193">Ajouter un utilisateur ou un propriétaire au niveau du laboratoire</span><span class="sxs-lookup"><span data-stu-id="a881a-193">Add an owner or user at the subscription level</span></span>
<span data-ttu-id="a881a-194">Les autorisations Azure sont propagées à partir de l’étendue parent vers l’étendue enfant dans Azure.</span><span class="sxs-lookup"><span data-stu-id="a881a-194">Azure permissions are propagated from parent scope to child scope in Azure.</span></span> <span data-ttu-id="a881a-195">Par conséquent, les propriétaires d’un abonnement Azure qui contient des laboratoires sont automatiquement les propriétaires de ces laboratoires.</span><span class="sxs-lookup"><span data-stu-id="a881a-195">Therefore, owners of an Azure subscription that contains labs are automatically owners of those labs.</span></span> <span data-ttu-id="a881a-196">Ils sont également propriétaires des machines virtuelles et des autres ressources créées par les utilisateurs du laboratoire et le service Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="a881a-196">They also own the VMs and other resources created by the lab's users, and the Azure DevTest Labs service.</span></span> 

<span data-ttu-id="a881a-197">Vous pouvez ajouter des propriétaires supplémentaires à un laboratoire via le panneau du laboratoire dans le [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="a881a-197">You can add additional owners to a lab via the lab's blade in the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span> <span data-ttu-id="a881a-198">Toutefois, l’étendue d’administration du propriétaire ajouté est plus étroite que l’étendue du propriétaire de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="a881a-198">However, the added owner's scope of administration is more narrow than the subscription owner's scope.</span></span> <span data-ttu-id="a881a-199">Par exemple, les propriétaires ajoutés n’ont pas un accès complet à certaines ressources qui sont créées dans l’abonnement par le service DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="a881a-199">For example, the added owners do not have full access to some of the resources that are created in the subscription by the DevTest Labs service.</span></span> 

<span data-ttu-id="a881a-200">Pour ajouter un propriétaire à un abonnement Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="a881a-200">To add an owner to an Azure subscription, follow these steps:</span></span>

1. <span data-ttu-id="a881a-201">Connectez-vous au [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="a881a-201">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="a881a-202">Sélectionnez **Plus de services**, puis **Abonnements** dans la liste.</span><span class="sxs-lookup"><span data-stu-id="a881a-202">Select **More Services**, and then select **Subscriptions** from the list.</span></span>
3. <span data-ttu-id="a881a-203">Sélectionnez l’abonnement souhaité.</span><span class="sxs-lookup"><span data-stu-id="a881a-203">Select the desired subscription.</span></span>
4. <span data-ttu-id="a881a-204">Sélectionnez l’icône **Accès** .</span><span class="sxs-lookup"><span data-stu-id="a881a-204">Select **Access** icon.</span></span> 
   
    ![Accéder aux utilisateurs](./media/devtest-lab-add-devtest-user/access-users.png)
5. <span data-ttu-id="a881a-206">Dans le panneau **Utilisateurs**, sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="a881a-206">On the **Users** blade, select **Add**.</span></span>
   
    ![Ajouter un utilisateur](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
6. <span data-ttu-id="a881a-208">Dans le panneau **Sélectionner un rôle**, sélectionnez **Propriétaire**.</span><span class="sxs-lookup"><span data-stu-id="a881a-208">On the **Select a role** blade, select **Owner**.</span></span>
7. <span data-ttu-id="a881a-209">Dans le panneau **Ajouter des utilisateurs** , entrez l’adresse de messagerie ou le nom de l’utilisateur que vous souhaitez ajouter en tant que propriétaire.</span><span class="sxs-lookup"><span data-stu-id="a881a-209">On the **Add users** blade, enter the email address or name of the user you want to add as an owner.</span></span> <span data-ttu-id="a881a-210">Si l’utilisateur n’est pas trouvé, vous obtenez un message d’erreur expliquant le problème.</span><span class="sxs-lookup"><span data-stu-id="a881a-210">If the user can't be found, you get an error message explaining the issue.</span></span> <span data-ttu-id="a881a-211">Si l’utilisateur est trouvé, cet utilisateur est répertorié sous la zone de texte **Utilisateur** .</span><span class="sxs-lookup"><span data-stu-id="a881a-211">If the user is found, that user is listed under the **User** text box.</span></span>
8. <span data-ttu-id="a881a-212">Sélectionnez le nom d'utilisateur trouvé.</span><span class="sxs-lookup"><span data-stu-id="a881a-212">Select the located user name.</span></span>
9. <span data-ttu-id="a881a-213">Sélectionnez **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="a881a-213">Select **Select**.</span></span>
10. <span data-ttu-id="a881a-214">Cliquez sur **OK** pour fermer le panneau **Ajouter un accès**.</span><span class="sxs-lookup"><span data-stu-id="a881a-214">Select **OK** to close the **Add access** blade.</span></span>
11. <span data-ttu-id="a881a-215">Lorsque vous revenez sur le panneau **Utilisateurs** , l’utilisateur a été ajouté en tant que propriétaire.</span><span class="sxs-lookup"><span data-stu-id="a881a-215">When you return to the **Users** blade, the user has been added as an owner.</span></span> <span data-ttu-id="a881a-216">Cet utilisateur est désormais propriétaire de tous les laboratoires créés sous cet abonnement et peut par conséquent effectuer des tâches de propriétaire.</span><span class="sxs-lookup"><span data-stu-id="a881a-216">This user is now an owner of any labs created under this subscription, and thus be able to perform owner tasks.</span></span> 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

