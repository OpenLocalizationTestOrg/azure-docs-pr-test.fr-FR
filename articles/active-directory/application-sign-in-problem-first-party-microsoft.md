---
title: aaaProblems connecter tooa application Microsoft | Documents Microsoft
description: "Résoudre les problèmes courants rencontrés lors de la connexion toofirst Microsoft Applications tierces à l’aide d’Azure AD (par exemple, Office 365)"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 35849ca8dbaa909d17b6d0da572f5c11041a8559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
## <a name="problems-signing-in-tooa-microsoft-application"></a><span data-ttu-id="1fbe2-103">Problèmes de connexion tooa application Microsoft</span><span class="sxs-lookup"><span data-stu-id="1fbe2-103">Problems signing in tooa Microsoft application</span></span>

<span data-ttu-id="1fbe2-104">Les applications Microsoft (comme Office 365 Exchange, SharePoint, Yammer, etc.) sont affectées et gérées un peu différemment des applications SaaS tierces et des autres applications que vous intégrez à Azure AD pour l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-104">Microsoft Applications (like Office 365 Exchange, SharePoint, Yammer, etc.) are assigned and managed a bit differently than 3rd party SaaS applications or other applications you integrate with Azure AD for single sign on.</span></span>

<span data-ttu-id="1fbe2-105">Il existe trois manières principales qu’un utilisateur peut obtenir l’accès tooa-Microsoft a publié l’application.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-105">There are three main ways that a user can get access tooa Microsoft-published application.</span></span>

-   <span data-ttu-id="1fbe2-106">Pour les applications dans hello Office 365 ou d’autres suites de tests payants, utilisateurs sont autorisés à accéder via **l’attribution de licence** soit directement tootheir compte d’utilisateur ou via un groupe à l’aide de notre capacité d’affectation basée sur le groupe de licences.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-106">For applications in hello Office 365 or other paid suites, users are granted access through **license assignment** either directly tootheir user account, or through a group using our group-based license assignment capability.</span></span>

-   <span data-ttu-id="1fbe2-107">Pour les applications que Microsoft ou un tiers publie librement pour toute personne toouse, les utilisateurs peuvent accéder via **consentement de l’utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-107">For applications that Microsoft or a Third Party publishes freely for anyone toouse, users may be granted access through **user consent**.</span></span> <span data-ttu-id="1fbe2-108">This0 signifie qu’ils application toohello avec leur compte Azure AD ou votre école de connexion et permettent de jeu de toosome limitée accès toohave de données sur son compte.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-108">This0 means that they sign in toohello application with their Azure AD Work or School account and allow it toohave access toosome limited set of data on their account.</span></span>

-   <span data-ttu-id="1fbe2-109">Pour les applications que Microsoft ou un tiers 3e publie librement pour toute personne toouse, les utilisateurs peuvent également être accordés l’accès via **consentement de l’administrateur**.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-109">For applications that Microsoft or a 3rd Party publishes freely for anyone toouse, users may also be granted access through **administrator consent**.</span></span> <span data-ttu-id="1fbe2-110">Cela signifie qu’un administrateur a déterminé l’application hello peut être utilisée par tous les membres de l’organisation de hello, afin qu’ils application toohello avec un compte d’administrateur Global de connexion et accorder tooeveryone d’accès dans l’organisation de hello.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-110">This means that an administrator has determined hello application may be used by everyone in hello organization, so they sign in toohello application with a Global Administrator account and grant access tooeveryone in hello organization.</span></span>

