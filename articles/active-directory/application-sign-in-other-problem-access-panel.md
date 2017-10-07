---
title: "aaaProblems de signature dans l’application tooan à partir du volet d’accès hello | Documents Microsoft"
description: "Comment les problèmes de tootroubleshoot l’accès à une application à partir de hello panneau d’accès Microsoft Azure AD MyApps.Microsoft.com"
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
ms.reviewer: japere
ms.openlocfilehash: 346c4da06416bb9b330bdd5b1201253af19ba58b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-application-from-hello-access-panel"></a><span data-ttu-id="ebf74-103">Problèmes de connexion dans l’application tooan à partir du volet d’accès hello</span><span class="sxs-lookup"><span data-stu-id="ebf74-103">Problems signing in tooan application from hello access panel</span></span>

<span data-ttu-id="ebf74-104">Hello volet d’accès est un portail web qui permet à un utilisateur avec un travail ou compte scolaire dans Azure Active Directory (Azure AD) tooview et démarrer les applications cloud qui hello administrateur Azure AD lui a accordé l’accès à.</span><span class="sxs-lookup"><span data-stu-id="ebf74-104">hello Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) tooview and start cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> 

<span data-ttu-id="ebf74-105">Ces applications sont configurées pour le compte d’utilisateur hello dans le portail Azure AD de hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-105">These applications are configured on behalf of hello user in hello Azure AD portal.</span></span> <span data-ttu-id="ebf74-106">application Hello doit être configurée correctement et toohello attribué ou un utilisateur de hello de groupe est un membre de l’application de hello toosee Bonjour panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="ebf74-106">hello application must be configured properly and assigned toohello user or a group hello user is a member of toosee hello application in hello Access Panel.</span></span>

<span data-ttu-id="ebf74-107">type Hello d’applications peut s’agir d’un utilisateur se situent dans hello suivant des catégories :</span><span class="sxs-lookup"><span data-stu-id="ebf74-107">hello type of apps a user may be seeing fall in hello following categories:</span></span>

-   <span data-ttu-id="ebf74-108">Applications Office 365</span><span class="sxs-lookup"><span data-stu-id="ebf74-108">Office 365 Applications</span></span>

-   <span data-ttu-id="ebf74-109">Applications Microsoft et tierces configurées avec l’authentification unique (SSO) basée sur la fédération</span><span class="sxs-lookup"><span data-stu-id="ebf74-109">Microsoft and third-party applications configured with federation-based SSO</span></span>

-   <span data-ttu-id="ebf74-110">Applications à authentification unique (SSO) par mot de passe</span><span class="sxs-lookup"><span data-stu-id="ebf74-110">Password-based SSO applications</span></span>

-   <span data-ttu-id="ebf74-111">Applications avec solutions d’authentification unique (SSO) existantes</span><span class="sxs-lookup"><span data-stu-id="ebf74-111">Applications with existing SSO solutions</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="ebf74-112">Général émet toocheck tout d’abord</span><span class="sxs-lookup"><span data-stu-id="ebf74-112">General issues toocheck first</span></span>

-   <span data-ttu-id="ebf74-113">Assurez-vous que votre en utilisant un **navigateur** qui répond aux hello configuration minimale requise pour hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="ebf74-113">Make sure your using a **browser** that meets hello minimum requirements for hello Access Panel.</span></span>

-   <span data-ttu-id="ebf74-114">Assurez-vous que navigateur de l’utilisateur hello a ajouté des URL hello de hello application tooits **sites de confiance**.</span><span class="sxs-lookup"><span data-stu-id="ebf74-114">Make sure hello user’s browser has added hello URL of hello application tooits **trusted sites**.</span></span>

-   <span data-ttu-id="ebf74-115">Assurez-vous que l’application de hello toocheck est **configuré** correctement.</span><span class="sxs-lookup"><span data-stu-id="ebf74-115">Make sure toocheck hello application is **configured** correctly.</span></span>

-   <span data-ttu-id="ebf74-116">Assurez-vous que le compte d’utilisateur hello est **activé** pour les connexions.</span><span class="sxs-lookup"><span data-stu-id="ebf74-116">Make sure hello user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="ebf74-117">Assurez-vous que le compte d’utilisateur hello est **ne pas verrouillé.**</span><span class="sxs-lookup"><span data-stu-id="ebf74-117">Make sure hello user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="ebf74-118">Vérifiez que hello l’utilisateur **mot de passe n’a pas expiré ou oublié.**</span><span class="sxs-lookup"><span data-stu-id="ebf74-118">Make sure hello user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="ebf74-119">Vérifiez que **Multi-Factor Authentication** ne bloque pas l’accès utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ebf74-119">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="ebf74-120">Vérifiez qu’une **stratégie d’accès conditionnel** ou **stratégie de protection d’identité** ne bloque pas l’accès utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ebf74-120">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="ebf74-121">S’assurer que l’utilisateur **les informations de contact d’authentification** est toodate tooallow multi-Factor Authentication ou accès conditionnel stratégies toobe appliquée.</span><span class="sxs-lookup"><span data-stu-id="ebf74-121">Make sure that a user’s **authentication contact info** is up toodate tooallow Multi-Factor Authentication or Conditional Access policies toobe enforced.</span></span>

-   <span data-ttu-id="ebf74-122">Assurez-vous que tooalso try effacer les cookies de votre navigateur et réessayer toosign dans.</span><span class="sxs-lookup"><span data-stu-id="ebf74-122">Make sure tooalso try clearing your browser’s cookies and trying toosign in again.</span></span>

## <a name="meeting-browser-requirements-for-hello-access-panel"></a><span data-ttu-id="ebf74-123">Configuration requise du navigateur de réunion hello panneau d’accès</span><span class="sxs-lookup"><span data-stu-id="ebf74-123">Meeting browser requirements for hello Access Panel</span></span>

