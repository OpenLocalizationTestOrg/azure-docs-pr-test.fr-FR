---
title: "aaaProblem de signature dans le site Web du panneau d’accès toohello | Documents Microsoft"
description: "Problèmes de tootroubleshoot de conseils que vous pouvez rencontrer lors de la tentative de toosign dans toouse hello panneau d’accès"
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
ms.reviwer: japere
ms.openlocfilehash: 1037f7c5fbaa9425760ad5739b383c716d5fc3a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-signing-in-toohello-access-panel-website"></a><span data-ttu-id="d0571-103">Problème de connexion dans le site Web du panneau d’accès toohello</span><span class="sxs-lookup"><span data-stu-id="d0571-103">Problem signing in toohello access panel website</span></span>

<span data-ttu-id="d0571-104">Hello volet d’accès est un portail web qui permet à un utilisateur qui dispose d’une entreprise ou école administrateur de compte dans Azure Active Directory (Azure AD) tooview et lancer les applications cloud qui hello Azure AD lui a accordé l’accès à.</span><span class="sxs-lookup"><span data-stu-id="d0571-104">hello Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) tooview and launch cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="d0571-105">Un utilisateur disposant des éditions d’Azure AD permet également de groupes en libre-service et les fonctionnalités de gestion d’application via hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="d0571-105">A user who has Azure AD editions can also use self-service group and app management capabilities through hello Access Panel.</span></span> <span data-ttu-id="d0571-106">Hello volet d’accès est séparé hello portail Azure et ne requiert pas d’utilisateurs toohave un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="d0571-106">hello Access Panel is separate from hello Azure portal and does not require users toohave an Azure subscription.</span></span>

<span data-ttu-id="d0571-107">Les utilisateurs peuvent se connecter toohello volet d’accès s’ils ont un compte professionnel ou scolaire dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d0571-107">Users can sign in toohello Access Panel if they have a work or school account in Azure AD.</span></span>

-   <span data-ttu-id="d0571-108">Les utilisateurs peuvent être authentifiés par Azure AD directement.</span><span class="sxs-lookup"><span data-stu-id="d0571-108">Users can be authenticated by Azure AD directly.</span></span>

-   <span data-ttu-id="d0571-109">Les utilisateurs peuvent être authentifiés à l’aide d’Active Directory Federation Services (ADFS).</span><span class="sxs-lookup"><span data-stu-id="d0571-109">Users can be authenticated by using Active Directory Federation Services (AD FS).</span></span>

-   <span data-ttu-id="d0571-110">Les utilisateurs peuvent être authentifiés par Windows Server Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d0571-110">Users can be authenticated by Windows Server Active Directory.</span></span>

<span data-ttu-id="d0571-111">Si un utilisateur dispose d’un abonnement pour Azure ou Office 365 et à l’aide hello portail Azure ou une application Office 365, ils serez en mesure de toouse hello volet d’accès en toute transparence sans avoir besoin de toosign de nouveau.</span><span class="sxs-lookup"><span data-stu-id="d0571-111">If a user has a subscription for Azure or Office 365 and has been using hello Azure portal or an Office 365 application, they'll be able toouse hello Access Panel seamlessly without needing toosign in again.</span></span> <span data-ttu-id="d0571-112">Les utilisateurs qui ne sont pas authentifiés être demandée toosign dans à l’aide de nom d’utilisateur hello et le mot de passe de leur compte dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d0571-112">Users who are not authenticated be prompted toosign in by using hello username and password for their account in Azure AD.</span></span> <span data-ttu-id="d0571-113">Si l’organisation de hello a configuré la fédération, il suffit de taper le nom d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="d0571-113">If hello organization has configured federation, typing hello username is sufficient.</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="d0571-114">Général émet toocheck tout d’abord</span><span class="sxs-lookup"><span data-stu-id="d0571-114">General issues toocheck first</span></span> 

-   <span data-ttu-id="d0571-115">Assurez-vous que la signature de l’utilisateur de hello dans toohello **Corrigez-la**: <https://myapps.microsoft.com></span><span class="sxs-lookup"><span data-stu-id="d0571-115">Make sure hello user is signing in toohello **correct URL**: <https://myapps.microsoft.com></span></span>

-   <span data-ttu-id="d0571-116">Assurez-vous que navigateur de l’utilisateur hello a ajouté hello URL tooits **sites de confiance**</span><span class="sxs-lookup"><span data-stu-id="d0571-116">Make sure hello user’s browser has added hello URL tooits **trusted sites**</span></span>

