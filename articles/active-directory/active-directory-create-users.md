---
title: aaaAdd nouveaux utilisateurs tooAzure Active Directory | Documents Microsoft
description: Explique comment tooadd nouveaux utilisateurs ou modifier les informations utilisateur dans Azure Active Directory.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e3673727-6bec-4fdc-87a4-d65b213c4c3c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 72f67ad41022fd19fd94c8e1301943b0db1e57bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-new-users-or-users-with-microsoft-accounts-tooazure-active-directory"></a><span data-ttu-id="54154-103">Ajouter de nouveaux utilisateurs ou utilisateurs avec tooAzure de comptes Microsoft Active Directory</span><span class="sxs-lookup"><span data-stu-id="54154-103">Add new users or users with Microsoft accounts tooAzure Active Directory</span></span>
<span data-ttu-id="54154-104">Ajoutez les utilisateurs toopopulate votre répertoire.</span><span class="sxs-lookup"><span data-stu-id="54154-104">Add users toopopulate your directory.</span></span> <span data-ttu-id="54154-105">Cet article explique comment tooadd les nouveaux utilisateurs de votre organisation et comment tooadd les utilisateurs qui disposent de comptes Microsoft.</span><span class="sxs-lookup"><span data-stu-id="54154-105">This article explains how tooadd new users in your organization, and how tooadd users who have Microsoft accounts.</span></span> <span data-ttu-id="54154-106">Pour en savoir plus sur l’ajout d’utilisateurs à partir d’autres répertoires dans Azure Active Directory, ou sur l’ajout d’utilisateurs à partir d’entreprises partenaires, voir [Ajouter des utilisateurs à partir d’autres répertoires ou entreprises partenaires dans Azure Active Directory](active-directory-create-users-external.md).</span><span class="sxs-lookup"><span data-stu-id="54154-106">For more information about adding users from other directories in Azure Active Directory or adding users from partner companies, see [Add users from other directories or partner companies in Azure Active Directory](active-directory-create-users-external.md).</span></span> <span data-ttu-id="54154-107">Les utilisateurs ajoutés ne disposent pas des autorisations d’administrateur par défaut, mais vous pouvez attribuer des rôles toothem à tout moment.</span><span class="sxs-lookup"><span data-stu-id="54154-107">Added users don't have administrator permissions by default, but you can assign roles toothem at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="54154-108">Microsoft recommande de gérer Azure AD en utilisant hello [centre d’administration Azure AD](https://aad.portal.azure.com) Bonjour portail Azure au lieu d’utiliser hello portail Azure classic référencée dans cet article.</span><span class="sxs-lookup"><span data-stu-id="54154-108">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> <span data-ttu-id="54154-109">Pour tooadd un utilisateur dans le centre d’administration hello Azure AD, voir [ajouter de nouveaux utilisateurs tooAzure Active Directory](active-directory-users-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="54154-109">For how tooadd a user in hello Azure AD admin center, see [Add new users tooAzure Active Directory](active-directory-users-create-azure-portal.md).</span></span>

