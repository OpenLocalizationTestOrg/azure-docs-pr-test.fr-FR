---
title: "toocontrol de contrôle d’accès en fonction du rôle (RBAC) aaaAzure toocreate de droits d’accès et de gérer les demandes de prise en charge | Documents Microsoft"
description: "Azure toocontrol de contrôle d’accès en fonction du rôle (RBAC) toocreate de droits d’accès et de gérer les demandes de prise en charge"
author: ganganarayanan
ms.author: gangan
ms.date: 1/31/2017
ms.topic: article
ms.service: microsoft-docs
ms.assetid: 58a0ca9d-86d2-469a-9714-3b8320c33cf5
ms.openlocfilehash: c68a699ac870fa6bf371deb8ed0424848f39acf0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-role-based-access-control-rbac-toocontrol-access-rights-toocreate-and-manage-support-requests"></a><span data-ttu-id="281b0-103">Azure toocontrol de contrôle d’accès en fonction du rôle (RBAC) toocreate de droits d’accès et de gérer les demandes de prise en charge</span><span class="sxs-lookup"><span data-stu-id="281b0-103">Azure Role-Based Access Control (RBAC) toocontrol access rights toocreate and manage support requests</span></span>

<span data-ttu-id="281b0-104">Le [contrôle d’accès en fonction du rôle (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) permet une gestion précise de l’accès pour Azure.</span><span class="sxs-lookup"><span data-stu-id="281b0-104">[Role-Based Access Control (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) enables fine-grained access management for Azure.</span></span>
<span data-ttu-id="281b0-105">Prend en charge la création de demande dans le portail Azure, de hello [portal.azure.com](https://portal.azure.com), utilise toodefine de modèle RBAC de Azure qui peut créer et gérer les demandes de prise en charge.</span><span class="sxs-lookup"><span data-stu-id="281b0-105">Support request creation in hello Azure portal, [portal.azure.com](https://portal.azure.com), uses Azure’s RBAC model toodefine who can create and manage support requests.</span></span>
<span data-ttu-id="281b0-106">L’accès est accordé en assignant hello toousers du rôle RBAC appropriés, les groupes et les applications à une certaine étendue, qui peut être un abonnement, groupe de ressources ou une ressource.</span><span class="sxs-lookup"><span data-stu-id="281b0-106">Access is granted by assigning hello appropriate RBAC role toousers, groups, and applications at a certain scope, which can be a subscription, resource group or a resource.</span></span>

<span data-ttu-id="281b0-107">Prenons un exemple : en tant que propriétaire d’un groupe de ressources avec des autorisations de lecture au niveau de l’étendue de l’abonnement hello, vous pouvez gérer toutes les ressources hello sous le groupe de ressources hello, telles que les sites Web, des ordinateurs virtuels et des sous-réseaux.</span><span class="sxs-lookup"><span data-stu-id="281b0-107">Let’s take an example: As a resource group owner with read permissions at hello subscription scope, you can manage all hello resources under hello resource group, like websites, virtual machines, and subnets.</span></span>
<span data-ttu-id="281b0-108">Toutefois, lorsque vous essayez de toocreate une demande de support par rapport à la ressource d’ordinateur virtuel hello, vous rencontrez hello l’erreur suivante</span><span class="sxs-lookup"><span data-stu-id="281b0-108">However, when you try toocreate a support request against hello virtual machine resource, you encounter hello following error</span></span>

![Erreur relative à l’abonnement](./media/create-manage-support-requests-using-access-control/subscription-error.png)

<span data-ttu-id="281b0-110">Dans la gestion des demandes de prise en charge, vous devez écrire d’autorisation ou un rôle qui a hello prennent en charge l’action Microsoft.Support/* à hello abonnement étendue toobe en mesure de toocreate et gérer les demandes de prise en charge.</span><span class="sxs-lookup"><span data-stu-id="281b0-110">In support request management, you need write permission or a role that has hello Support action Microsoft.Support/* at hello Subscription scope toobe able toocreate and manage support requests.</span></span>

<span data-ttu-id="281b0-111">Bonjour à l’article suivant explique comment vous pouvez utiliser toocreate de contrôle d’accès en fonction du rôle (RBAC) de Azure personnalisée et gérer les demandes de prise en charge dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="281b0-111">hello following article explains how you can use Azure’s custom Role-Based Access Control (RBAC) toocreate and manage support requests in hello Azure portal.</span></span>

## <a name="getting-started"></a><span data-ttu-id="281b0-112">Mise en route</span><span class="sxs-lookup"><span data-stu-id="281b0-112">Getting Started</span></span>

<span data-ttu-id="281b0-113">À l’aide d’exemple hello ci-dessus, vous serez en mesure de toocreate une demande de support pour votre ressource si vous ont été affectés à un rôle RBAC personnalisé sur l’abonnement de hello par le propriétaire de l’abonnement hello.</span><span class="sxs-lookup"><span data-stu-id="281b0-113">Using hello example above, you would be able toocreate a support request for your resource if you were assigned a custom RBAC role on hello subscription by hello subscription owner.</span></span>
<span data-ttu-id="281b0-114">[Des rôles personnalisés RBAC](https://azure.microsoft.com/documentation/articles/role-based-access-control-custom-roles/) peuvent être créés à l’aide d’Azure PowerShell et hello API REST Azure Interface de ligne de commande (CLI).</span><span class="sxs-lookup"><span data-stu-id="281b0-114">[Custom RBAC roles](https://azure.microsoft.com/documentation/articles/role-based-access-control-custom-roles/) can be created using Azure PowerShell, Azure Command-Line Interface (CLI), and hello REST API.</span></span>

<span data-ttu-id="281b0-115">propriété d’actions Hello d’un rôle personnalisé spécifie hello opérations Azure toowhich hello rôle accorde un accès.</span><span class="sxs-lookup"><span data-stu-id="281b0-115">hello actions property of a custom role specifies hello Azure operations toowhich hello role grants access.</span></span>
<span data-ttu-id="281b0-116">toocreate un rôle personnalisé pour la gestion des demandes de prise en charge, hello rôle doit disposer d’action de hello Microsoft.Support/*</span><span class="sxs-lookup"><span data-stu-id="281b0-116">toocreate a custom role for support request management, hello role must have hello action Microsoft.Support/*</span></span>

<span data-ttu-id="281b0-117">Voici un exemple d’un rôle personnalisé, vous pouvez utiliser toocreate et gérer prennent en charge des demandes.</span><span class="sxs-lookup"><span data-stu-id="281b0-117">Here’s an example of a custom role you can use toocreate and manage support requests.</span></span>
<span data-ttu-id="281b0-118">Nous avons nommé ce rôle « Contributeur de demande de prise en charge » et qui est la façon dont nous nous référons toohello le rôle personnalisé dans cet article.</span><span class="sxs-lookup"><span data-stu-id="281b0-118">We’ve named this role “Support Request Contributor” and that’s how we refer toohello custom role in this article.</span></span>

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

<span data-ttu-id="281b0-119">Suivez les étapes de hello décrites dans [cette vidéo](https://www.youtube.com/watch?v=-PaBaDmfwKI) toolearn comment toocreate un rôle personnalisé pour votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="281b0-119">Follow hello steps outlined in [this video](https://www.youtube.com/watch?v=-PaBaDmfwKI) toolearn how toocreate a custom role for your subscription.</span></span>

## <a name="create-and-manage-support-requests-in-hello-azure-portal"></a><span data-ttu-id="281b0-120">Créer et gérer des demandes de support Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="281b0-120">Create and manage support requests in hello Azure portal</span></span>

<span data-ttu-id="281b0-121">Prenons un exemple : vous êtes propriétaire hello d’abonnement « Visual Studio abonnement MSDN. »</span><span class="sxs-lookup"><span data-stu-id="281b0-121">Let’s take an example – you are hello owner of Subscription "Visual Studio MSDN Subscription."</span></span>
<span data-ttu-id="281b0-122">Joe est votre homologue qui est un toosome de propriétaire de la ressource de groupes de ressources de hello dans cet abonnement et a lu l’abonnement de toohello d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="281b0-122">Joe is your peer who is a resource owner toosome of hello resource groups in this subscription and has read permission toohello subscription.</span></span>
<span data-ttu-id="281b0-123">Vous souhaitez toogive accès tooyour homologue, Joe, hello capacité toocreate et gérez les tickets de prise en charge pour les ressources hello sous cet abonnement.</span><span class="sxs-lookup"><span data-stu-id="281b0-123">You wish toogive access tooyour peer, Joe, hello ability toocreate and manage support tickets for hello resources under this subscription.</span></span>

1. <span data-ttu-id="281b0-124">première étape de Hello est toogo toohello abonnement et sous « Paramètres », vous voyez une liste d’utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="281b0-124">hello first step is toogo toohello subscription and under "Settings" you see a list of users.</span></span> <span data-ttu-id="281b0-125">Cliquez sur l’utilisateur hello Joe qui a accès en lecture sur hello abonnement et nous allons affecter un nouveau toohim de rôle personnalisé.</span><span class="sxs-lookup"><span data-stu-id="281b0-125">Click hello user Joe who has reader access on hello Subscription and let’s assign a new custom role toohim.</span></span>

    ![Ajouter un rôle](./media/create-manage-support-requests-using-access-control/add-role.png)

2. <span data-ttu-id="281b0-127">Cliquez sur « Ajouter » sous le panneau des « Utilisateurs » hello.</span><span class="sxs-lookup"><span data-stu-id="281b0-127">Click "Add" under hello "Users" blade.</span></span> <span data-ttu-id="281b0-128">Sélectionnez le rôle de personnalisé de hello « Contributeur de demande de prise en charge » à partir de la liste de hello des rôles</span><span class="sxs-lookup"><span data-stu-id="281b0-128">Select hello custom role "Support Request Contributor" from hello list of roles</span></span>

    ![Ajouter le rôle Collaborateur du support](./media/create-manage-support-requests-using-access-control/add-support-contributor-role.png)

3. <span data-ttu-id="281b0-130">Après avoir sélectionné le nom de rôle hello, cliquez sur « Ajouter des utilisateurs » et entrez les informations d’identification de la messagerie de Jacques hello.</span><span class="sxs-lookup"><span data-stu-id="281b0-130">After selecting hello role name, click "Add users" and enter hello Joe's email credentials.</span></span> <span data-ttu-id="281b0-131">Cliquez sur « Sélectionner ».</span><span class="sxs-lookup"><span data-stu-id="281b0-131">Click "Select"</span></span>

    ![Ajouter des utilisateurs](./media/create-manage-support-requests-using-access-control/add-users.png)

4. <span data-ttu-id="281b0-133">Cliquez sur « Ok » tooproceed</span><span class="sxs-lookup"><span data-stu-id="281b0-133">Click "Ok" tooproceed</span></span>

    ![Ajout d'accès](./media/create-manage-support-requests-using-access-control/add-access.png)

5. <span data-ttu-id="281b0-135">Vous voyez à présent utilisateur hello avec rôle personnalisé nouvellement ajoutée « Prise en charge de demande contributeur » sous abonnement hello dont vous êtes propriétaire de hello hello</span><span class="sxs-lookup"><span data-stu-id="281b0-135">Now you see hello user with hello newly added custom role "Support Request Contributor" under hello Subscription for which you are hello owner</span></span>

    ![Utilisateur ajouté](./media/create-manage-support-requests-using-access-control/user-added.png)

    <span data-ttu-id="281b0-137">Lorsque Joe s’ouvre dans le portail de hello, il voit toowhich d’abonnement hello qu’il a été ajouté.</span><span class="sxs-lookup"><span data-stu-id="281b0-137">When Joe logs in hello portal, he sees hello subscription toowhich he was added.</span></span>

7. <span data-ttu-id="281b0-138">Jean clique sur « Nouvelle demande de Support » à partir du Panneau de « Aide et prise en charge » hello et créer des demandes de prise en charge pour « Visual Studio Ultimate avec MSDN »</span><span class="sxs-lookup"><span data-stu-id="281b0-138">Joe clicks "New Support request" from hello "Help and Support" blade and can create support requests for "Visual Studio Ultimate with MSDN"</span></span>

    ![Nouvelle demande de support](./media/create-manage-support-requests-using-access-control/new-support-request.png)

8. <span data-ttu-id="281b0-140">Cliquant sur « Tous en charge les demandes » Joe peut afficher hello liste de demandes de support créé pour cet abonnement ![cas afficher les détails](./media/create-manage-support-requests-using-access-control/case-details-view.png)</span><span class="sxs-lookup"><span data-stu-id="281b0-140">Clicking "All support requests" Joe can see hello list of support requests created for this Subscription  ![Case details view](./media/create-manage-support-requests-using-access-control/case-details-view.png)</span></span>

## <a name="remove-support-request-access-in-hello-azure-portal"></a><span data-ttu-id="281b0-141">Supprimer l’accès de demande de prise en charge dans hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="281b0-141">Remove support request access in hello Azure portal</span></span>

<span data-ttu-id="281b0-142">Comme il est possible de toogrant accès tooa utilisateur toocreate et gérer les demandes de prise en charge, il est tooremove possible l’accès pour l’utilisateur hello ainsi.</span><span class="sxs-lookup"><span data-stu-id="281b0-142">Just as it is possible toogrant access tooa user toocreate and manage support requests, it's possible tooremove access for hello user as well.</span></span>
<span data-ttu-id="281b0-143">tooremove hello toocreate de capacité et gérer les demandes de prise en charge, accédez toohello abonnement, cliquez sur « Paramètres » puis cliquez sur utilisateur hello (dans ce cas, Joe).</span><span class="sxs-lookup"><span data-stu-id="281b0-143">tooremove hello ability toocreate and manage support requests, go toohello Subscription, click "Settings" and click hello user (in this case, Joe).</span></span>
<span data-ttu-id="281b0-144">Cliquez sur le nom de rôle hello, « Prise en charge de demande contributeur » et cliquez sur « Supprimer »</span><span class="sxs-lookup"><span data-stu-id="281b0-144">Right-click hello role name, "Support Request Contributor" and click "Remove"</span></span>

![Supprimer l’accès aux demandes de support](./media/create-manage-support-requests-using-access-control/remove-support-request-access.png)

<span data-ttu-id="281b0-146">Lorsque Joe toohello portail se connecte et tente de toocreate une demande de support, il rencontre hello l’erreur suivante</span><span class="sxs-lookup"><span data-stu-id="281b0-146">When Joe logs in toohello portal and tries toocreate a support request, he encounters hello following error</span></span>

![Erreur relative à l’abonnement-2](./media/create-manage-support-requests-using-access-control/subscription-error-2.png)

<span data-ttu-id="281b0-148">Jean ne peut pas voir les demandes de support lorsqu’il clique sur « All support requests » (Toutes les demandes de support).</span><span class="sxs-lookup"><span data-stu-id="281b0-148">Joe cannot see any support requests when he clicks "All support requests"</span></span>

![Vue Détails des cas-2](./media/create-manage-support-requests-using-access-control/case-details-view-2.png)