<span data-ttu-id="1fbe2-111">tootroubleshoot votre problème, commencent par Bonjour [zones à problème général avec l’accès aux applications tooconsider](#general-problem-areas-with-application-access-to-consider) , puis lire hello [procédure pas à pas : étapes tootroubleshoot accès aux applications de Microsoft](#walkthrough-steps-to-troubleshoot-microsoft-application-access) tooget dans les détails de hello.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-111">tootroubleshoot your issue, start with hello [General Problem Areas with Application Access tooconsider](#general-problem-areas-with-application-access-to-consider) and then read hello [Walkthrough: Steps tootroubleshoot Microsoft Application access](#walkthrough-steps-to-troubleshoot-microsoft-application-access) tooget into hello details.</span></span>

## <a name="general-problem-areas-with-application-access-tooconsider"></a><span data-ttu-id="1fbe2-112">Zones à problème général avec l’accès aux applications tooconsider</span><span class="sxs-lookup"><span data-stu-id="1fbe2-112">General Problem Areas with Application Access tooconsider</span></span>

<span data-ttu-id="1fbe2-113">Voici une liste de hello zones à problème général que vous pouvez Explorer si vous avez une idée d’où toostart, mais nous vous conseillons de lire hello tooget de procédure pas à pas va rapidement : [procédure pas à pas : étapes tootroubleshoot accès de l’Application Microsoft](#walkthrough-steps-to-troubleshoot-microsoft-application-access).</span><span class="sxs-lookup"><span data-stu-id="1fbe2-113">Below is a list of hello general problem areas that you can drill into if you have an idea of where toostart, but we recommend you read hello walkthrough tooget going quickly: [Walkthrough: Steps tootroubleshoot Microsoft Application access](#walkthrough-steps-to-troubleshoot-microsoft-application-access).</span></span>

-   [<span data-ttu-id="1fbe2-114">Problèmes avec le compte d’utilisateur hello</span><span class="sxs-lookup"><span data-stu-id="1fbe2-114">Problems with hello user’s account</span></span>](#problems-with-the-users-account)

-   [<span data-ttu-id="1fbe2-115">Problèmes liés aux groupes</span><span class="sxs-lookup"><span data-stu-id="1fbe2-115">Problems with groups</span></span>](#problems-with-groups)

-   [<span data-ttu-id="1fbe2-116">Problèmes liés aux stratégies d’accès conditionnel</span><span class="sxs-lookup"><span data-stu-id="1fbe2-116">Problems with conditional access policies</span></span>](#problems-with-conditional-access-policies)

-   [<span data-ttu-id="1fbe2-117">Problèmes liés au consentement d’application</span><span class="sxs-lookup"><span data-stu-id="1fbe2-117">Problems with application consent</span></span>](#problems-with-application-consent)

## <a name="steps-tootroubleshoot-microsoft-application-access"></a><span data-ttu-id="1fbe2-118">Étapes tootroubleshoot accès aux applications de Microsoft</span><span class="sxs-lookup"><span data-stu-id="1fbe2-118">Steps tootroubleshoot Microsoft Application access</span></span>

<span data-ttu-id="1fbe2-119">Ci-dessous sont certaines personnes problèmes courants rencontrer quand les utilisateurs ne peuvent pas se connecter tooa application Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-119">Below are some common issues folks run into when their users cannot sign in tooa Microsoft application.</span></span>

-   <span data-ttu-id="1fbe2-120">Général émet toocheck tout d’abord</span><span class="sxs-lookup"><span data-stu-id="1fbe2-120">General issues toocheck first</span></span>

  * <span data-ttu-id="1fbe2-121">Assurez-vous que la signature de l’utilisateur de hello dans toohello **Corrigez-la** et pas une URL de l’application locale.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-121">Make sure hello user is signing in toohello **correct URL** and not a local application URL.</span></span>

  * <span data-ttu-id="1fbe2-122">Assurez-vous que le compte d’utilisateur hello est **ne pas verrouillé.**</span><span class="sxs-lookup"><span data-stu-id="1fbe2-122">Make sure hello user’s account is **not locked out.**</span></span>

  * <span data-ttu-id="1fbe2-123">Vérifiez que hello **compte d’utilisateur existe** dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-123">Make sure hello **user’s account exists** in Azure Active Directory.</span></span> [<span data-ttu-id="1fbe2-124">Vérifier l’existence d’un compte d’utilisateur dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1fbe2-124">Check if a user account exists in Azure Active Directory</span></span>](#problems-with-the-users-account)

  * <span data-ttu-id="1fbe2-125">Assurez-vous que le compte d’utilisateur hello est **activé** pour les connexions. [Vérifier l’état du compte d’un utilisateur](#problems-with-the-users-account)</span><span class="sxs-lookup"><span data-stu-id="1fbe2-125">Make sure hello user’s account is **enabled** for sign ins. [Check a user’s account status](#problems-with-the-users-account)</span></span>

  * <span data-ttu-id="1fbe2-126">Vérifiez que hello l’utilisateur **mot de passe n’a pas expiré ou oublié.**</span><span class="sxs-lookup"><span data-stu-id="1fbe2-126">Make sure hello user’s **password is not expired or forgotten.**</span></span> <span data-ttu-id="1fbe2-127">[Réinitialiser le mot de passe d’un utilisateur](#reset-a-users-password) ou [Activer la réinitialisation du mot de passe libre-service](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started)</span><span class="sxs-lookup"><span data-stu-id="1fbe2-127">[Reset a user’s password](#reset-a-users-password) or [Enable self-service password reset](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started)</span></span>

   * <span data-ttu-id="1fbe2-128">Vérifiez que **Multi-Factor Authentication** ne bloque pas l’accès utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-128">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span> <span data-ttu-id="1fbe2-129">[Vérifier l’état Multi-Factor Authentication d’un utilisateur](#check-a-users-multi-factor-authentication-status) ou [Vérifier les informations de contact de l’authentification d’un utilisateur](#check-a-users-authentication-contact-info)</span><span class="sxs-lookup"><span data-stu-id="1fbe2-129">[Check a user’s multi-factor authentication status](#check-a-users-multi-factor-authentication-status) or [Check a user’s authentication contact info](#check-a-users-authentication-contact-info)</span></span>

   * <span data-ttu-id="1fbe2-130">Vérifiez qu’une **stratégie d’accès conditionnel** ou qu’une **stratégie de protection d’identité** ne bloque pas l’accès utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-130">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span> <span data-ttu-id="1fbe2-131">[Vérifier une stratégie d’accès conditionnel](#problems-with-conditional-access-policies) ou [Vérifier la stratégie d’accès conditionnel d’une application spécifique](#check-a-specific-applications-conditional-access-policy) ou [Désactiver une stratégie d’accès conditionnel](#disable-a-specific-conditional-access-policy)</span><span class="sxs-lookup"><span data-stu-id="1fbe2-131">[Check a specific conditional access policy](#problems-with-conditional-access-policies) or [Check a specific application’s conditional access policy](#check-a-specific-applications-conditional-access-policy) or [Disable a specific conditional access policy](#disable-a-specific-conditional-access-policy)</span></span>

   * <span data-ttu-id="1fbe2-132">S’assurer que l’utilisateur **les informations de contact d’authentification** est toodate tooallow multi-Factor Authentication ou accès conditionnel stratégies toobe appliquée.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-132">Make sure that a user’s **authentication contact info** is up toodate tooallow Multi-Factor Authentication or Conditional Access policies toobe enforced.</span></span> <span data-ttu-id="1fbe2-133">[Vérifier l’état Multi-Factor Authentication d’un utilisateur](#check-a-users-multi-factor-authentication-status) ou [Vérifier les informations de contact de l’authentification d’un utilisateur](#check-a-users-authentication-contact-info)</span><span class="sxs-lookup"><span data-stu-id="1fbe2-133">[Check a user’s multi-factor authentication status](#check-a-users-multi-factor-authentication-status) or [Check a user’s authentication contact info](#check-a-users-authentication-contact-info)</span></span>

-   <span data-ttu-id="1fbe2-134">Pour **Microsoft** **les applications qui nécessitent une licence** (comme Office 365), Voici certains problèmes spécifiques de toocheck une fois que vous avez écarté problèmes généraux de hello ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="1fbe2-134">For **Microsoft** **applications that require a license** (like Office365), here are some specific issues toocheck once you have ruled out hello general issues above:</span></span>

   * <span data-ttu-id="1fbe2-135">S’assurer que hello utilisateur ou a un **licence attribuée.**</span><span class="sxs-lookup"><span data-stu-id="1fbe2-135">Ensure hello user or has a **license assigned.**</span></span> <span data-ttu-id="1fbe2-136">[Vérifier les licences affectées à un utilisateur](#check-a-users-assigned-licenses) ou [Vérifier les licences affectées à un groupe](#check-a-groups-assigned-licenses)</span><span class="sxs-lookup"><span data-stu-id="1fbe2-136">[Check a user’s assigned licenses](#check-a-users-assigned-licenses) or [Check a group’s assigned licenses](#check-a-groups-assigned-licenses)</span></span>

   * <span data-ttu-id="1fbe2-137">Si la licence hello est **affecté tooa** **groupe statique**, vérifiez que hello **utilisateur est membre** de ce groupe.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-137">If hello license is **assigned tooa** **static group**, ensure that hello **user is a member** of that group.</span></span> [<span data-ttu-id="1fbe2-138">Vérifier les appartenances d’un utilisateur à des groupes</span><span class="sxs-lookup"><span data-stu-id="1fbe2-138">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

   * <span data-ttu-id="1fbe2-139">Si la licence hello est **affecté tooa** **groupe dynamique**, vérifiez que hello **règle de groupe dynamique est correctement**.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-139">If hello license is **assigned tooa** **dynamic group**, ensure that hello **dynamic group rule is set correctly**.</span></span> [<span data-ttu-id="1fbe2-140">Vérifier les critères d’appartenance d’un groupe dynamique</span><span class="sxs-lookup"><span data-stu-id="1fbe2-140">Check a dynamic group’s membership criteria</span></span>](#check-a-dynamic-groups-membership-criteria)

   * <span data-ttu-id="1fbe2-141">Si la licence hello est **affecté tooa** **groupe dynamique**, vérifiez ce groupe dynamique hello a **terminé le traitement** son appartenance et ce hello **utilisateur est un membre** (Cela peut prendre un certain temps).</span><span class="sxs-lookup"><span data-stu-id="1fbe2-141">If hello license is **assigned tooa** **dynamic group**, ensure that hello dynamic group has **finished processing** its membership and that hello **user is a member** (this can take some time).</span></span> [<span data-ttu-id="1fbe2-142">Vérifier les appartenances d’un utilisateur à des groupes</span><span class="sxs-lookup"><span data-stu-id="1fbe2-142">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

   *  <span data-ttu-id="1fbe2-143">Une fois que vous vérifiez que les licences hello sont attribuée, assurez-vous que la licence hello est **ne pas expiré**.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-143">Once you make sure hello license is assigned, make sure hello license is **not expired**.</span></span>

   *  <span data-ttu-id="1fbe2-144">Assurez-vous que la licence hello est **pour l’application hello** ils accèdent.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-144">Make sure hello license is **for hello application** they are accessing.</span></span>

-   <span data-ttu-id="1fbe2-145">Pour **Microsoft** **les applications qui ne nécessitent pas une licence**, voici quelques autres toocheck choses :</span><span class="sxs-lookup"><span data-stu-id="1fbe2-145">For **Microsoft** **applications that don’t require a license**, here are some other things toocheck:</span></span>

   * <span data-ttu-id="1fbe2-146">Si l’application hello demande **autorisations au niveau de l’utilisateur** (par exemple « accéder à cette boîte aux lettres »), assurez-vous que l’utilisateur hello toohello application s’est connecté et a effectué une **opération d’accord de niveau de l’utilisateur**  application hello de toolet accéder à ses données.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-146">If hello application is requesting **user-level permissions** (for example “Access this user’s mailbox”), make sure that hello user has signed in toohello application and has performed a **user-level consent operation** toolet hello application access her data.</span></span>

   * <span data-ttu-id="1fbe2-147">Si l’application hello demande **autorisations de niveau administrateur** (par exemple « accéder aux boîtes aux lettres de tous les utilisateurs »), assurez-vous qu’un administrateur général a effectué une **opération d’accord de niveau administrateur sur nom de tous les utilisateurs** dans l’organisation de hello.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-147">If hello application is requesting **administrator-level permissions** (for example “Access all user’s mailboxes”), make sure that a Global Administrator has performed an **administrator-level consent operation on behalf of all users** in hello organization.</span></span>

## <a name="problems-with-hello-users-account"></a><span data-ttu-id="1fbe2-148">Problèmes avec le compte d’utilisateur hello</span><span class="sxs-lookup"><span data-stu-id="1fbe2-148">Problems with hello user’s account</span></span>

<span data-ttu-id="1fbe2-149">Accès à l’application peut être bloqué en raison du problème de tooa avec un utilisateur qui est attribué toohello application.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-149">Application access can be blocked due tooa problem with a user that is assigned toohello application.</span></span> <span data-ttu-id="1fbe2-150">Voici quelques méthodes pour vous aider à résoudre les problèmes avec les utilisateurs et leurs paramètres de compte :</span><span class="sxs-lookup"><span data-stu-id="1fbe2-150">Below are some ways you can troubleshoot and solve problems with users and their account settings:</span></span>

-   [<span data-ttu-id="1fbe2-151">Vérifier l’existence d’un compte d’utilisateur dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1fbe2-151">Check if a user account exists in Azure Active Directory</span></span>](#check-if-a-user-account-exists-in-azure-active-directory)

-   [<span data-ttu-id="1fbe2-152">Vérifier l’état du compte d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="1fbe2-152">Check a user’s account status</span></span>](#check-a-users-account-status)

-   [<span data-ttu-id="1fbe2-153">Réinitialiser le mot de passe d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="1fbe2-153">Reset a user’s password</span></span>](#reset-a-users-password)

-   [<span data-ttu-id="1fbe2-154">Activer la réinitialisation du mot de passe libre-service</span><span class="sxs-lookup"><span data-stu-id="1fbe2-154">Enable self-service password reset</span></span>](#enable-self-service-password-reset)

-   [<span data-ttu-id="1fbe2-155">Vérifier l’état Multi-Factor Authentication d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="1fbe2-155">Check a user’s multi-factor authentication status</span></span>](#check-a-users-multi-factor-authentication-status)

-   [<span data-ttu-id="1fbe2-156">Vérifier les informations de contact de l’authentification d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="1fbe2-156">Check a user’s authentication contact info</span></span>](#check-a-users-authentication-contact-info)

-   [<span data-ttu-id="1fbe2-157">Vérifier les appartenances d’un utilisateur à des groupes</span><span class="sxs-lookup"><span data-stu-id="1fbe2-157">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="1fbe2-158">Vérifier les licences affectées à un utilisateur</span><span class="sxs-lookup"><span data-stu-id="1fbe2-158">Check a user’s assigned licenses</span></span>](#check-a-users-assigned-licenses)

-   [<span data-ttu-id="1fbe2-159">Affecter une licence à un utilisateur</span><span class="sxs-lookup"><span data-stu-id="1fbe2-159">Assign a user a license</span></span>](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a><span data-ttu-id="1fbe2-160">Vérifier l’existence d’un compte d’utilisateur dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1fbe2-160">Check if a user account exists in Azure Active Directory</span></span>

<span data-ttu-id="1fbe2-161">toocheck si un compte d’utilisateur est présent, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1fbe2-161">toocheck if a user’s account is present, follow hello steps below:</span></span>

1.  <span data-ttu-id="1fbe2-162">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="1fbe2-162">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1fbe2-163">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-163">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1fbe2-164">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-164">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1fbe2-165">Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-165">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="1fbe2-166">Cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-166">click **All users**.</span></span>

6.  <span data-ttu-id="1fbe2-167">**Recherche** pour l’utilisateur hello vous intéressez et **cliquez sur la ligne hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-167">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="1fbe2-168">Vérifiez les propriétés de hello de hello utilisateur objet toobe assurer qu’elles apparaîtront comme prévu et aucune donnée n’est manquante.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-168">Check hello properties of hello user object toobe sure that they look as you expect and no data is missing.</span></span>

### <a name="check-a-users-account-status"></a><span data-ttu-id="1fbe2-169">Vérifier l’état du compte d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="1fbe2-169">Check a user’s account status</span></span>

<span data-ttu-id="1fbe2-170">toocheck un utilisateur état du compte, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1fbe2-170">toocheck a user’s account status, follow hello steps below:</span></span>

1.  <span data-ttu-id="1fbe2-171">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="1fbe2-171">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1fbe2-172">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-172">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1fbe2-173">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-173">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1fbe2-174">Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-174">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="1fbe2-175">Cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-175">click **All users**.</span></span>

6.  <span data-ttu-id="1fbe2-176">**Recherche** pour l’utilisateur hello vous intéressez et **cliquez sur la ligne hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-176">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="1fbe2-177">Cliquez sur **Profil**.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-177">click **Profile**.</span></span>

8.  <span data-ttu-id="1fbe2-178">Sous **paramètres** vous assurer que **bloc connectez-vous** est défini trop**non**.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-178">Under **Settings** ensure that **Block sign in** is set too**No**.</span></span>

### <a name="reset-a-users-password"></a><span data-ttu-id="1fbe2-179">Réinitialiser le mot de passe d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="1fbe2-179">Reset a user’s password</span></span>

<span data-ttu-id="1fbe2-180">tooreset un mot de passe, suivez les étapes hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1fbe2-180">tooreset a user’s password, follow hello steps below:</span></span>

1.  <span data-ttu-id="1fbe2-181">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="1fbe2-181">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1fbe2-182">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-182">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1fbe2-183">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-183">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1fbe2-184">Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-184">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="1fbe2-185">Cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-185">click **All users**.</span></span>

6.  <span data-ttu-id="1fbe2-186">**Recherche** pour l’utilisateur hello vous intéressez et **cliquez sur la ligne hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-186">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="1fbe2-187">Cliquez sur hello **réinitialisation de mot de passe** bouton en haut de hello du panneau d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-187">click hello **Reset password** button at hello top of hello user blade.</span></span>

8.  <span data-ttu-id="1fbe2-188">Cliquez sur hello **réinitialisation de mot de passe** bouton sur hello **réinitialisation de mot de passe** panneau s’affiche.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-188">click hello **Reset password** button on hello **Reset password** blade that appears.</span></span>

9.  <span data-ttu-id="1fbe2-189">Hello de copie **mot de passe temporaire** ou **Entrez un nouveau mot de passe** pour l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-189">Copy hello **temporary password** or **enter a new password** for hello user.</span></span>

10. <span data-ttu-id="1fbe2-190">Communiquer ce nouvel utilisateur toohello de mot de passe, ils requis toochange ce mot de passe lors de sa prochaine connexion tooAzure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-190">Communicate this new password toohello user, they be required toochange this password during their next sign in tooAzure Active Directory.</span></span>

### <a name="enable-self-service-password-reset"></a><span data-ttu-id="1fbe2-191">Activer la réinitialisation du mot de passe libre-service</span><span class="sxs-lookup"><span data-stu-id="1fbe2-191">Enable self-service password reset</span></span>

<span data-ttu-id="1fbe2-192">tooenable le mot de passe libre-service de réinitialisation, suivez les étapes de déploiement hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1fbe2-192">tooenable self-service password reset, follow hello deployment steps below:</span></span>

-   [<span data-ttu-id="1fbe2-193">Activer les utilisateurs tooreset leurs mots de passe Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1fbe2-193">Enable users tooreset their Azure Active Directory passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [<span data-ttu-id="1fbe2-194">Activer les utilisateurs tooreset ou de modifier leurs mots de passe Active Directory local</span><span class="sxs-lookup"><span data-stu-id="1fbe2-194">Enable users tooreset or change their Active Directory on-premises passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a><span data-ttu-id="1fbe2-195">Vérifier l’état Multi-Factor Authentication d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="1fbe2-195">Check a user’s multi-factor authentication status</span></span>

<span data-ttu-id="1fbe2-196">toocheck un utilisateur multi-Factor de l’état d’authentification, suivez les étapes hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1fbe2-196">toocheck a user’s multi-factor authentication status, follow hello steps below:</span></span>

1.  <span data-ttu-id="1fbe2-197">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="1fbe2-197">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1fbe2-198">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-198">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1fbe2-199">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-199">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1fbe2-200">Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-200">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="1fbe2-201">Cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-201">click **All users**.</span></span>

6.  <span data-ttu-id="1fbe2-202">Cliquez sur hello **multi-Factor Authentication** bouton en haut de hello du panneau des hello.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-202">click hello **Multi-Factor Authentication** button at hello top of hello blade.</span></span>

7.  <span data-ttu-id="1fbe2-203">Une fois hello **portail d’Administration de l’authentification multifacteur** charges, assurez-vous que vous êtes sur hello **utilisateurs** onglet.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-203">Once hello **Multi-Factor Authentication Administration Portal** loads, ensure you are on hello **Users** tab.</span></span>

8.  <span data-ttu-id="1fbe2-204">Rechercher les utilisateur hello dans liste hello des utilisateurs par la recherche, le filtrage ou le tri.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-204">Find hello user in hello list of users by searching, filtering, or sorting.</span></span>

9.  <span data-ttu-id="1fbe2-205">Utilisateur hello SELECT à partir de la liste de hello des utilisateurs et **activer**, **désactiver**, ou **appliquer** authentification multifacteur selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-205">Select hello user from hello list of users and **Enable**, **Disable**, or **Enforce** multi-factor authentication as desired.</span></span>

  * <span data-ttu-id="1fbe2-206">**Remarque**: si un utilisateur est dans un **appliqué** d’état, vous pouvez les définir trop**désactivé** temporairement toolet replacer dans son compte.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-206">**Note**: If a user is in an **Enforced** state, you may set them too**Disabled** temporarily toolet them back into their account.</span></span> <span data-ttu-id="1fbe2-207">Une fois qu’ils sont dans, vous pouvez ensuite modifier leur état trop**activé** toorequire à nouveau les toore-s’inscrire leurs informations de contact lors de sa prochaine connexion.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-207">Once they are back in, you can then change their state too**Enabled** again toorequire them toore-register their contact information during their next sign in.</span></span> <span data-ttu-id="1fbe2-208">Ou bien, vous pouvez suivre les étapes de hello Bonjour [vérifier les informations de contact de l’authentification d’un utilisateur](#check-a-users-authentication-contact-info) tooverify ou définir ces données pour eux.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-208">Alternatively, you can follow hello steps in hello [Check a user’s authentication contact info](#check-a-users-authentication-contact-info) tooverify or set this data for them.</span></span>

### <a name="check-a-users-authentication-contact-info"></a><span data-ttu-id="1fbe2-209">Vérifier les informations de contact de l’authentification d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="1fbe2-209">Check a user’s authentication contact info</span></span>

<span data-ttu-id="1fbe2-210">toocheck utilisée pour l’authentification multifacteur, l’accès conditionnel, Protection d’identité et réinitialisation du mot de passe, des informations de contact de l’authentification de l’utilisateur suit hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1fbe2-210">toocheck a user’s authentication contact info used for Multi-factor authentication, Conditional Access, Identity Protection, and Password Reset, follow hello steps below:</span></span>

1.  <span data-ttu-id="1fbe2-211">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="1fbe2-211">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1fbe2-212">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-212">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1fbe2-213">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-213">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1fbe2-214">Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-214">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="1fbe2-215">Cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-215">click **All users**.</span></span>

6.  <span data-ttu-id="1fbe2-216">**Recherche** pour l’utilisateur hello vous intéressez et **cliquez sur la ligne hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-216">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="1fbe2-217">Cliquez sur **Profil**.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-217">click **Profile**.</span></span>

8.  <span data-ttu-id="1fbe2-218">Faites défiler la liste trop**les informations de contact d’authentification**.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-218">Scroll down too**Authentication contact info**.</span></span>

9.  <span data-ttu-id="1fbe2-219">**Révision** les données de salutation inscrit pour l’utilisateur de hello et de mise à jour en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-219">**Review** hello data registered for hello user and update as needed.</span></span>

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="1fbe2-220">Vérifier les appartenances d’un utilisateur à des groupes</span><span class="sxs-lookup"><span data-stu-id="1fbe2-220">Check a user’s group memberships</span></span>

<span data-ttu-id="1fbe2-221">de toocheck un utilisateur appartenance aux groupes, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1fbe2-221">toocheck a user’s group memberships, follow hello steps below:</span></span>

1.  <span data-ttu-id="1fbe2-222">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="1fbe2-222">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1fbe2-223">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-223">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1fbe2-224">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-224">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1fbe2-225">Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-225">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="1fbe2-226">Cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-226">click **All users**.</span></span>

6.  <span data-ttu-id="1fbe2-227">**Recherche** pour l’utilisateur hello vous intéressez et **cliquez sur la ligne hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-227">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="1fbe2-228">Cliquez sur **groupes** toosee qui regroupe les utilisateur hello est membre.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-228">click **Groups** toosee which groups hello user is a member of.</span></span>

### <a name="check-a-users-assigned-licenses"></a><span data-ttu-id="1fbe2-229">Vérifier les licences affectées à un utilisateur</span><span class="sxs-lookup"><span data-stu-id="1fbe2-229">Check a user’s assigned licenses</span></span>

<span data-ttu-id="1fbe2-230">toocheck un utilisateur affecté des licences, suivez les étapes hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1fbe2-230">toocheck a user’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="1fbe2-231">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="1fbe2-231">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1fbe2-232">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-232">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1fbe2-233">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-233">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1fbe2-234">Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-234">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="1fbe2-235">Cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-235">click **All users**.</span></span>

6.  <span data-ttu-id="1fbe2-236">**Recherche** pour l’utilisateur hello vous intéressez et **cliquez sur la ligne hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-236">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="1fbe2-237">Cliquez sur **licences** toosee les licences hello d’utilisateur est affectée actuellement.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-237">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

### <a name="assign-a-user-a-license"></a><span data-ttu-id="1fbe2-238">Affecter une licence à un utilisateur</span><span class="sxs-lookup"><span data-stu-id="1fbe2-238">Assign a user a license</span></span> 

<span data-ttu-id="1fbe2-239">tooassign un utilisateur tooa de licences, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1fbe2-239">tooassign a license tooa user, follow hello steps below:</span></span>

1.  <span data-ttu-id="1fbe2-240">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="1fbe2-240">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1fbe2-241">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-241">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1fbe2-242">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-242">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1fbe2-243">Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-243">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="1fbe2-244">Cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-244">click **All users**.</span></span>

6.  <span data-ttu-id="1fbe2-245">**Recherche** pour l’utilisateur hello vous intéressez et **cliquez sur la ligne hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-245">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="1fbe2-246">Cliquez sur **licences** toosee les licences hello d’utilisateur est affectée actuellement.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-246">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

8.  <span data-ttu-id="1fbe2-247">Cliquez sur hello **affecter** bouton.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-247">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="1fbe2-248">Sélectionnez **un ou plusieurs produits** à partir de la liste de hello des produits disponibles.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-248">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="1fbe2-249">**Facultatif** cliquez sur hello **options d’attribution** élément toogranularly affecter des produits.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-249">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="1fbe2-250">Cliquez sur **OK** lorsque l’opération est terminée.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-250">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="1fbe2-251">Cliquez sur hello **affecter** bouton tooassign ces utilisateur toothis de licences.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-251">Click hello **Assign** button tooassign these licenses toothis user.</span></span>

## <a name="problems-with-groups"></a><span data-ttu-id="1fbe2-252">Problèmes liés aux groupes</span><span class="sxs-lookup"><span data-stu-id="1fbe2-252">Problems with groups</span></span>

<span data-ttu-id="1fbe2-253">Accès à l’application peut être bloqué en raison du problème de tooa avec un groupe auquel est attribué toohello application.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-253">Application access can be blocked due tooa problem with a group that is assigned toohello application.</span></span> <span data-ttu-id="1fbe2-254">Voici quelques méthodes pour vous aider à résoudre les problèmes liés aux groupes et à l’appartenance :</span><span class="sxs-lookup"><span data-stu-id="1fbe2-254">Below are some ways you can troubleshoot and solve problems with groups and group memberships:</span></span>

-   [<span data-ttu-id="1fbe2-255">Vérifier l’appartenance à un groupe</span><span class="sxs-lookup"><span data-stu-id="1fbe2-255">Check a group’s membership</span></span>](#check-a-groups-membership)

-   [<span data-ttu-id="1fbe2-256">Vérifier les critères d’appartenance d’un groupe dynamique</span><span class="sxs-lookup"><span data-stu-id="1fbe2-256">Check a dynamic group’s membership criteria</span></span>](#check-a-dynamic-groups-membership-criteria)

-   [<span data-ttu-id="1fbe2-257">Vérifier les licences affectées à un groupe</span><span class="sxs-lookup"><span data-stu-id="1fbe2-257">Check a group’s assigned licenses</span></span>](#check-a-groups-assigned-licenses)

-   [<span data-ttu-id="1fbe2-258">Retraiter les licences d’un groupe</span><span class="sxs-lookup"><span data-stu-id="1fbe2-258">Reprocess a group’s licenses</span></span>](#reprocess-a-groups-licenses)

-   [<span data-ttu-id="1fbe2-259">Affecter une licence à un groupe</span><span class="sxs-lookup"><span data-stu-id="1fbe2-259">Assign a group a license</span></span>](#assign-a-group-a-license)

### <a name="check-a-groups-membership"></a><span data-ttu-id="1fbe2-260">Vérifier l’appartenance à un groupe</span><span class="sxs-lookup"><span data-stu-id="1fbe2-260">Check a group’s membership</span></span>

<span data-ttu-id="1fbe2-261">toocheck une appartenance de groupe, suivez les étapes hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1fbe2-261">toocheck a group’s membership, follow hello steps below:</span></span>

1.  <span data-ttu-id="1fbe2-262">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="1fbe2-262">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1fbe2-263">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-263">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1fbe2-264">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-264">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1fbe2-265">Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-265">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="1fbe2-266">Cliquez sur **Tous les groupes**.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-266">click **All groups**.</span></span>

6.  <span data-ttu-id="1fbe2-267">**Recherche** pour groupe hello vous intéressez et **cliquez sur la ligne hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-267">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="1fbe2-268">Cliquez sur **membres** liste de hello tooreview d’utilisateurs affectés toothis groupe.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-268">click **Members** tooreview hello list of users assigned toothis group.</span></span>

### <a name="check-a-dynamic-groups-membership-criteria"></a><span data-ttu-id="1fbe2-269">Vérifier les critères d’appartenance d’un groupe dynamique</span><span class="sxs-lookup"><span data-stu-id="1fbe2-269">Check a dynamic group’s membership criteria</span></span> 

<span data-ttu-id="1fbe2-270">toocheck les critères d’appartenance d’un groupe dynamique, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1fbe2-270">toocheck a dynamic group’s membership criteria, follow hello steps below:</span></span>

1.  <span data-ttu-id="1fbe2-271">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="1fbe2-271">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1fbe2-272">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-272">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1fbe2-273">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-273">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1fbe2-274">Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-274">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="1fbe2-275">Cliquez sur **Tous les groupes**.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-275">click **All groups**.</span></span>

6.  <span data-ttu-id="1fbe2-276">**Recherche** pour groupe hello vous intéressez et **cliquez sur la ligne hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-276">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="1fbe2-277">Cliquez sur **Règles d’appartenance dynamique**.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-277">click **Dynamic membership rules.**</span></span>

8.  <span data-ttu-id="1fbe2-278">Hello de révision **simple** ou **avancées** définie pour ce groupe de règles et vérifiez que cet utilisateur hello souhaité toobe un membre de ce groupe répond à ces critères.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-278">Review hello **simple** or **advanced** rule defined for this group and ensure that hello user you want toobe a member of this group meets these criteria.</span></span>

### <a name="check-a-groups-assigned-licenses"></a><span data-ttu-id="1fbe2-279">Vérifier les licences affectées à un groupe</span><span class="sxs-lookup"><span data-stu-id="1fbe2-279">Check a group’s assigned licenses</span></span>

<span data-ttu-id="1fbe2-280">toocheck un groupe affecté des licences, suivez les étapes hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1fbe2-280">toocheck a group’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="1fbe2-281">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="1fbe2-281">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1fbe2-282">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-282">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1fbe2-283">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-283">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1fbe2-284">Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-284">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="1fbe2-285">Cliquez sur **Tous les groupes**.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-285">click **All groups**.</span></span>

6.  <span data-ttu-id="1fbe2-286">**Recherche** pour groupe hello vous intéressez et **cliquez sur la ligne hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-286">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="1fbe2-287">Cliquez sur **licences** toosee quel groupe hello de licences est affectée actuellement.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-287">click **Licenses** toosee which licenses hello group currently has assigned.</span></span>

### <a name="reprocess-a-groups-licenses"></a><span data-ttu-id="1fbe2-288">Retraiter les licences d’un groupe</span><span class="sxs-lookup"><span data-stu-id="1fbe2-288">Reprocess a group’s licenses</span></span>

<span data-ttu-id="1fbe2-289">tooreprocess un groupe affecté des licences, suivez les étapes hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1fbe2-289">tooreprocess a group’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="1fbe2-290">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="1fbe2-290">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1fbe2-291">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-291">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1fbe2-292">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-292">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1fbe2-293">Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-293">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="1fbe2-294">Cliquez sur **Tous les groupes**.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-294">click **All groups**.</span></span>

6.  <span data-ttu-id="1fbe2-295">**Recherche** pour groupe hello vous intéressez et **cliquez sur la ligne hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-295">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="1fbe2-296">Cliquez sur **licences** toosee quel groupe hello de licences est affectée actuellement.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-296">click **Licenses** toosee which licenses hello group currently has assigned.</span></span>

8.  <span data-ttu-id="1fbe2-297">Cliquez sur hello **retraiter** tooensure bouton qui hello les membres du groupe de licences attribuées toothis sont à jour.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-297">click hello **Reprocess** button tooensure that hello licenses assigned toothis group’s members are up-to-date.</span></span> <span data-ttu-id="1fbe2-298">Cette opération peut prendre beaucoup de temps, selon la taille de hello et la complexité du groupe de hello.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-298">This may take a long time, depending on hello size and complexity of hello group.</span></span>

   >[!NOTE]
   ><span data-ttu-id="1fbe2-299">toodo cela plus rapide, envisagez temporairement attribution directement à un utilisateur de toohello de licence.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-299">toodo this faster, consider temporarily assigning a license toohello user directly.</span></span> <span data-ttu-id="1fbe2-300">[Affecter une licence à un utilisateur](#problems-with-application-consent)</span><span class="sxs-lookup"><span data-stu-id="1fbe2-300">[Assign a user a license](#problems-with-application-consent).</span></span>
   >
   >

### <a name="assign-a-group-a-license"></a><span data-ttu-id="1fbe2-301">Affecter une licence à un groupe</span><span class="sxs-lookup"><span data-stu-id="1fbe2-301">Assign a group a license</span></span>

<span data-ttu-id="1fbe2-302">tooassign un groupe tooa de licences, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1fbe2-302">tooassign a license tooa group, follow hello steps below:</span></span>

1.  <span data-ttu-id="1fbe2-303">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="1fbe2-303">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1fbe2-304">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-304">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1fbe2-305">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-305">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1fbe2-306">Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-306">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="1fbe2-307">Cliquez sur **Tous les groupes**.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-307">click **All groups**.</span></span>

6.  <span data-ttu-id="1fbe2-308">**Recherche** pour groupe hello vous intéressez et **cliquez sur la ligne hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-308">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="1fbe2-309">Cliquez sur **licences** toosee quel groupe hello de licences est affectée actuellement.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-309">click **Licenses** toosee which licenses hello group currently has assigned.</span></span>

8.  <span data-ttu-id="1fbe2-310">Cliquez sur hello **affecter** bouton.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-310">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="1fbe2-311">Sélectionnez **un ou plusieurs produits** à partir de la liste de hello des produits disponibles.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-311">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="1fbe2-312">**Facultatif** cliquez sur hello **options d’attribution** élément toogranularly affecter des produits.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-312">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="1fbe2-313">Cliquez sur **OK** lorsque l’opération est terminée.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-313">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="1fbe2-314">Cliquez sur hello **affecter** bouton tooassign ces toothis de groupe de licences.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-314">Click hello **Assign** button tooassign these licenses toothis group.</span></span> <span data-ttu-id="1fbe2-315">Cette opération peut prendre beaucoup de temps, selon la taille de hello et la complexité du groupe de hello.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-315">This may take a long time, depending on hello size and complexity of hello group.</span></span>

   >[!NOTE]
   ><span data-ttu-id="1fbe2-316">toodo cela plus rapide, envisagez temporairement attribution directement à un utilisateur de toohello de licence.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-316">toodo this faster, consider temporarily assigning a license toohello user directly.</span></span> <span data-ttu-id="1fbe2-317">[Affecter une licence à un utilisateur](#problems-with-application-consent)</span><span class="sxs-lookup"><span data-stu-id="1fbe2-317">[Assign a user a license](#problems-with-application-consent).</span></span>
   > 
   >

## <a name="problems-with-conditional-access-policies"></a><span data-ttu-id="1fbe2-318">Problèmes liés aux stratégies d’accès conditionnel</span><span class="sxs-lookup"><span data-stu-id="1fbe2-318">Problems with conditional access policies</span></span>

### <a name="check-a-specific-conditional-access-policy"></a><span data-ttu-id="1fbe2-319">Vérifier une stratégie d’accès conditionnel</span><span class="sxs-lookup"><span data-stu-id="1fbe2-319">Check a specific conditional access policy</span></span>

<span data-ttu-id="1fbe2-320">toocheck ou valider une stratégie d’accès conditionnel unique :</span><span class="sxs-lookup"><span data-stu-id="1fbe2-320">toocheck or validate a single conditional access policy:</span></span>

1.  <span data-ttu-id="1fbe2-321">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="1fbe2-321">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1fbe2-322">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-322">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1fbe2-323">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-323">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1fbe2-324">Cliquez sur **des applications d’entreprise** dans le menu de navigation hello.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-324">click **Enterprise applications** in hello navigation menu.</span></span>

5.  <span data-ttu-id="1fbe2-325">Cliquez sur hello **accès conditionnel** élément de navigation.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-325">click hello **Conditional access** navigation item.</span></span>

6.  <span data-ttu-id="1fbe2-326">Cliquez sur stratégie hello vous êtes intéressé par inspection.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-326">click hello policy you are interested in inspecting.</span></span>

7.  <span data-ttu-id="1fbe2-327">Vérifiez la présence de conditions, d’affectations ou d’autres paramètres pouvant bloquer l’accès de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-327">Review that there are no specific conditions, assignments, or other settings which may be blocking user access.</span></span>

   >[!NOTE]
   ><span data-ttu-id="1fbe2-328">Vous souhaiterez peut-être tootemporarily désactiver cette tooensure stratégie qu’il n’affecte pas les signe assurance toodo, hello ensemble **activer la stratégie** basculer trop**non** et cliquez sur hello **enregistrer** bouton .</span><span class="sxs-lookup"><span data-stu-id="1fbe2-328">You may wish tootemporarily disable this policy tooensure it is not affecting sign ins. toodo this, set hello **Enable policy** toggle too**No** and click hello **Save** button.</span></span>
   >
   >

### <a name="check-a-specific-applications-conditional-access-policy"></a><span data-ttu-id="1fbe2-329">Vérifier une stratégie d’accès conditionnel d’une application</span><span class="sxs-lookup"><span data-stu-id="1fbe2-329">Check a specific application’s conditional access policy</span></span>

<span data-ttu-id="1fbe2-330">toocheck ou valider une seule stratégie de l’application actuellement configuré l’accès conditionnel :</span><span class="sxs-lookup"><span data-stu-id="1fbe2-330">toocheck or validate a single application’s currently configured conditional access policy:</span></span>

1.  <span data-ttu-id="1fbe2-331">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="1fbe2-331">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1fbe2-332">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-332">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1fbe2-333">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-333">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1fbe2-334">Cliquez sur **des applications d’entreprise** dans le menu de navigation hello.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-334">click **Enterprise applications** in hello navigation menu.</span></span>

5.  <span data-ttu-id="1fbe2-335">Cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-335">click **All applications**.</span></span>

6.  <span data-ttu-id="1fbe2-336">Recherche de l’application hello vous intéressez, ou hello utilisateur tente de toosign dans tooby application afficher les id de nom ou de l’application.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-336">Search for hello application you are interested in, or hello user is attempting toosign in tooby application display name or application id.</span></span>

     >[!NOTE]
     ><span data-ttu-id="1fbe2-337">Si vous ne voyez pas application hello souhaité, cliquez sur hello **filtre** bouton et étendre la portée de hello de liste de hello trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-337">If you don’t see hello application you are looking for, click hello **Filter** button and expand hello scope of hello list too**All applications**.</span></span> <span data-ttu-id="1fbe2-338">Si vous souhaitez toosee plus de colonnes, cliquez sur hello **colonnes** bouton tooadd des détails supplémentaires pour vos applications.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-338">If you want toosee more columns, click hello **Columns** button tooadd additional details for your applications.</span></span>
     >
     >

7.  <span data-ttu-id="1fbe2-339">Cliquez sur hello **accès conditionnel** élément de navigation.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-339">click hello **Conditional access** navigation item.</span></span>

8.  <span data-ttu-id="1fbe2-340">Cliquez sur stratégie hello vous êtes intéressé par inspection.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-340">click hello policy you are interested in inspecting.</span></span>

9.  <span data-ttu-id="1fbe2-341">Vérifiez la présence de conditions, d’affectations ou d’autres paramètres pouvant bloquer l’accès de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-341">Review that there are no specific conditions, assignments, or other settings which may be blocking user access.</span></span>

     >[!NOTE]
     ><span data-ttu-id="1fbe2-342">Vous souhaiterez peut-être tootemporarily désactiver cette tooensure stratégie qu’il n’affecte pas les signe assurance toodo, hello ensemble **activer la stratégie** basculer trop**non** et cliquez sur hello **enregistrer** bouton .</span><span class="sxs-lookup"><span data-stu-id="1fbe2-342">You may wish tootemporarily disable this policy tooensure it is not affecting sign ins. toodo this, set hello **Enable policy** toggle too**No** and click hello **Save** button.</span></span>
     >
     >

### <a name="disable-a-specific-conditional-access-policy"></a><span data-ttu-id="1fbe2-343">Désactiver une stratégie d’accès conditionnel</span><span class="sxs-lookup"><span data-stu-id="1fbe2-343">Disable a specific conditional access policy</span></span>

<span data-ttu-id="1fbe2-344">toocheck ou valider une stratégie d’accès conditionnel unique :</span><span class="sxs-lookup"><span data-stu-id="1fbe2-344">toocheck or validate a single conditional access policy:</span></span>

1.  <span data-ttu-id="1fbe2-345">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="1fbe2-345">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1fbe2-346">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-346">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1fbe2-347">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-347">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1fbe2-348">Cliquez sur **des applications d’entreprise** dans le menu de navigation hello.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-348">click **Enterprise applications** in hello navigation menu.</span></span>

5.  <span data-ttu-id="1fbe2-349">Cliquez sur hello **accès conditionnel** élément de navigation.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-349">click hello **Conditional access** navigation item.</span></span>

6.  <span data-ttu-id="1fbe2-350">Cliquez sur stratégie hello vous êtes intéressé par inspection.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-350">click hello policy you are interested in inspecting.</span></span>

7.  <span data-ttu-id="1fbe2-351">Désactivez hello de stratégie en définissant un hello **activer la stratégie** basculer trop**non** et cliquez sur hello **enregistrer** bouton.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-351">Disable hello policy by setting hello **Enable policy** toggle too**No** and click hello **Save** button.</span></span>

## <a name="problems-with-application-consent"></a><span data-ttu-id="1fbe2-352">Problèmes liés au consentement d’application</span><span class="sxs-lookup"><span data-stu-id="1fbe2-352">Problems with application consent</span></span>

<span data-ttu-id="1fbe2-353">Accès à l’application peut être bloqué, car l’opération de consentement d’autorisations adéquates hello n’a pas eu lieu.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-353">Application access can be blocked because hello proper permissions consent operation has not occurred.</span></span> <span data-ttu-id="1fbe2-354">Voici quelques méthodes pour résoudre les problèmes de consentement d’application :</span><span class="sxs-lookup"><span data-stu-id="1fbe2-354">Below are some ways you can troubleshoot and solve application consent issues:</span></span>

-   [<span data-ttu-id="1fbe2-355">Effectuer une opération de consentement de niveau utilisateur</span><span class="sxs-lookup"><span data-stu-id="1fbe2-355">Perform a user-level consent operation</span></span>](#perform-a-user-level-consent-operation)

-   [<span data-ttu-id="1fbe2-356">Effectuer une opération de consentement de niveau administrateur pour n’importe quelle application</span><span class="sxs-lookup"><span data-stu-id="1fbe2-356">Perform administrator-level consent operation for any application</span></span>](#perform-administrator-level-consent-operation-for-any-application)

-   [<span data-ttu-id="1fbe2-357">Effectuer une opération de consentement de niveau administrateur pour une application à locataire unique</span><span class="sxs-lookup"><span data-stu-id="1fbe2-357">Perform administrator-level consent for a single-tenant application</span></span>](#perform-administrator-level-consent-for-a-single-tenant-application)

-   [<span data-ttu-id="1fbe2-358">Effectuer une opération de consentement de niveau administrateur pour une application multilocataire</span><span class="sxs-lookup"><span data-stu-id="1fbe2-358">Perform administrator-level consent for a multi-tenant application</span></span>](#perform-administrator-level-consent-for-a-multi-tenant-application)

### <a name="perform-a-user-level-consent-operation"></a><span data-ttu-id="1fbe2-359">Effectuer une opération de consentement de niveau utilisateur</span><span class="sxs-lookup"><span data-stu-id="1fbe2-359">Perform a user-level consent operation</span></span>

-   <span data-ttu-id="1fbe2-360">Pour des applications compatibles ouvrir connecter d’ID qui demande des autorisations, la navigation d’écran de connexion de l’application toohello effectue une application de toohello utilisateur au niveau de consentement pour l’utilisateur connecté hello.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-360">For any Open ID Connect-enabled application that requests permissions, navigating toohello application’s sign in screen performs a user level consent toohello application for hello signed-in user.</span></span>

-   <span data-ttu-id="1fbe2-361">Si vous souhaitez toodo cela par programme, consultez [demander le consentement des utilisateurs](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#requesting-individual-user-consent).</span><span class="sxs-lookup"><span data-stu-id="1fbe2-361">If you wish toodo this programmatically, see [Requesting individual user consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#requesting-individual-user-consent).</span></span>

### <a name="perform-administrator-level-consent-operation-for-any-application"></a><span data-ttu-id="1fbe2-362">Effectuer une opération de consentement de niveau administrateur pour n’importe quelle application</span><span class="sxs-lookup"><span data-stu-id="1fbe2-362">Perform administrator-level consent operation for any application</span></span>

-   <span data-ttu-id="1fbe2-363">Pour **uniquement les applications développées à l’aide du modèle d’application hello V1**, vous pouvez forcer cette toooccur de niveau de consentement d’administrateur en ajoutant «**? invite = admin\_donner son consentement**« fin toohello d’un URL de connexion de l’application.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-363">For **only applications developed using hello V1 application model**, you can force this administrator level consent toooccur by adding “**?prompt=admin\_consent**” toohello end of an application’s sign in URL.</span></span>

-   <span data-ttu-id="1fbe2-364">Pour **toutes les applications développées à l’aide du modèle d’application hello V2**, vous pouvez appliquer cette toooccur au niveau de l’administrateur de consentement en suivant les instructions de hello sous hello **demander des autorisations de hello à partir d’un répertoire administrateur** section de [à l’aide du point de terminaison hello admin consentement](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span><span class="sxs-lookup"><span data-stu-id="1fbe2-364">For **any application developed using hello V2 application model**, you can enforce this administrator-level consent toooccur by following hello instructions under hello **Request hello permissions from a directory admin** section of [Using hello admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

### <a name="perform-administrator-level-consent-for-a-single-tenant-application"></a><span data-ttu-id="1fbe2-365">Effectuer une opération de consentement de niveau administrateur pour une application à locataire unique</span><span class="sxs-lookup"><span data-stu-id="1fbe2-365">Perform administrator-level consent for a single-tenant application</span></span>

-   <span data-ttu-id="1fbe2-366">Pour **locataire unique applications** qui demande les autorisations (telles que celles vous développez ou que vous possédez dans votre organisation), vous pouvez effectuer une **administratives consentement** opération pour le compte de toutes les les utilisateurs en vous connectant en tant qu’administrateur général et en cliquant sur hello **accorder des autorisations** bouton haut hello hello **Registre de l’Application -&gt; toutes les Applications -&gt; sélectionner une application - &gt; Autorisations requises** panneau.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-366">For **single-tenant applications** that request permissions (like those you are developing or own in your organization), you can perform an **administrative-level consent** operation on behalf of all users by signing in as a Global Administrator and clicking on hello **Grant permissions** button at hello top of hello **Application Registry -&gt; All Applications -&gt; Select an App -&gt; Required Permissions** blade.</span></span>

-   <span data-ttu-id="1fbe2-367">Pour **toutes les applications développées à l’aide de hello V1 ou V2 modèle d’application**, vous pouvez appliquer cette toooccur au niveau de l’administrateur de consentement en suivant les instructions de hello sous hello **demander des autorisations hello à un l’administrateur Active** section de [à l’aide du point de terminaison hello admin consentement](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span><span class="sxs-lookup"><span data-stu-id="1fbe2-367">For **any application developed using hello V1 or V2 application model**, you can enforce this administrator-level consent toooccur by following hello instructions under hello **Request hello permissions from a directory admin** section of [Using hello admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

### <a name="perform-administrator-level-consent-for-a-multi-tenant-application"></a><span data-ttu-id="1fbe2-368">Effectuer une opération de consentement de niveau administrateur pour une application multilocataire</span><span class="sxs-lookup"><span data-stu-id="1fbe2-368">Perform administrator-level consent for a multi-tenant application</span></span>

-   <span data-ttu-id="1fbe2-369">Pour les **applications multilocataires** qui demandent des autorisations (comme les applications développées par un tiers ou par Microsoft), vous pouvez effectuer une opération de **consentement de niveau administrateur**.</span><span class="sxs-lookup"><span data-stu-id="1fbe2-369">For **multi-tenant applications** that request permissions (like an application a third party, or Microsoft, develops), you can perform an **administrative-level consent** operation.</span></span> <span data-ttu-id="1fbe2-370">Connectez-vous en tant qu’administrateur général et en cliquant sur hello **accorder des autorisations** sous hello **des Applications d’entreprise -&gt; toutes les Applications -&gt; sélectionner une application -&gt; Autorisations** blade (disponible bientôt).</span><span class="sxs-lookup"><span data-stu-id="1fbe2-370">Sign in as a Global Administrator and clicking on hello **Grant permissions** button under hello **Enterprise Applications -&gt; All Applications -&gt; Select an App -&gt; Permissions** blade (available soon).</span></span>

-   <span data-ttu-id="1fbe2-371">Vous pouvez également appliquer cette toooccur au niveau de l’administrateur de consentement en suivant les instructions de hello sous hello **demander des autorisations de hello à un administrateur d’annuaire** section de [à l’aide du point de terminaison hello admin consentement](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span><span class="sxs-lookup"><span data-stu-id="1fbe2-371">You can also enforce this administrator-level consent toooccur by following hello instructions under hello **Request hello permissions from a directory admin** section of [Using hello admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1fbe2-372">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1fbe2-372">Next steps</span></span>
[<span data-ttu-id="1fbe2-373">À l’aide du point de terminaison consentement hello admin</span><span class="sxs-lookup"><span data-stu-id="1fbe2-373">Using hello admin consent endpoint</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint)

