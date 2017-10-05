---
title: "Problèmes de connexion à une application à l’aide d’un lien profond | Microsoft Docs"
description: "Comment résoudre les problèmes d’accès à une application à partir d’une URL de lien profond à l’aide d’Azure AD"
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
ms.openlocfilehash: 798015ab68afc65378cffc75afec9c7f91fc1926
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-an-application-using-a-deeplink"></a><span data-ttu-id="de7a7-103">Problèmes de connexion à une application à l’aide d’un lien profond</span><span class="sxs-lookup"><span data-stu-id="de7a7-103">Problems signing in to an application using a deeplink</span></span>

<span data-ttu-id="de7a7-104">Le volet d’accès est un portail web qui permet à un utilisateur disposant d’un compte professionnel ou scolaire dans Azure Active Directory (Azure AD) d’afficher et de démarrer des applications basées sur le cloud auxquelles l’administrateur Azure AD lui a accordé un accès.</span><span class="sxs-lookup"><span data-stu-id="de7a7-104">The Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) to view and start cloud-based applications that the Azure AD administrator has granted them access to.</span></span> 

<span data-ttu-id="de7a7-105">Ces applications sont configurées pour le compte de l’utilisateur dans le portail Azure AD.</span><span class="sxs-lookup"><span data-stu-id="de7a7-105">These applications are configured on behalf of the user in the Azure AD portal.</span></span> <span data-ttu-id="de7a7-106">Pour que l’application soit visible dans le volet d’accès, elle doit être correctement configurée et affectée à l’utilisateur ou à un groupe dont est membre l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="de7a7-106">The application must be configured properly and assigned to the user or a group the user is a member of to see the application in the Access Panel.</span></span>

<span data-ttu-id="de7a7-107">Les liens profonds ou URL d’accès utilisateur sont des liens que vos utilisateurs peuvent utiliser pour accéder à leurs applications à authentification unique par mot de passe directement à partir des barres d’URL de leurs navigateurs.</span><span class="sxs-lookup"><span data-stu-id="de7a7-107">Deep links or User access URLs are links your users may use to access their password-SSO applications directly from their browsers URL bars.</span></span> <span data-ttu-id="de7a7-108">En accédant à ce lien, les utilisateurs sont automatiquement connectés à l’application sans devoir passer par le volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="de7a7-108">By navigating to this link, users be automatically signed into the application without having to go to the Access Panel first.</span></span> <span data-ttu-id="de7a7-109">Il s’agit du lien dont les utilisateurs se servent pour accéder à ces applications à partir du lanceur d’applications Office 365.</span><span class="sxs-lookup"><span data-stu-id="de7a7-109">This is the same link that users use to access these applications from the Office 365 application launcher.</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="de7a7-110">Problèmes d’ordre général à vérifier en premier</span><span class="sxs-lookup"><span data-stu-id="de7a7-110">General issues to check first</span></span>

-   <span data-ttu-id="de7a7-111">Vérifiez que votre **navigateur** répond à la configuration minimale requise pour le volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="de7a7-111">Make sure your using a **browser** that meets the minimum requirements for the Access Panel.</span></span>

-   <span data-ttu-id="de7a7-112">Vérifiez que l’URL de l’application figure dans la liste des **sites de confiance** du navigateur de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="de7a7-112">Make sure the user’s browser has added the URL of the application to its **trusted sites**.</span></span>

-   <span data-ttu-id="de7a7-113">Vérifiez que l’application est **configurée** correctement.</span><span class="sxs-lookup"><span data-stu-id="de7a7-113">Make sure to check the application is **configured** correctly.</span></span>

