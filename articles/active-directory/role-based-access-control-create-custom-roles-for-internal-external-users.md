---
title: "Créer des rôles de contrôle d’accès en fonction du rôle personnalisés et les attribuer à des utilisateurs internes et externes dans Azure | Documents Microsoft"
description: "Attribuer des rôles RBAC personnalisés créés à l’aide de PowerShell et d’Azure CLI à des utilisateurs internes et externes"
services: active-directory
documentationcenter: 
author: andreicradu
manager: catadinu
editor: kgremban
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/10/2017
ms.author: a-crradu
ms.openlocfilehash: d687f94bebfd0b6c1ec0690da798be5409640954
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
## <a name="intro-on-role-based-access-control"></a><span data-ttu-id="25483-103">Contrôle d’accès en fonction du rôle Azure</span><span class="sxs-lookup"><span data-stu-id="25483-103">Intro on role-based access control</span></span>

<span data-ttu-id="25483-104">Le contrôle d’accès en fonction du rôle (RBAC) est une fonctionnalité exclusive du portail Azure permettant aux propriétaires d’abonnement d’attribuer des rôles granulaires à d’autres utilisateurs afin qu’ils puissent gérer des étendues de ressource spécifiques dans leur environnement.</span><span class="sxs-lookup"><span data-stu-id="25483-104">Role-based access control is an Azure portal only feature allowing the owners of a subscription to assign granular roles to other users who can manage specific resource scopes in their environment.</span></span>

<span data-ttu-id="25483-105">La fonctionnalité RBAC permet une meilleure gestion de la sécurité pour les grandes organisations et pour les PME travaillant avec des collaborateurs, fournisseurs ou travailleurs indépendants externes qui doivent pouvoir accéder à des ressources spécifiques de l’environnement de l’entreprise, mais pas nécessairement à l’infrastructure toute entière ou à des étendues liées à la facturation.</span><span class="sxs-lookup"><span data-stu-id="25483-105">RBAC allows better security management for large organizations and for SMBs working with external collaborators, vendors or freelancers which need access to specific resources in your environment but not necessarily to the entire infrastructure or any billing-related scopes.</span></span> <span data-ttu-id="25483-106">La fonctionnalité RBAC offre la flexibilité de pouvoir être propriétaire d’un seul abonnement Azure géré par le compte d’administrateur (rôle Administrateur du service au niveau d’un abonnement) et d’avoir plusieurs utilisateurs invités à travailler dans le cadre de cet abonnement, mais sans droits d’administration sur celui-ci.</span><span class="sxs-lookup"><span data-stu-id="25483-106">RBAC allows the flexibility of owning one Azure subscription managed by the administrator account (service administrator role at a subscription level) and have multiple users invited to work under the same subscription but without any administrative rights for it.</span></span> <span data-ttu-id="25483-107">Du point de vue de la facturation et de la gestion, la fonctionnalité RBAC s’avère être une option efficace en termes de temps et de gestion pour l’utilisation d’Azure dans diverses circonstances.</span><span class="sxs-lookup"><span data-stu-id="25483-107">From a management and billing perspective, the RBAC feature proves to be a time and management efficient option for using Azure in various scenarios.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="25483-108">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="25483-108">Prerequisites</span></span>
<span data-ttu-id="25483-109">L’utilisation de la fonctionnalité RBAC dans l’environnement Windows Azure nécessite ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="25483-109">Using RBAC in the Azure environment requires:</span></span>

