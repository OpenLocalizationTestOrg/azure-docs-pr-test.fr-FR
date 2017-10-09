---
title: "aaaProblems connecter tooan application Azure AD galerie configurée pour fédéré sur l’authentification unique | Documents Microsoft"
description: "Comment tootroubleshoot problèmes avec application de la galerie de Azure AD configurée pour le mot de passe l’authentification unique"
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
ms.openlocfilehash: 7ba28765e1d1f13025d740790a2f87654ae0daed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-azure-ad-gallery-application-configured-for-federated-single-sign-on"></a><span data-ttu-id="29997-103">Problèmes de connexion tooan application Azure AD galerie configurée pour fédérée l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="29997-103">Problems signing in tooan Azure AD Gallery application configured for federated single sign-on</span></span>

<span data-ttu-id="29997-104">Hello volet d’accès est un portail web qui permet à un utilisateur qui dispose d’une entreprise ou école administrateur de compte dans Azure Active Directory (Azure AD) tooview et lancer les applications cloud qui hello Azure AD lui a accordé l’accès à.</span><span class="sxs-lookup"><span data-stu-id="29997-104">hello Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) tooview and launch cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="29997-105">Un utilisateur disposant des éditions d’Azure AD permet également de groupes en libre-service et les fonctionnalités de gestion d’application via hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="29997-105">A user who has Azure AD editions can also use self-service group and app management capabilities through hello Access Panel.</span></span> <span data-ttu-id="29997-106">Hello volet d’accès est séparé hello portail Azure et ne requiert pas d’utilisateurs toohave un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="29997-106">hello Access Panel is separate from hello Azure portal and does not require users toohave an Azure subscription.</span></span>

<span data-ttu-id="29997-107">toouse mot de passe-session unique (SSO) Bonjour hello extension du volet d’accès, volet d’accès doit être installé dans le navigateur de l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="29997-107">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="29997-108">Cette extension est téléchargée automatiquement lorsqu’un utilisateur sélectionne une application configurée pour l’authentification unique (SSO) avec mot de passe.</span><span class="sxs-lookup"><span data-stu-id="29997-108">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

## <a name="meeting-browser-requirements-for-hello-access-panel"></a><span data-ttu-id="29997-109">Configuration requise du navigateur de réunion hello panneau d’accès</span><span class="sxs-lookup"><span data-stu-id="29997-109">Meeting browser requirements for hello Access Panel</span></span>

<span data-ttu-id="29997-110">Hello volet d’accès nécessite un navigateur qui prend en charge JavaScript et a activé les CSS.</span><span class="sxs-lookup"><span data-stu-id="29997-110">hello Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="29997-111">toouse mot de passe-session unique (SSO) Bonjour hello extension du volet d’accès, volet d’accès doit être installé dans le navigateur de l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="29997-111">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="29997-112">Cette extension est téléchargée automatiquement lorsqu’un utilisateur sélectionne une application configurée pour l’authentification unique (SSO) avec mot de passe.</span><span class="sxs-lookup"><span data-stu-id="29997-112">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="29997-113">Pour l’authentification unique basée sur le mot de passe, hello navigateurs des utilisateurs finaux peuvent être :</span><span class="sxs-lookup"><span data-stu-id="29997-113">For password-based SSO, hello end user’s browsers can be:</span></span>

-   <span data-ttu-id="29997-114">Internet Explorer 8, 9, 10, 11 -- sur Windows 7 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="29997-114">Internet Explorer 8, 9, 10, 11 - on Windows 7 or later</span></span>

-   <span data-ttu-id="29997-115">Chrome -- sur Windows 7 ou ultérieur, et sur Mac OS X ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="29997-115">Chrome - on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="29997-116">Firefox 26.0 ou ultérieur -- sur Windows XP SP2 ou version ultérieure, et sur Mac OS X 10.6 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="29997-116">Firefox 26.0 or later - on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

