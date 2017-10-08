---
title: "aaaProblems de signature dans l’application tooan à l’aide d’un lien ciblé | Documents Microsoft"
description: "Comment les problèmes de tootroubleshoot l’accès à une application à partir d’une URL de lien ciblé à l’aide d’Azure AD"
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
ms.openlocfilehash: dc82410001ac05895cc0244c3a89ace71bcf01a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-application-using-a-deeplink"></a><span data-ttu-id="5b4d5-103">Problèmes de connexion dans l’application tooan à l’aide d’un lien ciblé</span><span class="sxs-lookup"><span data-stu-id="5b4d5-103">Problems signing in tooan application using a deeplink</span></span>

<span data-ttu-id="5b4d5-104">Hello volet d’accès est un portail web qui permet à un utilisateur avec un travail ou compte scolaire dans Azure Active Directory (Azure AD) tooview et démarrer les applications cloud qui hello administrateur Azure AD lui a accordé l’accès à.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-104">hello Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) tooview and start cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> 

<span data-ttu-id="5b4d5-105">Ces applications sont configurées pour le compte d’utilisateur hello dans le portail Azure AD de hello.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-105">These applications are configured on behalf of hello user in hello Azure AD portal.</span></span> <span data-ttu-id="5b4d5-106">application Hello doit être configurée correctement et toohello attribué ou un utilisateur de hello de groupe est un membre de l’application de hello toosee Bonjour panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-106">hello application must be configured properly and assigned toohello user or a group hello user is a member of toosee hello application in hello Access Panel.</span></span>

<span data-ttu-id="5b4d5-107">Des liens profonds ou l’accès des utilisateurs des URL sont vos utilisateurs peuvent utiliser tooaccess leurs applications SSO de mot de passe directement à partir de leur URL navigateurs barres de liens.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-107">Deep links or User access URLs are links your users may use tooaccess their password-SSO applications directly from their browsers URL bars.</span></span> <span data-ttu-id="5b4d5-108">En accédant à toothis lien, les utilisateurs soient automatiquement connecté à application hello sans avoir tout d’abord les toogo toohello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-108">By navigating toothis link, users be automatically signed into hello application without having toogo toohello Access Panel first.</span></span> <span data-ttu-id="5b4d5-109">Il s’agit de hello même lien que les utilisateurs utilisent tooaccess ces applications à partir du Lanceur d’applications hello Office 365.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-109">This is hello same link that users use tooaccess these applications from hello Office 365 application launcher.</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="5b4d5-110">Général émet toocheck tout d’abord</span><span class="sxs-lookup"><span data-stu-id="5b4d5-110">General issues toocheck first</span></span>

-   <span data-ttu-id="5b4d5-111">Assurez-vous que votre en utilisant un **navigateur** qui répond aux hello configuration minimale requise pour hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-111">Make sure your using a **browser** that meets hello minimum requirements for hello Access Panel.</span></span>

-   <span data-ttu-id="5b4d5-112">Assurez-vous que navigateur de l’utilisateur hello a ajouté des URL hello de hello application tooits **sites de confiance**.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-112">Make sure hello user’s browser has added hello URL of hello application tooits **trusted sites**.</span></span>

-   <span data-ttu-id="5b4d5-113">Assurez-vous que l’application de hello toocheck est **configuré** correctement.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-113">Make sure toocheck hello application is **configured** correctly.</span></span>

-   <span data-ttu-id="5b4d5-114">Assurez-vous que le compte d’utilisateur hello est **activé** pour les connexions.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-114">Make sure hello user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="5b4d5-115">Assurez-vous que le compte d’utilisateur hello est **ne pas verrouillé.**</span><span class="sxs-lookup"><span data-stu-id="5b4d5-115">Make sure hello user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="5b4d5-116">Vérifiez que hello l’utilisateur **mot de passe n’a pas expiré ou oublié.**</span><span class="sxs-lookup"><span data-stu-id="5b4d5-116">Make sure hello user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="5b4d5-117">Vérifiez que **Multi-Factor Authentication** ne bloque pas l’accès utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-117">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="5b4d5-118">Vérifiez qu’une **stratégie d’accès conditionnel** ou **stratégie de protection d’identité** ne bloque pas l’accès utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-118">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="5b4d5-119">S’assurer que l’utilisateur **les informations de contact d’authentification** est toodate tooallow multi-Factor Authentication ou accès conditionnel stratégies toobe appliquée.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-119">Make sure that a user’s **authentication contact info** is up toodate tooallow Multi-Factor Authentication or Conditional Access policies toobe enforced.</span></span>