* <span data-ttu-id="25483-110">Avoir un abonnement Azure autonome attribué à l’utilisateur en tant que propriétaire (rôle d’abonnement)</span><span class="sxs-lookup"><span data-stu-id="25483-110">Having a standalone Azure subscription assigned to the user as owner (subscription role)</span></span>
* <span data-ttu-id="25483-111">Avoir le rôle Propriétaire de l’abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="25483-111">Have the Owner role of the Azure subscription</span></span>
* <span data-ttu-id="25483-112">Avoir accès au [portail Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="25483-112">Have access to the [Azure portal](https://portal.azure.com)</span></span>
* <span data-ttu-id="25483-113">Avoir le fournisseur de ressources suivant inscrit pour l’abonnement de l’utilisateur : **Microsoft.Authorization**.</span><span class="sxs-lookup"><span data-stu-id="25483-113">Make sure to have the following Resource Providers registered for the user subscription: **Microsoft.Authorization**.</span></span> <span data-ttu-id="25483-114">Pour plus d’informations sur l’enregistrement des fournisseurs de ressources, voir [Fournisseurs, régions, schémas et versions d’API Resource Manager](/azure-resource-manager/resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="25483-114">For more information on how to register the resource providers, see [Resource Manager providers, regions, API versions and schemas](/azure-resource-manager/resource-manager-supported-services.md).</span></span>

> [!NOTE]
> <span data-ttu-id="25483-115">Ni les abonnements Office 365 ni les licences Azure Active Directory (par exemple, Accès à Azure Active Directory) approvisionnées à partir du portail O365 ne sont éligibles pour l’utilisation de la fonctionnalité RBAC.</span><span class="sxs-lookup"><span data-stu-id="25483-115">Office 365 subscriptions or Azure Active Directory licenses (for example: Access to Azure Active Directory) provisioned from the O365 portal don't quality for using RBAC.</span></span>

## <a name="how-can-rbac-be-used"></a><span data-ttu-id="25483-116">Comment la fonctionnalité RBAC peut être utilisée</span><span class="sxs-lookup"><span data-stu-id="25483-116">How can RBAC be used</span></span>
<span data-ttu-id="25483-117">La fonctionnalité RBAC peut être appliquée à trois étendues différentes dans Azure.</span><span class="sxs-lookup"><span data-stu-id="25483-117">RBAC can be applied at three different scopes in Azure.</span></span> <span data-ttu-id="25483-118">De la plus élevée à la plus basse, ces étendues sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="25483-118">From the highest scope to the lowest one, they are as follows:</span></span>

* <span data-ttu-id="25483-119">Abonnement (la plus élevée)</span><span class="sxs-lookup"><span data-stu-id="25483-119">Subscription (highest)</span></span>
* <span data-ttu-id="25483-120">Groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="25483-120">Resource group</span></span>
* <span data-ttu-id="25483-121">Ressource (niveau d’accès le plus bas offrant des autorisations ciblées pour une étendue de ressource Azure)</span><span class="sxs-lookup"><span data-stu-id="25483-121">Resource scope (the lowest access level offering targeted permissions to an individual Azure resource scope)</span></span>

## <a name="assign-rbac-roles-at-the-subscription-scope"></a><span data-ttu-id="25483-122">Attribuer des rôles RBAC à l’étendue d’abonnement</span><span class="sxs-lookup"><span data-stu-id="25483-122">Assign RBAC roles at the subscription scope</span></span>
<span data-ttu-id="25483-123">Il existe notamment deux cas courants d’utilisation de la fonctionnalité RBAC :</span><span class="sxs-lookup"><span data-stu-id="25483-123">There are two common examples when RBAC is used (but not limited to):</span></span>

* <span data-ttu-id="25483-124">Invitation d’utilisateurs externes à l’organisation (ne faisant pas partie du client Azure Active Directory de l’utilisateur administrateur) à gérer certaines ressources ou la totalité de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="25483-124">Having external users from the organizations (not part of the admin user's Azure Active Directory tenant) invited to manage certain resources or the whole subscription</span></span>
* <span data-ttu-id="25483-125">Collaboration avec des utilisateurs internes à l’organisation (faisant partie du client Azure Active Directory de l’utilisateur) qui appartiennent à différents groupes ou équipes qui doivent avoir un accès granulaire soit à la totalité de l’abonnement, soit à certains groupes ou étendues de ressources dans l’environnement.</span><span class="sxs-lookup"><span data-stu-id="25483-125">Working with users inside the organization (they are part of the user's Azure Active Directory tenant) but part of different teams or groups which need granular access either to the whole subscription or to certain resource groups or resource scopes in the environment</span></span>

## <a name="grant-access-at-a-subscription-level-for-a-user-outside-of-azure-active-directory"></a><span data-ttu-id="25483-126">Octroyer l’accès au niveau d’un abonnement à un utilisateur extérieur à Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="25483-126">Grant access at a subscription level for a user outside of Azure Active Directory</span></span>
<span data-ttu-id="25483-127">Les rôles RBAC peuvent être octroyés uniquement par des **propriétaires** d’abonnement. Par conséquent, l’utilisateur administrateur doit être connecté avec un nom d’utilisateur auquel ce rôle est pré-attribué ou qui a créé l’abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="25483-127">RBAC roles can be granted only by **Owners** of the subscription therefore the admin user must be logged with a username which has this role pre-assigned or has created the Azure subscription.</span></span>

<span data-ttu-id="25483-128">Dans le portail Azure, après vous être connecté en tant qu’administrateur, sélectionnez « Abonnements », puis choisissez l’abonnement souhaité.</span><span class="sxs-lookup"><span data-stu-id="25483-128">From the Azure portal, after you sign-in as admin, select “Subscriptions” and chose the desired one.</span></span>
<span data-ttu-id="25483-129">![Panneau d’abonnement dans le portail Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png) Par défaut, si l’utilisateur administrateur a acheté l’abonnement Azure, il apparaît en tant que **Administrateur de compte**, ce qui correspond au rôle d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="25483-129">![subscription blade in Azure portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png) By default, if the admin user has purchased the Azure subscription, the user will show up as **Account Admin**, this being the subscription role.</span></span> <span data-ttu-id="25483-130">Pour plus d’informations sur les rôles d’abonnement Azure, voir [Ajouter ou modifier des rôles Administrateur Azure qui gèrent l’abonnement ou les services](/billing/billing-add-change-azure-subscription-administrator.md).</span><span class="sxs-lookup"><span data-stu-id="25483-130">For more details on the Azure subscription roles, see [Add or change Azure administrator roles that manage the subscription or services](/billing/billing-add-change-azure-subscription-administrator.md).</span></span>

<span data-ttu-id="25483-131">Dans cet exemple, l’utilisateur « alflanigan@outlook.com » est le **Propriétaire** de l’abonnement « Évaluation gratuite » dans le client AAD « Client Azure par défaut ».</span><span class="sxs-lookup"><span data-stu-id="25483-131">In this example, the user "alflanigan@outlook.com" is the **Owner** of the "Free Trial" subscription in the AAD tenant "Default tenant Azure".</span></span> <span data-ttu-id="25483-132">Étant donné que cet utilisateur est le créateur de l’abonnement Azure avec le compte Microsoft initial « Outlook » (compte Microsoft = Outlook, Live, etc.), le nom de domaine par défaut pour tous les autres utilisateurs ajoutés à ce client sera **« @alflaniganuoutlook.onmicrosoft.com »**.</span><span class="sxs-lookup"><span data-stu-id="25483-132">Since this user is the creator of the Azure subscription with the initial Microsoft Account “Outlook” (Microsoft Account = Outlook, Live etc.) the default domain name for all other users added in this tenant will be **"@alflaniganuoutlook.onmicrosoft.com"**.</span></span> <span data-ttu-id="25483-133">Par conception, la syntaxe du nouveau domaine est formée par assemblage du nom d’utilisateur et du nom domaine de l’utilisateur qui a créé le client, avec ajout de l’extension **« .onmicrosoft.com »**.</span><span class="sxs-lookup"><span data-stu-id="25483-133">By design, the syntax of the new domain is formed by putting together the username and domain name of the user who created the tenant and adding the extension **".onmicrosoft.com"**.</span></span>
<span data-ttu-id="25483-134">De plus, les utilisateurs peuvent se connecter avec un nom de domaine personnalisé dans le client, après ajout et vérification de ce nom de domaine pour le nouveau client.</span><span class="sxs-lookup"><span data-stu-id="25483-134">Furthermore, users can sign-in with a custom domain name in the tenant after adding and verifying it for the new tenant.</span></span> <span data-ttu-id="25483-135">Pour plus d’informations sur la façon de vérifier un nom de domaine personnalisé dans un client Azure Active Directory, voir [Ajouter un nom de domaine personnalisé à votre annuaire](/active-directory/active-directory-add-domain).</span><span class="sxs-lookup"><span data-stu-id="25483-135">For more details on how to verify a custom domain name in an Azure Active Directory tenant, see [Add a custom domain name to your directory](/active-directory/active-directory-add-domain).</span></span>

<span data-ttu-id="25483-136">Dans cet exemple, l’annuaire « Client par défaut Azure » contient uniquement les utilisateurs dont le nom de domaine est « @alflanigan.onmicrosoft.com ».</span><span class="sxs-lookup"><span data-stu-id="25483-136">In this example, the "Default tenant Azure" directory contains only users with the domain name "@alflanigan.onmicrosoft.com".</span></span>

<span data-ttu-id="25483-137">Après avoir sélectionné l’abonnement, l’utilisateur administrateur doit cliquer sur **Contrôle d’accès (IAM)**, puis sur **Ajouter un nouveau rôle**.</span><span class="sxs-lookup"><span data-stu-id="25483-137">After selecting the subscription, the admin user must click **Access Control (IAM)** and then **Add a new role**.</span></span>





![fonctionnalité de contrôle d’accès IAM dans le portail Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/1.png)





![ajouter un utilisateur dans la fonctionnalité de contrôle d’accès IAM dans le portail Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/2.png)

<span data-ttu-id="25483-140">L’étape suivante consiste à sélectionner le rôle à attribuer et l’utilisateur à qui le rôle RBAC doit être attribué.</span><span class="sxs-lookup"><span data-stu-id="25483-140">The next step is to select the role to be assigned and the user whom the RBAC role will be assigned to.</span></span> <span data-ttu-id="25483-141">Dans le menu déroulant **Rôle**, l’utilisateur administrateur voit uniquement les rôles RBAC intégrés disponibles dans Azure.</span><span class="sxs-lookup"><span data-stu-id="25483-141">In the **Role** dropdown menu the admin user sees only the built-in RBAC roles which are available in Azure.</span></span> <span data-ttu-id="25483-142">Pour plus d’explications sur chaque rôle et les étendues qui peuvent lui être attribuées, voir [Rôles intégrés pour contrôle d’accès en fonction du rôle Azure](/active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="25483-142">For more detailed explanations of each role and their assignable scopes, see [Built-in roles for Azure Role-Based Access Control](/active-directory/role-based-access-built-in-roles.md).</span></span>

<span data-ttu-id="25483-143">L’utilisateur administrateur doit ensuite ajouter l’adresse de messagerie de l’utilisateur externe.</span><span class="sxs-lookup"><span data-stu-id="25483-143">The admin user then needs to add the email address of the external user.</span></span> <span data-ttu-id="25483-144">Le comportement attendu est que l’utilisateur externe n'apparaisse pas dans le client existant.</span><span class="sxs-lookup"><span data-stu-id="25483-144">The expected behavior is for the external user to not show up in the existing tenant.</span></span> <span data-ttu-id="25483-145">Une fois l’utilisateur externe invité, il est visible sous **Abonnements > Contrôle d’accès (IAM)** avec tous les utilisateurs auxquels un rôle RBAC est actuellement attribué dans l’étendue de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="25483-145">After the external user has been invited, he will be visible under **Subscriptions > Access Control (IAM)** with all the current users which are currently assigned an RBAC role at the Subscription scope.</span></span>





![ajouter des autorisations au nouveau rôle RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/3.png)





![liste des rôles RBAC au niveau abonnement](./media/role-based-access-control-create-custom-roles-for-internal-external-users/4.png)

<span data-ttu-id="25483-148">L’utilisateur « chessercarlton@gmail.com » a été invité à être **Propriétaire** d’un abonnement « Évaluation gratuite ».</span><span class="sxs-lookup"><span data-stu-id="25483-148">The user "chessercarlton@gmail.com" has been invited to be an **Owner** for the “Free Trial” subscription.</span></span> <span data-ttu-id="25483-149">Une fois l’invitation envoyée, l’utilisateur externe reçoit un e-mail de confirmation contenant un lien d’activation.</span><span class="sxs-lookup"><span data-stu-id="25483-149">After sending the invitation, the external user will receive an email confirmation with an activation link.</span></span>
<span data-ttu-id="25483-150">![e-mail d'invitation pour le rôles RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)</span><span class="sxs-lookup"><span data-stu-id="25483-150">![email invitation for RBAC role](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)</span></span>

<span data-ttu-id="25483-151">Étant externe à l’organisation, le nouvel utilisateur ne dispose pas de tous les attributs existants dans l’annuaire « Client Azure par défaut ».</span><span class="sxs-lookup"><span data-stu-id="25483-151">Being external to the organization, the new user does not have any existing attributes in the "Default tenant Azure" directory.</span></span> <span data-ttu-id="25483-152">Ceux-ci sont créés après que l’utilisateur externe a consenti à être inscrit dans l’annuaire associé à l’abonnement pour lequel un rôle lui a été attribué.</span><span class="sxs-lookup"><span data-stu-id="25483-152">They will be created after the external user has given consent to be recorded in the directory which is associated with the subscription which he has been assigned a role to.</span></span>





![e-mail d’invitation pour le rôle RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/6.png)

<span data-ttu-id="25483-154">L’utilisateur externe apparaît désormais dans le client Azure Active Directory en tant qu’utilisateur externe, et est visible tant sur le portail Azure que sur le portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="25483-154">The external user shows in the Azure Active Directory tenant from now on as external user and this can be viewed both in the Azure portal and in the classic portal.</span></span>





![panneau des utilisateurs azure active directory sur le portail azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/7.png)





![panneau des utilisateurs azure active directory sur le portail azure classic](./media/role-based-access-control-create-custom-roles-for-internal-external-users/8.png)

<span data-ttu-id="25483-157">Dans l’affichage **Utilisateurs** sur les deux portails, les utilisateurs externes peuvent être identifiés comme suit :</span><span class="sxs-lookup"><span data-stu-id="25483-157">In the **Users** view in both portals the external users can be recognized by:</span></span>

* <span data-ttu-id="25483-158">par le type d’icône distinct sur le portail Azure ;</span><span class="sxs-lookup"><span data-stu-id="25483-158">The different icon type in the Azure portal</span></span>
* <span data-ttu-id="25483-159">par le point d’approvisionnement sur le portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="25483-159">The different sourcing point in the classic portal</span></span>

<span data-ttu-id="25483-160">Toutefois, l’octroi à un utilisateur externe d’un accès **Propriétaire** ou **Contributeur** à l’étendue **Abonnement** n’autorise pas l’accès à l’annuaire de l’utilisateur administrateur, sauf si l’**Administrateur général** l’autorise.</span><span class="sxs-lookup"><span data-stu-id="25483-160">However, granting **Owner** or **Contributor** access to an external user at the **Subscription** scope, does not allow the access to the admin user's directory, unless the **Global Admin** allows it.</span></span> <span data-ttu-id="25483-161">Dans les propriétés de l’utilisateur, le **Type d’utilisateur** qui a deux paramètres communs, **Membre** et **Invité**, peut être identifié.</span><span class="sxs-lookup"><span data-stu-id="25483-161">In the user proprieties,  the **User Type** which has two common parameters, **Member** and **Guest** can be identified.</span></span> <span data-ttu-id="25483-162">Un membre est un utilisateur inscrit dans l’annuaire, tandis qu’un invité est un utilisateur invité dans l’annuaire à partir d’une source externe.</span><span class="sxs-lookup"><span data-stu-id="25483-162">A member is a user which is registered in the directory while a guest is a user invited to the directory from an external source.</span></span> <span data-ttu-id="25483-163">Pour plus d’informations, voir [Comment les administrateurs Azure Active Directory ajoutent des utilisateurs B2B Collaboration](/active-directory/active-directory-b2b-admin-add-users).</span><span class="sxs-lookup"><span data-stu-id="25483-163">For more information, see [How do Azure Active Directory admins add B2B collaboration users](/active-directory/active-directory-b2b-admin-add-users).</span></span>

> [!NOTE]
> <span data-ttu-id="25483-164">Assurez-vous qu’une fois les informations d’identification entrées dans le portail, l’utilisateur externe sélectionne l’annuaire approprié auquel se connecter.</span><span class="sxs-lookup"><span data-stu-id="25483-164">Make sure that after entering the credentials in the portal, the external user selects the correct directory to sign-in to.</span></span> <span data-ttu-id="25483-165">Le même utilisateur peut avoir accès à plusieurs annuaires et sélectionner l’un d'eux en cliquant sur le nom d’utilisateur dans la partie supérieure droite du portail Azure, puis en choisissant l’annuaire approprié dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="25483-165">The same user can have access to multiple directories and can select either one of  them by clicking the username in the top right-hand side in the Azure portal and then choose the appropriate directory from the dropdown list.</span></span>

<span data-ttu-id="25483-166">Bien qu’étant un invité dans l’annuaire, l’utilisateur externe peut gérer toutes les ressources de l’abonnement Azure. En revanche, il ne peut pas accéder à l’annuaire.</span><span class="sxs-lookup"><span data-stu-id="25483-166">While being a guest in the directory, the external user can manage all resources for the Azure subscription, but can't access the directory.</span></span>





![accès restreint au portail azure active directory](./media/role-based-access-control-create-custom-roles-for-internal-external-users/9.png)

<span data-ttu-id="25483-168">Azure Active Directory et un abonnement Azure n’ont pas de relation enfant-parent comme l’ont d’autres ressources Azure (par exemple, Azure Virtual Machines, Azure Virtual Networks, Web Apps, Stockage Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="25483-168">Azure Active Directory and an Azure subscription don't have a child-parent relation like other Azure resources (for example: virtual machines, virtual networks, web apps, storage etc.) have with an Azure subscription.</span></span> <span data-ttu-id="25483-169">Ces dernières sont créées, gérées et facturées en relation avec un abonnement Azure, tandis que celui-ci est utilisé pour gérer l’accès à un annuaire Azure.</span><span class="sxs-lookup"><span data-stu-id="25483-169">All the latter is created, managed and billed under an Azure subscription while an Azure subscription is used to manage the access to an Azure directory.</span></span> <span data-ttu-id="25483-170">Pour plus d’informations, voir [Association des abonnements Azure avec Azure Active Directory](/active-directory/active-directory-how-subscriptions-associated-directory).</span><span class="sxs-lookup"><span data-stu-id="25483-170">For more details, see [How an Azure subscription is related to Azure AD](/active-directory/active-directory-how-subscriptions-associated-directory).</span></span>

<span data-ttu-id="25483-171">Parmi tous les rôles RBAC intégrés, les rôles **Propriétaire** et **Contributeur** offrent un accès en gestion complet à toutes les ressources de l’environnement, à la seule différence qu’un Contributeur ne peut pas créer ou supprimer des rôles RBAC.</span><span class="sxs-lookup"><span data-stu-id="25483-171">From all the built-in RBAC roles, **Owner** and **Contributor** offer full management access to all resources in the environment, the difference being that a Contributor can't create and delete new RBAC roles.</span></span> <span data-ttu-id="25483-172">Les autres rôles intégrés, tels que **Contributeur de machines virtuelles**, offrent un accès en gestion complet uniquement aux ressources indiquées par le nom, quel que soit le **Groupe de ressources** dans lequel ils sont créés.</span><span class="sxs-lookup"><span data-stu-id="25483-172">The other built-in roles like **Virtual Machine Contributor** offer full management access only to the resources indicated by the name, regardless of the **Resource Group** they are being created into.</span></span>

<span data-ttu-id="25483-173">L’attribution du rôle RBAC intégré **Contributeur de machines virtuelles** au niveau d’un abonnement signifie que l’utilisateur auquel le rôle est attribué :</span><span class="sxs-lookup"><span data-stu-id="25483-173">Assigning the built-in RBAC role of **Virtual Machine Contributor** at a subscription level, means that the user assigned the role:</span></span>

* <span data-ttu-id="25483-174">peut afficher tous les machines virtuelles, quelle que soit leur date de déploiement, ainsi que les groupes de ressources auxquels elles appartiennent ;</span><span class="sxs-lookup"><span data-stu-id="25483-174">Can view all virtual machines regardless their deployment date and the resource groups they are part of</span></span>
* <span data-ttu-id="25483-175">dispose d’accès en gestion complet aux machines virtuelles faisant partie de l’abonnement ;</span><span class="sxs-lookup"><span data-stu-id="25483-175">Has full management access to the virtual machines in the subscription</span></span>
* <span data-ttu-id="25483-176">ne peut pas afficher d’autres types de ressources faisant partie de l’abonnement ;</span><span class="sxs-lookup"><span data-stu-id="25483-176">Can't view any other resource types in the subscription</span></span>
* <span data-ttu-id="25483-177">ne peut apporter aucune modification sur le plan de la facturation.</span><span class="sxs-lookup"><span data-stu-id="25483-177">Can't operate any changes from a billing perspective</span></span>

> [!NOTE]
> <span data-ttu-id="25483-178">La fonctionnalité RBAC étant une fonctionnalité exclusive du portail Azure, elle ne donne pas accès au portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="25483-178">RBAC being an Azure portal only feature, it doesn't grant access to the classic portal.</span></span>

## <a name="assign-a-built-in-rbac-role-to-an-external-user"></a><span data-ttu-id="25483-179">Attribuer un rôle RBAC intégré à un utilisateur externe</span><span class="sxs-lookup"><span data-stu-id="25483-179">Assign a built-in RBAC role to an external user</span></span>
<span data-ttu-id="25483-180">Pour un autre scénario dans ce test, l’utilisateur externe « alflanigan@gmail.com » est ajouté en tant que **Contributeur de machines virtuelles**.</span><span class="sxs-lookup"><span data-stu-id="25483-180">For a different scenario in this test, the external user "alflanigan@gmail.com" is added as a **Virtual Machine Contributor**.</span></span>




![rôle prédéfini de contributeur de machines virtuelles](./media/role-based-access-control-create-custom-roles-for-internal-external-users/11.png)

<span data-ttu-id="25483-182">Le comportement normal de cet utilisateur externe avec ce rôle intégré est de voir et gérer uniquement les machines virtuelles et uniquement les ressources adjacentes de Resource Manager nécessaires lors du déploiement.</span><span class="sxs-lookup"><span data-stu-id="25483-182">The normal behavior for this external user with this built-in role is to see and manage only virtual machines and their adjacent Resource Manager only resources necessary while deploying.</span></span> <span data-ttu-id="25483-183">Par conception, ces rôles limités permettent d’accéder aux ressources correspondantes créées dans le portail Azure, même si certains peuvent encore être également déployés dans le portail Azure Classic (par exemple, les machines virtuelles).</span><span class="sxs-lookup"><span data-stu-id="25483-183">By design, these limited roles offer access only to their correspondent resources created in the Azure portal, regardless some can still be deployed in the classic portal as well (for example: virtual machines).</span></span>





![présentation du rôle contributeur de machines virtuelles dans le portail azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/12.png)

## <a name="grant-access-at-a-subscription-level-for-a-user-in-the-same-directory"></a><span data-ttu-id="25483-185">Octroyer l’accès au niveau d’un abonnement à un utilisateur figurant dans le même annuaire</span><span class="sxs-lookup"><span data-stu-id="25483-185">Grant access at a subscription level for a user in the same directory</span></span>
<span data-ttu-id="25483-186">Le flux du processus est identique à celui de l’ajout d’un utilisateur externe, tant dans la perspective de l’administrateur octroyant le rôle RBAC, que de celle de l’utilisateur auquel l’accès au rôle est octroyé.</span><span class="sxs-lookup"><span data-stu-id="25483-186">The process flow is identical to adding an external user, both from the admin perspective granting the RBAC role as well as the user being granted access to the role.</span></span> <span data-ttu-id="25483-187">La différence est que l’utilisateur invité ne reçoit pas d’e-mail d’invitation, car toutes les étendues de ressource au sein de l’abonnement sont disponibles dans le tableau de bord une fois la connexion établie.</span><span class="sxs-lookup"><span data-stu-id="25483-187">The difference here is that the invited user will not receive any email invitations as all the resource scopes within the subscription will be available in the dashboard after signing in.</span></span>

## <a name="assign-rbac-roles-at-the-resource-group-scope"></a><span data-ttu-id="25483-188">Attribution de rôles RBAC au niveau de l’étendue d’un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="25483-188">Assign RBAC roles at the resource group scope</span></span>
<span data-ttu-id="25483-189">L’attribution d’un rôle RBAC au niveau de l’étendue d’un **Groupe de ressources** est un processus identique à celui de l’attribution du rôle au niveau de l’abonnement pour les deux types d’utilisateurs, externes ou internes (au sein du même annuaire).</span><span class="sxs-lookup"><span data-stu-id="25483-189">Assigning an RBAC role at a **Resource Group** scope has an identical process for assigning the role at the subscription level, for both types of users - either external or internal (part of the same directory).</span></span> <span data-ttu-id="25483-190">Les utilisateurs auxquels le rôle RBAC est attribué peuvent voir dans leur environnement uniquement le groupe de ressources auquel ils ont accès à partir de l’icône **Groupes de ressources** dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="25483-190">The users which are assigned the RBAC role is to see in their environment only the resource group they have been assigned access from the **Resource Groups** icon in the Azure portal.</span></span>

## <a name="assign-rbac-roles-at-the-resource-scope"></a><span data-ttu-id="25483-191">Attribuer des rôles RBAC au niveau de l’étendue d’une ressource</span><span class="sxs-lookup"><span data-stu-id="25483-191">Assign RBAC roles at the resource scope</span></span>
<span data-ttu-id="25483-192">L’attribution d’un rôle RBAC au niveau de l’étendue d’une ressource dans Azure est un processus identique à celui de l’attribution du rôle au niveau de l’abonnement ou du groupe de ressources. Le flux de travail est le même pour les deux scénarios.</span><span class="sxs-lookup"><span data-stu-id="25483-192">Assigning an RBAC role at a resource scope in Azure has an identical process for assigning the role at the subscription level or at the resource group level, following the same workflow for both scenarios.</span></span> <span data-ttu-id="25483-193">Une fois encore, les utilisateurs auxquels le rôle RBAC est attribué peuvent voir uniquement les éléments auxquels ils ont accès, soit sous l’onglet **Toutes les ressources**, soit directement sur leur tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="25483-193">Again, the users which are assigned the RBAC role can see only the items that they have been assigned access to, either in the **All Resources** tab or directly in their dashboard.</span></span>

<span data-ttu-id="25483-194">Un aspect important de la fonctionnalité RBAC, tant au niveau de l’étendue de groupe de ressources qu’à celui de l’étendue de la ressource, est que les utilisateurs doivent veiller à se connecter à l’annuaire approprié.</span><span class="sxs-lookup"><span data-stu-id="25483-194">An important aspect for RBAC both at resource group scope or resource scope is for the users to make sure to sign-in to the correct directory.</span></span>





![connexion à un annuaire dans le portail azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/13.png)

## <a name="assign-rbac-roles-for-an-azure-active-directory-group"></a><span data-ttu-id="25483-196">Attribuer des rôles RBAC pour un groupe Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="25483-196">Assign RBAC roles for an Azure Active Directory group</span></span>
<span data-ttu-id="25483-197">Tous les scénarios utilisant la fonctionnalité RBAC aux trois niveaux d’étendue dans Azure offrent le privilège de pouvoir gérer, déployer et administrer diverses ressources comme un utilisateur assigné sans avoir besoin de gérer un abonnement personnel.</span><span class="sxs-lookup"><span data-stu-id="25483-197">All the scenarios using RBAC at the three different scopes in Azure offer the privilege of managing, deploying and administering various resources as an assigned user without the need of managing a personal subscription.</span></span> <span data-ttu-id="25483-198">Quel que soit le rôle RBAC attribué pour un abonnement, qu’il s’agisse de groupe de ressources ou d’étendue de ressource, toutes les ressources créées ensuite par les utilisateurs affectés sont facturés sous le seul abonnement Azure auquel ils ont accès.</span><span class="sxs-lookup"><span data-stu-id="25483-198">Regardless the RBAC role is assigned for a subscription, resource group or resource scope, all the resources created further on by the assigned users are billed under the one Azure subscription where the users have access to.</span></span> <span data-ttu-id="25483-199">Ainsi, les utilisateurs qui disposent d’autorisations d’administrateur de facturation pour cet abonnement Azure entier ont une vue d’ensemble complète de la consommation, quelle que soit la personne qui gère les ressources.</span><span class="sxs-lookup"><span data-stu-id="25483-199">This way, the users who have billing administrator permissions for that entire Azure subscription has a complete overview on the consumption, regardless who is managing the resources.</span></span>

<span data-ttu-id="25483-200">Pour les entreprises de grande taille, les rôles RBAC peuvent être appliqués de la même façon pour des groupes Azure Active Directory, en considérant que l’utilisateur administrateur souhaite octroyer l’accès granulaire à des équipes ou à des départements entiers plutôt qu’individuellement à chaque utilisateur, et donc en considérant qu’il s’agit d’une option extrêmement efficace sur les plans du temps et de la gestion.</span><span class="sxs-lookup"><span data-stu-id="25483-200">For larger organizations, RBAC roles can be applied in the same way for Azure Active Directory groups considering the perspective that the admin user wants to grant the granular access for teams or entire departments, not individually for each user, thus considering it as an extremely time and management efficient option.</span></span> <span data-ttu-id="25483-201">Pour illustrer cet exemple, le rôle **Contributeur** a été ajouté à l’un des groupes dans le client au niveau de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="25483-201">To illustrate this example, the **Contributor** role has been added to one of the groups in the tenant at the subscription level.</span></span>





![ajouter un rôle RBAC pour les groupes AAD](./media/role-based-access-control-create-custom-roles-for-internal-external-users/14.png)

<span data-ttu-id="25483-203">Ces groupes sont des groupes de sécurité qui sont approvisionnés et gérés uniquement dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="25483-203">These groups are security groups which are provisioned and managed only within Azure Active Directory.</span></span>

## <a name="create-a-custom-rbac-role-to-open-support-requests-using-powershell"></a><span data-ttu-id="25483-204">Créer un rôle RBAC personnalisé pour ouvrir les demandes de support à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="25483-204">Create a custom RBAC role to open support requests using PowerShell</span></span>
<span data-ttu-id="25483-205">Les rôles RBAC intégrés disponibles dans Azure garantissent certains niveaux d’autorisation en fonction ressources disponibles dans l’environnement.</span><span class="sxs-lookup"><span data-stu-id="25483-205">The built-in RBAC roles which are available in Azure ensure certain permission levels based on the available resources in the environment.</span></span> <span data-ttu-id="25483-206">Toutefois, si aucun de ces rôles ne répond aux besoins de l’utilisateur administrateur, il est possible de limiter davantage l’accès en créant des rôles RBAC personnalisés.</span><span class="sxs-lookup"><span data-stu-id="25483-206">However, if none of these roles suit the admin user's needs, there is the option to limit access even more by creating custom RBAC roles.</span></span>

<span data-ttu-id="25483-207">La création d’un rôle RBAC personnalisé requiert de prendre un rôle intégré, de le modifier, puis de le réimporter dans l’environnement.</span><span class="sxs-lookup"><span data-stu-id="25483-207">Creating custom RBAC roles requires to take one built-in role, edit it and then import it back in the environment.</span></span> <span data-ttu-id="25483-208">Le téléchargement et le chargement du rôle sont gérés à l’aide de PowerShell ou d’Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="25483-208">The download and upload of the role are managed using either PowerShell or CLI.</span></span>

<span data-ttu-id="25483-209">Il est important de comprendre les conditions préalables à la création d’un rôle personnalisé qui peut octroyer un accès granulaire au niveau de l’abonnement et offrir à l’utilisateur invité la flexibilité nécessaire pour ouvrir des demandes de support.</span><span class="sxs-lookup"><span data-stu-id="25483-209">It is important to understand the prerequisites of creating a custom role which can grant granular access at the subscription level and also allow the invited user the flexibility of opening support requests.</span></span>

<span data-ttu-id="25483-210">Pour cet exemple, le rôle intégré **Lecteur** qui permet à l’utilisateur d’accéder pour afficher toutes les étendues d’une ressource, mais pas de les modifier ou d’en créer, a été personnalisé afin de permettre à l’utilisateur d’ouvrir des demandes de support.</span><span class="sxs-lookup"><span data-stu-id="25483-210">For this example the built-in role **Reader** which allows users access to view all the resource scopes but not to edit them or create new ones has been customized to allow the user the option of opening support requests.</span></span>

<span data-ttu-id="25483-211">La première action d’exportation du rôle **Lecteur** doit être accomplie dans PowerShell exécuté avec des autorisations élevées d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="25483-211">The first action of exporting the **Reader** role needs to be completed in PowerShell ran with elevated permissions as administrator.</span></span>

```
Login-AzureRMAccount

Get-AzureRMRoleDefinition -Name "Reader"

Get-AzureRMRoleDefinition -Name "Reader" | ConvertTo-Json | Out-File C:\rbacrole2.json

```





![Capture d’écran de PowerShell pour le rôle RBAC Lecteur](./media/role-based-access-control-create-custom-roles-for-internal-external-users/15.png)

<span data-ttu-id="25483-213">Vous devez extraire le modèle JSON du rôle.</span><span class="sxs-lookup"><span data-stu-id="25483-213">Then you need to extract the JSON template of the role.</span></span>





![Modèle JSON pour le rôle RBAC Lecteur personnalisé](./media/role-based-access-control-create-custom-roles-for-internal-external-users/16.png)

<span data-ttu-id="25483-215">Un rôle RBAC classique comprend trois sections principales, **Actions**, **NotActions** et **AssignableScopes**.</span><span class="sxs-lookup"><span data-stu-id="25483-215">A typical RBAC role is composed out of three main sections, **Actions**, **NotActions** and **AssignableScopes**.</span></span>

<span data-ttu-id="25483-216">La section **Action** répertorie toutes les opérations autorisées pour ce rôle.</span><span class="sxs-lookup"><span data-stu-id="25483-216">In the **Action** section are listed all the permitted operations for this role.</span></span> <span data-ttu-id="25483-217">Il est important de comprendre que chaque action est affectée à partir d’un fournisseur de ressources.</span><span class="sxs-lookup"><span data-stu-id="25483-217">It's important to understand that each action is assigned from a resource provider.</span></span> <span data-ttu-id="25483-218">Dans ce cas, pour la création de tickets de support, le fournisseur de ressources **Microsoft.Support** doit être répertorié.</span><span class="sxs-lookup"><span data-stu-id="25483-218">In this case, for creating support tickets the **Microsoft.Support** resource provider must be listed.</span></span>

<span data-ttu-id="25483-219">Pour voir tous les fournisseurs de ressources disponibles et enregistrés dans votre abonnement, vous pouvez utiliser PowerShell.</span><span class="sxs-lookup"><span data-stu-id="25483-219">To be able to see all the resource providers available and registered in your subscription, you can use PowerShell.</span></span>
```
Get-AzureRMResourceProvider

```
<span data-ttu-id="25483-220">En outre, vous pouvez vérifier la disponibilité de toutes les applets de commande PowerShell pour gérer les fournisseurs de ressources.</span><span class="sxs-lookup"><span data-stu-id="25483-220">Additionally, you can check for the all the available PowerShell cmdlets to manage the resource providers.</span></span>
    <span data-ttu-id="25483-221">![Capture d’écran de PowerShell pour la gestion de fournisseur de ressources](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)</span><span class="sxs-lookup"><span data-stu-id="25483-221">![PowerShell screenshot for resource provider management](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)</span></span>

<span data-ttu-id="25483-222">Pour restreindre toutes les actions pour un rôle RBAC particulier, les fournisseurs de ressources sont répertoriés sous la section **NotActions**.</span><span class="sxs-lookup"><span data-stu-id="25483-222">To restrict all the actions for a particular RBAC role, resource providers are listed under the section **NotActions**.</span></span>
<span data-ttu-id="25483-223">Enfin, le rôle RBAC doit obligatoirement contenir les ID d’abonnement explicites correspondant aux emplacements où il est utilisé.</span><span class="sxs-lookup"><span data-stu-id="25483-223">Last, it's mandatory that the RBAC role contains the explicit subscription IDs where it is used.</span></span> <span data-ttu-id="25483-224">Les ID d’abonnement sont répertoriés sous la section **AssignableScopes**. Sans ceux-ci, vous ne serez pas autorisé à importer le rôle dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="25483-224">The subscription IDs are listed under the **AssignableScopes**, otherwise you will not be allowed to import the role in your subscription.</span></span>

<span data-ttu-id="25483-225">Une fois créé et personnalisé, le rôle RBAC doit être réimporté dans l’environnement.</span><span class="sxs-lookup"><span data-stu-id="25483-225">After creating and customizing the RBAC role, it needs to be imported back the environment.</span></span>

```
New-AzureRMRoleDefinition -InputFile "C:\rbacrole2.json"

```

<span data-ttu-id="25483-226">Dans cet exemple, le nom de ce rôle RBAC personnalisé est « Niveau d’accès des tickets de support du Lecteur ». Il permet à l’utilisateur d’afficher tout le contenu de l’abonnement et d’ouvrir des demandes de support.</span><span class="sxs-lookup"><span data-stu-id="25483-226">In this example, the custom name for this RBAC role is "Reader support tickets access level" allowing the user to view everything in the subscription and also to open support requests.</span></span>

> [!NOTE]
> <span data-ttu-id="25483-227">Les deux seuls rôles RBAC intégrés autorisant l’action d’ouverture de demandes de support sont **Propriétaire** et **Contributeur**.</span><span class="sxs-lookup"><span data-stu-id="25483-227">The only two built-in RBAC roles allowing the action of opening of support requests are **Owner** and **Contributor**.</span></span> <span data-ttu-id="25483-228">Pour pouvoir ouvrir des demandes de support, un utilisateur doit avoir un rôle RBAC uniquement au niveau de l’étendue de l’abonnement, car toutes les demandes de prise en charge sont créées sur la base d’un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="25483-228">For a user to be able to open support requests, he must be assigned an RBAC role only at the subscription scope, because all support requests are created based on an Azure subscription.</span></span>

<span data-ttu-id="25483-229">Ce nouveau rôle personnalisé a été attribué à un utilisateur figurant dans le même annuaire.</span><span class="sxs-lookup"><span data-stu-id="25483-229">This new custom role has been assigned to an user from the same directory.</span></span>





![capture d’écran d’un rôle RBAC personnalisé importé dans le portail Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/18.png)





![capture d’écran de l’attribution d’un rôle RBAC importé personnalisé à un utilisateur dans le même annuaire](./media/role-based-access-control-create-custom-roles-for-internal-external-users/19.png)





![capture d’écran d’autorisations pour un rôle RBAC importé personnalisé](./media/role-based-access-control-create-custom-roles-for-internal-external-users/20.png)

<span data-ttu-id="25483-233">L’exemple a été détaillé davantage pour mettre en évidence les limites de ce rôle RBAC personnalisé comme suit :</span><span class="sxs-lookup"><span data-stu-id="25483-233">The example has been further detailed to emphasize the limits of this custom RBAC role as follows:</span></span>
* <span data-ttu-id="25483-234">Peut créer des demandes de support</span><span class="sxs-lookup"><span data-stu-id="25483-234">Can create new support requests</span></span>
* <span data-ttu-id="25483-235">Ne peut pas créer d’étendues de ressource (par exemple, machine virtuelle)</span><span class="sxs-lookup"><span data-stu-id="25483-235">Can't create new resource scopes (for example: virtual machine)</span></span>
* <span data-ttu-id="25483-236">Ne peut pas créer de groupes de ressources</span><span class="sxs-lookup"><span data-stu-id="25483-236">Can't create new resource groups</span></span>





![capture d’écran d’un rôle RBAC personnalisé créant des demandes de support](./media/role-based-access-control-create-custom-roles-for-internal-external-users/21.png)





![capture d’écran d’un rôle RBAC personnalisé ne pouvant pas créer de machine virtuelle](./media/role-based-access-control-create-custom-roles-for-internal-external-users/22.png)





![capture d’écran d’un rôle RBAC personnalisé ne pouvant pas créer de groupe de ressources](./media/role-based-access-control-create-custom-roles-for-internal-external-users/23.png)

## <a name="create-a-custom-rbac-role-to-open-support-requests-using-azure-cli"></a><span data-ttu-id="25483-240">Créer un rôle RBAC personnalisé pour ouvrir les demandes de support à l’aide d’Azure CLI</span><span class="sxs-lookup"><span data-stu-id="25483-240">Create a custom RBAC role to open support requests using Azure CLI</span></span>
<span data-ttu-id="25483-241">S’exécutant sur un Mac et sans avoir accès à PowerShell, Azure CLI est le bon choix.</span><span class="sxs-lookup"><span data-stu-id="25483-241">Running on a Mac and without having access to PowerShell, Azure CLI is the way to go.</span></span>

<span data-ttu-id="25483-242">Les étapes pour la création d’un rôle personnalisé sont les mêmes, à la seule exception que le rôle peut pas être téléchargé dans un modèle JSON à l’aide de l’interface de ligne de commande, mais uniquement affiché dans celle-ci.</span><span class="sxs-lookup"><span data-stu-id="25483-242">The steps to create a custom role are the same, with the sole exception that using CLI the role can't be downloaded in a JSON template, but it can be viewed in the CLI.</span></span>

<span data-ttu-id="25483-243">Pour cet exemple, j’ai choisi le rôle intégré **Lecteur de secours**.</span><span class="sxs-lookup"><span data-stu-id="25483-243">For this example I have chosen the built-in role of **Backup Reader**.</span></span>

```

azure role show "backup reader" --json

```





![Capture d’écran d’interface de ligne de commande pour l’affichage du rôle Lecteur de secours (Backup Reader)](./media/role-based-access-control-create-custom-roles-for-internal-external-users/24.png)

<span data-ttu-id="25483-245">Après la modification du rôle dans Visual Studio et la copie des propriétés dans un modèle JSON, le fournisseur de ressources **Microsoft.Support** a été ajouté dans la section **Actions** de façon à ce que cet utilisateur puisse ouvrir des demandes de support tout en continuant d’être un lecteur pour les coffres de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="25483-245">Editing the role in Visual Studio after copying the proprieties in a JSON template, the **Microsoft.Support** resource provider has been added in the **Actions** sections so that this user can open support requests while continuing to be a reader for the backup vaults.</span></span> <span data-ttu-id="25483-246">Là encore, il est nécessaire d’ajouter dans la section **AssignableScopes** l’ID de l’abonnement dans lequel ce rôle sera utilisé.</span><span class="sxs-lookup"><span data-stu-id="25483-246">Again it is necessary to add the subscription ID where this role will be used in the **AssignableScopes** section.</span></span>

```

azure role create --inputfile <path>

```





![Capture d’écran de l’Interface de ligne de commande pour l’importation de rôle RBAC personnalisé](./media/role-based-access-control-create-custom-roles-for-internal-external-users/25.png)

<span data-ttu-id="25483-248">Le nouveau rôle est désormais disponible dans le portail Azure, et le processus d’attribution est le même que dans les exemples précédents.</span><span class="sxs-lookup"><span data-stu-id="25483-248">The new role is now available in the Azure portal and the assignation process is the same as in the previous examples.</span></span>





![Capture d’écran du portail Azure montrant le rôle RBAC personnalisé créé à l’aide d’Azure CLI 1.0](./media/role-based-access-control-create-custom-roles-for-internal-external-users/26.png)

<span data-ttu-id="25483-250">Depuis la dernière build 2017, Azure Cloud Shell est généralement disponible.</span><span class="sxs-lookup"><span data-stu-id="25483-250">As of the latest Build 2017, the Azure Cloud Shell is generally available.</span></span> <span data-ttu-id="25483-251">Azure Cloud Shell est un complément de l’environnement de développement intégré (IDE) et du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="25483-251">Azure Cloud Shell is a complement to IDE and the Azure Portal.</span></span> <span data-ttu-id="25483-252">Avec ce service, vous bénéficiez d’un interpréteur de commandes basé sur un navigateur, qui est authentifié et hébergé dans Azure, et que vous pouvez utiliser à la place de l’interface de ligne de commande installée sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="25483-252">With this service, you get a browser-based shell that is authenticated and hosted within Azure and you can use it instead of CLI installed on your machine.</span></span>





![Azure Cloud Shell](./media/role-based-access-control-create-custom-roles-for-internal-external-users/27.png)