## <a name="add-a-user"></a><span data-ttu-id="54154-110">Ajouter un utilisateur</span><span class="sxs-lookup"><span data-stu-id="54154-110">Add a user</span></span>
1. <span data-ttu-id="54154-111">Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com) avec un compte qui est un administrateur global pour le répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="54154-111">Sign in toohello [Azure classic portal](https://manage.windowsazure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="54154-112">Sélectionnez **Active Directory**, puis sélectionnez le nom hello du répertoire de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="54154-112">Select **Active Directory**, and then select hello name of your organization directory.</span></span>
3. <span data-ttu-id="54154-113">Sélectionnez hello **utilisateurs** et puis, dans la barre de commandes hello, sélectionnez **ajouter un utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="54154-113">Select hello **Users** tab, and then, in hello command bar, select **Add User**.</span></span>
4. <span data-ttu-id="54154-114">Sur hello **faites-nous part de cet utilisateur** sous **Type d’utilisateur**, sélectionnez :</span><span class="sxs-lookup"><span data-stu-id="54154-114">On hello **Tell us about this user** page, under **Type of user**, select either:</span></span>

   * <span data-ttu-id="54154-115">**Nouvel utilisateur dans votre organisation** : permet d’ajouter un nouveau compte d’utilisateur dans votre répertoire.</span><span class="sxs-lookup"><span data-stu-id="54154-115">**New user in your organization** – adds a new user account in your directory.</span></span>
   * <span data-ttu-id="54154-116">**Utilisateur avec un compte Microsoft existant** – ajoute un annuaire Microsoft existant consommateur compte tooyour (par exemple, un compte Outlook)</span><span class="sxs-lookup"><span data-stu-id="54154-116">**User with an existing Microsoft account** – adds an existing Microsoft consumer account tooyour directory (for example, an Outlook account)</span></span>
5. <span data-ttu-id="54154-117">En fonction de la valeur du champ **Type d’utilisateur**, saisissez un nom d’utilisateur (pour un nouvel utilisateur) ou une adresse e-mail (pour un utilisateur doté d’un compte Microsoft).</span><span class="sxs-lookup"><span data-stu-id="54154-117">Depending on **Type of user**, enter a user name (for new user) or an email address (for a user with a Microsoft account).</span></span>
6. <span data-ttu-id="54154-118">Utilisateur de hello **profil** , fournissez un nom et prénom, un nom convivial et un rôle d’utilisateur à partir de hello **rôles** liste.</span><span class="sxs-lookup"><span data-stu-id="54154-118">On hello user **Profile** page, provide a first and last name, a user-friendly name, and a user role from hello **Roles** list.</span></span> <span data-ttu-id="54154-119">Pour plus d’informations sur les utilisateurs et les rôles d’administrateur, consultez la page [Attribution de rôles d’administrateur dans Azure AD](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="54154-119">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span> <span data-ttu-id="54154-120">Spécifiez si trop**activer l’authentification multifacteur** pour l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="54154-120">Specify whether too**Enable Multi-Factor Authentication** for hello user.</span></span>
7. <span data-ttu-id="54154-121">Sur hello **mot de passe temporaire Get** page, sélectionnez **créer**.</span><span class="sxs-lookup"><span data-stu-id="54154-121">On hello **Get temporary password** page, select **Create**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="54154-122">Si votre organisation utilise plusieurs domaines, vous devez savoir sur hello suivants lorsque vous ajoutez un compte d’utilisateur :</span><span class="sxs-lookup"><span data-stu-id="54154-122">If your organization uses more than one domain, you should know about hello following issues when you add a user account:</span></span>
>
> * <span data-ttu-id="54154-123">comptes d’utilisateur tooadd avec hello même nom d’utilisateur principal (UPN) sur plusieurs domaines, **première** ajouter, par exemple, geoffgrisso@contoso.onmicrosoft.com, **suivie** geoffgrisso@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="54154-123">tooadd user accounts with hello same user principal name (UPN) across domains, **first** add, for example, geoffgrisso@contoso.onmicrosoft.com, **followed by** geoffgrisso@contoso.com.</span></span>
> * <span data-ttu-id="54154-124">**N’ajoutez pas**geoffgrisso@contoso.com avant d’avoir ajouté geoffgrisso@contoso.onmicrosoft.com. Cet ordre est important et peut être fastidieuse tooundo.</span><span class="sxs-lookup"><span data-stu-id="54154-124">**Don't** add geoffgrisso@contoso.com before you add geoffgrisso@contoso.onmicrosoft.com. This order is important, and can be cumbersome tooundo.</span></span>
>
>

## <a name="change-user-information"></a><span data-ttu-id="54154-125">Modification des informations utilisateur</span><span class="sxs-lookup"><span data-stu-id="54154-125">Change user information</span></span>
<span data-ttu-id="54154-126">Vous pouvez modifier n’importe quel attribut utilisateur à l’exception des ID d’objet hello.</span><span class="sxs-lookup"><span data-stu-id="54154-126">You can change any user attribute except for hello object ID.</span></span>

1. <span data-ttu-id="54154-127">Ouvrez votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="54154-127">Open your directory.</span></span>
2. <span data-ttu-id="54154-128">Sélectionnez hello **utilisateurs** onglet et puis sélectionnez hello de hello utilisateur toochange.</span><span class="sxs-lookup"><span data-stu-id="54154-128">Select hello **Users** tab, and then select hello display name of hello user you want toochange.</span></span>
3. <span data-ttu-id="54154-129">Apportez les modifications nécessaires, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="54154-129">Complete your changes, and then click **Save**.</span></span>

<span data-ttu-id="54154-130">Si l’utilisateur hello que vous êtes en train de modifier est synchronisé avec votre service d’Active Directory local, vous ne pouvez modifier hello utilisateur à l’aide de cette procédure.</span><span class="sxs-lookup"><span data-stu-id="54154-130">If hello user that you're changing is synchronized with your on-premises Active Directory service, you can't change hello user information using this procedure.</span></span> <span data-ttu-id="54154-131">utilisateur de hello toochange, utilisez vos outils de gestion Active Directory local.</span><span class="sxs-lookup"><span data-stu-id="54154-131">toochange hello user, use your on-premises Active Directory management tools.</span></span>

## <a name="guest-user-management-and-limitations"></a><span data-ttu-id="54154-132">Gestion des utilisateurs invités et limitations</span><span class="sxs-lookup"><span data-stu-id="54154-132">Guest user management and limitations</span></span>
<span data-ttu-id="54154-133">Les comptes Invité sont les utilisateurs à partir d’autres annuaires qui ont été invités tooyour Active tooaccess SharePoint documents, d’applications ou d’autres ressources Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="54154-133">Guest accounts are users from other directories who were invited tooyour directory tooaccess SharePoint documents, applications, or other Azure resources.</span></span> <span data-ttu-id="54154-134">Un compte invité dans votre annuaire a son attribut UserType sous-jacent défini trop « Guest ».</span><span class="sxs-lookup"><span data-stu-id="54154-134">A guest account in your directory has its underlying UserType attribute set too"Guest."</span></span> <span data-ttu-id="54154-135">Utilisateurs habituels (plus précisément, les membres de votre annuaire) est attribut UserType de hello « Membre ».</span><span class="sxs-lookup"><span data-stu-id="54154-135">Regular users (specifically, members of your directory) have hello UserType attribute "Member."</span></span>

<span data-ttu-id="54154-136">Invités ont un ensemble limité de droits dans le répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="54154-136">Guests have a limited set of rights in hello directory.</span></span> <span data-ttu-id="54154-137">Ces droits limitent hello pour plus d’informations invités toodiscover sur les autres utilisateurs dans le répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="54154-137">These rights limit hello ability for Guests toodiscover information about other users in hello directory.</span></span> <span data-ttu-id="54154-138">Toutefois, les utilisateurs invités peuvent toujours interagir avec les utilisateurs de hello et associées aux ressources hello sur qu'ils travaillent des groupes.</span><span class="sxs-lookup"><span data-stu-id="54154-138">However, guest users can still interact with hello users and groups associated with hello resources they're working on.</span></span> <span data-ttu-id="54154-139">Les utilisateurs invités peuvent :</span><span class="sxs-lookup"><span data-stu-id="54154-139">Guest users can:</span></span>

* <span data-ttu-id="54154-140">Voir les autres utilisateurs et les groupes associés à un toowhich d’abonnement Azure qu'auquel elles sont affectées</span><span class="sxs-lookup"><span data-stu-id="54154-140">See other users and groups associated with an Azure subscription toowhich they're assigned</span></span>
* <span data-ttu-id="54154-141">Afficher les membres de hello de toowhich de groupes qu’ils appartiennent.</span><span class="sxs-lookup"><span data-stu-id="54154-141">See hello members of groups toowhich they belong</span></span>
* <span data-ttu-id="54154-142">Rechercher d’autres utilisateurs dans le répertoire de hello, s’ils ne connaissent l’adresse de messagerie complète hello d’utilisateur de hello</span><span class="sxs-lookup"><span data-stu-id="54154-142">Look up other users in hello directory, if they know hello full email address of hello user</span></span>
* <span data-ttu-id="54154-143">Voir qu’un ensemble limité d’attributs d’utilisateurs hello qu’ils recherchent--toodisplay limité nom, adresse de messagerie, nom d’utilisateur principal (UPN) et la photo miniature</span><span class="sxs-lookup"><span data-stu-id="54154-143">See only a limited set of attributes of hello users they look up--limited toodisplay name, email address, user principal name (UPN), and thumbnail photo</span></span>
* <span data-ttu-id="54154-144">Obtenir la liste des domaines vérifiés dans le répertoire de hello</span><span class="sxs-lookup"><span data-stu-id="54154-144">Get a list of verified domains in hello directory</span></span>
* <span data-ttu-id="54154-145">Tooapplications de consentement, leur octroyer hello même accès des membres de votre annuaire</span><span class="sxs-lookup"><span data-stu-id="54154-145">Consent tooapplications, granting them hello same access that Members have in your directory</span></span>

## <a name="set-guest-user-access-policies"></a><span data-ttu-id="54154-146">Définir les stratégies d’accès utilisateur</span><span class="sxs-lookup"><span data-stu-id="54154-146">Set guest user access policies</span></span>
<span data-ttu-id="54154-147">Hello **configurer** onglet d’un répertoire contient des options toocontrol accès pour les utilisateurs invités.</span><span class="sxs-lookup"><span data-stu-id="54154-147">hello **Configure** tab of a directory includes options toocontrol access for guest users.</span></span> <span data-ttu-id="54154-148">Ces options peuvent uniquement être modifiées dans le portail Azure Classic par un administrateur général du répertoire.</span><span class="sxs-lookup"><span data-stu-id="54154-148">These options can be changed only in Azure classic portal by a directory global administrator.</span></span> <span data-ttu-id="54154-149">Pour le moment, il n’existe aucune méthode PowerShell ou API.</span><span class="sxs-lookup"><span data-stu-id="54154-149">Currently, there's no PowerShell or API method.</span></span>

<span data-ttu-id="54154-150">tooopen hello **configurer** onglet hello sélectionnez de portail classique Azure **Active Directory**, puis sélectionnez le nom hello du répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="54154-150">tooopen hello **Configure** tab in hello Azure classic portal, select **Active Directory**, and then select hello name of hello directory.</span></span>

![Onglet Configurer d’Azure Active Directory][1]

<span data-ttu-id="54154-152">Vous pouvez ensuite modifier hello options toocontrol accès pour les utilisateurs invités.</span><span class="sxs-lookup"><span data-stu-id="54154-152">Then you can edit hello options toocontrol access for guest users.</span></span>

![Options de contrôle d’accès des utilisateurs invités][2]

## <a name="whats-next"></a><span data-ttu-id="54154-154">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="54154-154">What's next</span></span>
* [<span data-ttu-id="54154-155">Ajouter des utilisateurs à partir d’autres répertoires ou entreprises partenaires dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="54154-155">Add users from other directories or partner companies in Azure Active Directory</span></span>](active-directory-create-users-external.md)
* [<span data-ttu-id="54154-156">Administration d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="54154-156">Administering Azure AD</span></span>](active-directory-administer.md)
* [<span data-ttu-id="54154-157">Gestion des mots de passe dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="54154-157">Manage passwords in Azure AD</span></span>](active-directory-manage-passwords.md)
* [<span data-ttu-id="54154-158">Gestion des groupes dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="54154-158">Manage groups in Azure AD</span></span>](active-directory-manage-groups.md)

<!--Image references-->
[1]: ./media/active-directory-create-users/RBACDirConfigTab.png
[2]: ./media/active-directory-create-users/RBACGuestAccessControls.png
