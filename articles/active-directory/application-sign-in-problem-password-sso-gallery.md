---
title: "Problèmes de connexion à une application de la galerie Azure AD configurée pour l’authentification unique fédérée | Microsoft Docs"
description: "Comment résoudre les problèmes de connexion à une application de la galerie Azure AD configurée pour l’authentification unique par mot de passe"
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
ms.openlocfilehash: f8521d1386bba8004e84fe8862a5f59a65ea19ad
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-an-azure-ad-gallery-application-configured-for-federated-single-sign-on"></a><span data-ttu-id="1eb46-103">Problèmes de connexion à une application de la galerie Azure AD configurée pour l’authentification unique fédérée</span><span class="sxs-lookup"><span data-stu-id="1eb46-103">Problems signing in to an Azure AD Gallery application configured for federated single sign-on</span></span>

<span data-ttu-id="1eb46-104">Le volet d’accès est un portail web qui permet à un utilisateur disposant d’un compte professionnel ou scolaire dans Azure Active Directory (Azure AD) d’afficher et de lancer des applications basées sur le cloud auxquelles l’administrateur Azure AD lui a accordé un accès.</span><span class="sxs-lookup"><span data-stu-id="1eb46-104">The Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) to view and launch cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="1eb46-105">Un utilisateur disposant d’éditions Azure AD peut également utiliser des fonctionnalités de gestion de groupes et d’applications en libre-service par le biais du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="1eb46-105">A user who has Azure AD editions can also use self-service group and app management capabilities through the Access Panel.</span></span> <span data-ttu-id="1eb46-106">Le volet d’accès est distinct du portail Azure et n’exige pas des utilisateurs qu’ils aient un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="1eb46-106">The Access Panel is separate from the Azure portal and does not require users to have an Azure subscription.</span></span>

<span data-ttu-id="1eb46-107">Pour utiliser l’authentification unique (SSO) par mot de passe dans le volet d’accès, l’extension du volet d’accès doit être installée dans le navigateur de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1eb46-107">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="1eb46-108">Cette extension est téléchargée automatiquement lorsqu’un utilisateur sélectionne une application configurée pour l’authentification unique (SSO) avec mot de passe.</span><span class="sxs-lookup"><span data-stu-id="1eb46-108">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

## <a name="meeting-browser-requirements-for-the-access-panel"></a><span data-ttu-id="1eb46-109">Configuration requise du navigateur pour le volet d’accès</span><span class="sxs-lookup"><span data-stu-id="1eb46-109">Meeting browser requirements for the Access Panel</span></span>

<span data-ttu-id="1eb46-110">Le volet d’accès nécessite un navigateur qui prend en charge JavaScript et dans lequel le CSS est activé.</span><span class="sxs-lookup"><span data-stu-id="1eb46-110">The Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="1eb46-111">Pour utiliser l’authentification unique (SSO) par mot de passe dans le volet d’accès, l’extension du volet d’accès doit être installée dans le navigateur de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1eb46-111">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="1eb46-112">Cette extension est téléchargée automatiquement lorsqu’un utilisateur sélectionne une application configurée pour l’authentification unique (SSO) avec mot de passe.</span><span class="sxs-lookup"><span data-stu-id="1eb46-112">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="1eb46-113">Pour l’authentification unique par mot de passe, les navigateurs de l’utilisateur final peuvent être :</span><span class="sxs-lookup"><span data-stu-id="1eb46-113">For password-based SSO, the end user’s browsers can be:</span></span>

-   <span data-ttu-id="1eb46-114">Internet Explorer 8, 9, 10, 11 -- sur Windows 7 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="1eb46-114">Internet Explorer 8, 9, 10, 11 - on Windows 7 or later</span></span>

-   <span data-ttu-id="1eb46-115">Chrome -- sur Windows 7 ou ultérieur, et sur Mac OS X ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="1eb46-115">Chrome - on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="1eb46-116">Firefox 26.0 ou ultérieur -- sur Windows XP SP2 ou version ultérieure, et sur Mac OS X 10.6 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="1eb46-116">Firefox 26.0 or later - on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