<span data-ttu-id="ebf74-124">Hello volet d’accès nécessite un navigateur qui prend en charge JavaScript et a activé les CSS.</span><span class="sxs-lookup"><span data-stu-id="ebf74-124">hello Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="ebf74-125">toouse mot de passe-session unique (SSO) Bonjour hello extension du volet d’accès, volet d’accès doit être installé dans le navigateur de l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-125">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="ebf74-126">Cette extension est téléchargée automatiquement lorsqu’un utilisateur sélectionne une application configurée pour l’authentification unique (SSO) avec mot de passe.</span><span class="sxs-lookup"><span data-stu-id="ebf74-126">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="ebf74-127">Pour l’authentification unique basée sur le mot de passe, hello navigateurs des utilisateurs finaux peuvent être :</span><span class="sxs-lookup"><span data-stu-id="ebf74-127">For password-based SSO, hello end user’s browsers can be:</span></span>

-   <span data-ttu-id="ebf74-128">Internet Explorer 8, 9, 10, 11 -- sur Windows 7 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="ebf74-128">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="ebf74-129">Edge sur Windows 10 Édition anniversaire ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="ebf74-129">Edge on Windows 10 Anniversary Edition or later</span></span>

-   <span data-ttu-id="ebf74-130">Chrome -- sur Windows 7 ou ultérieur, et sur Mac OS X ou ultérieur</span><span class="sxs-lookup"><span data-stu-id="ebf74-130">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="ebf74-131">Firefox 26.0 ou ultérieur -- sur Windows XP SP2 ou ultérieur, et sur Mac OS X 10.6 ou ultérieur</span><span class="sxs-lookup"><span data-stu-id="ebf74-131">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="ebf74-132">Comment tooinstall hello extension du navigateur de panneau d’accès</span><span class="sxs-lookup"><span data-stu-id="ebf74-132">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="ebf74-133">tooinstall hello extension du navigateur de panneau d’accès, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ebf74-133">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="ebf74-134">Ouvrez hello [volet d’accès](https://myapps.microsoft.com) dans un des navigateurs de hello pris en charge et vous connecter en tant qu’un **utilisateur** dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ebf74-134">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="ebf74-135">Cliquez sur un **application d’authentification unique du mot de passe** Bonjour panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="ebf74-135">Click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="ebf74-136">Dans hello invite vous demandant tooinstall hello logiciel, sélectionnez **installer maintenant**.</span><span class="sxs-lookup"><span data-stu-id="ebf74-136">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="ebf74-137">En fonction de votre navigateur vous être lien de téléchargement toohello dirigée.</span><span class="sxs-lookup"><span data-stu-id="ebf74-137">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="ebf74-138">**Ajouter** navigateur de tooyour extension hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-138">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="ebf74-139">Si votre navigateur vous invite à sélectionner tooeither **activer** ou **autoriser** hello extension.</span><span class="sxs-lookup"><span data-stu-id="ebf74-139">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="ebf74-140">Une fois l’extension installée, **redémarrez** votre session de navigateur.</span><span class="sxs-lookup"><span data-stu-id="ebf74-140">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="ebf74-141">Connectez-vous en hello volet d’accès et de voir si vous pouvez **lancer** vos applications SSO de mot de passe</span><span class="sxs-lookup"><span data-stu-id="ebf74-141">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="ebf74-142">Vous pouvez également télécharger l’extension de hello pour Chrome et le bord à partir de liens directs de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ebf74-142">You may also download hello extension for Chrome and Edge from hello direct links below:</span></span>

