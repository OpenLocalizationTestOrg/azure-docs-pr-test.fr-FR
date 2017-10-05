---
title: "Présentation du volet d’accès dans Azure Active Directory ? | Microsoft Docs"
description: "Découvrez comment utiliser les différentes versions du volet d’accès (navigateur web, application Android, iPhone et iPad) pour accéder aux applications SaaS."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: c0252d01-7e6e-4f79-a70e-600479577dfd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bd9066c251188c0f18fe1a9403baa2beaeeb987c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="what-is-the-access-panel"></a><span data-ttu-id="c11eb-104">Présentation du volet d’accès</span><span class="sxs-lookup"><span data-stu-id="c11eb-104">What is the access panel?</span></span>

<span data-ttu-id="c11eb-105">Le volet d’accès est un portail basé sur le web.</span><span class="sxs-lookup"><span data-stu-id="c11eb-105">The access panel is a web-based portal.</span></span> <span data-ttu-id="c11eb-106">Il permet à un utilisateur qui dispose d’un compte professionnel ou scolaire dans Azure Active Directory d’afficher et de démarrer des applications basées sur le cloud auxquelles l’administrateur Azure AD lui a accordé un accès.</span><span class="sxs-lookup"><span data-stu-id="c11eb-106">It enables a user with a work or school account in Azure Active Directory to view and start cloud-based applications an Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="c11eb-107">Vous pouvez également utiliser des fonctionnalités de gestion de groupes et d’applications libre-service par le biais du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="c11eb-107">You can also use self-service group and app management capabilities through the access panel.</span></span>

<span data-ttu-id="c11eb-108">Le volet d’accès est distinct du portail Azure et n’exige pas un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="c11eb-108">The access panel is separate from the Azure portal and does not you to have an Azure subscription.</span></span>