>[!NOTE]
><span data-ttu-id="1eb46-117">L’extension de l’authentification unique par mot de passe sera disponible pour Edge dans Windows 10 quand les extensions de navigateur seront prises en charge pour Edge.</span><span class="sxs-lookup"><span data-stu-id="1eb46-117">The password-based SSO extension become available for Edge in Windows 10 when browser extensions become supported for Edge.</span></span>
>
>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="1eb46-118">Comment installer l’extension de navigateur du volet d’accès</span><span class="sxs-lookup"><span data-stu-id="1eb46-118">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="1eb46-119">Pour installer l’extension de navigateur du volet d’accès, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="1eb46-119">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="1eb46-120">Ouvrez le [volet d’accès](https://myapps.microsoft.com) dans l’un des navigateurs pris en charge et connectez-vous en tant **qu’utilisateur** dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1eb46-120">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="1eb46-121">Cliquez sur une **application avec authentification unique par mot de passe** dans le volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="1eb46-121">click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="1eb46-122">Dans l’invite vous demandant d’installer le logiciel, sélectionnez **Installer maintenant**.</span><span class="sxs-lookup"><span data-stu-id="1eb46-122">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="1eb46-123">Vous êtes redirigé vers le lien de téléchargement selon votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="1eb46-123">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="1eb46-124">**Ajoutez** l’extension à votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="1eb46-124">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="1eb46-125">Si votre navigateur vous le demande, sélectionnez l’option **Activer** ou **Autoriser** pour l’extension.</span><span class="sxs-lookup"><span data-stu-id="1eb46-125">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="1eb46-126">Une fois l’extension installée, **redémarrez** votre session de navigateur.</span><span class="sxs-lookup"><span data-stu-id="1eb46-126">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="1eb46-127">Connectez-vous au volet d’accès et essayez de **lancer** vos applications à authentification unique par mot de passe.</span><span class="sxs-lookup"><span data-stu-id="1eb46-127">Sign in into the Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="1eb46-128">Vous pouvez également télécharger l’extension pour Chrome et Firefox à partir des liens directs ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1eb46-128">You may also download the extension for Chrome and Firefox from the direct links below:</span></span>

-   [<span data-ttu-id="1eb46-129">Extension du volet d’accès pour Chrome</span><span class="sxs-lookup"><span data-stu-id="1eb46-129">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="1eb46-130">Extension du volet d’accès pour Firefox</span><span class="sxs-lookup"><span data-stu-id="1eb46-130">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="setting-up-a-group-policy-for-internet-explorer"></a><span data-ttu-id="1eb46-131">Configuration d’une stratégie de groupe pour Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="1eb46-131">Setting up a group policy for Internet Explorer</span></span>

<span data-ttu-id="1eb46-132">Vous pouvez configurer une stratégie de groupe pour installer à distance l’extension du volet d’accès pour Internet Explorer sur les ordinateurs de vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="1eb46-132">You can setup a group policy that allow you to remotely install the Access Panel extension for Internet Explorer on your users' machines.</span></span>

<span data-ttu-id="1eb46-133">Vous devez respecter certaines conditions préalables, notamment les suivantes :</span><span class="sxs-lookup"><span data-stu-id="1eb46-133">The prerequisites include:</span></span>

-   <span data-ttu-id="1eb46-134">Vous avez configuré les [services de domaine Active Directory](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx)et vous avez joint les ordinateurs de vos utilisateurs à votre domaine.</span><span class="sxs-lookup"><span data-stu-id="1eb46-134">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines to your domain.</span></span>

-   <span data-ttu-id="1eb46-135">Vous devez disposer de l’autorisation « Modifier les paramètres » pour modifier l’objet de stratégie de groupe (GPO).</span><span class="sxs-lookup"><span data-stu-id="1eb46-135">You must have the "Edit settings" permission to edit the Group Policy Object (GPO).</span></span> <span data-ttu-id="1eb46-136">Par défaut, les membres des groupes de sécurité suivants jouissent de cette autorisation : administrateurs de domaine, administrateurs d’entreprise et propriétaires créateurs de la stratégie de groupe.</span><span class="sxs-lookup"><span data-stu-id="1eb46-136">By default, members of the following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> <span data-ttu-id="1eb46-137">[En savoir plus](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="1eb46-137">[Learn more](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span></span>

<span data-ttu-id="1eb46-138">Suivez le didacticiel [Déploiement de l’extension du volet d’accès pour Internet Explorer à l’aide de la stratégie de groupe](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) pour obtenir des instructions pas à pas sur la configuration et le déploiement d’une stratégie de groupe.</span><span class="sxs-lookup"><span data-stu-id="1eb46-138">Follow the tutorial [How to Deploy the Access Panel Extension for Internet Explorer using Group Policy](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) for step by step instructions on how to configure the group policy and deploy it to users.</span></span>

## <a name="troubleshoot-the-access-panel-in-internet-explorer"></a><span data-ttu-id="1eb46-139">Résolution des problèmes liés au volet d’accès dans Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="1eb46-139">Troubleshoot the Access Panel in Internet Explorer</span></span>

<span data-ttu-id="1eb46-140">Consultez le guide [Résolution des problèmes liés à l’extension Volet d’accès pour Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) pour accéder à un outil de diagnostic et pour obtenir des instructions pas à pas sur la configuration de l’extension pour Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="1eb46-140">Follow the [Troubleshoot the Access Panel Extension for Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) guide for access a diagnostics tool and step by step instructions on configuring the extension for IE.</span></span>

## <a name="how-to-configure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="1eb46-141">Comment configurer l’authentification unique par mot de passe pour une application de la galerie Azure AD</span><span class="sxs-lookup"><span data-stu-id="1eb46-141">How to configure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="1eb46-142">Pour configurer une application à partir de la galerie Azure AD, vous devez effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="1eb46-142">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="1eb46-143">Ajouter une application à partir de la galerie Azure AD</span><span class="sxs-lookup"><span data-stu-id="1eb46-143">Add an application from the Azure AD gallery</span></span>](#_Add_an_application)

-   [<span data-ttu-id="1eb46-144">Configurer l’application pour l’authentification unique par mot de passe</span><span class="sxs-lookup"><span data-stu-id="1eb46-144">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="1eb46-145">Affecter des utilisateurs à l’application</span><span class="sxs-lookup"><span data-stu-id="1eb46-145">Assign users to the application</span></span>](#assign-users-to-the-application)

### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="1eb46-146">Ajouter une application à partir de la galerie Azure AD</span><span class="sxs-lookup"><span data-stu-id="1eb46-146">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="1eb46-147">Pour ajouter une application à partir de la galerie Azure AD, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="1eb46-147">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="1eb46-148">Ouvrez le [portail Azure](https://portal.azure.com) et connectez-vous en tant qu’**administrateur général** ou **coadministrateur**</span><span class="sxs-lookup"><span data-stu-id="1eb46-148">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="1eb46-149">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="1eb46-149">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1eb46-150">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1eb46-150">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1eb46-151">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1eb46-151">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1eb46-152">Cliquez sur le bouton **Ajouter** dans le coin supérieur droit du panneau **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="1eb46-152">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="1eb46-153">Dans la zone de texte **Entrer un nom** de la section **Ajouter à partir de la galerie**, tapez le nom de l’application.</span><span class="sxs-lookup"><span data-stu-id="1eb46-153">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="1eb46-154">Sélectionnez l’application pour laquelle vous souhaitez configurer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="1eb46-154">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="1eb46-155">Avant d’ajouter l’application, vous pouvez la renommer dans la zone de texte **Nom**.</span><span class="sxs-lookup"><span data-stu-id="1eb46-155">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="1eb46-156">Pour ajouter l’application, cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="1eb46-156">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="1eb46-157">Après une courte période, vous pouvez voir le panneau de configuration de l’application.</span><span class="sxs-lookup"><span data-stu-id="1eb46-157">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="1eb46-158">Configurer l’application pour l’authentification unique par mot de passe</span><span class="sxs-lookup"><span data-stu-id="1eb46-158">Configure the application for password single sign-on</span></span>

<span data-ttu-id="1eb46-159">Pour configurer l’authentification unique pour une application, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="1eb46-159">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="1eb46-160">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général** ou **coadministrateur**</span><span class="sxs-lookup"><span data-stu-id="1eb46-160">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="1eb46-161">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="1eb46-161">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1eb46-162">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1eb46-162">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1eb46-163">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1eb46-163">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1eb46-164">Cliquez sur **Toutes les applications** pour afficher la liste complète de vos applications.</span><span class="sxs-lookup"><span data-stu-id="1eb46-164">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="1eb46-165">Si l’application que vous recherchez ne figure pas dans la liste, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1eb46-165">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="1eb46-166">Sélectionnez l’application pour laquelle vous souhaitez configurer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="1eb46-166">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="1eb46-167">Une fois l’application chargée, cliquez sur **Authentification unique** dans le menu de navigation gauche de l’application.</span><span class="sxs-lookup"><span data-stu-id="1eb46-167">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="1eb46-168">Sélectionnez le mode **Authentification par mot de passe.**</span><span class="sxs-lookup"><span data-stu-id="1eb46-168">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="1eb46-169">[Affectez des utilisateurs à l’application](#_How_to_assign).</span><span class="sxs-lookup"><span data-stu-id="1eb46-169">[Assign users to the application](#_How_to_assign).</span></span>

10. <span data-ttu-id="1eb46-170">En outre, vous pouvez également fournir des informations d’identification pour le compte de l’utilisateur en sélectionnant les lignes des utilisateurs, en cliquant sur **Mettre à jour les informations d’identification** et en entrant le nom d’utilisateur et le mot de passe à la place des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="1eb46-170">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="1eb46-171">Autrement, les utilisateurs devront entrer les informations d’identification eux-mêmes lors du lancement.</span><span class="sxs-lookup"><span data-stu-id="1eb46-171">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

### <a name="assign-users-to-the-application"></a><span data-ttu-id="1eb46-172">Affecter des utilisateurs à l’application</span><span class="sxs-lookup"><span data-stu-id="1eb46-172">Assign users to the application</span></span>

<span data-ttu-id="1eb46-173">Pour affecter un ou plusieurs utilisateurs directement à une application, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="1eb46-173">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="1eb46-174">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général.**</span><span class="sxs-lookup"><span data-stu-id="1eb46-174">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1eb46-175">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="1eb46-175">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1eb46-176">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1eb46-176">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1eb46-177">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1eb46-177">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1eb46-178">Cliquez sur **Toutes les applications** pour afficher la liste complète de vos applications.</span><span class="sxs-lookup"><span data-stu-id="1eb46-178">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="1eb46-179">Si l’application que vous recherchez ne figure pas dans la liste, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications.**</span><span class="sxs-lookup"><span data-stu-id="1eb46-179">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="1eb46-180">Dans la liste qui s’affiche, sélectionnez l’application à laquelle vous souhaitez affecter un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1eb46-180">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="1eb46-181">Une fois l’application chargée, cliquez sur **Utilisateurs et groupes** dans le menu de navigation de gauche de l’application.</span><span class="sxs-lookup"><span data-stu-id="1eb46-181">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="1eb46-182">Cliquez sur le bouton **Ajouter** en haut de la liste **Utilisateurs et groupes** pour ouvrir le panneau **Ajouter une attribution**.</span><span class="sxs-lookup"><span data-stu-id="1eb46-182">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="1eb46-183">Cliquez sur le sélecteur **Utilisateurs et groupes** à partir du panneau **Ajouter une attribution**.</span><span class="sxs-lookup"><span data-stu-id="1eb46-183">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="1eb46-184">Tapez **le nom complet** ou **l’adresse de messagerie** de l’utilisateur souhaité pour l’attribution dans la zone de recherche **Rechercher par nom ou adresse de messagerie**.</span><span class="sxs-lookup"><span data-stu-id="1eb46-184">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="1eb46-185">Pointez sur **l’utilisateur** dans la liste pour afficher une **case à cocher**.</span><span class="sxs-lookup"><span data-stu-id="1eb46-185">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="1eb46-186">Cliquez sur la case à cocher en regard de la photo de profil ou du logo de l’utilisateur pour ajouter ce dernier à la liste **Sélectionné**.</span><span class="sxs-lookup"><span data-stu-id="1eb46-186">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="1eb46-187">**Facultatif :** si vous souhaitez **ajouter plusieurs utilisateurs**, entrez un autre **nom complet** ou une autre **adresse de messagerie** dans la zone de recherche **Rechercher par nom ou adresse de messagerie**, puis cliquez sur la case à cocher pour ajouter cet utilisateur à la liste **Sélectionné**.</span><span class="sxs-lookup"><span data-stu-id="1eb46-187">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="1eb46-188">Après avoir sélectionné les utilisateurs, cliquez sur le bouton **Sélectionner** pour les ajouter à la liste des utilisateurs et des groupes à affecter à l’application.</span><span class="sxs-lookup"><span data-stu-id="1eb46-188">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="1eb46-189">**Facultatif :** cliquez sur le sélecteur **Sélectionner un rôle** dans le panneau **Ajouter une attribution** pour sélectionner un rôle à affecter aux utilisateurs que vous avez sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="1eb46-189">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="1eb46-190">Cliquez sur le bouton **Attribuer** pour affecter l’application aux utilisateurs sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="1eb46-190">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="1eb46-191">Après une courte période, les utilisateurs que vous avez sélectionnés sont en mesure de lancer ces applications dans le volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="1eb46-191">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="if-these-troubleshoot-steps-dont-resolve-the-issue"></a><span data-ttu-id="1eb46-192">Si ces étapes de dépannage ne résolvent pas le problème</span><span class="sxs-lookup"><span data-stu-id="1eb46-192">If these troubleshoot steps don't resolve the issue</span></span> 
<span data-ttu-id="1eb46-193">Créez un ticket de support en fournissant les informations suivantes, si disponibles :</span><span class="sxs-lookup"><span data-stu-id="1eb46-193">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="1eb46-194">ID d’erreur de corrélation</span><span class="sxs-lookup"><span data-stu-id="1eb46-194">Correlation error ID</span></span>

-   <span data-ttu-id="1eb46-195">UPN (adresse e-mail de l’utilisateur)</span><span class="sxs-lookup"><span data-stu-id="1eb46-195">UPN (user email address)</span></span>

-   <span data-ttu-id="1eb46-196">ID de locataire</span><span class="sxs-lookup"><span data-stu-id="1eb46-196">TenantID</span></span>

-   <span data-ttu-id="1eb46-197">Type de navigateur</span><span class="sxs-lookup"><span data-stu-id="1eb46-197">Browser type</span></span>

-   <span data-ttu-id="1eb46-198">Fuseau horaire et heure/période à laquelle l’erreur se produit</span><span class="sxs-lookup"><span data-stu-id="1eb46-198">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="1eb46-199">Traces Fiddler</span><span class="sxs-lookup"><span data-stu-id="1eb46-199">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="1eb46-200">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1eb46-200">Next steps</span></span>
[<span data-ttu-id="1eb46-201">Fournir une authentification unique à vos applications avec le proxy d’application</span><span class="sxs-lookup"><span data-stu-id="1eb46-201">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
