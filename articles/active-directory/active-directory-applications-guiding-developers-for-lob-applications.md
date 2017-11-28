---
title: les applications pour Azure AD aaaDevelop | Des documents Microsoft
description: "Rédigée pour les professionnels de l’informatique de hello, cet article fournit des instructions pour l’intégration d’applications Azure avec Active Directory."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: 
ms.assetid: dd69f2bc-37c5-457c-857d-27acb84267fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d2924be752af0be2843b1d9b74d9ec446d3fe1ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-line-of-business-apps-for-azure-active-directory"></a><span data-ttu-id="c00ca-103">Développer des applications métier pour Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c00ca-103">Develop line-of-business apps for Azure Active Directory</span></span>
<span data-ttu-id="c00ca-104">Ce guide fournit une vue d’ensemble du développement d’applications line-of-business (LoB) Azure Active Directory (AD) .hello destinée audience est un administrateur global Active Directory/Office 365.</span><span class="sxs-lookup"><span data-stu-id="c00ca-104">This guide provides an overview of developing line-of-business (LoB) applications for Azure Active Directory (AD).hello intended audience is Active Directory/Office 365 global administrators.</span></span>

## <a name="overview"></a><span data-ttu-id="c00ca-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="c00ca-105">Overview</span></span>
<span data-ttu-id="c00ca-106">La création d’applications intégrées à Azure AD permet aux utilisateurs de votre organisation de bénéficier de l’authentification unique avec Office 365.</span><span class="sxs-lookup"><span data-stu-id="c00ca-106">Building applications integrated with Azure AD gives users in your organization single sign-on with Office 365.</span></span> <span data-ttu-id="c00ca-107">Ayant l’application hello dans Azure AD vous permet de que contrôler la stratégie d’authentification pour l’application hello hello.</span><span class="sxs-lookup"><span data-stu-id="c00ca-107">Having hello application in Azure AD gives you control over hello authentication policy for hello application.</span></span> <span data-ttu-id="c00ca-108">toolearn plus d’informations sur l’accès conditionnel et comment les applications tooprotect avec l’authentification multifacteur (MFA), consultez [règles d’accès de configuration](active-directory-conditional-access-azuread-connected-apps.md).</span><span class="sxs-lookup"><span data-stu-id="c00ca-108">toolearn more about conditional access and how tooprotect apps with multi-factor authentication (MFA) see [Configuring access rules](active-directory-conditional-access-azuread-connected-apps.md).</span></span>

<span data-ttu-id="c00ca-109">Inscrire votre toouse application Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c00ca-109">Register your application toouse Azure Active Directory.</span></span> <span data-ttu-id="c00ca-110">L’inscription d’application hello signifie que les développeurs peuvent utiliser Azure AD tooauthenticate utilisateurs et demander des ressources de toouser d’accès telles que la messagerie, de calendrier et de documents.</span><span class="sxs-lookup"><span data-stu-id="c00ca-110">Registering hello application means that your developers can use Azure AD tooauthenticate users and request access toouser resources such as email, calendar, and documents.</span></span>

<span data-ttu-id="c00ca-111">Tout membre de votre annuaire (pas les invités) peut inscrire une application, procédé également appelé *création d’un objet d’application*.</span><span class="sxs-lookup"><span data-stu-id="c00ca-111">Any member of your directory (not guests) can register an application, otherwise known as *creating an application object*.</span></span>

<span data-ttu-id="c00ca-112">Inscription d’une application permet à toutes les de hello toodo utilisateur :</span><span class="sxs-lookup"><span data-stu-id="c00ca-112">Registering an application allows any user toodo hello following:</span></span>

* <span data-ttu-id="c00ca-113">Obtenir pour son application une identité reconnue par Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c00ca-113">Get an identity for their application that Azure AD recognizes</span></span>
* <span data-ttu-id="c00ca-114">Obtenir un ou plusieurs secrets/clés hello application peut utiliser tooauthenticate lui-même tooAD</span><span class="sxs-lookup"><span data-stu-id="c00ca-114">Get one or more secrets/keys that hello application can use tooauthenticate itself tooAD</span></span>
* <span data-ttu-id="c00ca-115">Application hello marque dans le portail Azure avec un nom personnalisé, le logo, etc. de hello.</span><span class="sxs-lookup"><span data-stu-id="c00ca-115">Brand hello application in hello Azure portal with a custom name, logo, etc.</span></span>
* <span data-ttu-id="c00ca-116">Appliquer l’application de tootheir fonctionnalités Azure AD d’autorisation, y compris :</span><span class="sxs-lookup"><span data-stu-id="c00ca-116">Apply Azure AD authorization features tootheir app, including:</span></span>

  * <span data-ttu-id="c00ca-117">Contrôle d’accès en fonction du rôle</span><span class="sxs-lookup"><span data-stu-id="c00ca-117">Role-Based Access Control (RBAC)</span></span>
  * <span data-ttu-id="c00ca-118">Azure Active Directory en tant que serveur d’autorisation oAuth (sécuriser une API exposée par l’application hello)</span><span class="sxs-lookup"><span data-stu-id="c00ca-118">Azure Active Directory as oAuth authorization server (secure an API exposed by hello application)</span></span>