-   <span data-ttu-id="5b4d5-120">Assurez-vous que tooalso try effacer les cookies de votre navigateur et réessayer toosign dans.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-120">Make sure tooalso try clearing your browser’s cookies and trying toosign in again.</span></span>

## <a name="checking-hello-deeplink"></a><span data-ttu-id="5b4d5-121">La vérification de lien ciblé hello</span><span class="sxs-lookup"><span data-stu-id="5b4d5-121">Checking hello deeplink</span></span>

<span data-ttu-id="5b4d5-122">toocheck si vous avez via un lien ciblé hello correcte, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="5b4d5-122">toocheck if you have hello correct deeplink, follow hello steps below:</span></span>

1.  <span data-ttu-id="5b4d5-123">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**</span><span class="sxs-lookup"><span data-stu-id="5b4d5-123">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="5b4d5-124">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-124">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5b4d5-125">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-125">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5b4d5-126">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-126">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5b4d5-127">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-127">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="5b4d5-128">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="5b4d5-128">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="5b4d5-129">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**</span><span class="sxs-lookup"><span data-stu-id="5b4d5-129">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

7.  <span data-ttu-id="5b4d5-130">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-130">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

8.  <span data-ttu-id="5b4d5-131">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-131">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

9.  <span data-ttu-id="5b4d5-132">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-132">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

10. <span data-ttu-id="5b4d5-133">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-133">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="5b4d5-134">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="5b4d5-134">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

11. <span data-ttu-id="5b4d5-135">Sélectionnez l’application hello hello de vérification hello lien ciblé pour.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-135">Select hello application you want hello check hello deeplink for.</span></span>

