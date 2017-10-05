---
title: "Développer des applications pour Azure AD | Microsoft Docs"
description: "Destiné aux professionnels de l’informatique, cet article fournit des instructions pour l’intégration d’applications Azure à Active Directory."
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
ms.openlocfilehash: 6b119be9c06d8c1ccc8e747168429e6c2d2e7a8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="develop-line-of-business-apps-for-azure-active-directory"></a><span data-ttu-id="b0121-103">Développer des applications métier pour Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b0121-103">Develop line-of-business apps for Azure Active Directory</span></span>
<span data-ttu-id="b0121-104">Ce guide fournit une vue d’ensemble du développement d’applications métier pour Azure Active Directory. Il s’adresse aux administrateurs généraux de systèmes Active Directory/Office 365.</span><span class="sxs-lookup"><span data-stu-id="b0121-104">This guide provides an overview of developing line-of-business (LoB) applications for Azure Active Directory (AD).The intended audience is Active Directory/Office 365 global administrators.</span></span>

## <a name="overview"></a><span data-ttu-id="b0121-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="b0121-105">Overview</span></span>
<span data-ttu-id="b0121-106">La création d’applications intégrées à Azure AD permet aux utilisateurs de votre organisation de bénéficier de l’authentification unique avec Office 365.</span><span class="sxs-lookup"><span data-stu-id="b0121-106">Building applications integrated with Azure AD gives users in your organization single sign-on with Office 365.</span></span> <span data-ttu-id="b0121-107">En disposant de l’application dans Azure AD, vous pouvez contrôler la stratégie d’authentification pour celle-ci.</span><span class="sxs-lookup"><span data-stu-id="b0121-107">Having the application in Azure AD gives you control over the authentication policy for the application.</span></span> <span data-ttu-id="b0121-108">Pour en savoir plus sur l’accès conditionnel et la façon de protéger les applications avec l’authentification multifacteur, consultez [Configuration des règles d’accès](active-directory-conditional-access-azuread-connected-apps.md).</span><span class="sxs-lookup"><span data-stu-id="b0121-108">To learn more about conditional access and how to protect apps with multi-factor authentication (MFA) see [Configuring access rules](active-directory-conditional-access-azuread-connected-apps.md).</span></span>

<span data-ttu-id="b0121-109">Inscrivez votre application pour utiliser Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b0121-109">Register your application to use Azure Active Directory.</span></span> <span data-ttu-id="b0121-110">Inscrire l’application signifie que vos développeurs peuvent utiliser Azure AD pour authentifier les utilisateurs et demander l’accès aux ressources de l’utilisateur, telles que le courrier électronique, le calendrier et des documents.</span><span class="sxs-lookup"><span data-stu-id="b0121-110">Registering the application means that your developers can use Azure AD to authenticate users and request access to user resources such as email, calendar, and documents.</span></span>

<span data-ttu-id="b0121-111">Tout membre de votre annuaire (pas les invités) peut inscrire une application, procédé également appelé *création d’un objet d’application*.</span><span class="sxs-lookup"><span data-stu-id="b0121-111">Any member of your directory (not guests) can register an application, otherwise known as *creating an application object*.</span></span>

<span data-ttu-id="b0121-112">En inscrivant une application, tout utilisateur peut effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="b0121-112">Registering an application allows any user to do the following:</span></span>

* <span data-ttu-id="b0121-113">Obtenir pour son application une identité reconnue par Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b0121-113">Get an identity for their application that Azure AD recognizes</span></span>
* <span data-ttu-id="b0121-114">Obtenir un ou plusieurs secrets/clés que l’application peut utiliser pour s’authentifier auprès d’Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b0121-114">Get one or more secrets/keys that the application can use to authenticate itself to AD</span></span>
* <span data-ttu-id="b0121-115">Personnaliser l’application avec un nom personnalisé, un logo, etc., dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="b0121-115">Brand the application in the Azure portal with a custom name, logo, etc.</span></span>
* <span data-ttu-id="b0121-116">Appliquer les fonctionnalités d’autorisation Azure AD pour l’application, notamment :</span><span class="sxs-lookup"><span data-stu-id="b0121-116">Apply Azure AD authorization features to their app, including:</span></span>

  * <span data-ttu-id="b0121-117">Contrôle d’accès en fonction du rôle</span><span class="sxs-lookup"><span data-stu-id="b0121-117">Role-Based Access Control (RBAC)</span></span>
  * <span data-ttu-id="b0121-118">Azure Active Directory en tant que serveur d’autorisation oAuth (sécuriser une API exposée par l’application)</span><span class="sxs-lookup"><span data-stu-id="b0121-118">Azure Active Directory as oAuth authorization server (secure an API exposed by the application)</span></span>