* <span data-ttu-id="c00ca-119">Déclarer les autorisations requises nécessaires pour hello application toofunction comme prévu, y compris :</span><span class="sxs-lookup"><span data-stu-id="c00ca-119">Declare required permissions necessary for hello application toofunction as expected, including:</span></span>

      - <span data-ttu-id="c00ca-120">Autorisations de l’application (administrateurs généraux uniquement).</span><span class="sxs-lookup"><span data-stu-id="c00ca-120">App permissions (global administrators only).</span></span> <span data-ttu-id="c00ca-121">Par exemple : l’appartenance au rôle dans un autre Azure Active Directory application ou du rôle d’appartenance relative tooan ressource, groupe de ressources Azure, ou un abonnement</span><span class="sxs-lookup"><span data-stu-id="c00ca-121">For example: Role membership in another Azure AD application or role membership relative tooan Azure Resource, Resource Group, or Subscription</span></span>
      - <span data-ttu-id="c00ca-122">Autorisations déléguées (tout utilisateur).</span><span class="sxs-lookup"><span data-stu-id="c00ca-122">Delegated permissions (any user).</span></span> <span data-ttu-id="c00ca-123">Par exemple : Azure AD, connexion et lecture de profil</span><span class="sxs-lookup"><span data-stu-id="c00ca-123">For example: Azure AD, Sign-in, and Read Profile</span></span>

> [!NOTE]
> <span data-ttu-id="c00ca-124">Par défaut, tout membre peut inscrire une application.</span><span class="sxs-lookup"><span data-stu-id="c00ca-124">By default, any member can register an application.</span></span> <span data-ttu-id="c00ca-125">toolearn toorestrict les autorisations pour l’inscription des membres de toospecific d’applications, voir [comment les applications sont ajoutées tooAzure AD](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance).</span><span class="sxs-lookup"><span data-stu-id="c00ca-125">toolearn how toorestrict permissions for registering applications toospecific members, see [How applications are added tooAzure AD](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance).</span></span>
>
>

<span data-ttu-id="c00ca-126">Voici ce que vous, administrateur global de hello, doivent toodo toohelp les développeurs rendre leur application prête pour la production :</span><span class="sxs-lookup"><span data-stu-id="c00ca-126">Here’s what you, hello global administrator, need toodo toohelp developers make their application ready for production:</span></span>

* <span data-ttu-id="c00ca-127">Configurer des règles d’accès (stratégie d’accès/MFA)</span><span class="sxs-lookup"><span data-stu-id="c00ca-127">Configure access rules (access policy/MFA)</span></span>
* <span data-ttu-id="c00ca-128">Configurer l’affectation d’utilisateurs toorequire application hello et affecter des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="c00ca-128">Configure hello app toorequire user assignment and assign users</span></span>
* <span data-ttu-id="c00ca-129">Supprimer l’expérience de consentement utilisateur hello par défaut</span><span class="sxs-lookup"><span data-stu-id="c00ca-129">Suppress hello default user consent experience</span></span>

## <a name="configure-access-rules"></a><span data-ttu-id="c00ca-130">Configurer des règles d’accès</span><span class="sxs-lookup"><span data-stu-id="c00ca-130">Configure access rules</span></span>
<span data-ttu-id="c00ca-131">Configurer l’accès par application règles tooyour SaaS applications.</span><span class="sxs-lookup"><span data-stu-id="c00ca-131">Configure per-application access rules tooyour SaaS apps.</span></span> <span data-ttu-id="c00ca-132">Par exemple, vous pouvez exiger l’authentification Multifacteur ou autoriser uniquement les accès toousers sur des réseaux approuvés.</span><span class="sxs-lookup"><span data-stu-id="c00ca-132">For example, you can require MFA or only allow access toousers on trusted networks.</span></span> <span data-ttu-id="c00ca-133">Détails de Hello pour ce sont disponibles dans le document de hello [règles d’accès de configuration](active-directory-conditional-access-azuread-connected-apps.md).</span><span class="sxs-lookup"><span data-stu-id="c00ca-133">hello details for this are available in hello document [Configuring access rules](active-directory-conditional-access-azuread-connected-apps.md).</span></span>

## <a name="configure-hello-app-toorequire-user-assignment-and-assign-users"></a><span data-ttu-id="c00ca-134">Configurer l’affectation d’utilisateurs toorequire application hello et affecter des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="c00ca-134">Configure hello app toorequire user assignment and assign users</span></span>
<span data-ttu-id="c00ca-135">Par défaut, les utilisateurs peuvent accéder aux applications sans affectation.</span><span class="sxs-lookup"><span data-stu-id="c00ca-135">By default, users can access applications without being assigned.</span></span> <span data-ttu-id="c00ca-136">Toutefois, si l’application hello expose des rôles, ou si vous souhaitez tooappear d’application hello sur le volet d’accès d’un utilisateur, vous devez demander l’affectation d’utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="c00ca-136">However, if hello application exposes roles or if you want hello application tooappear on a user’s access panel, you should require user assignment.</span></span>