12. <span data-ttu-id="5b4d5-136">Trouver l’étiquette de hello **URL d’accès utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-136">Find hello label **User Access URL**.</span></span> <span data-ttu-id="5b4d5-137">Votre lien profond doit correspondre à cette URL.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-137">You deeplink should match this URL.</span></span>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="5b4d5-138">Comment tooinstall hello extension du navigateur de panneau d’accès</span><span class="sxs-lookup"><span data-stu-id="5b4d5-138">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="5b4d5-139">tooinstall hello extension du navigateur de panneau d’accès, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="5b4d5-139">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="5b4d5-140">Ouvrez hello [volet d’accès](https://myapps.microsoft.com) dans un des navigateurs de hello pris en charge et vous connecter en tant qu’un **utilisateur** dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-140">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="5b4d5-141">Cliquez sur un **application d’authentification unique du mot de passe** Bonjour panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-141">click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="5b4d5-142">Dans hello invite vous demandant tooinstall hello logiciel, sélectionnez **installer maintenant**.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-142">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="5b4d5-143">En fonction de votre navigateur vous être lien de téléchargement toohello dirigée.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-143">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="5b4d5-144">**Ajouter** navigateur de tooyour extension hello.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-144">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="5b4d5-145">Si votre navigateur vous invite à sélectionner tooeither **activer** ou **autoriser** hello extension.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-145">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="5b4d5-146">Une fois l’extension installée, **redémarrez** votre session de navigateur.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-146">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="5b4d5-147">Connectez-vous en hello volet d’accès et de voir si vous pouvez **lancer** vos applications SSO de mot de passe</span><span class="sxs-lookup"><span data-stu-id="5b4d5-147">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="5b4d5-148">Vous pouvez également télécharger l’extension de hello pour Chrome et Firefox à partir de liens directs de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="5b4d5-148">You may also download hello extension for Chrome and Firefox from hello direct links below:</span></span>

-   [<span data-ttu-id="5b4d5-149">Extension du volet d’accès pour Chrome</span><span class="sxs-lookup"><span data-stu-id="5b4d5-149">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="5b4d5-150">Extension du volet d’accès pour Firefox</span><span class="sxs-lookup"><span data-stu-id="5b4d5-150">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="5b4d5-151">Comment tooconfigure le mot de passe sur l’authentification unique pour une application de la galerie Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b4d5-151">How tooconfigure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="5b4d5-152">tooconfigure une application à partir de la galerie d’Azure AD hello vous devez :</span><span class="sxs-lookup"><span data-stu-id="5b4d5-152">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="5b4d5-153">Ajouter une application à partir de la galerie d’Azure AD hello</span><span class="sxs-lookup"><span data-stu-id="5b4d5-153">Add an application from hello Azure AD gallery</span></span>](#add-an-application-from-the-Azure-AD-gallery)

-   [<span data-ttu-id="5b4d5-154">Configurer une application hello pour mot de passe l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="5b4d5-154">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="5b4d5-155">Ajouter une application à partir de la galerie d’Azure AD hello</span><span class="sxs-lookup"><span data-stu-id="5b4d5-155">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="5b4d5-156">tooadd une application à partir de hello Galerie d’Azure AD, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="5b4d5-156">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="5b4d5-157">Ouvrez hello [Azure Portal](https://portal.azure.com) et connectez-vous en tant qu’un **administrateur Global** ou **Co-admin**.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-157">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="5b4d5-158">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-158">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5b4d5-159">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-159">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5b4d5-160">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-160">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5b4d5-161">Cliquez sur hello **ajouter** bouton au coin supérieur droit de hello sur hello **des Applications d’entreprise** panneau.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-161">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="5b4d5-162">Bonjour **Entrez un nom** zone de texte à partir de hello **ajouter à partir de la galerie de hello** section, entrez un nom hello de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-162">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="5b4d5-163">Sélectionnez hello application tooconfigure pour l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-163">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="5b4d5-164">Avant d’ajouter l’application hello, vous pouvez modifier son nom à partir de hello **nom** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-164">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="5b4d5-165">Cliquez sur **ajouter** bouton, l’application de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-165">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="5b4d5-166">Après une courte période, vous être Panneau de configuration de l’application en mesure de toosee hello.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-166">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="5b4d5-167">Configurer une application hello pour mot de passe l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="5b4d5-167">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="5b4d5-168">tooconfigure l’authentification unique pour une application, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="5b4d5-168">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="5b4d5-169">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**</span><span class="sxs-lookup"><span data-stu-id="5b4d5-169">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="5b4d5-170">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-170">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5b4d5-171">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-171">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5b4d5-172">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-172">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5b4d5-173">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-173">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="5b4d5-174">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="5b4d5-174">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="5b4d5-175">Sélectionnez l’application hello tooconfigure l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-175">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="5b4d5-176">Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-176">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="5b4d5-177">Mode de sélection hello **mot de passe de session.**</span><span class="sxs-lookup"><span data-stu-id="5b4d5-177">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="5b4d5-178">[Affecter des utilisateurs toohello application](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="5b4d5-178">[Assign users toohello application](#how-to-assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="5b4d5-179">En outre, vous pouvez également fournir des informations d’identification pour le compte d’utilisateur de hello en sélectionnant les lignes hello d’utilisateurs de hello en cliquant sur **informations d’identification de la mise à jour** et en entrant hello username et password pour le compte d’utilisateurs de hello.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-179">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="5b4d5-180">Dans le cas contraire, les utilisateurs être invité à tooenter hello informations d’identification elles-mêmes lors du lancement.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-180">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="5b4d5-181">Comment tooconfigure le mot de passe sur l’authentification unique pour une application non-galerie</span><span class="sxs-lookup"><span data-stu-id="5b4d5-181">How tooconfigure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="5b4d5-182">tooconfigure une application à partir de la galerie d’Azure AD hello vous devez :</span><span class="sxs-lookup"><span data-stu-id="5b4d5-182">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="5b4d5-183">Ajouter une application ne figurant pas dans la galerie</span><span class="sxs-lookup"><span data-stu-id="5b4d5-183">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="5b4d5-184">Configurer une application hello pour mot de passe l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="5b4d5-184">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="5b4d5-185">Ajouter une application ne figurant pas dans la galerie</span><span class="sxs-lookup"><span data-stu-id="5b4d5-185">Add a non-gallery application</span></span>

<span data-ttu-id="5b4d5-186">tooadd une application à partir de hello Galerie d’Azure AD, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="5b4d5-186">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="5b4d5-187">Ouvrez hello [Azure Portal](https://portal.azure.com) et connectez-vous en tant qu’un **administrateur Global** ou **Co-admin**.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-187">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="5b4d5-188">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-188">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5b4d5-189">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-189">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5b4d5-190">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-190">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5b4d5-191">Cliquez sur hello **ajouter** bouton au coin supérieur droit de hello sur hello **des Applications d’entreprise** panneau.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-191">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="5b4d5-192">Cliquez sur **Application ne figurant pas dans la galerie**.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-192">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="5b4d5-193">Entrez le nom hello de votre application Bonjour **nom** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-193">Enter hello name of your application in hello **Name** textbox.</span></span> <span data-ttu-id="5b4d5-194">Sélectionnez **Ajouter.**</span><span class="sxs-lookup"><span data-stu-id="5b4d5-194">Select **Add.**</span></span>

<span data-ttu-id="5b4d5-195">Après une courte période, vous être Panneau de configuration de l’application en mesure de toosee hello.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-195">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="5b4d5-196">Configurer une application hello pour mot de passe l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="5b4d5-196">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="5b4d5-197">tooconfigure l’authentification unique pour une application, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="5b4d5-197">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="5b4d5-198">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**</span><span class="sxs-lookup"><span data-stu-id="5b4d5-198">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="5b4d5-199">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-199">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5b4d5-200">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-200">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5b4d5-201">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-201">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5b4d5-202">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-202">click **All Applications** tooview a list of all your applications.</span></span>

    1.  <span data-ttu-id="5b4d5-203">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="5b4d5-203">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="5b4d5-204">Sélectionnez l’application hello tooconfigure l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-204">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="5b4d5-205">Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-205">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="5b4d5-206">Mode de sélection hello **mot de passe de session.**</span><span class="sxs-lookup"><span data-stu-id="5b4d5-206">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="5b4d5-207">Entrez hello **URL de connexion**.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-207">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="5b4d5-208">Il s’agit d’URL de hello où les utilisateurs entrent leur nom d’utilisateur et mot de passe des toosign dans pour.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-208">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="5b4d5-209">Vérifiez la connexion hello dans les champs est visibles à l’URL de hello.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-209">Ensure hello sign in fields are visible at hello URL.</span></span>

10. <span data-ttu-id="5b4d5-210">Affecter des utilisateurs toohello application.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-210">Assign users toohello application.</span></span>

11. <span data-ttu-id="5b4d5-211">En outre, vous pouvez également fournir des informations d’identification pour le compte d’utilisateur de hello en sélectionnant les lignes hello d’utilisateurs de hello en cliquant sur **informations d’identification de la mise à jour** et en entrant hello username et password pour le compte d’utilisateurs de hello.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-211">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="5b4d5-212">Dans le cas contraire, les utilisateurs être invité à tooenter hello informations d’identification elles-mêmes lors du lancement.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-212">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="how-tooassign-a-user-tooan-application-directly"></a><span data-ttu-id="5b4d5-213">Comment tooassign directement une application de tooan utilisateur</span><span class="sxs-lookup"><span data-stu-id="5b4d5-213">How tooassign a user tooan application directly</span></span>

<span data-ttu-id="5b4d5-214">tooassign un ou plusieurs utilisateurs tooan application directement, comme suit hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="5b4d5-214">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="5b4d5-215">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="5b4d5-215">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="5b4d5-216">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-216">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5b4d5-217">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-217">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5b4d5-218">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-218">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5b4d5-219">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-219">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="5b4d5-220">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="5b4d5-220">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="5b4d5-221">Sélectionnez l’application hello tooassign une liste des utilisateurs toofrom hello.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-221">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="5b4d5-222">Une fois le charge de l’application hello, cliquez sur **utilisateurs et groupes** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-222">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="5b4d5-223">Cliquez sur hello **ajouter** bouton par-dessus hello **utilisateurs et groupes** hello tooopen de liste **ajouter l’affectation** panneau.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-223">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="5b4d5-224">Cliquez sur hello **utilisateurs et groupes** sélecteur de hello **ajouter l’affectation** panneau.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-224">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="5b4d5-225">Type Bonjour **nom complet** ou **adresse de messagerie** d’utilisateur hello vous êtes intéressé par attribution dans hello **recherche par nom ou adresse de messagerie** zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-225">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="5b4d5-226">Placez le curseur sur hello **utilisateur** dans hello liste tooreveal un **case à cocher**.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-226">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="5b4d5-227">Cliquez sur tooadd de photo ou le logo de profil hello case à cocher suivante toohello l’utilisateur à votre toohello utilisateur **sélectionnés** liste.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-227">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="5b4d5-228">**Facultatif :** si vous souhaitez que trop**ajouter plusieurs utilisateurs**, type dans un autre **nom complet** ou **adresse de messagerie** dans hello **Rechercher par nom ou l’adresse de messagerie** zone de recherche, cliquez sur tooadd de case à cocher hello cette toohello utilisateur **sélectionnés** liste.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-228">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="5b4d5-229">Lorsque vous avez fini de sélectionner les utilisateurs, cliquez sur hello **sélectionnez** bouton tooadd les toohello la liste des toobe utilisateurs et groupes affectés toohello application.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-229">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="5b4d5-230">**Facultatif :** cliquez sur hello **sélectionner un rôle** sélecteur Bonjour **ajouter l’affectation** panneau tooselect un rôle aux utilisateurs de toohello tooassign que vous avez sélectionné.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-230">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="5b4d5-231">Cliquez sur hello **affecter** bouton tooassign hello application toohello les utilisateurs sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-231">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="5b4d5-232">Après une courte période, les utilisateurs de hello que vous avez sélectionné est en mesure de toolaunch ces applications dans hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-232">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a><span data-ttu-id="5b4d5-233">Si ces étapes de dépannage hello pas résoudre les problème de hello.</span><span class="sxs-lookup"><span data-stu-id="5b4d5-233">If these troubleshooting steps do not hello resolve hello issue.</span></span> 

<span data-ttu-id="5b4d5-234">Ouvrez un ticket de support avec hello informations suivantes si elle est disponible :</span><span class="sxs-lookup"><span data-stu-id="5b4d5-234">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="5b4d5-235">ID d’erreur de corrélation</span><span class="sxs-lookup"><span data-stu-id="5b4d5-235">Correlation error ID</span></span>

-   <span data-ttu-id="5b4d5-236">UPN (adresse e-mail de l’utilisateur)</span><span class="sxs-lookup"><span data-stu-id="5b4d5-236">UPN (user email address)</span></span>

-   <span data-ttu-id="5b4d5-237">ID de locataire</span><span class="sxs-lookup"><span data-stu-id="5b4d5-237">TenantID</span></span>

-   <span data-ttu-id="5b4d5-238">Type de navigateur</span><span class="sxs-lookup"><span data-stu-id="5b4d5-238">Browser type</span></span>

-   <span data-ttu-id="5b4d5-239">Fuseau horaire et heure/période à laquelle l’erreur se produit</span><span class="sxs-lookup"><span data-stu-id="5b4d5-239">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="5b4d5-240">Traces Fiddler</span><span class="sxs-lookup"><span data-stu-id="5b4d5-240">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b4d5-241">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5b4d5-241">Next steps</span></span>
[<span data-ttu-id="5b4d5-242">Fournissent des applications de tooyour de l’authentification unique avec le Proxy d’Application</span><span class="sxs-lookup"><span data-stu-id="5b4d5-242">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