-   <span data-ttu-id="de7a7-114">Vérifiez que les connexions sont **activées** dans le compte de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="de7a7-114">Make sure the user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="de7a7-115">Vérifiez que le compte d’utilisateur **n’est pas verrouillé**.</span><span class="sxs-lookup"><span data-stu-id="de7a7-115">Make sure the user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="de7a7-116">Vérifiez que le **mot de passe de l’utilisateur n’a pas expiré ou qu’il n’a pas été oublié**.</span><span class="sxs-lookup"><span data-stu-id="de7a7-116">Make sure the user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="de7a7-117">Vérifiez que **Multi-Factor Authentication** ne bloque pas l’accès utilisateur.</span><span class="sxs-lookup"><span data-stu-id="de7a7-117">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="de7a7-118">Vérifiez qu’une **stratégie d’accès conditionnel** ou **stratégie de protection d’identité** ne bloque pas l’accès utilisateur.</span><span class="sxs-lookup"><span data-stu-id="de7a7-118">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="de7a7-119">Vérifiez que les **informations de contact d’authentification** de l’utilisateur sont à jour et permettent d’appliquer les stratégies d’accès conditionnel ou de Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="de7a7-119">Make sure that a user’s **authentication contact info** is up to date to allow Multi-Factor Authentication or Conditional Access policies to be enforced.</span></span>

-   <span data-ttu-id="de7a7-120">Essayez également d’effacer les cookies de votre navigateur, puis réessayez de vous connecter.</span><span class="sxs-lookup"><span data-stu-id="de7a7-120">Make sure to also try clearing your browser’s cookies and trying to sign in again.</span></span>

## <a name="checking-the-deeplink"></a><span data-ttu-id="de7a7-121">Vérification du lien profond</span><span class="sxs-lookup"><span data-stu-id="de7a7-121">Checking the deeplink</span></span>

<span data-ttu-id="de7a7-122">Pour vérifier si vous avez le lien profond correct, effectuez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="de7a7-122">To check if you have the correct deeplink, follow the steps below:</span></span>

1.  <span data-ttu-id="de7a7-123">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général** ou **coadministrateur**.</span><span class="sxs-lookup"><span data-stu-id="de7a7-123">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="de7a7-124">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="de7a7-124">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="de7a7-125">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="de7a7-125">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="de7a7-126">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="de7a7-126">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="de7a7-127">Cliquez sur **Toutes les applications** pour afficher la liste complète de vos applications.</span><span class="sxs-lookup"><span data-stu-id="de7a7-127">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="de7a7-128">Si l’application que vous recherchez ne figure pas dans la liste, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="de7a7-128">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="de7a7-129">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général** ou **coadministrateur**.</span><span class="sxs-lookup"><span data-stu-id="de7a7-129">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

7.  <span data-ttu-id="de7a7-130">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="de7a7-130">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

8.  <span data-ttu-id="de7a7-131">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="de7a7-131">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

9.  <span data-ttu-id="de7a7-132">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="de7a7-132">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

10. <span data-ttu-id="de7a7-133">Cliquez sur **Toutes les applications** pour afficher la liste complète de vos applications.</span><span class="sxs-lookup"><span data-stu-id="de7a7-133">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="de7a7-134">Si l’application que vous recherchez ne figure pas dans la liste, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="de7a7-134">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

11. <span data-ttu-id="de7a7-135">Sélectionnez l’application pour laquelle vous souhaitez vérifier le lien profond.</span><span class="sxs-lookup"><span data-stu-id="de7a7-135">Select the application you want the check the deeplink for.</span></span>