[<span data-ttu-id="c00ca-137">Demande de l’affectation de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="c00ca-137">Requiring user assignment</span></span>](active-directory-applications-guiding-developers-requiring-user-assignment.md)

<span data-ttu-id="c00ca-138">Si vous êtes abonné à Azure AD Premium ou Enterprise Mobility Suite (EMS), nous vous recommandons fortement d’utiliser les groupes.</span><span class="sxs-lookup"><span data-stu-id="c00ca-138">If you’re an Azure AD Premium or Enterprise Mobility Suite (EMS) subscriber, we strongly recommend using groups.</span></span> <span data-ttu-id="c00ca-139">Affectation de groupes toohello application vous permet de propriétaire de toohello toodelegate accès permanent de gestion de groupe de hello.</span><span class="sxs-lookup"><span data-stu-id="c00ca-139">Assigning groups toohello application allows you toodelegate ongoing access management toohello owner of hello group.</span></span> <span data-ttu-id="c00ca-140">Vous pouvez créer le groupe de hello ou demander la partie responsable de hello dans votre organisation toocreate hello du groupe à l’aide du centre de gestion de groupe.</span><span class="sxs-lookup"><span data-stu-id="c00ca-140">You can create hello group or ask hello responsible party in your organization toocreate hello group using your group management facility.</span></span>

[<span data-ttu-id="c00ca-141">Affectation d’utilisateurs tooan application</span><span class="sxs-lookup"><span data-stu-id="c00ca-141">Assigning users tooan application</span></span>](active-directory-applications-guiding-developers-assigning-users.md)  
[<span data-ttu-id="c00ca-142">Affectation de groupes tooan application</span><span class="sxs-lookup"><span data-stu-id="c00ca-142">Assigning groups tooan application</span></span>](active-directory-applications-guiding-developers-assigning-groups.md)

## <a name="suppress-user-consent"></a><span data-ttu-id="c00ca-143">Supprimer le consentement de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="c00ca-143">Suppress user consent</span></span>
<span data-ttu-id="c00ca-144">Par défaut, chaque utilisateur traverse un toosign d’expérience de consentement dans.</span><span class="sxs-lookup"><span data-stu-id="c00ca-144">By default, each user goes through a consent experience toosign in.</span></span> <span data-ttu-id="c00ca-145">expérience de consentement Hello, demandant aux utilisateurs des autorisations toogrant tooan application, peut être déconcertant pour les utilisateurs qui ne sont pas familiarisés avec ces décisions.</span><span class="sxs-lookup"><span data-stu-id="c00ca-145">hello consent experience, asking users toogrant permissions tooan application, can be disconcerting for users who are unfamiliar with making such decisions.</span></span>

<span data-ttu-id="c00ca-146">Pour les applications de confiance, vous pouvez simplifier l’expérience utilisateur hello par terme autorisation toohello application pour votre organisation.</span><span class="sxs-lookup"><span data-stu-id="c00ca-146">For applications that you trust, you can simplify hello user experience by consenting toohello application on behalf of your organization.</span></span>

<span data-ttu-id="c00ca-147">Pour plus d’informations sur le consentement de l’utilisateur et de consentement de hello expérience dans Azure, consultez [intégration d’Applications avec Azure Active Directory](active-directory-integrating-applications.md).</span><span class="sxs-lookup"><span data-stu-id="c00ca-147">For more information about user consent and hello consent experience in Azure, see [Integrating Applications with Azure Active Directory](active-directory-integrating-applications.md).</span></span>

## <a name="related-articles"></a><span data-ttu-id="c00ca-148">Articles connexes</span><span class="sxs-lookup"><span data-stu-id="c00ca-148">Related Articles</span></span>
* [<span data-ttu-id="c00ca-149">Permettre aux applications tooon local de sécuriser l’accès à distance avec le Proxy d’Application Azure AD</span><span class="sxs-lookup"><span data-stu-id="c00ca-149">Enable secure remote access tooon-premises applications with Azure AD Application Proxy</span></span>](active-directory-application-proxy-get-started.md)
* [<span data-ttu-id="c00ca-150">Vue d’ensemble de l’accès conditionnel Azure pour les applications SaaS</span><span class="sxs-lookup"><span data-stu-id="c00ca-150">Azure Conditional Access Preview for SaaS Apps</span></span>](active-directory-conditional-access-azuread-connected-apps.md)
* [<span data-ttu-id="c00ca-151">Gestion des tooapps d’accès auprès d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="c00ca-151">Managing access tooapps with Azure AD</span></span>](active-directory-managing-access-to-apps.md)
* [<span data-ttu-id="c00ca-152">Index d’articles pour la gestion des applications dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c00ca-152">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