![Volet d'accès][1]

<span data-ttu-id="c11eb-110">Le volet d’accès vous permet de modifier certains paramètres de profil, notamment :</span><span class="sxs-lookup"><span data-stu-id="c11eb-110">The access panel enables you to edit some of your profile settings, including the ability to:</span></span>

- <span data-ttu-id="c11eb-111">Changer le mot de passe associé à un compte professionnel ou scolaire</span><span class="sxs-lookup"><span data-stu-id="c11eb-111">Change the password associated with a work or school account</span></span>

- <span data-ttu-id="c11eb-112">Modifier les paramètres de réinitialisation de mot de passe</span><span class="sxs-lookup"><span data-stu-id="c11eb-112">Edit password reset settings</span></span>

- <span data-ttu-id="c11eb-113">Modifier les paramètres de contact et de préférence liés à l’authentification multifacteur (pour les comptes qui ont été contraints de l’utiliser par un administrateur)</span><span class="sxs-lookup"><span data-stu-id="c11eb-113">Edit contact and preference settings related to multi-factor authentication (for accounts that have been required to use it by an administrator)</span></span>

- <span data-ttu-id="c11eb-114">Afficher les détails de compte tels que l’ID d’utilisateur, l’adresse e-mail de secours, les numéros de téléphone mobile et de bureau et les appareils</span><span class="sxs-lookup"><span data-stu-id="c11eb-114">View account details, such as user ID, alternate email, and mobile and office phone numbers, and devices</span></span>

- <span data-ttu-id="c11eb-115">Afficher et démarrer des applications basées sur le cloud auxquelles l’administrateur Azure AD lui a accordé un accès</span><span class="sxs-lookup"><span data-stu-id="c11eb-115">View and start cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="c11eb-116">Pour plus d’informations sur le volet d’accès du point de vue de l’utilisateur, consultez Utilisation du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="c11eb-116">For more information about the access panel from the users’ perspective, see Using the access panel.</span></span> 

- <span data-ttu-id="c11eb-117">Gérer les groupes en libre-service.</span><span class="sxs-lookup"><span data-stu-id="c11eb-117">Self-manage groups.</span></span> <span data-ttu-id="c11eb-118">Plus précisément, l’administrateur peut créer et gérer des groupes de sécurité et demander l’appartenance à des groupes de sécurité dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c11eb-118">More specifically, the administrator can create and manage security groups and request security group memberships in Azure AD.</span></span> <span data-ttu-id="c11eb-119">Pour plus d’informations, consultez [Gestion de groupe libre-service pour les utilisateurs dans Azure AD](active-directory-accessmanagement-self-service-group-management.md) et [Gérer vos groupes](active-directory-manage-groups.md).</span><span class="sxs-lookup"><span data-stu-id="c11eb-119">For more information, see [Self-service group management for users in Azure AD](active-directory-accessmanagement-self-service-group-management.md) and [Manage your groups](active-directory-manage-groups.md).</span></span>




## <a name="accessing-the-access-panel"></a><span data-ttu-id="c11eb-120">Accès au volet d’accès</span><span class="sxs-lookup"><span data-stu-id="c11eb-120">Accessing the access panel</span></span>

<span data-ttu-id="c11eb-121">Vous pouvez accéder au volet d’accès en visitant l’URL suivante dans un navigateur web : `http://myapps.microsoft.com`</span><span class="sxs-lookup"><span data-stu-id="c11eb-121">You can access the access panel by visiting the following URL in a web browser: `http://myapps.microsoft.com`</span></span>

<span data-ttu-id="c11eb-122">Si vous avez configuré la personnalisation de votre page de connexion, vous pouvez charger cette personnalisation en ajoutant le domaine de votre organisation à la fin de l’URL : `http://myapps.microsoft.com/<your domain>.com`</span><span class="sxs-lookup"><span data-stu-id="c11eb-122">If you have custom branding configured for your sign-in page, you can load this branding by appending your organization’s domain to the end of the URL: `http://myapps.microsoft.com/<your domain>.com`</span></span>

<span data-ttu-id="c11eb-123">Dans ce cas, vous pouvez utiliser n’importe quel nom de domaine actif ou vérifié ayant été configuré dans votre portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c11eb-123">In this case, you can use any active or verified domain name that has been configured in your Azure portal.</span></span>

![Nom de domaine Jouets Wingtip][2]  

<span data-ttu-id="c11eb-125">Vous devez distribuer l’URL à tous les utilisateurs qui se connecteront aux applications intégrées à Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c11eb-125">You need to distribute the URL to all users who will sign in to applications that are integrated with Azure AD.</span></span>

## <a name="authentication"></a><span data-ttu-id="c11eb-126">Authentification</span><span class="sxs-lookup"><span data-stu-id="c11eb-126">Authentication</span></span>

<span data-ttu-id="c11eb-127">Pour accéder au volet d’accès, vous devez être authentifié via un compte professionnel ou scolaire dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c11eb-127">To reach the access panel, you must be authenticated through a work or school account in Azure AD.</span></span> <span data-ttu-id="c11eb-128">Vous pouvez être authentifié dans Azure AD directement.</span><span class="sxs-lookup"><span data-stu-id="c11eb-128">You can be authenticated to Azure AD directly.</span></span> <span data-ttu-id="c11eb-129">En guise d’alternative, si une organisation a configuré la fédération à l’aide des services Active Directory Federation Services (AD FS) ou d’autres technologies, vous pouvez être authentifié par Windows Server Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c11eb-129">Alternatively, if an organization has configured federation by using Active Directory Federation Services (AD FS) or other technologies, you can be authenticated by Windows Server Active Directory.</span></span>

<span data-ttu-id="c11eb-130">Si vous disposez d’un abonnement Azure ou Office 365 et que vous utilisez le portail Azure ou une application Office 365, vous pouvez voir la liste des applications sans avoir à vous reconnecter.</span><span class="sxs-lookup"><span data-stu-id="c11eb-130">If you have a subscription for Azure or Office 365 and you have been using the Azure portal or an Office 365 application, you can see the list of applications without signing-in again.</span></span> <span data-ttu-id="c11eb-131">Si vous n’êtes pas authentifié, vous êtes invité à vous connecter à l’aide du nom d’utilisateur et du mot de passe correspondant à votre compte dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c11eb-131">If you are are not authenticated you are prompted to sign in by using the username and password for your account in Azure AD.</span></span> <span data-ttu-id="c11eb-132">Si votre organisation a configuré la fédération, la saisie du nom d’utilisateur suffit.</span><span class="sxs-lookup"><span data-stu-id="c11eb-132">If your organization has configured federation, typing the username is sufficient.</span></span>

<span data-ttu-id="c11eb-133">Une fois authentifié, vous pouvez interagir avec les applications que l’administrateur a intégrées à l’annuaire.</span><span class="sxs-lookup"><span data-stu-id="c11eb-133">When you are authenticated, you can interact with the applications that your administrator has integrated with the directory.</span></span> <span data-ttu-id="c11eb-134">Pour découvrir comment intégrer des applications à Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c11eb-134">To learn how to integrate applications with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="web-browser-requirements"></a><span data-ttu-id="c11eb-135">Configuration requise du navigateur web</span><span class="sxs-lookup"><span data-stu-id="c11eb-135">Web browser requirements</span></span>

<span data-ttu-id="c11eb-136">Au minimum, le volet d’accès nécessite un navigateur prenant en charge JavaScript et dans lequel CSS est activée.</span><span class="sxs-lookup"><span data-stu-id="c11eb-136">At a minimum, the access panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="c11eb-137">Pour que vous soyez connecté aux applications via l’authentification unique (SSO) avec mot de passe, l’extension du volet d’accès doit être installée dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="c11eb-137">For the user to be signed in to applications through password-based single sign-on (SSO), the access panel extension must be installed in your browser.</span></span> <span data-ttu-id="c11eb-138">Cette extension est téléchargée automatiquement quand vous sélectionnez une application configurée pour l’authentification unique (SSO) avec mot de passe.</span><span class="sxs-lookup"><span data-stu-id="c11eb-138">The extension is downloaded automatically when you select an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="c11eb-139">L’extension du volet d’accès est actuellement disponible pour les navigateurs Internet Explorer 8 et ultérieur, Edge, Chrome et Firefox.</span><span class="sxs-lookup"><span data-stu-id="c11eb-139">The access panel extension is currently available for Internet Explorer 8 and later, Edge, Chrome, and Firefox browsers.</span></span>

## <a name="mobile-app-support"></a><span data-ttu-id="c11eb-140">Prise en charge des applications mobiles</span><span class="sxs-lookup"><span data-stu-id="c11eb-140">Mobile app support</span></span>

<span data-ttu-id="c11eb-141">L’équipe Azure Active Directory publie l’application mobile My Apps.</span><span class="sxs-lookup"><span data-stu-id="c11eb-141">The Azure Active Directory team publishes the my apps mobile app.</span></span> <span data-ttu-id="c11eb-142">Quand vous installez cette application, vous pouvez vous connecter aux applications SSO avec mot de passe sur des appareils iOS et Android.</span><span class="sxs-lookup"><span data-stu-id="c11eb-142">When you install the app, you can sign in to password-based SSO applications on iOS and Android devices.</span></span>

> [!NOTE]
> <span data-ttu-id="c11eb-143">Vous pouvez vous connecter aux applications qui prennent en charge la fédération avec Azure AD (notamment Salesforce, Google Apps, Dropbox, Box, Concur, Workday, Office 365 et plus de 70 autres) sur presque n’importe quel navigateur web sur n’importe quel appareil sans nécessiter de plug-in ou d’application mobile.</span><span class="sxs-lookup"><span data-stu-id="c11eb-143">You can sign in to applications that support federation with Azure AD (including Salesforce, Google Apps, Dropbox, Box, Concur, Workday, Office 365, and more than 70 others) on virtually any web browser, on any device, without needing a plug-in or mobile app.</span></span> <span data-ttu-id="c11eb-144">Le reste de l’[expérience de volet d’accès](https://myapps.microsoft.com/) ne nécessite pas non plus l’utilisation de l’application mobile My Apps sur un appareil mobile.</span><span class="sxs-lookup"><span data-stu-id="c11eb-144">All other [access panel experiences](https://myapps.microsoft.com/) do also not require the my apps mobile app to be used on a mobile device.</span></span>
>
>

### <a name="my-apps-for-android"></a><span data-ttu-id="c11eb-145">My Apps pour Android</span><span class="sxs-lookup"><span data-stu-id="c11eb-145">My apps for Android</span></span>

<span data-ttu-id="c11eb-146">My Apps pour Android est prise en charge sur n’importe quel appareil Android exécutant Android version 4.1 et ultérieures.</span><span class="sxs-lookup"><span data-stu-id="c11eb-146">My apps for Android is supported on any Android device that is running Android version 4.1 and later.</span></span>  
<span data-ttu-id="c11eb-147">Elle est disponible dans le [Google Play Store](https://play.google.com/store/apps/details?id=com.microsoft.myapps).</span><span class="sxs-lookup"><span data-stu-id="c11eb-147">It is available in the [Google Play store](https://play.google.com/store/apps/details?id=com.microsoft.myapps).</span></span>

![My Apps pour Android][3]   

### <a name="my-apps-for-iphone-and-ipad"></a><span data-ttu-id="c11eb-149">My Apps pour iPhone et iPad</span><span class="sxs-lookup"><span data-stu-id="c11eb-149">My apps for iPhone and iPad</span></span>

<span data-ttu-id="c11eb-150">My Apps pour iOS est prise en charge sur n’importe quel iPhone ou iPad exécutant iOS version 7 et ultérieures.</span><span class="sxs-lookup"><span data-stu-id="c11eb-150">My apps for iOS is supported on any iPhone or iPad that is running iOS version 7 and later.</span></span>  
<span data-ttu-id="c11eb-151">Elle est disponible dans l’[Apple App Store](https://itunes.apple.com/us/app/my-apps-azure-active-directory/id824048653?mt=8).</span><span class="sxs-lookup"><span data-stu-id="c11eb-151">It is available in the [Apple App Store](https://itunes.apple.com/us/app/my-apps-azure-active-directory/id824048653?mt=8).</span></span>

![My Apps pour iOS][4]    



## <a name="managed-browser-for-my-apps"></a><span data-ttu-id="c11eb-153">Managed Browser pour My apps</span><span class="sxs-lookup"><span data-stu-id="c11eb-153">Managed browser for my apps</span></span>

<span data-ttu-id="c11eb-154">My apps est également intégré à Intune Managed Browser.</span><span class="sxs-lookup"><span data-stu-id="c11eb-154">My apps is also integrated in the Intune Managed Browser.</span></span> <span data-ttu-id="c11eb-155">Intune Managed Browser pour les appareils iOS et Android joue un rôle clé pour garantir la sécurisation des données sur les appareils mobiles.</span><span class="sxs-lookup"><span data-stu-id="c11eb-155">The Intune Managed Browser for iOS and Android devices plays a key role in ensuring that data on mobile devices stays secure.</span></span> <span data-ttu-id="c11eb-156">Il vous permet d’afficher et de parcourir des pages web pouvant contenir des informations d’entreprise, et fournit une expérience de navigation web sécurisée.</span><span class="sxs-lookup"><span data-stu-id="c11eb-156">It lets you safely view and navigate web pages that might contain company information, and provides a secure web-browsing experience.</span></span>  
<span data-ttu-id="c11eb-157">Vous bénéficiez d’un accès rapide à My Apps dans votre page d’accueil Managed Browser et dans vos favoris, ce qui vous permet d’accéder aux applications souhaitées en moins de clics.</span><span class="sxs-lookup"><span data-stu-id="c11eb-157">You find quick access to my apps on your Managed Browser homepage and in your bookmarks, giving you fewer clicks to reach any application you want to access.</span></span>

<span data-ttu-id="c11eb-158">Il est disponible dans l’[Apple App Store](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) et le [Google Play Store](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en).</span><span class="sxs-lookup"><span data-stu-id="c11eb-158">It is available in the [Apple App Store](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) and [Google Play Store](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en).</span></span>

![Managed Browser pour My apps][5]    





## <a name="tips-for-testing-the-user-experience"></a><span data-ttu-id="c11eb-160">Conseils pour tester l’expérience utilisateur</span><span class="sxs-lookup"><span data-stu-id="c11eb-160">Tips for testing the user experience</span></span>

<span data-ttu-id="c11eb-161">Si vous êtes administrateur Azure et que vous êtes connecté au portail Azure à l’aide d’un compte dans l’annuaire, vous êtes automatiquement connecté au volet d’accès sous votre compte actuel.</span><span class="sxs-lookup"><span data-stu-id="c11eb-161">If you are an Azure administrator and you are signed in to the Azure portal by using an account in the directory, you are automatically signed in to the access panel as your current account.</span></span> <span data-ttu-id="c11eb-162">Dans ce cas, vous pourrez voir toutes les applications qui vous ont été affectées.</span><span class="sxs-lookup"><span data-stu-id="c11eb-162">In this case, you can see all applications that have been assigned to you.</span></span>

<span data-ttu-id="c11eb-163">**Pour tester sous un compte d’utilisateur *différent* :**</span><span class="sxs-lookup"><span data-stu-id="c11eb-163">**To test as a *different* user account:**</span></span>

1. <span data-ttu-id="c11eb-164">Cliquez sur le menu utilisateur dans le coin supérieur droit du portail Azure ou du volet d’accès, puis sélectionnez **Déconnexion**.</span><span class="sxs-lookup"><span data-stu-id="c11eb-164">Click the user menu in the upper-right corner of the Azure portal or the access panel, and then select **Sign Out**.</span></span> 
2. <span data-ttu-id="c11eb-165">Accédez au [volet d’accès](http://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="c11eb-165">Go to the [access panel](http://myapps.microsoft.com).</span></span>
3. <span data-ttu-id="c11eb-166">Dans la page de connexion, tapez le nom d’utilisateur et le mot de passe du compte dans l’annuaire que vous souhaitez tester.</span><span class="sxs-lookup"><span data-stu-id="c11eb-166">On the sign-in page, type the username and password for the account in your directory you want to test.</span></span>


## <a name="starting-applications"></a><span data-ttu-id="c11eb-167">Démarrage des applications</span><span class="sxs-lookup"><span data-stu-id="c11eb-167">Starting applications</span></span>

<span data-ttu-id="c11eb-168">Plusieurs types d’applications peuvent apparaître dans le volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="c11eb-168">Several types of applications can appear on the access panel.</span></span>

### <a name="office-365-applications"></a><span data-ttu-id="c11eb-169">Applications Office 365</span><span class="sxs-lookup"><span data-stu-id="c11eb-169">Office 365 applications</span></span>

<span data-ttu-id="c11eb-170">Si votre organisation utilise des applications Office 365 et que vous disposez d’une licence pour celles-ci, les applications Office 365 apparaissent dans votre volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="c11eb-170">If your organization is using Office 365 applications and you are licensed for them, the Office 365 applications appear on your access panel.</span></span>

<span data-ttu-id="c11eb-171">Quand vous cliquez sur la vignette d’une application Office 365, vous êtes redirigé vers l’application et connecté automatiquement.</span><span class="sxs-lookup"><span data-stu-id="c11eb-171">When you click an application tile for an Office 365 application, you are redirected to the application and automatically signed in.</span></span>

### <a name="microsoft-and-third-party-applications-configured-with-federation-based-sso"></a><span data-ttu-id="c11eb-172">Applications Microsoft et tierces configurées avec l’authentification unique (SSO) basée sur la fédération</span><span class="sxs-lookup"><span data-stu-id="c11eb-172">Microsoft and third-party applications configured with federation-based SSO</span></span>

<span data-ttu-id="c11eb-173">Votre administrateur peut ajouter des applications à la section Active Directory du portail Azure avec le mode d’authentification unique (SSO) défini sur **Authentification unique avec Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="c11eb-173">Your administrator can add applications in the Active Directory section of the Azure portal with the SSO mode set to **Azure AD Single Sign-On**.</span></span> <span data-ttu-id="c11eb-174">Vous ne voyez ces applications que si votre administrateur vous a explicitement accordé un accès aux applications.</span><span class="sxs-lookup"><span data-stu-id="c11eb-174">You can only see these applications if your administrator has explicitly granted you access to the applications.</span></span>

<span data-ttu-id="c11eb-175">Quand vous cliquez sur la vignette de l’une de ces applications, vous êtes redirigé vers l’application et connecté automatiquement.</span><span class="sxs-lookup"><span data-stu-id="c11eb-175">When you click a tile for one of these applications, you are redirected and automatically signed in to the application.</span></span>

### <a name="password-based-sso-without-identity-provisioning"></a><span data-ttu-id="c11eb-176">Authentification unique avec mot de passe sans approvisionnement d’identité</span><span class="sxs-lookup"><span data-stu-id="c11eb-176">Password-based SSO without identity provisioning</span></span>

<span data-ttu-id="c11eb-177">Votre administrateur peut ajouter des applications à la section Active Directory du portail Azure avec le mode d’authentification unique (SSO) défini sur **Authentification unique avec mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="c11eb-177">Your administrator can add applications in the Active Directory section of the Azure portal with the SSO mode set to **Password-based Single Sign-On**.</span></span> <span data-ttu-id="c11eb-178">Tous les utilisateurs de l’annuaire peuvent voir toutes les applications qui ont été configurées dans ce mode.</span><span class="sxs-lookup"><span data-stu-id="c11eb-178">All users in the directory can see all applications that have been configured in this mode.</span></span>

<span data-ttu-id="c11eb-179">La première fois que vous cliquez sur la vignette de l’une de ces applications, vous êtes invité à installer le plug-in d’authentification unique (SSO) avec mot de passe pour Internet Explorer ou Chrome.</span><span class="sxs-lookup"><span data-stu-id="c11eb-179">The first time, you click a tile for one of these applications, you are prompted to install the Password SSO plug-in for Internet Explorer or Chrome.</span></span> <span data-ttu-id="c11eb-180">L’installation peut nécessiter le redémarrage de votre navigateur web.</span><span class="sxs-lookup"><span data-stu-id="c11eb-180">The installation might require you to restart your web browser.</span></span> <span data-ttu-id="c11eb-181">Quand vous êtes renvoyé au volet d’accès et que vous recliquez sur la vignette de l’application, vous êtes invité à fournir un nom d’utilisateur et un mot de passe pour l’application.</span><span class="sxs-lookup"><span data-stu-id="c11eb-181">When you return to the access panel and click the application tile again, you are prompted for a username and password for the application.</span></span> <span data-ttu-id="c11eb-182">Une fois que vous avez entré le nom d’utilisateur et le mot de passe, ces informations d’identification sont stockées de manière sécurisée dans Azure AD et liées à votre compte dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c11eb-182">When you have entered your username and password, these credentials are securely stored and linked to your account in Azure AD.</span></span>

<span data-ttu-id="c11eb-183">La prochaine fois que vous cliquez sur la vignette de l’application, vous êtes connecté automatiquement à l’application.</span><span class="sxs-lookup"><span data-stu-id="c11eb-183">The next time you click the application tile, you are automatically signed in to the application.</span></span>  
<span data-ttu-id="c11eb-184">Vous ne serez pas obligé de retaper vos informations d’identification ou d’installer le plug-in d’authentification unique (SSO) avec mot de passe.</span><span class="sxs-lookup"><span data-stu-id="c11eb-184">You don't have to enter your credentials again and or install the Password SSO plug-in.</span></span>

<span data-ttu-id="c11eb-185">Si vos informations d’identification ont changé dans l’application tierce cible, vous devez également mettre à jour vos informations d’identification stockées dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c11eb-185">If your credentials have changed in the target third-party application, you must also update your credentials that are stored in Azure AD.</span></span> 

<span data-ttu-id="c11eb-186">**Pour mettre à jour les informations d’identification**</span><span class="sxs-lookup"><span data-stu-id="c11eb-186">**To update credentials:**</span></span>

1. <span data-ttu-id="c11eb-187">Sélectionnez l’icône sur la vignette de l’application.</span><span class="sxs-lookup"><span data-stu-id="c11eb-187">Select the icon on the application tile.</span></span>
2. <span data-ttu-id="c11eb-188">Sélectionnez **mettre à jour les informations d’identification** pour retaper le nom d’utilisateur et le mot de passe de l’application.</span><span class="sxs-lookup"><span data-stu-id="c11eb-188">Select **update credentials** to reenter the username and password for the application.</span></span>


### <a name="password-based-sso-with-identity-provisioning"></a><span data-ttu-id="c11eb-189">Authentification unique avec mot de passe avec approvisionnement d’identité</span><span class="sxs-lookup"><span data-stu-id="c11eb-189">Password-based SSO with identity provisioning</span></span>

<span data-ttu-id="c11eb-190">Vous pouvez ajouter des applications à la section ****Active Directory du portail Azure avec le mode d’authentification unique (SSO) défini sur **Authentification unique avec mot de passe**, ainsi que l’approvisionnement d’identité.</span><span class="sxs-lookup"><span data-stu-id="c11eb-190">Your administrator can add applications in the **Active Directory** section of the Azure portal with the SSO mode set to **Password-based Single Sign-On**, along with identity provisioning.</span></span>

<span data-ttu-id="c11eb-191">La première fois que vous cliquez sur la vignette de l’une de ces applications, vous êtes invité à installer le **plug-in d’authentification unique (SSO) avec mot de passe pour Internet Explorer ou Chrome**.</span><span class="sxs-lookup"><span data-stu-id="c11eb-191">The first time, you click an application tile for one of these applications, you are prompted to install the **Password SSO plug-in for Internet Explorer or Chrome**.</span></span> <span data-ttu-id="c11eb-192">L’installation peut nécessiter le redémarrage de votre navigateur web.</span><span class="sxs-lookup"><span data-stu-id="c11eb-192">The installation might require you to restart your web browser.</span></span>  
<span data-ttu-id="c11eb-193">Quand vous revenez au volet d’accès et que vous recliquez sur la vignette de l’application, vous êtes connecté automatiquement à l’application.</span><span class="sxs-lookup"><span data-stu-id="c11eb-193">When you return to the access panel and click the application tile again, you are automatically signed in to the application.</span></span>

<span data-ttu-id="c11eb-194">Certaines applications peuvent exiger que vous changiez votre mot de passe lors de la première connexion.</span><span class="sxs-lookup"><span data-stu-id="c11eb-194">Some applications might require you to change your password on the first sign-in.</span></span> <span data-ttu-id="c11eb-195">Si vos informations d’identification ont changé dans l’application tierce cible, vous devez également mettre à jour les informations d’identification stockées dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c11eb-195">If your credentials have changed in the target third-party application, you must also update the credentials that are stored in Azure AD.</span></span> 

<span data-ttu-id="c11eb-196">**Pour mettre à jour les informations d’identification**</span><span class="sxs-lookup"><span data-stu-id="c11eb-196">**To update credentials:**</span></span>

1. <span data-ttu-id="c11eb-197">Sélectionnez l’icône sur la vignette de l’application.</span><span class="sxs-lookup"><span data-stu-id="c11eb-197">Select the icon on the application tile.</span></span>
2. <span data-ttu-id="c11eb-198">Sélectionnez **mettre à jour les informations d’identification** pour retaper le nom d’utilisateur et le mot de passe de l’application.</span><span class="sxs-lookup"><span data-stu-id="c11eb-198">Select **update credentials** to reenter the username and password for the application.</span></span>


### <a name="application-with-existing-sso-solutions"></a><span data-ttu-id="c11eb-199">Application avec solutions d’authentification unique (SSO) existantes</span><span class="sxs-lookup"><span data-stu-id="c11eb-199">Application with existing SSO solutions</span></span>

<span data-ttu-id="c11eb-200">Pour configurer l’authentification unique (SSO) pour une application, le portail Azure propose une troisième option appelée **authentification unique existante**.</span><span class="sxs-lookup"><span data-stu-id="c11eb-200">To configure SSO for an application, the Azure portal provides a third option called **Existing Single Sign-On**.</span></span> <span data-ttu-id="c11eb-201">Cette option permet à votre administrateur de créer un lien vers une application et de le placer dans le volet d’accès pour les utilisateurs sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="c11eb-201">This option enables your administrator to create a link to an application and place it on the access panel for selected users.</span></span>

<span data-ttu-id="c11eb-202">Par exemple, si une application est configurée pour authentifier les utilisateurs avec les services AD FS 2.0, votre administrateur peut utiliser l’option d’**authentification unique existante** pour créer un lien vers cette application dans le volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="c11eb-202">For example, if an application is configured to authenticate users by using AD FS 2.0, your administrator can use the **Existing Single Sign-On** option to create a link to it on the access panel.</span></span> <span data-ttu-id="c11eb-203">Quand vous accédez au lien, vous êtes authentifié par le biais des services AD FS 2.0 ou de la solution d’authentification unique (SSO) existante fournie par l’application.</span><span class="sxs-lookup"><span data-stu-id="c11eb-203">When you access the link, you are authenticated through AD FS 2.0 or whatever existing SSO solution the application provides.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c11eb-204">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c11eb-204">Next steps</span></span>

- <span data-ttu-id="c11eb-205">Pour obtenir une liste de toutes les rubriques liées à la gestion des applications, consultez l’[index des articles relatifs à la gestion des applications dans Azure Active Directory](active-directory-apps-index.md).</span><span class="sxs-lookup"><span data-stu-id="c11eb-205">To see a list of all topics that are related to application management, see the [article index for application management in Azure Active Directory](active-directory-apps-index.md).</span></span>
 
- <span data-ttu-id="c11eb-206">Pour découvrir comment intégrer une application SaaS dans Azure AD, consultez la [liste des didacticiels sur l’intégration d’applications SaaS](active-directory-saas-tutorial-list.md).</span><span class="sxs-lookup"><span data-stu-id="c11eb-206">To learn how to integrate a SaaS app into Azure AD, see the [list of tutorials on how to integrate SaaS apps](active-directory-saas-tutorial-list.md).</span></span>
 
- <span data-ttu-id="c11eb-207">Pour en savoir plus sur la gestion des applications avec Azure AD, consultez l’[introduction à l’authentification unique et à la gestion de l’accès aux applications avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c11eb-207">To learn more about managing apps with Azure AD, see the [introduction to single sign-on and managing app access with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>
 
- <span data-ttu-id="c11eb-208">Pour plus d’informations sur l’approvisionnement des utilisateurs, consultez [Automatiser l’approvisionnement et l’annulation de l’approvisionnement des utilisateurs pour les applications SaaS avec Azure Active Directory](active-directory-saas-app-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="c11eb-208">To learn more about user provisioning, see [automate user provisioning and deprovisioning to SaaS applications](active-directory-saas-app-provisioning.md).</span></span>

<!--Image references-->
[1]: ./media/active-directory-saas-access-panel-introduction/01.png
[2]: ./media/active-directory-saas-access-panel-introduction/02.png
[3]: ./media/active-directory-saas-access-panel-introduction/03.png
[4]: ./media/active-directory-saas-access-panel-introduction/04.png
[5]: ./media/active-directory-saas-access-panel-introduction/05.png