-   [<span data-ttu-id="ebf74-143">Extension du volet d’accès pour Chrome</span><span class="sxs-lookup"><span data-stu-id="ebf74-143">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="ebf74-144">Extension du volet d’accès pour Edge</span><span class="sxs-lookup"><span data-stu-id="ebf74-144">Edge Access Panel Extension</span></span>](https://www.microsoft.com/store/apps/9pc9sckkzk84)

## <a name="how-tooconfigure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="ebf74-145">Comment tooconfigure fédéré l’authentification unique pour une application de la galerie Azure AD</span><span class="sxs-lookup"><span data-stu-id="ebf74-145">How tooconfigure federated single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="ebf74-146">Toutes les applications dans la galerie d’Azure AD hello activée avec la fonctionnalité Enterprise Single Sign-On a un didacticiel pas à pas disponible.</span><span class="sxs-lookup"><span data-stu-id="ebf74-146">All application in hello Azure AD gallery enabled with Enterprise Single Sign-On capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="ebf74-147">Vous pouvez accéder à hello [liste des didacticiels sur la façon de toointegrate les applications SaaS avec Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) pour obtenir une aide pas à pas détaillé.</span><span class="sxs-lookup"><span data-stu-id="ebf74-147">You can access hello [List of tutorials on how toointegrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

<span data-ttu-id="ebf74-148">tooconfigure une application à partir de la galerie d’Azure AD hello vous devez :</span><span class="sxs-lookup"><span data-stu-id="ebf74-148">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="ebf74-149">Ajouter une application à partir de la galerie d’Azure AD hello</span><span class="sxs-lookup"><span data-stu-id="ebf74-149">Add an application from hello Azure AD gallery</span></span>](#add-an-application)

-   [<span data-ttu-id="ebf74-150">Configurer les valeurs de métadonnées de l’application hello dans Azure AD (URL de réponse d’URL, identificateur, authentification)</span><span class="sxs-lookup"><span data-stu-id="ebf74-150">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="ebf74-151">Identificateur de l’utilisateur de sélectionner et ajouter l’application utilisateur attributs toobe envoyé toohello</span><span class="sxs-lookup"><span data-stu-id="ebf74-151">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="ebf74-152">Récupérer le certificat et les métadonnées Azure AD</span><span class="sxs-lookup"><span data-stu-id="ebf74-152">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="ebf74-153">Configurer les valeurs de métadonnées Azure AD dans l’application hello (authentification URL, l’émetteur, URL de déconnexion et un certificat)</span><span class="sxs-lookup"><span data-stu-id="ebf74-153">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="ebf74-154">Affecter des utilisateurs toohello application</span><span class="sxs-lookup"><span data-stu-id="ebf74-154">Assign users toohello application</span></span>](#assign-users-to-the-application)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="ebf74-155">Ajouter une application à partir de la galerie d’Azure AD hello</span><span class="sxs-lookup"><span data-stu-id="ebf74-155">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="ebf74-156">tooadd une application à partir de hello Galerie d’Azure AD, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ebf74-156">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="ebf74-157">Ouvrez hello [Azure Portal](https://portal.azure.com) et connectez-vous en tant qu’un **administrateur Global** ou **Co-admin**</span><span class="sxs-lookup"><span data-stu-id="ebf74-157">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="ebf74-158">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-158">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ebf74-159">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="ebf74-159">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ebf74-160">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ebf74-160">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ebf74-161">Cliquez sur hello **ajouter** bouton au coin supérieur droit de hello sur hello **des Applications d’entreprise** panneau</span><span class="sxs-lookup"><span data-stu-id="ebf74-161">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="ebf74-162">Bonjour **Entrez un nom** zone de texte à partir de hello **ajouter à partir de la galerie de hello** section, entrez un nom hello de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-162">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="ebf74-163">Sélectionnez hello application tooconfigure pour l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="ebf74-163">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="ebf74-164">Avant d’ajouter l’application hello, vous pouvez modifier son nom à partir de hello **nom** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="ebf74-164">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="ebf74-165">Cliquez sur **ajouter** bouton, l’application de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="ebf74-165">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="ebf74-166">Après une courte période, vous être Panneau de configuration de l’application en mesure de toosee hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-166">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-single-sign-on-for-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="ebf74-167">Configurer l’authentification unique pour une application à partir de la galerie d’Azure AD hello</span><span class="sxs-lookup"><span data-stu-id="ebf74-167">Configure single sign-on for an application from hello Azure AD gallery</span></span>

<span data-ttu-id="ebf74-168">tooconfigure l’authentification unique pour une application, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ebf74-168">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="ebf74-169"><span id="_Hlk477187909" class="anchor"><span id="_Hlk477001983" class="anchor"></span></span>Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**</span><span class="sxs-lookup"><span data-stu-id="ebf74-169"><span id="_Hlk477187909" class="anchor"><span id="_Hlk477001983" class="anchor"></span></span>Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="ebf74-170">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-170">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ebf74-171">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="ebf74-171">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ebf74-172">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ebf74-172">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ebf74-173">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="ebf74-173">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="ebf74-174">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="ebf74-174">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="ebf74-175">Sélectionnez l’application hello tooconfigure l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="ebf74-175">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="ebf74-176">Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-176">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="ebf74-177">Sélectionnez **SAML-authentification** de hello **Mode** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="ebf74-177">Select **SAML-based Sign-on** from hello **Mode** dropdown.</span></span>

9.  <span data-ttu-id="ebf74-178">Entrez les valeurs hello requis dans **URL et domaine.**</span><span class="sxs-lookup"><span data-stu-id="ebf74-178">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="ebf74-179">Vous devez obtenir ces valeurs à partir du fournisseur de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-179">You should get these values from hello application vendor.</span></span>

   1. <span data-ttu-id="ebf74-180">application de hello tooconfigure en tant que l’authentification unique initiée par SP, hello signe sur l’URL, il est obligatoire.</span><span class="sxs-lookup"><span data-stu-id="ebf74-180">tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span> <span data-ttu-id="ebf74-181">Pour certaines applications, hello identificateur est également une valeur requise.</span><span class="sxs-lookup"><span data-stu-id="ebf74-181">For some applications, hello Identifier is also a required value.</span></span>

   2. <span data-ttu-id="ebf74-182">application hello tooconfigure initiées IdP, hello URL de réponse qu’il est obligatoire.</span><span class="sxs-lookup"><span data-stu-id="ebf74-182">tooconfigure hello application as IdP-initiated SSO, hello Reply URL it’s a required value.</span></span> <span data-ttu-id="ebf74-183">Pour certaines applications, hello identificateur est également une valeur requise.</span><span class="sxs-lookup"><span data-stu-id="ebf74-183">For some applications, hello Identifier is also a required value.</span></span>

10. <span data-ttu-id="ebf74-184">**Facultatif :** cliquez sur **afficher les paramètres d’URL avancés** si vous souhaitez que les valeurs toosee hello non requis.</span><span class="sxs-lookup"><span data-stu-id="ebf74-184">**Optional:** click **Show advanced URL settings** if you want toosee hello non-required values.</span></span>

11. <span data-ttu-id="ebf74-185">Bonjour **attributs utilisateur**, sélectionnez hello un identificateur unique pour vos utilisateurs Bonjour **identificateur de l’utilisateur** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="ebf74-185">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="ebf74-186">**Facultatif :** cliquez sur **afficher et modifier tous les autres attributs utilisateur** tooedit hello attributs application de toohello toobe envoyé dans un jeton SAML de hello lorsque l’utilisateur se connecter.</span><span class="sxs-lookup"><span data-stu-id="ebf74-186">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="ebf74-187">tooadd un attribut :</span><span class="sxs-lookup"><span data-stu-id="ebf74-187">tooadd an attribute:</span></span>

   1. <span data-ttu-id="ebf74-188">Cliquez sur **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="ebf74-188">click **Add attribute**.</span></span> <span data-ttu-id="ebf74-189">Entrez hello **nom** et Bonjour sélectionnez Bonjour **valeur** à partir de la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-189">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="ebf74-190">Cliquez sur **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="ebf74-190">Click **Save.**</span></span> <span data-ttu-id="ebf74-191">Vous consultez hello nouvel attribut dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-191">You see hello new attribute in hello table.</span></span>

13. <span data-ttu-id="ebf74-192">Cliquez sur **configurer &lt;nom de l’application&gt;**  documentation tooaccess sur la tooconfigure l’authentification unique dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-192">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="ebf74-193">En outre, vous a hello les URL des métadonnées et le certificat requis toosetup SSO avec l’application hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-193">Also, you has hello metadata URLs and certificate required toosetup SSO with hello application.</span></span>

14. <span data-ttu-id="ebf74-194">Cliquez sur **enregistrer** configuration de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="ebf74-194">Click **Save** toosave hello configuration.</span></span>

15. <span data-ttu-id="ebf74-195">Affecter des utilisateurs toohello application.</span><span class="sxs-lookup"><span data-stu-id="ebf74-195">Assign users toohello application.</span></span>

### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="ebf74-196">Identificateur de l’utilisateur de sélectionner et ajouter l’application utilisateur attributs toobe envoyé toohello</span><span class="sxs-lookup"><span data-stu-id="ebf74-196">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="ebf74-197">tooselect hello identificateur d’utilisateur ou ajouter des attributs d’utilisateur, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ebf74-197">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="ebf74-198">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**</span><span class="sxs-lookup"><span data-stu-id="ebf74-198">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="ebf74-199">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-199">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ebf74-200">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="ebf74-200">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ebf74-201">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ebf74-201">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ebf74-202">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="ebf74-202">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="ebf74-203">Si vous ne voyez pas l’application hello souhaité tooshow ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="ebf74-203">If you do not see hello application you want tooshow up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="ebf74-204">Sélectionnez l’application hello que vous avez configuré l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="ebf74-204">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="ebf74-205">Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-205">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="ebf74-206">Sous hello **attributs utilisateur** section, sélectionnez hello un identificateur unique pour vos utilisateurs Bonjour **identificateur de l’utilisateur** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="ebf74-206">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="ebf74-207">Hello option sélectionnée doit valeur attendue toomatch hello utilisateur hello de tooauthenticate l’application hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-207">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

    >[!NOTE]
    ><span data-ttu-id="ebf74-208">Format de hello sélectionnez Azure AD pour l’attribut de NameID hello (identifiant d’utilisateur) en fonction de la valeur hello sélectionnée ou hello format demandé par l’application hello Bonjour SAML AuthRequest.</span><span class="sxs-lookup"><span data-stu-id="ebf74-208">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="ebf74-209">Pour plus d’informations, consultez l’article de hello [protocole SAML de l’authentification unique](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) sous hello section NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="ebf74-209">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
    >
    >

9.  <span data-ttu-id="ebf74-210">attributs d’utilisateur tooadd, cliquez sur **afficher et modifier tous les autres attributs de l’utilisateur** tooedit hello attributs application de toohello toobe envoyé dans un jeton SAML de hello lorsque l’utilisateur se connecter.</span><span class="sxs-lookup"><span data-stu-id="ebf74-210">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="ebf74-211">tooadd un attribut :</span><span class="sxs-lookup"><span data-stu-id="ebf74-211">tooadd an attribute:</span></span>

   1. <span data-ttu-id="ebf74-212">Cliquez sur **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="ebf74-212">click **Add attribute**.</span></span> <span data-ttu-id="ebf74-213">Entrez hello **nom** et Bonjour sélectionnez Bonjour **valeur** à partir de la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-213">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="ebf74-214">Cliquez sur **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="ebf74-214">Click **Save.**</span></span> <span data-ttu-id="ebf74-215">Vous consultez hello nouvel attribut dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-215">You see hello new attribute in hello table.</span></span>

### <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="ebf74-216">Télécharger des métadonnées Azure AD hello ou certificat</span><span class="sxs-lookup"><span data-stu-id="ebf74-216">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="ebf74-217">métadonnées de l’application hello toodownload ou un certificat d’Azure AD, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ebf74-217">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="ebf74-218">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**</span><span class="sxs-lookup"><span data-stu-id="ebf74-218">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="ebf74-219">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-219">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ebf74-220">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="ebf74-220">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ebf74-221">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ebf74-221">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ebf74-222">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="ebf74-222">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="ebf74-223">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="ebf74-223">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="ebf74-224">Sélectionnez l’application hello que vous avez configuré l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="ebf74-224">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="ebf74-225">Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-225">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="ebf74-226">Accédez trop**le certificat de signature SAML** section, puis cliquez sur **télécharger** valeur de la colonne.</span><span class="sxs-lookup"><span data-stu-id="ebf74-226">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="ebf74-227">En fonction de l’application hello nécessite la configuration de l’authentification unique, vous voyez deux toodownload d’option hello hello Metadata XML ou hello du certificat.</span><span class="sxs-lookup"><span data-stu-id="ebf74-227">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

    <span data-ttu-id="ebf74-228">Azure AD ne fournit pas une URL de métadonnées hello tooget.</span><span class="sxs-lookup"><span data-stu-id="ebf74-228">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="ebf74-229">Hello métadonnées peuvent uniquement être récupérées dans un fichier XML.</span><span class="sxs-lookup"><span data-stu-id="ebf74-229">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="how-tooconfigure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="ebf74-230">Comment tooconfigure fédéré l’authentification unique pour une application non-galerie</span><span class="sxs-lookup"><span data-stu-id="ebf74-230">How tooconfigure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="ebf74-231">tooconfigure une application non-galerie, vous devez toohave Azure AD premium et l’application hello prend en charge SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="ebf74-231">tooconfigure a non-gallery application, you need toohave Azure AD premium and hello application supports SAML 2.0.</span></span> <span data-ttu-id="ebf74-232">Pour plus d’informations sur les versions d’Azure AD, consultez [Tarification d’Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="ebf74-232">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

-   [<span data-ttu-id="ebf74-233">Configurer les valeurs de métadonnées de l’application hello dans Azure AD (URL de réponse d’URL, identificateur, authentification)</span><span class="sxs-lookup"><span data-stu-id="ebf74-233">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configuring-single-sign-on)

-   [<span data-ttu-id="ebf74-234">Identificateur de l’utilisateur de sélectionner et ajouter l’application utilisateur attributs toobe envoyé toohello</span><span class="sxs-lookup"><span data-stu-id="ebf74-234">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="ebf74-235">Récupérer le certificat et les métadonnées Azure AD</span><span class="sxs-lookup"><span data-stu-id="ebf74-235">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="ebf74-236">Configurer les valeurs de métadonnées Azure AD dans l’application hello (authentification URL, l’émetteur, URL de déconnexion et un certificat)</span><span class="sxs-lookup"><span data-stu-id="ebf74-236">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configuring-single-sign-on)

### <a name="configure-hello-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a><span data-ttu-id="ebf74-237">Configurer les valeurs de métadonnées de l’application hello dans Azure AD (URL de réponse d’URL, identificateur, authentification)</span><span class="sxs-lookup"><span data-stu-id="ebf74-237">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>

<span data-ttu-id="ebf74-238">tooconfigure l’authentification unique pour une application qui n’est pas dans la galerie d’Azure AD hello, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ebf74-238">tooconfigure single sign-on for an application that is not in hello Azure AD gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="ebf74-239">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**</span><span class="sxs-lookup"><span data-stu-id="ebf74-239">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="ebf74-240">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-240">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ebf74-241">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="ebf74-241">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ebf74-242">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ebf74-242">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ebf74-243">Cliquez sur hello **ajouter** bouton au coin supérieur droit de hello sur hello **des Applications d’entreprise** panneau</span><span class="sxs-lookup"><span data-stu-id="ebf74-243">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="ebf74-244">Cliquez sur **application Non-gallery** Bonjour **ajouter votre propre application** section</span><span class="sxs-lookup"><span data-stu-id="ebf74-244">click **Non-gallery application** in hello **Add your own app** section</span></span>

7.  <span data-ttu-id="ebf74-245">Entrez le nom hello de l’application hello Bonjour **nom** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="ebf74-245">Enter hello name of hello application in hello **Name** textbox.</span></span>

8.  <span data-ttu-id="ebf74-246">Cliquez sur **ajouter** bouton, l’application de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="ebf74-246">Click **Add** button, tooadd hello application.</span></span>

9.  <span data-ttu-id="ebf74-247">Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-247">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="ebf74-248">Sélectionnez **SAML-authentification** Bonjour **Mode** liste déroulante</span><span class="sxs-lookup"><span data-stu-id="ebf74-248">Select **SAML-based Sign-on** in hello **Mode** dropdown</span></span>

11. <span data-ttu-id="ebf74-249">Entrez les valeurs hello requis dans **URL et domaine.**</span><span class="sxs-lookup"><span data-stu-id="ebf74-249">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="ebf74-250">Vous devez obtenir ces valeurs à partir du fournisseur de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-250">You should get these values from hello application vendor.</span></span>

  1. <span data-ttu-id="ebf74-251">application de hello tooconfigure en tant que l’authentification unique initiée par les fournisseurs d’identité, entrez hello URL de réponse et hello identificateur.</span><span class="sxs-lookup"><span data-stu-id="ebf74-251">tooconfigure hello application as IdP-initiated SSO, enter hello Reply URL and hello Identifier.</span></span>

  2. <span data-ttu-id="ebf74-252">**Facultatif :** application hello tooconfigure authentifications uniques initiées, hello signe sur l’URL, il est obligatoire.</span><span class="sxs-lookup"><span data-stu-id="ebf74-252">**Optional:** tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="ebf74-253">Bonjour **attributs utilisateur**, sélectionnez hello un identificateur unique pour vos utilisateurs Bonjour **identificateur de l’utilisateur** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="ebf74-253">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="ebf74-254">**Facultatif :** cliquez sur **afficher et modifier tous les autres attributs utilisateur** tooedit hello attributs application de toohello toobe envoyé dans un jeton SAML de hello lorsque l’utilisateur se connecter.</span><span class="sxs-lookup"><span data-stu-id="ebf74-254">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="ebf74-255">tooadd un attribut :</span><span class="sxs-lookup"><span data-stu-id="ebf74-255">tooadd an attribute:</span></span>

   1. <span data-ttu-id="ebf74-256">Cliquez sur **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="ebf74-256">click **Add attribute**.</span></span> <span data-ttu-id="ebf74-257">Entrez hello **nom** et Bonjour sélectionnez Bonjour **valeur** à partir de la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-257">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="ebf74-258">Cliquez sur **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="ebf74-258">Click **Save.**</span></span> <span data-ttu-id="ebf74-259">Vous consultez hello nouvel attribut dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-259">You see hello new attribute in hello table.</span></span>

14. <span data-ttu-id="ebf74-260">Cliquez sur **configurer &lt;nom de l’application&gt;**  documentation tooaccess sur la tooconfigure l’authentification unique dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-260">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="ebf74-261">Possède également Azure AD URL et le certificat requis pour l’application hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-261">Also, you has Azure AD URLs and certificate required for hello application.</span></span>

### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="ebf74-262">Identificateur de l’utilisateur de sélectionner et ajouter l’application utilisateur attributs toobe envoyé toohello</span><span class="sxs-lookup"><span data-stu-id="ebf74-262">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="ebf74-263">tooselect hello identificateur d’utilisateur ou ajouter des attributs d’utilisateur, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ebf74-263">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="ebf74-264">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**</span><span class="sxs-lookup"><span data-stu-id="ebf74-264">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="ebf74-265">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-265">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ebf74-266">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="ebf74-266">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ebf74-267">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ebf74-267">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ebf74-268">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="ebf74-268">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="ebf74-269">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="ebf74-269">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="ebf74-270">Sélectionnez l’application hello que vous avez configuré l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="ebf74-270">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="ebf74-271">Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-271">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="ebf74-272">Sous hello **attributs utilisateur** section, sélectionnez hello un identificateur unique pour vos utilisateurs Bonjour **identificateur de l’utilisateur** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="ebf74-272">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="ebf74-273">Hello option sélectionnée doit valeur attendue toomatch hello utilisateur hello de tooauthenticate l’application hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-273">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

   >[!NOTE]
   ><span data-ttu-id="ebf74-274">Format de hello sélectionnez Azure AD pour l’attribut de NameID hello (identifiant d’utilisateur) en fonction de la valeur hello sélectionnée ou hello format demandé par l’application hello Bonjour SAML AuthRequest.</span><span class="sxs-lookup"><span data-stu-id="ebf74-274">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="ebf74-275">Pour plus d’informations, consultez l’article de hello [protocole SAML de l’authentification unique](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) sous hello section NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="ebf74-275">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="ebf74-276">attributs d’utilisateur tooadd, cliquez sur **afficher et modifier tous les autres attributs de l’utilisateur** tooedit hello attributs application de toohello toobe envoyé dans un jeton SAML de hello lorsque l’utilisateur se connecter.</span><span class="sxs-lookup"><span data-stu-id="ebf74-276">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="ebf74-277">tooadd un attribut :</span><span class="sxs-lookup"><span data-stu-id="ebf74-277">tooadd an attribute:</span></span>

   <span data-ttu-id="ebf74-278">1. Cliquez sur **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="ebf74-278">1.click **Add attribute**.</span></span> <span data-ttu-id="ebf74-279">Entrez hello **nom** et Bonjour sélectionnez Bonjour **valeur** à partir de la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-279">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   <span data-ttu-id="ebf74-280">2. Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="ebf74-280">2 Click **Save.**</span></span> <span data-ttu-id="ebf74-281">Vous consultez hello nouvel attribut dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-281">You see hello new attribute in hello table.</span></span>

### <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="ebf74-282">Télécharger des métadonnées Azure AD hello ou certificat</span><span class="sxs-lookup"><span data-stu-id="ebf74-282">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="ebf74-283">métadonnées de l’application hello toodownload ou un certificat d’Azure AD, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ebf74-283">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="ebf74-284">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**</span><span class="sxs-lookup"><span data-stu-id="ebf74-284">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="ebf74-285">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-285">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ebf74-286">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="ebf74-286">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ebf74-287">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ebf74-287">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ebf74-288">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="ebf74-288">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="ebf74-289">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="ebf74-289">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="ebf74-290">Sélectionnez l’application hello que vous avez configuré l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="ebf74-290">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="ebf74-291">Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-291">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="ebf74-292">Accédez trop**le certificat de signature SAML** section, puis cliquez sur **télécharger** valeur de la colonne.</span><span class="sxs-lookup"><span data-stu-id="ebf74-292">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="ebf74-293">En fonction de l’application hello nécessite la configuration de l’authentification unique, vous voyez deux toodownload d’option hello hello Metadata XML ou hello du certificat.</span><span class="sxs-lookup"><span data-stu-id="ebf74-293">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

    <span data-ttu-id="ebf74-294">Azure AD ne fournit pas une URL de métadonnées hello tooget.</span><span class="sxs-lookup"><span data-stu-id="ebf74-294">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="ebf74-295">Hello métadonnées peuvent uniquement être récupérées dans un fichier XML.</span><span class="sxs-lookup"><span data-stu-id="ebf74-295">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="ebf74-296">Comment tooconfigure le mot de passe sur l’authentification unique pour une application de la galerie Azure AD</span><span class="sxs-lookup"><span data-stu-id="ebf74-296">How tooconfigure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="ebf74-297">tooconfigure une application à partir de la galerie d’Azure AD hello vous devez :</span><span class="sxs-lookup"><span data-stu-id="ebf74-297">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="ebf74-298">Ajouter une application à partir de la galerie d’Azure AD hello</span><span class="sxs-lookup"><span data-stu-id="ebf74-298">Add an application from hello Azure AD gallery</span></span>](#add-an-application)

-   [<span data-ttu-id="ebf74-299">Configurer une application hello pour mot de passe l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="ebf74-299">Configure hello application for password single sign-on</span></span>](#configure-the-application)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="ebf74-300">Ajouter une application à partir de la galerie d’Azure AD hello</span><span class="sxs-lookup"><span data-stu-id="ebf74-300">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="ebf74-301">tooadd une application à partir de hello Galerie d’Azure AD, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ebf74-301">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="ebf74-302">Ouvrez hello [Azure Portal](https://portal.azure.com) et connectez-vous en tant qu’un **administrateur Global** ou **Co-admin**</span><span class="sxs-lookup"><span data-stu-id="ebf74-302">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="ebf74-303">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-303">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ebf74-304">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="ebf74-304">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ebf74-305">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ebf74-305">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ebf74-306">Cliquez sur hello **ajouter** bouton au coin supérieur droit de hello sur hello **des Applications d’entreprise** panneau</span><span class="sxs-lookup"><span data-stu-id="ebf74-306">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="ebf74-307">Bonjour **Entrez un nom** zone de texte à partir de hello **ajouter à partir de la galerie de hello** section, entrez un nom hello de l’application hello</span><span class="sxs-lookup"><span data-stu-id="ebf74-307">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application</span></span>

7.  <span data-ttu-id="ebf74-308">Sélectionnez hello application tooconfigure pour l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="ebf74-308">Select hello application you want tooconfigure for single sign-on</span></span>

8.  <span data-ttu-id="ebf74-309">Avant d’ajouter l’application hello, vous pouvez modifier son nom à partir de hello **nom** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="ebf74-309">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="ebf74-310">Cliquez sur **ajouter** bouton, l’application de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="ebf74-310">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="ebf74-311">Après une courte période, vous être Panneau de configuration de l’application en mesure de toosee hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-311">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="ebf74-312">Configurer une application hello pour mot de passe l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="ebf74-312">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="ebf74-313">tooconfigure l’authentification unique pour une application, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ebf74-313">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="ebf74-314">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**</span><span class="sxs-lookup"><span data-stu-id="ebf74-314">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="ebf74-315">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-315">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ebf74-316">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="ebf74-316">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ebf74-317">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ebf74-317">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ebf74-318">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="ebf74-318">click **All Applications** tooview a list of all your applications.</span></span>

 * <span data-ttu-id="ebf74-319">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="ebf74-319">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="ebf74-320">Sélectionnez application hello tooconfigure l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="ebf74-320">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="ebf74-321">Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-321">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="ebf74-322">Mode de sélection hello **mot de passe de session.**</span><span class="sxs-lookup"><span data-stu-id="ebf74-322">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="ebf74-323">Affecter des utilisateurs toohello application.</span><span class="sxs-lookup"><span data-stu-id="ebf74-323">Assign users toohello application.</span></span>

10. <span data-ttu-id="ebf74-324">En outre, vous pouvez également fournir des informations d’identification pour le compte d’utilisateur de hello en sélectionnant les lignes hello d’utilisateurs de hello en cliquant sur **informations d’identification de la mise à jour** et en entrant hello username et password pour le compte d’utilisateurs de hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-324">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="ebf74-325">Dans le cas contraire, les utilisateurs être invité à tooenter hello informations d’identification elles-mêmes lors du lancement.</span><span class="sxs-lookup"><span data-stu-id="ebf74-325">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="ebf74-326">Comment tooconfigure le mot de passe sur l’authentification unique pour une application non-galerie</span><span class="sxs-lookup"><span data-stu-id="ebf74-326">How tooconfigure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="ebf74-327">tooconfigure une application à partir de la galerie d’Azure AD hello vous devez :</span><span class="sxs-lookup"><span data-stu-id="ebf74-327">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="ebf74-328">Ajouter une application ne figurant pas dans la galerie</span><span class="sxs-lookup"><span data-stu-id="ebf74-328">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="ebf74-329">Configurer une application hello pour mot de passe l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="ebf74-329">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="ebf74-330">Ajouter une application ne figurant pas dans la galerie</span><span class="sxs-lookup"><span data-stu-id="ebf74-330">Add a non-gallery application</span></span>

<span data-ttu-id="ebf74-331">tooadd une application à partir de hello Galerie d’Azure AD, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ebf74-331">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="ebf74-332">Ouvrez hello [Azure Portal](https://portal.azure.com) et connectez-vous en tant qu’un **administrateur Global** ou **Co-admin**</span><span class="sxs-lookup"><span data-stu-id="ebf74-332">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="ebf74-333">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-333">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ebf74-334">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="ebf74-334">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ebf74-335">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ebf74-335">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ebf74-336">Cliquez sur hello **ajouter** bouton au coin supérieur droit de hello sur hello **des Applications d’entreprise** panneau</span><span class="sxs-lookup"><span data-stu-id="ebf74-336">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="ebf74-337">Cliquez sur **Application ne figurant pas dans la galerie**.</span><span class="sxs-lookup"><span data-stu-id="ebf74-337">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="ebf74-338">Entrez le nom hello de votre application Bonjour **nom** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="ebf74-338">Enter hello name of your application in hello **Name** textbox.</span></span> <span data-ttu-id="ebf74-339">Sélectionnez **Ajouter.**</span><span class="sxs-lookup"><span data-stu-id="ebf74-339">Select **Add.**</span></span>

<span data-ttu-id="ebf74-340">Après une courte période, vous être Panneau de configuration de l’application en mesure de toosee hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-340">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="ebf74-341">Configurer une application hello pour mot de passe l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="ebf74-341">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="ebf74-342">tooconfigure l’authentification unique pour une application, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ebf74-342">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="ebf74-343">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**</span><span class="sxs-lookup"><span data-stu-id="ebf74-343">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="ebf74-344">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-344">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ebf74-345">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="ebf74-345">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ebf74-346">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ebf74-346">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ebf74-347">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="ebf74-347">click **All Applications** tooview a list of all your applications.</span></span>

 * <span data-ttu-id="ebf74-348">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="ebf74-348">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="ebf74-349">Sélectionnez l’application hello tooconfigure l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="ebf74-349">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="ebf74-350">Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-350">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="ebf74-351">Mode de sélection hello **mot de passe de session.**</span><span class="sxs-lookup"><span data-stu-id="ebf74-351">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="ebf74-352">Entrez hello **URL de connexion**.</span><span class="sxs-lookup"><span data-stu-id="ebf74-352">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="ebf74-353">Il s’agit d’URL de hello où les utilisateurs entrent leur nom d’utilisateur et mot de passe des toosign dans pour.</span><span class="sxs-lookup"><span data-stu-id="ebf74-353">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="ebf74-354">Vérifiez la connexion hello dans les champs est visibles à l’URL de hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-354">Ensure hello sign in fields are visible at hello URL.</span></span>

10. <span data-ttu-id="ebf74-355">Affecter des utilisateurs toohello application.</span><span class="sxs-lookup"><span data-stu-id="ebf74-355">Assign users toohello application.</span></span>

11. <span data-ttu-id="ebf74-356">En outre, vous pouvez également fournir des informations d’identification pour le compte d’utilisateur de hello en sélectionnant les lignes hello d’utilisateurs de hello en cliquant sur **informations d’identification de la mise à jour** et en entrant hello username et password pour le compte d’utilisateurs de hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-356">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="ebf74-357">Dans le cas contraire, les utilisateurs être invité à tooenter hello informations d’identification elles-mêmes lors du lancement.</span><span class="sxs-lookup"><span data-stu-id="ebf74-357">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="how-tooassign-a-user-tooan-application-directly"></a><span data-ttu-id="ebf74-358">Comment tooassign directement une application de tooan utilisateur</span><span class="sxs-lookup"><span data-stu-id="ebf74-358">How tooassign a user tooan application directly</span></span>

<span data-ttu-id="ebf74-359">tooassign un ou plusieurs utilisateurs tooan application directement, comme suit hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ebf74-359">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="ebf74-360">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="ebf74-360">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="ebf74-361">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-361">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ebf74-362">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="ebf74-362">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ebf74-363">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ebf74-363">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ebf74-364">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="ebf74-364">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="ebf74-365">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="ebf74-365">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="ebf74-366">Sélectionnez l’application hello tooassign une liste des utilisateurs toofrom hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-366">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="ebf74-367">Une fois le charge de l’application hello, cliquez sur **utilisateurs et groupes** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="ebf74-367">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="ebf74-368">Cliquez sur hello **ajouter** bouton par-dessus hello **utilisateurs et groupes** hello tooopen de liste **ajouter l’affectation** panneau.</span><span class="sxs-lookup"><span data-stu-id="ebf74-368">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="ebf74-369">Cliquez sur hello **utilisateurs et groupes** sélecteur de hello **ajouter l’affectation** panneau.</span><span class="sxs-lookup"><span data-stu-id="ebf74-369">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="ebf74-370">Type Bonjour **nom complet** ou **adresse de messagerie** d’utilisateur hello vous êtes intéressé par attribution dans hello **recherche par nom ou adresse de messagerie** zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="ebf74-370">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="ebf74-371">Placez le curseur sur hello **utilisateur** dans hello liste tooreveal un **case à cocher**.</span><span class="sxs-lookup"><span data-stu-id="ebf74-371">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="ebf74-372">Cliquez sur tooadd de photo ou le logo de profil hello case à cocher suivante toohello l’utilisateur à votre toohello utilisateur **sélectionnés** liste.</span><span class="sxs-lookup"><span data-stu-id="ebf74-372">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="ebf74-373">**Facultatif :** si vous souhaitez que trop**ajouter plusieurs utilisateurs**, type dans un autre **nom complet** ou **adresse de messagerie** dans hello **Rechercher par nom ou l’adresse de messagerie** zone de recherche, cliquez sur tooadd de case à cocher hello cette toohello utilisateur **sélectionnés** liste.</span><span class="sxs-lookup"><span data-stu-id="ebf74-373">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="ebf74-374">Lorsque vous avez fini de sélectionner les utilisateurs, cliquez sur hello **sélectionnez** bouton tooadd les toohello la liste des toobe utilisateurs et groupes affectés toohello application.</span><span class="sxs-lookup"><span data-stu-id="ebf74-374">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="ebf74-375">**Facultatif :** cliquez sur hello **sélectionner un rôle** sélecteur Bonjour **ajouter l’affectation** panneau tooselect un rôle aux utilisateurs de toohello tooassign que vous avez sélectionné.</span><span class="sxs-lookup"><span data-stu-id="ebf74-375">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="ebf74-376">Cliquez sur hello **affecter** bouton tooassign hello application toohello les utilisateurs sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="ebf74-376">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="ebf74-377">Après une courte période, les utilisateurs de hello que vous avez sélectionné est en mesure de toolaunch ces applications dans hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="ebf74-377">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a><span data-ttu-id="ebf74-378">Si ces étapes de dépannage ne pas hello hello résoudre</span><span class="sxs-lookup"><span data-stu-id="ebf74-378">If these troubleshooting steps do not hello resolve hello issue</span></span>

<span data-ttu-id="ebf74-379">Ouvrez un ticket de support avec hello informations suivantes si elle est disponible :</span><span class="sxs-lookup"><span data-stu-id="ebf74-379">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="ebf74-380">ID d’erreur de corrélation</span><span class="sxs-lookup"><span data-stu-id="ebf74-380">Correlation error ID</span></span>

-   <span data-ttu-id="ebf74-381">UPN (adresse e-mail de l’utilisateur)</span><span class="sxs-lookup"><span data-stu-id="ebf74-381">UPN (user email address)</span></span>

-   <span data-ttu-id="ebf74-382">ID de locataire</span><span class="sxs-lookup"><span data-stu-id="ebf74-382">TenantID</span></span>

-   <span data-ttu-id="ebf74-383">Type de navigateur</span><span class="sxs-lookup"><span data-stu-id="ebf74-383">Browser type</span></span>

-   <span data-ttu-id="ebf74-384">Fuseau horaire et heure/période à laquelle l’erreur se produit</span><span class="sxs-lookup"><span data-stu-id="ebf74-384">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="ebf74-385">Traces Fiddler</span><span class="sxs-lookup"><span data-stu-id="ebf74-385">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="ebf74-386">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ebf74-386">Next steps</span></span>
[<span data-ttu-id="ebf74-387">Fournissent des applications de tooyour de l’authentification unique avec le Proxy d’Application</span><span class="sxs-lookup"><span data-stu-id="ebf74-387">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