12. <span data-ttu-id="de7a7-136">Recherchez l’étiquette **URL d’accès utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="de7a7-136">Find the label **User Access URL**.</span></span> <span data-ttu-id="de7a7-137">Votre lien profond doit correspondre à cette URL.</span><span class="sxs-lookup"><span data-stu-id="de7a7-137">You deeplink should match this URL.</span></span>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="de7a7-138">Comment installer l’extension de navigateur du volet d’accès</span><span class="sxs-lookup"><span data-stu-id="de7a7-138">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="de7a7-139">Pour installer l’extension de navigateur du volet d’accès, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="de7a7-139">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="de7a7-140">Ouvrez le [volet d’accès](https://myapps.microsoft.com) dans l’un des navigateurs pris en charge et connectez-vous en tant **qu’utilisateur** dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="de7a7-140">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="de7a7-141">Cliquez sur une **application avec authentification unique par mot de passe** dans le volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="de7a7-141">click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="de7a7-142">Dans l’invite vous demandant d’installer le logiciel, sélectionnez **Installer maintenant**.</span><span class="sxs-lookup"><span data-stu-id="de7a7-142">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="de7a7-143">Vous êtes redirigé vers le lien de téléchargement selon votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="de7a7-143">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="de7a7-144">**Ajoutez** l’extension à votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="de7a7-144">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="de7a7-145">Si votre navigateur vous le demande, sélectionnez l’option **Activer** ou **Autoriser** pour l’extension.</span><span class="sxs-lookup"><span data-stu-id="de7a7-145">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="de7a7-146">Une fois l’extension installée, **redémarrez** votre session de navigateur.</span><span class="sxs-lookup"><span data-stu-id="de7a7-146">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="de7a7-147">Connectez-vous au volet d’accès et essayez de **lancer** vos applications à authentification unique par mot de passe.</span><span class="sxs-lookup"><span data-stu-id="de7a7-147">Sign in into the Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="de7a7-148">Vous pouvez également télécharger l’extension pour Chrome et Firefox à partir des liens directs ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="de7a7-148">You may also download the extension for Chrome and Firefox from the direct links below:</span></span>

-   [<span data-ttu-id="de7a7-149">Extension du volet d’accès pour Chrome</span><span class="sxs-lookup"><span data-stu-id="de7a7-149">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="de7a7-150">Extension du volet d’accès pour Firefox</span><span class="sxs-lookup"><span data-stu-id="de7a7-150">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-to-configure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="de7a7-151">Comment configurer l’authentification unique par mot de passe pour une application de la galerie Azure AD</span><span class="sxs-lookup"><span data-stu-id="de7a7-151">How to configure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="de7a7-152">Pour configurer une application à partir de la galerie Azure AD, vous devez effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="de7a7-152">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="de7a7-153">Ajouter une application à partir de la galerie Azure AD</span><span class="sxs-lookup"><span data-stu-id="de7a7-153">Add an application from the Azure AD gallery</span></span>](#add-an-application-from-the-Azure-AD-gallery)

-   [<span data-ttu-id="de7a7-154">Configurer l’application pour l’authentification unique par mot de passe</span><span class="sxs-lookup"><span data-stu-id="de7a7-154">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="de7a7-155">Ajouter une application à partir de la galerie Azure AD</span><span class="sxs-lookup"><span data-stu-id="de7a7-155">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="de7a7-156">Pour ajouter une application à partir de la galerie Azure AD, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="de7a7-156">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="de7a7-157">Ouvrez le [portail Azure](https://portal.azure.com) et connectez-vous en tant qu’**administrateur général** ou **coadministrateur**.</span><span class="sxs-lookup"><span data-stu-id="de7a7-157">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="de7a7-158">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="de7a7-158">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="de7a7-159">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="de7a7-159">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="de7a7-160">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="de7a7-160">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="de7a7-161">Cliquez sur le bouton **Ajouter** dans le coin supérieur droit du panneau **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="de7a7-161">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="de7a7-162">Dans la zone de texte **Entrer un nom** de la section **Ajouter à partir de la galerie**, tapez le nom de l’application.</span><span class="sxs-lookup"><span data-stu-id="de7a7-162">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="de7a7-163">Sélectionnez l’application pour laquelle vous souhaitez configurer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="de7a7-163">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="de7a7-164">Avant d’ajouter l’application, vous pouvez la renommer dans la zone de texte **Nom**.</span><span class="sxs-lookup"><span data-stu-id="de7a7-164">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="de7a7-165">Pour ajouter l’application, cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="de7a7-165">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="de7a7-166">Après une courte période, vous pouvez voir le panneau de configuration de l’application.</span><span class="sxs-lookup"><span data-stu-id="de7a7-166">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="de7a7-167">Configurer l’application pour l’authentification unique par mot de passe</span><span class="sxs-lookup"><span data-stu-id="de7a7-167">Configure the application for password single sign-on</span></span>

<span data-ttu-id="de7a7-168">Pour configurer l’authentification unique pour une application, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="de7a7-168">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="de7a7-169">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général** ou **coadministrateur**</span><span class="sxs-lookup"><span data-stu-id="de7a7-169">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="de7a7-170">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="de7a7-170">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="de7a7-171">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="de7a7-171">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="de7a7-172">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="de7a7-172">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="de7a7-173">Cliquez sur **Toutes les applications** pour afficher la liste complète de vos applications.</span><span class="sxs-lookup"><span data-stu-id="de7a7-173">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="de7a7-174">Si l’application que vous recherchez ne figure pas dans la liste, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications.**</span><span class="sxs-lookup"><span data-stu-id="de7a7-174">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="de7a7-175">Sélectionnez l’application pour laquelle vous souhaitez configurer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="de7a7-175">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="de7a7-176">Une fois l’application chargée, cliquez sur **Authentification unique** dans le menu de navigation de gauche de l’application.</span><span class="sxs-lookup"><span data-stu-id="de7a7-176">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="de7a7-177">Sélectionnez le mode **Authentification par mot de passe.**</span><span class="sxs-lookup"><span data-stu-id="de7a7-177">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="de7a7-178">[Affectez des utilisateurs à l’application](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="de7a7-178">[Assign users to the application](#how-to-assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="de7a7-179">En outre, vous pouvez également fournir des informations d’identification pour le compte de l’utilisateur en sélectionnant les lignes des utilisateurs, en cliquant sur **Mettre à jour les informations d’identification** et en entrant le nom d’utilisateur et le mot de passe à la place des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="de7a7-179">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="de7a7-180">Autrement, les utilisateurs devront entrer les informations d’identification eux-mêmes lors du lancement.</span><span class="sxs-lookup"><span data-stu-id="de7a7-180">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="de7a7-181">Comment configurer l’authentification unique par mot de passe pour une application ne figurant pas dans la galerie</span><span class="sxs-lookup"><span data-stu-id="de7a7-181">How to configure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="de7a7-182">Pour configurer une application à partir de la galerie Azure AD, vous devez effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="de7a7-182">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="de7a7-183">Ajouter une application ne figurant pas dans la galerie</span><span class="sxs-lookup"><span data-stu-id="de7a7-183">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="de7a7-184">Configurer l’application pour l’authentification unique par mot de passe</span><span class="sxs-lookup"><span data-stu-id="de7a7-184">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="de7a7-185">Ajouter une application ne figurant pas dans la galerie</span><span class="sxs-lookup"><span data-stu-id="de7a7-185">Add a non-gallery application</span></span>

<span data-ttu-id="de7a7-186">Pour ajouter une application à partir de la galerie Azure AD, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="de7a7-186">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="de7a7-187">Ouvrez le [portail Azure](https://portal.azure.com) et connectez-vous en tant qu’**administrateur général** ou **coadministrateur**.</span><span class="sxs-lookup"><span data-stu-id="de7a7-187">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="de7a7-188">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="de7a7-188">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="de7a7-189">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="de7a7-189">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="de7a7-190">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="de7a7-190">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="de7a7-191">Cliquez sur le bouton **Ajouter** dans le coin supérieur droit du panneau **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="de7a7-191">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="de7a7-192">Cliquez sur **Application ne figurant pas dans la galerie.**</span><span class="sxs-lookup"><span data-stu-id="de7a7-192">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="de7a7-193">Entrez le nom de votre application dans la zone de texte **Nom**.</span><span class="sxs-lookup"><span data-stu-id="de7a7-193">Enter the name of your application in the **Name** textbox.</span></span> <span data-ttu-id="de7a7-194">Sélectionnez **Ajouter.**</span><span class="sxs-lookup"><span data-stu-id="de7a7-194">Select **Add.**</span></span>

<span data-ttu-id="de7a7-195">Après une courte période, vous pourrez voir le panneau de configuration de l’application.</span><span class="sxs-lookup"><span data-stu-id="de7a7-195">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="de7a7-196">Configurer l’application pour l’authentification unique par mot de passe</span><span class="sxs-lookup"><span data-stu-id="de7a7-196">Configure the application for password single sign-on</span></span>

<span data-ttu-id="de7a7-197">Pour configurer l’authentification unique pour une application, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="de7a7-197">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="de7a7-198">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général** ou **coadministrateur**</span><span class="sxs-lookup"><span data-stu-id="de7a7-198">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="de7a7-199">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="de7a7-199">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="de7a7-200">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="de7a7-200">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="de7a7-201">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="de7a7-201">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="de7a7-202">Cliquez sur **Toutes les applications** pour afficher la liste complète de vos applications.</span><span class="sxs-lookup"><span data-stu-id="de7a7-202">click **All Applications** to view a list of all your applications.</span></span>

    1.  <span data-ttu-id="de7a7-203">Si l’application que vous recherchez ne figure pas dans la liste, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications.**</span><span class="sxs-lookup"><span data-stu-id="de7a7-203">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="de7a7-204">Sélectionnez l’application pour laquelle vous souhaitez configurer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="de7a7-204">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="de7a7-205">Une fois l’application chargée, cliquez sur **Authentification unique** dans le menu de navigation de gauche de l’application.</span><span class="sxs-lookup"><span data-stu-id="de7a7-205">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="de7a7-206">Sélectionnez le mode **Authentification par mot de passe.**</span><span class="sxs-lookup"><span data-stu-id="de7a7-206">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="de7a7-207">Entrez **l’URL de connexion**.</span><span class="sxs-lookup"><span data-stu-id="de7a7-207">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="de7a7-208">Il s’agit de l’URL où les utilisateurs entrent leurs nom d’utilisateur et mot de passe pour se connecter.</span><span class="sxs-lookup"><span data-stu-id="de7a7-208">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="de7a7-209">Vérifiez que les champs de connexion sont visibles dans l’URL.</span><span class="sxs-lookup"><span data-stu-id="de7a7-209">Ensure the sign in fields are visible at the URL.</span></span>

10. <span data-ttu-id="de7a7-210">Affectez des utilisateurs à l’application.</span><span class="sxs-lookup"><span data-stu-id="de7a7-210">Assign users to the application.</span></span>

11. <span data-ttu-id="de7a7-211">En outre, vous pouvez également fournir des informations d’identification pour le compte de l’utilisateur en sélectionnant les lignes des utilisateurs, en cliquant sur **Mettre à jour les informations d’identification** et en entrant le nom d’utilisateur et le mot de passe à la place des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="de7a7-211">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="de7a7-212">Autrement, les utilisateurs devront entrer les informations d’identification eux-mêmes lors du lancement.</span><span class="sxs-lookup"><span data-stu-id="de7a7-212">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="how-to-assign-a-user-to-an-application-directly"></a><span data-ttu-id="de7a7-213">Comment affecter un utilisateur directement à une application</span><span class="sxs-lookup"><span data-stu-id="de7a7-213">How to assign a user to an application directly</span></span>

<span data-ttu-id="de7a7-214">Pour affecter un ou plusieurs utilisateurs directement à une application, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="de7a7-214">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="de7a7-215">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général.**</span><span class="sxs-lookup"><span data-stu-id="de7a7-215">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="de7a7-216">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="de7a7-216">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="de7a7-217">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="de7a7-217">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="de7a7-218">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="de7a7-218">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="de7a7-219">Cliquez sur **Toutes les applications** pour afficher la liste complète de vos applications.</span><span class="sxs-lookup"><span data-stu-id="de7a7-219">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="de7a7-220">Si l’application que vous recherchez ne figure pas dans la liste, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications.**</span><span class="sxs-lookup"><span data-stu-id="de7a7-220">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="de7a7-221">Dans la liste qui s’affiche, sélectionnez l’application à laquelle vous souhaitez affecter un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="de7a7-221">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="de7a7-222">Une fois l’application chargée, cliquez sur **Utilisateurs et groupes** dans le menu de navigation de gauche de l’application.</span><span class="sxs-lookup"><span data-stu-id="de7a7-222">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="de7a7-223">Cliquez sur le bouton **Ajouter** en haut de la liste **Utilisateurs et groupes** pour ouvrir le panneau **Ajouter une attribution**.</span><span class="sxs-lookup"><span data-stu-id="de7a7-223">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="de7a7-224">Cliquez sur le sélecteur **Utilisateurs et groupes** à partir du panneau **Ajouter une attribution**.</span><span class="sxs-lookup"><span data-stu-id="de7a7-224">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="de7a7-225">Tapez **le nom complet** ou **l’adresse de messagerie** de l’utilisateur souhaité pour l’attribution dans la zone de recherche **Rechercher par nom ou adresse de messagerie**.</span><span class="sxs-lookup"><span data-stu-id="de7a7-225">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="de7a7-226">Pointez sur **l’utilisateur** dans la liste pour afficher une **case à cocher**.</span><span class="sxs-lookup"><span data-stu-id="de7a7-226">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="de7a7-227">Cliquez sur la case à cocher en regard de la photo de profil ou du logo de l’utilisateur pour ajouter ce dernier à la liste **Sélectionné**.</span><span class="sxs-lookup"><span data-stu-id="de7a7-227">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="de7a7-228">**Facultatif :** si vous souhaitez **ajouter plusieurs utilisateurs**, entrez un autre **nom complet** ou une autre **adresse de messagerie** dans la zone de recherche **Rechercher par nom ou adresse de messagerie**, puis cliquez sur la case à cocher pour ajouter cet utilisateur à la liste **Sélectionné**.</span><span class="sxs-lookup"><span data-stu-id="de7a7-228">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="de7a7-229">Après avoir sélectionné les utilisateurs, cliquez sur le bouton **Sélectionner** pour les ajouter à la liste des utilisateurs et des groupes à affecter à l’application.</span><span class="sxs-lookup"><span data-stu-id="de7a7-229">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="de7a7-230">**Facultatif :** cliquez sur le sélecteur **Sélectionner un rôle** dans le panneau **Ajouter une attribution** pour sélectionner un rôle à affecter aux utilisateurs que vous avez sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="de7a7-230">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="de7a7-231">Cliquez sur le bouton **Attribuer** pour affecter l’application aux utilisateurs sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="de7a7-231">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="de7a7-232">Après une courte période, les utilisateurs que vous avez sélectionnés sont en mesure de lancer ces applications dans le volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="de7a7-232">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-the-resolve-the-issue"></a><span data-ttu-id="de7a7-233">Si ces étapes de dépannage ne résolvent pas le problème,</span><span class="sxs-lookup"><span data-stu-id="de7a7-233">If these troubleshooting steps do not the resolve the issue.</span></span> 

<span data-ttu-id="de7a7-234">créez un ticket de support en fournissant les informations suivantes, si disponibles :</span><span class="sxs-lookup"><span data-stu-id="de7a7-234">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="de7a7-235">ID d’erreur de corrélation</span><span class="sxs-lookup"><span data-stu-id="de7a7-235">Correlation error ID</span></span>

-   <span data-ttu-id="de7a7-236">UPN (adresse e-mail de l’utilisateur)</span><span class="sxs-lookup"><span data-stu-id="de7a7-236">UPN (user email address)</span></span>

-   <span data-ttu-id="de7a7-237">ID de locataire</span><span class="sxs-lookup"><span data-stu-id="de7a7-237">TenantID</span></span>

-   <span data-ttu-id="de7a7-238">Type de navigateur</span><span class="sxs-lookup"><span data-stu-id="de7a7-238">Browser type</span></span>

-   <span data-ttu-id="de7a7-239">Fuseau horaire et heure/période à laquelle l’erreur se produit</span><span class="sxs-lookup"><span data-stu-id="de7a7-239">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="de7a7-240">Traces Fiddler</span><span class="sxs-lookup"><span data-stu-id="de7a7-240">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="de7a7-241">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="de7a7-241">Next steps</span></span>
[<span data-ttu-id="de7a7-242">Fournir une authentification unique à vos applications avec le proxy d’application</span><span class="sxs-lookup"><span data-stu-id="de7a7-242">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