-   <span data-ttu-id="d0571-117">Assurez-vous que le compte d’utilisateur hello est **activé** pour les connexions.</span><span class="sxs-lookup"><span data-stu-id="d0571-117">Make sure hello user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="d0571-118">Assurez-vous que le compte d’utilisateur hello est **ne pas verrouillé.**</span><span class="sxs-lookup"><span data-stu-id="d0571-118">Make sure hello user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="d0571-119">Vérifiez que hello l’utilisateur **mot de passe n’a pas expiré ou oublié.**</span><span class="sxs-lookup"><span data-stu-id="d0571-119">Make sure hello user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="d0571-120">Vérifiez que **Multi-Factor Authentication** ne bloque pas l’accès utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d0571-120">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="d0571-121">Vérifiez qu’une **stratégie d’accès conditionnel** ou **stratégie de protection d’identité** ne bloque pas l’accès utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d0571-121">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="d0571-122">S’assurer que l’utilisateur **les informations de contact d’authentification** est toodate tooallow multi-Factor Authentication ou accès conditionnel stratégies toobe appliquée.</span><span class="sxs-lookup"><span data-stu-id="d0571-122">Make sure that a user’s **authentication contact info** is up toodate tooallow Multi-Factor Authentication or Conditional Access policies toobe enforced.</span></span>

-   <span data-ttu-id="d0571-123">Assurez-vous que tooalso try effacer les cookies de votre navigateur et réessayer toosign dans.</span><span class="sxs-lookup"><span data-stu-id="d0571-123">Make sure tooalso try clearing your browser’s cookies and trying toosign in again.</span></span>

## <a name="meeting-browser-requirements-for-hello-access-panel"></a><span data-ttu-id="d0571-124">Configuration requise du navigateur de réunion hello panneau d’accès</span><span class="sxs-lookup"><span data-stu-id="d0571-124">Meeting browser requirements for hello Access Panel</span></span>

<span data-ttu-id="d0571-125">Hello volet d’accès nécessite un navigateur qui prend en charge JavaScript et a activé les CSS.</span><span class="sxs-lookup"><span data-stu-id="d0571-125">hello Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="d0571-126">toouse mot de passe-session unique (SSO) Bonjour hello extension du volet d’accès, volet d’accès doit être installé dans le navigateur de l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="d0571-126">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="d0571-127">Cette extension est téléchargée automatiquement lorsqu’un utilisateur sélectionne une application configurée pour l’authentification unique (SSO) avec mot de passe.</span><span class="sxs-lookup"><span data-stu-id="d0571-127">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="d0571-128">Pour l’authentification unique basée sur le mot de passe, hello navigateurs des utilisateurs finaux peuvent être :</span><span class="sxs-lookup"><span data-stu-id="d0571-128">For password-based SSO, hello end user’s browsers can be:</span></span>

-   <span data-ttu-id="d0571-129">Internet Explorer 8, 9, 10, 11 -- sur Windows 7 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="d0571-129">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="d0571-130">Edge sur Windows 10 Édition anniversaire ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="d0571-130">Edge on Windows 10 Anniversary Edition or later</span></span> 

-   <span data-ttu-id="d0571-131">Chrome -- sur Windows 7 ou ultérieur, et sur Mac OS X ou ultérieur</span><span class="sxs-lookup"><span data-stu-id="d0571-131">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="d0571-132">Firefox 26.0 ou ultérieur -- sur Windows XP SP2 ou ultérieur, et sur Mac OS X 10.6 ou ultérieur</span><span class="sxs-lookup"><span data-stu-id="d0571-132">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>


## <a name="problems-with-hello-users-account"></a><span data-ttu-id="d0571-133">Problèmes avec le compte d’utilisateur hello</span><span class="sxs-lookup"><span data-stu-id="d0571-133">Problems with hello user’s account</span></span>

<span data-ttu-id="d0571-134">Accès toohello volet d’accès peut être bloqué en raison du problème de tooa avec un compte d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="d0571-134">Access toohello Access Panel can be blocked due tooa problem with hello user’s account.</span></span> <span data-ttu-id="d0571-135">Voici quelques méthodes pour vous aider à résoudre les problèmes avec les utilisateurs et leurs paramètres de compte :</span><span class="sxs-lookup"><span data-stu-id="d0571-135">Below are some ways you can troubleshoot and solve problems with users and their account settings:</span></span>