* <span data-ttu-id="b0121-119">Déclarer les autorisations requises nécessaires au bon fonctionnement de l’application, notamment :</span><span class="sxs-lookup"><span data-stu-id="b0121-119">Declare required permissions necessary for the application to function as expected, including:</span></span>

      - <span data-ttu-id="b0121-120">Autorisations de l’application (administrateurs généraux uniquement).</span><span class="sxs-lookup"><span data-stu-id="b0121-120">App permissions (global administrators only).</span></span> <span data-ttu-id="b0121-121">Par exemple : Appartenance au rôle dans une autre application Azure AD ou appartenance au rôle par rapport à une ressource, un groupe de ressources ou un abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="b0121-121">For example: Role membership in another Azure AD application or role membership relative to an Azure Resource, Resource Group, or Subscription</span></span>
      - <span data-ttu-id="b0121-122">Autorisations déléguées (tout utilisateur).</span><span class="sxs-lookup"><span data-stu-id="b0121-122">Delegated permissions (any user).</span></span> <span data-ttu-id="b0121-123">Par exemple : Azure AD, connexion et lecture de profil</span><span class="sxs-lookup"><span data-stu-id="b0121-123">For example: Azure AD, Sign-in, and Read Profile</span></span>

> [!NOTE]
> <span data-ttu-id="b0121-124">Par défaut, tout membre peut inscrire une application.</span><span class="sxs-lookup"><span data-stu-id="b0121-124">By default, any member can register an application.</span></span> <span data-ttu-id="b0121-125">Pour savoir comment limiter les autorisations d’inscription d’applications à des membres spécifiques, reportez-vous au document [Comment les applications sont ajoutées à Azure AD](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance).</span><span class="sxs-lookup"><span data-stu-id="b0121-125">To learn how to restrict permissions for registering applications to specific members, see [How applications are added to Azure AD](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance).</span></span>
>
>

<span data-ttu-id="b0121-126">Voici les opérations que vous devez effectuer en tant qu’administrateur général pour aider les développeurs à préparer leurs applications pour la production :</span><span class="sxs-lookup"><span data-stu-id="b0121-126">Here’s what you, the global administrator, need to do to help developers make their application ready for production:</span></span>

* <span data-ttu-id="b0121-127">Configurer des règles d’accès (stratégie d’accès/MFA)</span><span class="sxs-lookup"><span data-stu-id="b0121-127">Configure access rules (access policy/MFA)</span></span>
* <span data-ttu-id="b0121-128">Configurer l’application pour qu’elle demande l’affectation de l’utilisateur et affecter des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="b0121-128">Configure the app to require user assignment and assign users</span></span>
* <span data-ttu-id="b0121-129">Supprimer l’expérience de consentement d’utilisateur par défaut</span><span class="sxs-lookup"><span data-stu-id="b0121-129">Suppress the default user consent experience</span></span>

## <a name="configure-access-rules"></a><span data-ttu-id="b0121-130">Configurer des règles d’accès</span><span class="sxs-lookup"><span data-stu-id="b0121-130">Configure access rules</span></span>
<span data-ttu-id="b0121-131">Configurer des règles d’accès par application de vos applications SaaS.</span><span class="sxs-lookup"><span data-stu-id="b0121-131">Configure per-application access rules to your SaaS apps.</span></span> <span data-ttu-id="b0121-132">Par exemple, vous pouvez requérir un MFA, ou autoriser l’accès aux utilisateurs uniquement sur les réseaux approuvés.</span><span class="sxs-lookup"><span data-stu-id="b0121-132">For example, you can require MFA or only allow access to users on trusted networks.</span></span> <span data-ttu-id="b0121-133">Pour plus d’informations à ce sujet, voir [Configuration des règles d’accès](active-directory-conditional-access-azuread-connected-apps.md).</span><span class="sxs-lookup"><span data-stu-id="b0121-133">The details for this are available in the document [Configuring access rules](active-directory-conditional-access-azuread-connected-apps.md).</span></span>

## <a name="configure-the-app-to-require-user-assignment-and-assign-users"></a><span data-ttu-id="b0121-134">Configurer l’application pour qu’elle demande l’affectation de l’utilisateur et affecter des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="b0121-134">Configure the app to require user assignment and assign users</span></span>
<span data-ttu-id="b0121-135">Par défaut, les utilisateurs peuvent accéder aux applications sans affectation.</span><span class="sxs-lookup"><span data-stu-id="b0121-135">By default, users can access applications without being assigned.</span></span> <span data-ttu-id="b0121-136">Toutefois, si l’application expose des rôles ou que vous souhaitez qu’elle s’affiche sur le panneau d’accès d’un utilisateur, vous devez demander l’affectation de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b0121-136">However, if the application exposes roles or if you want the application to appear on a user’s access panel, you should require user assignment.</span></span>

