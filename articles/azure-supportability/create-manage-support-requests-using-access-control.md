---
title: "Contrôle d’accès en fonction du rôle (RBAC) Azure pour contrôler les droits d’accès en vue de créer et de gérer des demandes de support | Microsoft Docs"
description: "Contrôle d’accès en fonction du rôle (RBAC) Azure pour contrôler les droits d’accès en vue de créer et de gérer des demandes de support"
author: ganganarayanan
ms.author: gangan
ms.date: 1/31/2017
ms.topic: article
ms.service: microsoft-docs
ms.assetid: 58a0ca9d-86d2-469a-9714-3b8320c33cf5
ms.openlocfilehash: 20ebd324cbf379980b43d255d468673de2b6d950
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-role-based-access-control-rbac-to-control-access-rights-to-create-and-manage-support-requests"></a><span data-ttu-id="25858-103">Contrôle d’accès en fonction du rôle (RBAC) Azure pour contrôler les droits d’accès en vue de créer et de gérer des demandes de support</span><span class="sxs-lookup"><span data-stu-id="25858-103">Azure Role-Based Access Control (RBAC) to control access rights to create and manage support requests</span></span>

<span data-ttu-id="25858-104">Le [contrôle d’accès en fonction du rôle (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) permet une gestion précise de l’accès pour Azure.</span><span class="sxs-lookup"><span data-stu-id="25858-104">[Role-Based Access Control (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) enables fine-grained access management for Azure.</span></span>
<span data-ttu-id="25858-105">La création de demandes de support dans le portail Azure, [portal.azure.com](https://portal.azure.com), utilise le modèle RBAC d’Azure pour définir qui peut créer et gérer les demandes de support.</span><span class="sxs-lookup"><span data-stu-id="25858-105">Support request creation in the Azure portal, [portal.azure.com](https://portal.azure.com), uses Azure’s RBAC model to define who can create and manage support requests.</span></span>
<span data-ttu-id="25858-106">L’accès est octroyé en attribuant le rôle RBAC approprié aux utilisateurs, groupes et applications, dans une étendue donnée, qui peut correspondre à un abonnement, un groupe de ressources ou une ressource.</span><span class="sxs-lookup"><span data-stu-id="25858-106">Access is granted by assigning the appropriate RBAC role to users, groups, and applications at a certain scope, which can be a subscription, resource group or a resource.</span></span>

<span data-ttu-id="25858-107">Prenons un exemple : en tant que propriétaire d’un groupe de ressources avec des autorisations de lecture dans l’étendue de l’abonnement, vous pouvez gérer toutes les ressources du groupe de ressources, telles que les sites Web, les machines virtuelles et les sous-réseaux.</span><span class="sxs-lookup"><span data-stu-id="25858-107">Let’s take an example: As a resource group owner with read permissions at the subscription scope, you can manage all the resources under the resource group, like websites, virtual machines, and subnets.</span></span>
<span data-ttu-id="25858-108">Toutefois, lorsque vous essayez de créer une demande de support par rapport à la ressource de machine virtuelle, vous rencontrez l’erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="25858-108">However, when you try to create a support request against the virtual machine resource, you encounter the following error</span></span>

![Erreur relative à l’abonnement](./media/create-manage-support-requests-using-access-control/subscription-error.png)

<span data-ttu-id="25858-110">Dans la gestion des demandes de support, vous devez disposer d’autorisations d’écriture ou d’un rôle qui possède l’action de support Microsoft.Support/* dans l’étendue de l’abonnement pour pouvoir créer et gérer des demandes de support.</span><span class="sxs-lookup"><span data-stu-id="25858-110">In support request management, you need write permission or a role that has the Support action Microsoft.Support/* at the Subscription scope to be able to create and manage support requests.</span></span>

<span data-ttu-id="25858-111">L’article suivant explique comment vous pouvez utiliser le contrôle RBAC personnalisé d’Azure pour créer et gérer les demandes de support dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="25858-111">The following article explains how you can use Azure’s custom Role-Based Access Control (RBAC) to create and manage support requests in the Azure portal.</span></span>

## <a name="getting-started"></a><span data-ttu-id="25858-112">Mise en route</span><span class="sxs-lookup"><span data-stu-id="25858-112">Getting Started</span></span>

<span data-ttu-id="25858-113">À l’aide de l’exemple ci-dessus, vous devriez être en mesure de créer une demande de support pour votre ressource, si un rôle RBAC personnalisé vous a été affecté pour l’abonnement par son propriétaire.</span><span class="sxs-lookup"><span data-stu-id="25858-113">Using the example above, you would be able to create a support request for your resource if you were assigned a custom RBAC role on the subscription by the subscription owner.</span></span>
<span data-ttu-id="25858-114">Il est possible de créer des [rôles RBAC personnalisés](https://azure.microsoft.com/documentation/articles/role-based-access-control-custom-roles/) à l’aide d’Azure PowerShell, de l’interface de ligne de commande Azure et de l’API REST.</span><span class="sxs-lookup"><span data-stu-id="25858-114">[Custom RBAC roles](https://azure.microsoft.com/documentation/articles/role-based-access-control-custom-roles/) can be created using Azure PowerShell, Azure Command-Line Interface (CLI), and the REST API.</span></span>

<span data-ttu-id="25858-115">La propriété Actions d’un rôle personnalisé spécifie les opérations Azure auxquelles le rôle accorde l’accès.</span><span class="sxs-lookup"><span data-stu-id="25858-115">The actions property of a custom role specifies the Azure operations to which the role grants access.</span></span>
<span data-ttu-id="25858-116">Pour créer un rôle personnalisé pour la gestion des demandes de support, le rôle doit disposer de l’action Microsoft.Support/*.</span><span class="sxs-lookup"><span data-stu-id="25858-116">To create a custom role for support request management, the role must have the action Microsoft.Support/*</span></span>

<span data-ttu-id="25858-117">Voici un exemple de rôle personnalisé que vous pouvez utiliser pour créer et gérer des demandes de support.</span><span class="sxs-lookup"><span data-stu-id="25858-117">Here’s an example of a custom role you can use to create and manage support requests.</span></span>
<span data-ttu-id="25858-118">Nous avons appelé ce rôle « Collaborateur de demande de support » et c’est ainsi que nous nous référerons au rôle personnalisé dans cet article.</span><span class="sxs-lookup"><span data-stu-id="25858-118">We’ve named this role “Support Request Contributor” and that’s how we refer to the custom role in this article.</span></span>

``` Json
{
    "Name":  "Support Request Contributor",
    "Id":  "1f2aad59-39b0-41da-b052-2fb070bd7942",
    "IsCustom":  true,
    "Description":  "Lets you create and manage support tickets.",
    "Actions":  [
                    "Microsoft.Support/*"
                ],
    "NotActions":  [
                   ],
    "AssignableScopes":  [
                             "/"
                         ]
}
```

<span data-ttu-id="25858-119">Suivez les étapes décrites dans [cette vidéo](https://www.youtube.com/watch?v=-PaBaDmfwKI) pour apprendre à créer un rôle personnalisé pour votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="25858-119">Follow the steps outlined in [this video](https://www.youtube.com/watch?v=-PaBaDmfwKI) to learn how to create a custom role for your subscription.</span></span>

## <a name="create-and-manage-support-requests-in-the-azure-portal"></a><span data-ttu-id="25858-120">Créer et gérer des demandes de support dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="25858-120">Create and manage support requests in the Azure portal</span></span>

<span data-ttu-id="25858-121">Prenons un exemple : vous êtes le propriétaire de l’abonnement « Abonnement Visual Studio MSDN ».</span><span class="sxs-lookup"><span data-stu-id="25858-121">Let’s take an example – you are the owner of Subscription "Visual Studio MSDN Subscription."</span></span>
<span data-ttu-id="25858-122">Jean, votre collègue, est propriétaire des ressources de certains groupes de ressources dans cet abonnement et dispose des autorisations de lecture sur l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="25858-122">Joe is your peer who is a resource owner to some of the resource groups in this subscription and has read permission to the subscription.</span></span>
<span data-ttu-id="25858-123">Vous souhaitez que votre collègue Jean ait la possibilité de créer et de gérer les tickets de support pour les ressources de cet abonnement.</span><span class="sxs-lookup"><span data-stu-id="25858-123">You wish to give access to your peer, Joe, the ability to create and manage support tickets for the resources under this subscription.</span></span>

1. <span data-ttu-id="25858-124">La première étape consiste à accéder à l’abonnement, puis, sous « Paramètres », vous verrez la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="25858-124">The first step is to go to the subscription and under "Settings" you see a list of users.</span></span> <span data-ttu-id="25858-125">Cliquez sur l’utilisateur Jean qui a accès en lecture à l’abonnement et affectez-lui un nouveau rôle personnalisé.</span><span class="sxs-lookup"><span data-stu-id="25858-125">Click the user Joe who has reader access on the Subscription and let’s assign a new custom role to him.</span></span>

    ![Ajouter un rôle](./media/create-manage-support-requests-using-access-control/add-role.png)

2. <span data-ttu-id="25858-127">Cliquez sur « Ajouter » dans le panneau « Utilisateurs ».</span><span class="sxs-lookup"><span data-stu-id="25858-127">Click "Add" under the "Users" blade.</span></span> <span data-ttu-id="25858-128">Sélectionnez le rôle personnalisé « Collaborateur de demande de support » dans la liste des rôles.</span><span class="sxs-lookup"><span data-stu-id="25858-128">Select the custom role "Support Request Contributor" from the list of roles</span></span>

    ![Ajouter le rôle Collaborateur du support](./media/create-manage-support-requests-using-access-control/add-support-contributor-role.png)

3. <span data-ttu-id="25858-130">Après avoir sélectionné le nom du rôle, cliquez sur « Ajouter des utilisateurs » et entrez les informations d’identification de la messagerie de Jean.</span><span class="sxs-lookup"><span data-stu-id="25858-130">After selecting the role name, click "Add users" and enter the Joe's email credentials.</span></span> <span data-ttu-id="25858-131">Cliquez sur « Sélectionner ».</span><span class="sxs-lookup"><span data-stu-id="25858-131">Click "Select"</span></span>

    ![Ajouter des utilisateurs](./media/create-manage-support-requests-using-access-control/add-users.png)

4. <span data-ttu-id="25858-133">Cliquez sur « OK » pour continuer.</span><span class="sxs-lookup"><span data-stu-id="25858-133">Click "Ok" to proceed</span></span>

    ![Ajout d'accès](./media/create-manage-support-requests-using-access-control/add-access.png)

5. <span data-ttu-id="25858-135">Vous voyez maintenant l’utilisateur avec le rôle personnalisé que vous venez d’ajouter « Collaborateur de demande de support » sous l’abonnement dont vous êtes le propriétaire.</span><span class="sxs-lookup"><span data-stu-id="25858-135">Now you see the user with the newly added custom role "Support Request Contributor" under the Subscription for which you are the owner</span></span>

    ![Utilisateur ajouté](./media/create-manage-support-requests-using-access-control/user-added.png)

    <span data-ttu-id="25858-137">Lorsque Jean ouvre une session dans le portail, il voit l’abonnement auquel il a été ajouté.</span><span class="sxs-lookup"><span data-stu-id="25858-137">When Joe logs in the portal, he sees the subscription to which he was added.</span></span>

7. <span data-ttu-id="25858-138">Jean clique sur « Nouvelle demande de support » dans le panneau « Aide et support » et il peut créer des demandes de support pour « Visual Studio Ultimate avec MSDN ».</span><span class="sxs-lookup"><span data-stu-id="25858-138">Joe clicks "New Support request" from the "Help and Support" blade and can create support requests for "Visual Studio Ultimate with MSDN"</span></span>

    ![Nouvelle demande de support](./media/create-manage-support-requests-using-access-control/new-support-request.png)

8. <span data-ttu-id="25858-140">Cliquant sur « Tous en charge les demandes » Joe peut afficher la liste des demandes de support créé pour cet abonnement ![cas afficher les détails](./media/create-manage-support-requests-using-access-control/case-details-view.png)</span><span class="sxs-lookup"><span data-stu-id="25858-140">Clicking "All support requests" Joe can see the list of support requests created for this Subscription  ![Case details view](./media/create-manage-support-requests-using-access-control/case-details-view.png)</span></span>

## <a name="remove-support-request-access-in-the-azure-portal"></a><span data-ttu-id="25858-141">Supprimer l’accès aux demandes de support dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="25858-141">Remove support request access in the Azure portal</span></span>

<span data-ttu-id="25858-142">De la même manière qu’il est possible d’accorder l’accès à un utilisateur pour créer et gérer des demandes de support, il est possible de le supprimer.</span><span class="sxs-lookup"><span data-stu-id="25858-142">Just as it is possible to grant access to a user to create and manage support requests, it's possible to remove access for the user as well.</span></span>
<span data-ttu-id="25858-143">Pour supprimer la possibilité de créer et de gérer les demandes de support, accédez à l’abonnement, cliquez sur « Paramètres », puis sur l’utilisateur (dans ce cas, Jean).</span><span class="sxs-lookup"><span data-stu-id="25858-143">To remove the ability to create and manage support requests, go to the Subscription, click "Settings" and click the user (in this case, Joe).</span></span>
<span data-ttu-id="25858-144">Cliquez avec le bouton droit sur le nom du rôle, « Collaborateur de demande de support » et cliquez sur « Supprimer ».</span><span class="sxs-lookup"><span data-stu-id="25858-144">Right-click the role name, "Support Request Contributor" and click "Remove"</span></span>

![Supprimer l’accès aux demandes de support](./media/create-manage-support-requests-using-access-control/remove-support-request-access.png)

<span data-ttu-id="25858-146">Lorsque Jean se connecte au portail et tente de créer une demande de support, il rencontre l’erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="25858-146">When Joe logs in to the portal and tries to create a support request, he encounters the following error</span></span>

![Erreur relative à l’abonnement-2](./media/create-manage-support-requests-using-access-control/subscription-error-2.png)

<span data-ttu-id="25858-148">Jean ne peut pas voir les demandes de support lorsqu’il clique sur « All support requests » (Toutes les demandes de support).</span><span class="sxs-lookup"><span data-stu-id="25858-148">Joe cannot see any support requests when he clicks "All support requests"</span></span>

![Vue Détails des cas-2](./media/create-manage-support-requests-using-access-control/case-details-view-2.png)