-   [<span data-ttu-id="d0571-136">Vérifier l’existence d’un compte d’utilisateur dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d0571-136">Check if a user account exists in Azure Active Directory</span></span>](#check-if-a-user-account-exists-in-azure-active-directory)

-   [<span data-ttu-id="d0571-137">Vérifier l’état du compte d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="d0571-137">Check a user’s account status</span></span>](#check-a-users-account-status)

-   [<span data-ttu-id="d0571-138">Réinitialiser le mot de passe d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="d0571-138">Reset a user’s password</span></span>](#reset-a-users-password)

-   [<span data-ttu-id="d0571-139">Activer la réinitialisation du mot de passe libre-service</span><span class="sxs-lookup"><span data-stu-id="d0571-139">Enable self-service password reset</span></span>](#enable-self-service-password-reset)

-   [<span data-ttu-id="d0571-140">Vérifier l’état Multi-Factor Authentication d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="d0571-140">Check a user’s multi-factor authentication status</span></span>](#check-a-users-multi-factor-authentication-status)

-   [<span data-ttu-id="d0571-141">Vérifier les informations de contact de l’authentification d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="d0571-141">Check a user’s authentication contact info</span></span>](#check-a-users-authentication-contact-info)

-   [<span data-ttu-id="d0571-142">Vérifier les appartenances d’un utilisateur à des groupes</span><span class="sxs-lookup"><span data-stu-id="d0571-142">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="d0571-143">Vérifier les licences affectées à un utilisateur</span><span class="sxs-lookup"><span data-stu-id="d0571-143">Check a user’s assigned licenses</span></span>](#check-a-users-assigned-licenses)

-   [<span data-ttu-id="d0571-144">Affecter une licence à un utilisateur</span><span class="sxs-lookup"><span data-stu-id="d0571-144">Assign a user a license</span></span>](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a><span data-ttu-id="d0571-145">Vérifier l’existence d’un compte d’utilisateur dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d0571-145">Check if a user account exists in Azure Active Directory</span></span>

<span data-ttu-id="d0571-146">toocheck si un compte d’utilisateur est présent, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="d0571-146">toocheck if a user’s account is present, follow hello steps below:</span></span>

1.  <span data-ttu-id="d0571-147">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="d0571-147">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d0571-148">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="d0571-148">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d0571-149">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="d0571-149">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d0571-150">Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.</span><span class="sxs-lookup"><span data-stu-id="d0571-150">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="d0571-151">Cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="d0571-151">click **All users**.</span></span>

6.  <span data-ttu-id="d0571-152">**Recherche** pour l’utilisateur hello vous intéressez et **cliquez sur la ligne hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="d0571-152">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="d0571-153">Vérifiez les propriétés de hello de hello utilisateur objet toobe assurer qu’elles apparaîtront comme prévu et aucune donnée n’est manquante.</span><span class="sxs-lookup"><span data-stu-id="d0571-153">Check hello properties of hello user object toobe sure that they look as you expect and no data is missing.</span></span>

### <a name="check-a-users-account-status"></a><span data-ttu-id="d0571-154">Vérifier l’état du compte d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="d0571-154">Check a user’s account status</span></span>

<span data-ttu-id="d0571-155">toocheck un utilisateur état du compte, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="d0571-155">toocheck a user’s account status, follow hello steps below:</span></span>

1.  <span data-ttu-id="d0571-156">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="d0571-156">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d0571-157">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="d0571-157">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d0571-158">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="d0571-158">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d0571-159">Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.</span><span class="sxs-lookup"><span data-stu-id="d0571-159">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="d0571-160">Cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="d0571-160">click **All users**.</span></span>

6.  <span data-ttu-id="d0571-161">**Recherche** pour l’utilisateur hello vous intéressez et **cliquez sur la ligne hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="d0571-161">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="d0571-162">Cliquez sur **Profil**.</span><span class="sxs-lookup"><span data-stu-id="d0571-162">click **Profile**.</span></span>

8.  <span data-ttu-id="d0571-163">Sous **paramètres** vous assurer que **bloc connectez-vous** est défini trop**non**.</span><span class="sxs-lookup"><span data-stu-id="d0571-163">Under **Settings** ensure that **Block sign in** is set too**No**.</span></span>

### <a name="reset-a-users-password"></a><span data-ttu-id="d0571-164">Réinitialiser le mot de passe d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="d0571-164">Reset a user’s password</span></span>

<span data-ttu-id="d0571-165">tooreset un mot de passe, suivez les étapes hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="d0571-165">tooreset a user’s password, follow hello steps below:</span></span>

1.  <span data-ttu-id="d0571-166">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="d0571-166">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d0571-167">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="d0571-167">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d0571-168">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="d0571-168">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d0571-169">Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.</span><span class="sxs-lookup"><span data-stu-id="d0571-169">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="d0571-170">Cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="d0571-170">click **All users**.</span></span>

6.  <span data-ttu-id="d0571-171">**Recherche** pour l’utilisateur hello vous intéressez et **cliquez sur la ligne hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="d0571-171">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="d0571-172">Cliquez sur hello **réinitialisation de mot de passe** bouton en haut de hello du panneau d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="d0571-172">click hello **Reset password** button at hello top of hello user blade.</span></span>

8.  <span data-ttu-id="d0571-173">Cliquez sur hello **réinitialisation de mot de passe** bouton sur hello **réinitialisation de mot de passe** panneau s’affiche.</span><span class="sxs-lookup"><span data-stu-id="d0571-173">click hello **Reset password** button on hello **Reset password** blade that appears.</span></span>

9.  <span data-ttu-id="d0571-174">Hello de copie **mot de passe temporaire** ou **Entrez un nouveau mot de passe** pour l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="d0571-174">Copy hello **temporary password** or **enter a new password** for hello user.</span></span>

10. <span data-ttu-id="d0571-175">Communiquer ce nouvel utilisateur toohello de mot de passe, ils requis toochange ce mot de passe lors de sa prochaine connexion tooAzure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d0571-175">Communicate this new password toohello user, they be required toochange this password during their next sign in tooAzure Active Directory.</span></span>

### <a name="enable-self-service-password-reset"></a><span data-ttu-id="d0571-176">Activer la réinitialisation du mot de passe libre-service</span><span class="sxs-lookup"><span data-stu-id="d0571-176">Enable self-service password reset</span></span>

<span data-ttu-id="d0571-177">tooenable le mot de passe libre-service de réinitialisation, suivez les étapes de déploiement hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="d0571-177">tooenable self-service password reset, follow hello deployment steps below:</span></span>

-   [<span data-ttu-id="d0571-178">Activer les utilisateurs tooreset leurs mots de passe Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d0571-178">Enable users tooreset their Azure Active Directory passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [<span data-ttu-id="d0571-179">Activer les utilisateurs tooreset ou de modifier leurs mots de passe Active Directory local</span><span class="sxs-lookup"><span data-stu-id="d0571-179">Enable users tooreset or change their Active Directory on-premises passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a><span data-ttu-id="d0571-180">Vérifier l’état Multi-Factor Authentication d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="d0571-180">Check a user’s multi-factor authentication status</span></span>

<span data-ttu-id="d0571-181">toocheck un utilisateur multi-Factor de l’état d’authentification, suivez les étapes hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="d0571-181">toocheck a user’s multi-factor authentication status, follow hello steps below:</span></span>

1.  <span data-ttu-id="d0571-182">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="d0571-182">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d0571-183">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="d0571-183">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d0571-184">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="d0571-184">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d0571-185">Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.</span><span class="sxs-lookup"><span data-stu-id="d0571-185">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="d0571-186">Cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="d0571-186">click **All users**.</span></span>

6.  <span data-ttu-id="d0571-187">Cliquez sur hello **multi-Factor Authentication** bouton en haut de hello du panneau des hello.</span><span class="sxs-lookup"><span data-stu-id="d0571-187">click hello **Multi-Factor Authentication** button at hello top of hello blade.</span></span>

7.  <span data-ttu-id="d0571-188">Une fois hello **portail d’Administration de l’authentification multifacteur** charges, assurez-vous que vous êtes sur hello **utilisateurs** onglet.</span><span class="sxs-lookup"><span data-stu-id="d0571-188">Once hello **Multi-Factor Authentication Administration Portal** loads, ensure you are on hello **Users** tab.</span></span>

8.  <span data-ttu-id="d0571-189">Rechercher les utilisateur hello dans liste hello des utilisateurs par la recherche, le filtrage ou le tri.</span><span class="sxs-lookup"><span data-stu-id="d0571-189">Find hello user in hello list of users by searching, filtering, or sorting.</span></span>

9.  <span data-ttu-id="d0571-190">Utilisateur hello SELECT à partir de la liste de hello des utilisateurs et **activer**, **désactiver**, ou **appliquer** authentification multifacteur selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="d0571-190">Select hello user from hello list of users and **Enable**, **Disable**, or **Enforce** multi-factor authentication as desired.</span></span>

   >[!NOTE]
   ><span data-ttu-id="d0571-191">Si un utilisateur est dans un **appliqué** d’état, vous pouvez les définir trop**désactivé** temporairement toolet replacer dans son compte.</span><span class="sxs-lookup"><span data-stu-id="d0571-191">If a user is in an **Enforced** state, you may set them too**Disabled** temporarily toolet them back into their account.</span></span> <span data-ttu-id="d0571-192">Une fois qu’ils sont dans, vous pouvez ensuite modifier leur état trop**activé** toorequire à nouveau les toore-s’inscrire leurs informations de contact lors de sa prochaine connexion.</span><span class="sxs-lookup"><span data-stu-id="d0571-192">Once they are back in, you can then change their state too**Enabled** again toorequire them toore-register their contact information during their next sign in.</span></span> <span data-ttu-id="d0571-193">Ou bien, vous pouvez suivre les étapes de hello Bonjour [vérifier les informations de contact de l’authentification d’un utilisateur](#check-a-users-authentication-contact-info) tooverify ou définir ces données pour eux.</span><span class="sxs-lookup"><span data-stu-id="d0571-193">Alternatively, you can follow hello steps in hello [Check a user’s authentication contact info](#check-a-users-authentication-contact-info) tooverify or set this data for them.</span></span>
   >
   >

### <a name="check-a-users-authentication-contact-info"></a><span data-ttu-id="d0571-194">Vérifier les informations de contact de l’authentification d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="d0571-194">Check a user’s authentication contact info</span></span>

<span data-ttu-id="d0571-195">toocheck utilisée pour l’authentification multifacteur, l’accès conditionnel, Protection d’identité et réinitialisation du mot de passe, des informations de contact de l’authentification de l’utilisateur suit hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="d0571-195">toocheck a user’s authentication contact info used for Multi-factor authentication, Conditional Access, Identity Protection, and Password Reset, follow hello steps below:</span></span>

1.  <span data-ttu-id="d0571-196">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="d0571-196">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d0571-197">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="d0571-197">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d0571-198">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="d0571-198">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d0571-199">Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.</span><span class="sxs-lookup"><span data-stu-id="d0571-199">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="d0571-200">Cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="d0571-200">click **All users**.</span></span>

6.  <span data-ttu-id="d0571-201">**Recherche** pour l’utilisateur hello vous intéressez et **cliquez sur la ligne hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="d0571-201">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="d0571-202">Cliquez sur **Profil**.</span><span class="sxs-lookup"><span data-stu-id="d0571-202">click **Profile**.</span></span>

8.  <span data-ttu-id="d0571-203">Faites défiler la liste trop**les informations de contact d’authentification**.</span><span class="sxs-lookup"><span data-stu-id="d0571-203">Scroll down too**Authentication contact info**.</span></span>

9.  <span data-ttu-id="d0571-204">**Révision** les données de salutation inscrit pour l’utilisateur de hello et de mise à jour en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="d0571-204">**Review** hello data registered for hello user and update as needed.</span></span>

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="d0571-205">Vérifier les appartenances d’un utilisateur à des groupes</span><span class="sxs-lookup"><span data-stu-id="d0571-205">Check a user’s group memberships</span></span>

<span data-ttu-id="d0571-206">de toocheck un utilisateur appartenance aux groupes, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="d0571-206">toocheck a user’s group memberships, follow hello steps below:</span></span>

1.  <span data-ttu-id="d0571-207">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="d0571-207">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d0571-208">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="d0571-208">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d0571-209">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="d0571-209">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d0571-210">Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.</span><span class="sxs-lookup"><span data-stu-id="d0571-210">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="d0571-211">Cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="d0571-211">click **All users**.</span></span>

6.  <span data-ttu-id="d0571-212">**Recherche** pour l’utilisateur hello vous intéressez et **cliquez sur la ligne hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="d0571-212">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="d0571-213">Cliquez sur **groupes** toosee qui regroupe les utilisateur hello est membre.</span><span class="sxs-lookup"><span data-stu-id="d0571-213">click **Groups** toosee which groups hello user is a member of.</span></span>

### <a name="check-a-users-assigned-licenses"></a><span data-ttu-id="d0571-214">Vérifier les licences affectées à un utilisateur</span><span class="sxs-lookup"><span data-stu-id="d0571-214">Check a user’s assigned licenses</span></span>

<span data-ttu-id="d0571-215">toocheck un utilisateur affecté des licences, suivez les étapes hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="d0571-215">toocheck a user’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="d0571-216">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="d0571-216">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d0571-217">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="d0571-217">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d0571-218">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="d0571-218">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d0571-219">Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.</span><span class="sxs-lookup"><span data-stu-id="d0571-219">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="d0571-220">Cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="d0571-220">click **All users**.</span></span>

6.  <span data-ttu-id="d0571-221">**Recherche** pour l’utilisateur hello vous intéressez et **cliquez sur la ligne hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="d0571-221">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="d0571-222">Cliquez sur **licences** toosee les licences hello d’utilisateur est affectée actuellement.</span><span class="sxs-lookup"><span data-stu-id="d0571-222">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

### <a name="assign-a-user-a-license"></a><span data-ttu-id="d0571-223">Affecter une licence à un utilisateur</span><span class="sxs-lookup"><span data-stu-id="d0571-223">Assign a user a license</span></span> 

<span data-ttu-id="d0571-224">tooassign un utilisateur tooa de licences, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="d0571-224">tooassign a license tooa user, follow hello steps below:</span></span>

1.  <span data-ttu-id="d0571-225">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="d0571-225">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d0571-226">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="d0571-226">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d0571-227">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="d0571-227">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d0571-228">Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.</span><span class="sxs-lookup"><span data-stu-id="d0571-228">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="d0571-229">Cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="d0571-229">click **All users**.</span></span>

6.  <span data-ttu-id="d0571-230">**Recherche** pour l’utilisateur hello vous intéressez et **cliquez sur la ligne hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="d0571-230">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="d0571-231">Cliquez sur **licences** toosee les licences hello d’utilisateur est affectée actuellement.</span><span class="sxs-lookup"><span data-stu-id="d0571-231">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

8.  <span data-ttu-id="d0571-232">Cliquez sur hello **affecter** bouton.</span><span class="sxs-lookup"><span data-stu-id="d0571-232">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="d0571-233">Sélectionnez **un ou plusieurs produits** à partir de la liste de hello des produits disponibles.</span><span class="sxs-lookup"><span data-stu-id="d0571-233">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="d0571-234">**Facultatif** cliquez sur hello **options d’attribution** élément toogranularly affecter des produits.</span><span class="sxs-lookup"><span data-stu-id="d0571-234">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="d0571-235">Cliquez sur **OK** lorsque l’opération est terminée.</span><span class="sxs-lookup"><span data-stu-id="d0571-235">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="d0571-236">Cliquez sur hello **affecter** bouton tooassign ces utilisateur toothis de licences.</span><span class="sxs-lookup"><span data-stu-id="d0571-236">Click hello **Assign** button tooassign these licenses toothis user.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a><span data-ttu-id="d0571-237">Si ces étapes de dépannage ne résolvent pas le problème de hello</span><span class="sxs-lookup"><span data-stu-id="d0571-237">If these troubleshooting steps do not resolve hello issue</span></span>

<span data-ttu-id="d0571-238">Ouvrez un ticket de support avec hello informations suivantes si elle est disponible :</span><span class="sxs-lookup"><span data-stu-id="d0571-238">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="d0571-239">ID d’erreur de corrélation</span><span class="sxs-lookup"><span data-stu-id="d0571-239">Correlation error ID</span></span>

-   <span data-ttu-id="d0571-240">Nom d’utilisateur principal (adresse de messagerie de l’utilisateur)</span><span class="sxs-lookup"><span data-stu-id="d0571-240">UPN (user email address)</span></span>

-   <span data-ttu-id="d0571-241">ID client</span><span class="sxs-lookup"><span data-stu-id="d0571-241">Tenant ID</span></span>

-   <span data-ttu-id="d0571-242">Type de navigateur</span><span class="sxs-lookup"><span data-stu-id="d0571-242">Browser type</span></span>

-   <span data-ttu-id="d0571-243">Fuseau horaire et heure/période à laquelle l’erreur se produit</span><span class="sxs-lookup"><span data-stu-id="d0571-243">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="d0571-244">Traces Fiddler</span><span class="sxs-lookup"><span data-stu-id="d0571-244">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0571-245">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d0571-245">Next steps</span></span>
[<span data-ttu-id="d0571-246">Fournissent des applications de tooyour de l’authentification unique avec le Proxy d’Application</span><span class="sxs-lookup"><span data-stu-id="d0571-246">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