>[!NOTE]
><span data-ttu-id="29997-117">extension de l’authentification unique basée sur le mot de passe Hello deviennent disponibles pour Edge dans Windows 10 lorsque les extensions du navigateur sont pris en charge pour la session.</span><span class="sxs-lookup"><span data-stu-id="29997-117">hello password-based SSO extension become available for Edge in Windows 10 when browser extensions become supported for Edge.</span></span>
>
>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="29997-118">Comment tooinstall hello extension du navigateur de panneau d’accès</span><span class="sxs-lookup"><span data-stu-id="29997-118">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="29997-119">tooinstall hello extension du navigateur de panneau d’accès, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="29997-119">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="29997-120">Ouvrez hello [volet d’accès](https://myapps.microsoft.com) dans un des navigateurs de hello pris en charge et vous connecter en tant qu’un **utilisateur** dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29997-120">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="29997-121">Cliquez sur un **application d’authentification unique du mot de passe** Bonjour panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="29997-121">click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="29997-122">Dans hello invite vous demandant tooinstall hello logiciel, sélectionnez **installer maintenant**.</span><span class="sxs-lookup"><span data-stu-id="29997-122">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="29997-123">En fonction de votre navigateur vous être lien de téléchargement toohello dirigée.</span><span class="sxs-lookup"><span data-stu-id="29997-123">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="29997-124">**Ajouter** navigateur de tooyour extension hello.</span><span class="sxs-lookup"><span data-stu-id="29997-124">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="29997-125">Si votre navigateur vous invite à sélectionner tooeither **activer** ou **autoriser** hello extension.</span><span class="sxs-lookup"><span data-stu-id="29997-125">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="29997-126">Une fois l’extension installée, **redémarrez** votre session de navigateur.</span><span class="sxs-lookup"><span data-stu-id="29997-126">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="29997-127">Connectez-vous en hello volet d’accès et de voir si vous pouvez **lancer** vos applications SSO de mot de passe</span><span class="sxs-lookup"><span data-stu-id="29997-127">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="29997-128">Vous pouvez également télécharger l’extension de hello pour Chrome et Firefox à partir de liens directs de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="29997-128">You may also download hello extension for Chrome and Firefox from hello direct links below:</span></span>

-   [<span data-ttu-id="29997-129">Extension du volet d’accès pour Chrome</span><span class="sxs-lookup"><span data-stu-id="29997-129">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="29997-130">Extension du volet d’accès pour Firefox</span><span class="sxs-lookup"><span data-stu-id="29997-130">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="setting-up-a-group-policy-for-internet-explorer"></a><span data-ttu-id="29997-131">Configuration d’une stratégie de groupe pour Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="29997-131">Setting up a group policy for Internet Explorer</span></span>

<span data-ttu-id="29997-132">Vous pouvez configurer une stratégie de groupe qui vous tooremotely installer une extension volet d’accès hello pour Internet Explorer sur les ordinateurs de vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="29997-132">You can setup a group policy that allow you tooremotely install hello Access Panel extension for Internet Explorer on your users' machines.</span></span>

<span data-ttu-id="29997-133">conditions préalables de Hello sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="29997-133">hello prerequisites include:</span></span>

-   <span data-ttu-id="29997-134">Vous avez configuré [les Services de domaine Active Directory](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), et vous avez joint le domaine de tooyour ordinateurs de vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="29997-134">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines tooyour domain.</span></span>

-   <span data-ttu-id="29997-135">Vous devez avoir hello hello « Modifier les paramètres » autorisation tooedit objet de stratégie de groupe (GPO).</span><span class="sxs-lookup"><span data-stu-id="29997-135">You must have hello "Edit settings" permission tooedit hello Group Policy Object (GPO).</span></span> <span data-ttu-id="29997-136">Par défaut, les membres de hello les groupes de sécurité suivants ont cette autorisation : les administrateurs de domaine, les administrateurs d’entreprise et les propriétaires créateurs de la stratégie de groupe.</span><span class="sxs-lookup"><span data-stu-id="29997-136">By default, members of hello following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> <span data-ttu-id="29997-137">[En savoir plus](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="29997-137">[Learn more](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span></span>

<span data-ttu-id="29997-138">Suivez le didacticiel de hello [comment tooDeploy hello Extension volet d’accès pour Internet Explorer à l’aide de la stratégie de groupe](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) pour obtenir des instructions étape par étape comment tooconfigure hello de stratégie de groupe et déployez-le toousers.</span><span class="sxs-lookup"><span data-stu-id="29997-138">Follow hello tutorial [How tooDeploy hello Access Panel Extension for Internet Explorer using Group Policy](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) for step by step instructions on how tooconfigure hello group policy and deploy it toousers.</span></span>

## <a name="troubleshoot-hello-access-panel-in-internet-explorer"></a><span data-ttu-id="29997-139">Résoudre les problèmes de hello volet d’accès dans Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="29997-139">Troubleshoot hello Access Panel in Internet Explorer</span></span>

<span data-ttu-id="29997-140">Suivez hello [dépannage hello Extension volet d’accès pour Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) guide pour l’accès d’un outil de diagnostic et des instructions étape par étape sur la configuration de l’extension de hello pour Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="29997-140">Follow hello [Troubleshoot hello Access Panel Extension for Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) guide for access a diagnostics tool and step by step instructions on configuring hello extension for IE.</span></span>

## <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="29997-141">Comment tooconfigure le mot de passe sur l’authentification unique pour une application de la galerie Azure AD</span><span class="sxs-lookup"><span data-stu-id="29997-141">How tooconfigure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="29997-142">tooconfigure une application à partir de la galerie d’Azure AD hello vous devez :</span><span class="sxs-lookup"><span data-stu-id="29997-142">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="29997-143">Ajouter une application à partir de la galerie d’Azure AD hello</span><span class="sxs-lookup"><span data-stu-id="29997-143">Add an application from hello Azure AD gallery</span></span>](#_Add_an_application)

-   [<span data-ttu-id="29997-144">Configurer une application hello pour mot de passe l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="29997-144">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="29997-145">Affecter des utilisateurs toohello application</span><span class="sxs-lookup"><span data-stu-id="29997-145">Assign users toohello application</span></span>](#assign-users-to-the-application)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="29997-146">Ajouter une application à partir de la galerie d’Azure AD hello</span><span class="sxs-lookup"><span data-stu-id="29997-146">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="29997-147">tooadd une application à partir de hello Galerie d’Azure AD, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="29997-147">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="29997-148">Ouvrez hello [Azure Portal](https://portal.azure.com) et connectez-vous en tant qu’un **administrateur Global** ou **Co-admin**</span><span class="sxs-lookup"><span data-stu-id="29997-148">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="29997-149">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="29997-149">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="29997-150">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="29997-150">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="29997-151">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="29997-151">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="29997-152">Cliquez sur hello **ajouter** bouton au coin supérieur droit de hello sur hello **des Applications d’entreprise** panneau.</span><span class="sxs-lookup"><span data-stu-id="29997-152">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="29997-153">Bonjour **Entrez un nom** zone de texte à partir de hello **ajouter à partir de la galerie de hello** section, entrez un nom hello de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="29997-153">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="29997-154">Sélectionnez hello application tooconfigure pour l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="29997-154">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="29997-155">Avant d’ajouter l’application hello, vous pouvez modifier son nom à partir de hello **nom** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="29997-155">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="29997-156">Cliquez sur **ajouter** bouton, l’application de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="29997-156">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="29997-157">Après une courte période, vous être Panneau de configuration de l’application en mesure de toosee hello.</span><span class="sxs-lookup"><span data-stu-id="29997-157">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="29997-158">Configurer une application hello pour mot de passe l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="29997-158">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="29997-159">tooconfigure l’authentification unique pour une application, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="29997-159">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="29997-160">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**</span><span class="sxs-lookup"><span data-stu-id="29997-160">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="29997-161">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="29997-161">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="29997-162">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="29997-162">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="29997-163">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="29997-163">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="29997-164">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="29997-164">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="29997-165">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="29997-165">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="29997-166">Sélectionnez application hello tooconfigure l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="29997-166">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="29997-167">Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="29997-167">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="29997-168">Mode de sélection hello **mot de passe de session.**</span><span class="sxs-lookup"><span data-stu-id="29997-168">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="29997-169">[Affecter des utilisateurs toohello application](#_How_to_assign).</span><span class="sxs-lookup"><span data-stu-id="29997-169">[Assign users toohello application](#_How_to_assign).</span></span>

10. <span data-ttu-id="29997-170">En outre, vous pouvez également fournir des informations d’identification pour le compte d’utilisateur de hello en sélectionnant les lignes hello d’utilisateurs de hello en cliquant sur **informations d’identification de la mise à jour** et en entrant hello username et password pour le compte d’utilisateurs de hello.</span><span class="sxs-lookup"><span data-stu-id="29997-170">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="29997-171">Dans le cas contraire, les utilisateurs être invité à tooenter hello informations d’identification elles-mêmes lors du lancement.</span><span class="sxs-lookup"><span data-stu-id="29997-171">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

### <a name="assign-users-toohello-application"></a><span data-ttu-id="29997-172">Affecter des utilisateurs toohello application</span><span class="sxs-lookup"><span data-stu-id="29997-172">Assign users toohello application</span></span>

<span data-ttu-id="29997-173">tooassign un ou plusieurs utilisateurs tooan application directement, comme suit hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="29997-173">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="29997-174">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="29997-174">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="29997-175">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="29997-175">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="29997-176">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="29997-176">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="29997-177">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="29997-177">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="29997-178">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="29997-178">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="29997-179">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="29997-179">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="29997-180">Sélectionnez l’application hello tooassign une liste des utilisateurs toofrom hello.</span><span class="sxs-lookup"><span data-stu-id="29997-180">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="29997-181">Une fois le charge de l’application hello, cliquez sur **utilisateurs et groupes** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="29997-181">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="29997-182">Cliquez sur hello **ajouter** bouton par-dessus hello **utilisateurs et groupes** hello tooopen de liste **ajouter l’affectation** panneau.</span><span class="sxs-lookup"><span data-stu-id="29997-182">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="29997-183">Cliquez sur hello **utilisateurs et groupes** sélecteur de hello **ajouter l’affectation** panneau.</span><span class="sxs-lookup"><span data-stu-id="29997-183">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="29997-184">Type Bonjour **nom complet** ou **adresse de messagerie** d’utilisateur hello vous êtes intéressé par attribution dans hello **recherche par nom ou adresse de messagerie** zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="29997-184">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="29997-185">Placez le curseur sur hello **utilisateur** dans hello liste tooreveal un **case à cocher**.</span><span class="sxs-lookup"><span data-stu-id="29997-185">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="29997-186">Cliquez sur tooadd de photo ou le logo de profil hello case à cocher suivante toohello l’utilisateur à votre toohello utilisateur **sélectionnés** liste.</span><span class="sxs-lookup"><span data-stu-id="29997-186">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="29997-187">**Facultatif :** si vous souhaitez que trop**ajouter plusieurs utilisateurs**, type dans un autre **nom complet** ou **adresse de messagerie** dans hello **Rechercher par nom ou l’adresse de messagerie** zone de recherche, cliquez sur tooadd de case à cocher hello cette toohello utilisateur **sélectionnés** liste.</span><span class="sxs-lookup"><span data-stu-id="29997-187">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="29997-188">Lorsque vous avez fini de sélectionner les utilisateurs, cliquez sur hello **sélectionnez** bouton tooadd les toohello la liste des toobe utilisateurs et groupes affectés toohello application.</span><span class="sxs-lookup"><span data-stu-id="29997-188">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="29997-189">**Facultatif :** cliquez sur hello **sélectionner un rôle** sélecteur Bonjour **ajouter l’affectation** panneau tooselect un rôle aux utilisateurs de toohello tooassign que vous avez sélectionné.</span><span class="sxs-lookup"><span data-stu-id="29997-189">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="29997-190">Cliquez sur hello **affecter** bouton tooassign hello application toohello les utilisateurs sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="29997-190">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="29997-191">Après une courte période, les utilisateurs de hello que vous avez sélectionné est en mesure de toolaunch ces applications dans hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="29997-191">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="if-these-troubleshoot-steps-dont-resolve-hello-issue"></a><span data-ttu-id="29997-192">Si ces résoudre les étapes ne résolvent hello</span><span class="sxs-lookup"><span data-stu-id="29997-192">If these troubleshoot steps don't resolve hello issue</span></span> 
<span data-ttu-id="29997-193">Ouvrez un ticket de support avec hello informations suivantes si elle est disponible :</span><span class="sxs-lookup"><span data-stu-id="29997-193">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="29997-194">ID d’erreur de corrélation</span><span class="sxs-lookup"><span data-stu-id="29997-194">Correlation error ID</span></span>

-   <span data-ttu-id="29997-195">UPN (adresse e-mail de l’utilisateur)</span><span class="sxs-lookup"><span data-stu-id="29997-195">UPN (user email address)</span></span>

-   <span data-ttu-id="29997-196">ID de locataire</span><span class="sxs-lookup"><span data-stu-id="29997-196">TenantID</span></span>

-   <span data-ttu-id="29997-197">Type de navigateur</span><span class="sxs-lookup"><span data-stu-id="29997-197">Browser type</span></span>

-   <span data-ttu-id="29997-198">Fuseau horaire et heure/période à laquelle l’erreur se produit</span><span class="sxs-lookup"><span data-stu-id="29997-198">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="29997-199">Traces Fiddler</span><span class="sxs-lookup"><span data-stu-id="29997-199">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="29997-200">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="29997-200">Next steps</span></span>
[<span data-ttu-id="29997-201">Fournissent des applications de tooyour de l’authentification unique avec le Proxy d’Application</span><span class="sxs-lookup"><span data-stu-id="29997-201">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