[<span data-ttu-id="b0121-137">Demande de l’affectation de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="b0121-137">Requiring user assignment</span></span>](active-directory-applications-guiding-developers-requiring-user-assignment.md)

<span data-ttu-id="b0121-138">Si vous êtes abonné à Azure AD Premium ou Enterprise Mobility Suite (EMS), nous vous recommandons fortement d’utiliser les groupes.</span><span class="sxs-lookup"><span data-stu-id="b0121-138">If you’re an Azure AD Premium or Enterprise Mobility Suite (EMS) subscriber, we strongly recommend using groups.</span></span> <span data-ttu-id="b0121-139">L’affectation de groupes à l’application vous permet de déléguer la gestion d’accès en continu au propriétaire du groupe.</span><span class="sxs-lookup"><span data-stu-id="b0121-139">Assigning groups to the application allows you to delegate ongoing access management to the owner of the group.</span></span> <span data-ttu-id="b0121-140">Vous pouvez créer un groupe ou demander à la personne responsable au sein de votre organisation de créer un groupe à l’aide de votre dispositif de gestion de groupe.</span><span class="sxs-lookup"><span data-stu-id="b0121-140">You can create the group or ask the responsible party in your organization to create the group using your group management facility.</span></span>

[<span data-ttu-id="b0121-141">Affectation d’utilisateurs à une application</span><span class="sxs-lookup"><span data-stu-id="b0121-141">Assigning users to an application</span></span>](active-directory-applications-guiding-developers-assigning-users.md)  
[<span data-ttu-id="b0121-142">Affectation de groupes à une application</span><span class="sxs-lookup"><span data-stu-id="b0121-142">Assigning groups to an application</span></span>](active-directory-applications-guiding-developers-assigning-groups.md)

## <a name="suppress-user-consent"></a><span data-ttu-id="b0121-143">Supprimer le consentement de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="b0121-143">Suppress user consent</span></span>
<span data-ttu-id="b0121-144">Par défaut, chaque utilisateur doit se soumettre à une expérience de consentement pour se connecter.</span><span class="sxs-lookup"><span data-stu-id="b0121-144">By default, each user goes through a consent experience to sign in.</span></span> <span data-ttu-id="b0121-145">L’expérience de la demande aux utilisateurs d’un consentement à l’octroi d’autorisations à une application peut être déconcertante pour les utilisateurs qui ne sont pas familiarisés avec la prise de décision de ce type.</span><span class="sxs-lookup"><span data-stu-id="b0121-145">The consent experience, asking users to grant permissions to an application, can be disconcerting for users who are unfamiliar with making such decisions.</span></span>

<span data-ttu-id="b0121-146">Pour les applications de confiance, vous pouvez simplifier l’expérience utilisateur en accordant le consentement à l’application au nom de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="b0121-146">For applications that you trust, you can simplify the user experience by consenting to the application on behalf of your organization.</span></span>

<span data-ttu-id="b0121-147">Pour en savoir plus sur le consentement de l’utilisateur et sur l’expérience du consentement dans Azure, consultez [Intégration d’applications dans Azure Active Directory](active-directory-integrating-applications.md).</span><span class="sxs-lookup"><span data-stu-id="b0121-147">For more information about user consent and the consent experience in Azure, see [Integrating Applications with Azure Active Directory](active-directory-integrating-applications.md).</span></span>

## <a name="related-articles"></a><span data-ttu-id="b0121-148">Articles connexes</span><span class="sxs-lookup"><span data-stu-id="b0121-148">Related Articles</span></span>
* [<span data-ttu-id="b0121-149">Offrir un accès à distance sécurisé aux applications locales</span><span class="sxs-lookup"><span data-stu-id="b0121-149">Enable secure remote access to on-premises applications with Azure AD Application Proxy</span></span>](active-directory-application-proxy-get-started.md)
* [<span data-ttu-id="b0121-150">Vue d’ensemble de l’accès conditionnel Azure pour les applications SaaS</span><span class="sxs-lookup"><span data-stu-id="b0121-150">Azure Conditional Access Preview for SaaS Apps</span></span>](active-directory-conditional-access-azuread-connected-apps.md)
* [<span data-ttu-id="b0121-151">Gestion de l’accès aux applications</span><span class="sxs-lookup"><span data-stu-id="b0121-151">Managing access to apps with Azure AD</span></span>](active-directory-managing-access-to-apps.md)
* [<span data-ttu-id="b0121-152">Index d’articles pour la gestion des applications dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b0121-152">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
