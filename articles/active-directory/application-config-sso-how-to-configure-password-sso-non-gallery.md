---
title: "Comment configurer l’authentification unique avec mot de passe pour une application ne relevant pas de la galerie | Microsoft Docs"
description: "Comment configurer une application personnalisée ne relevant pas de la galerie pour l’authentification unique avec mot de passe lorsqu’elle n’est pas répertoriée dans la galerie d’applications Azure AD"
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
ms.openlocfilehash: f629ec99824199306ebf825901beaa99d83d434d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="248bb-103">Comment configurer l’authentification unique avec mot de passe pour une application ne relevant pas de la galerie</span><span class="sxs-lookup"><span data-stu-id="248bb-103">How to configure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="248bb-104">Outre les options présentes dans la galerie d’applications Azure AD, vous avez également la possibilité d’ajouter une **application ne relevant pas de la galerie** lorsque l’application souhaitée n’y est pas répertoriée.</span><span class="sxs-lookup"><span data-stu-id="248bb-104">In addition to the choices found within the Azure AD Application Gallery, you also have the option to add a **non-gallery application** when the application you want is not listed there.</span></span> <span data-ttu-id="248bb-105">À l’aide de cette fonctionnalité, vous pouvez ajouter n’importe quelle application qui existe déjà dans votre organisation, ou n’importe quelle application tierce d’un fournisseur qui ne fait pas déjà partie de la [Galerie d’applications Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span><span class="sxs-lookup"><span data-stu-id="248bb-105">Using this capability, you can add any application that already exists in your organization, or any third-party application that you might use from a vendor who is not already part of the [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span></span>

<span data-ttu-id="248bb-106">Une fois que vous avez ajouté une application ne relevant pas de la galerie, vous pouvez ensuite configurer la méthode d’authentification unique que cette application utilise en sélectionnant l’élément de navigation **Authentification unique** avec une application d’entreprise dans le [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="248bb-106">Once you add a non-gallery application, you can then configure the Single sign-on method this application uses by selecting the **Single Sign-on** navigation item on an Enterprise Application in the [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="248bb-107">L’une des méthodes d’authentification unique disponibles est l’option [Authentification unique par mot de passe](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work).</span><span class="sxs-lookup"><span data-stu-id="248bb-107">One of the Single Sign-on methods available to you is the [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) option.</span></span> <span data-ttu-id="248bb-108">Avec l’expérience **d’ajout d’une application ne relevant pas de la galerie**, vous pouvez intégrer n’importe quelle application qui affiche un champ d’entrée HTML de nom d’utilisateur et de mot de passe, même si elle ne figure pas dans notre jeu d’applications pré-intégrées.</span><span class="sxs-lookup"><span data-stu-id="248bb-108">With the **add a non-gallery application** experience, you can integrate any application that renders an HTML-based username and password input field, even if it is not in our set of pre-integrated applications.</span></span>

<span data-ttu-id="248bb-109">Cela fonctionne grâce à la technologie de récupération de pages qui fait partie de l’extension du volet d’accès qui permet de détecter automatiquement les champs d’entrée de nom d’utilisateur et de mot de passe, et de les stocker en toute sécurité pour votre instance d’application spécifique.</span><span class="sxs-lookup"><span data-stu-id="248bb-109">The way this works is by a page scraping technology that is part of the Access Panel extension that allows us to auto-detect username and password input fields, store them securely for your specific application instance.</span></span> <span data-ttu-id="248bb-110">Puis, en toute sécurité, les noms d’utilisateur et mots de passe sont relus et transmis à ces champs lorsqu’un utilisateur accède à cette application sur le volet d’accès de l’application.</span><span class="sxs-lookup"><span data-stu-id="248bb-110">Then securely replay usernames and passwords to those fields when a user navigates to that application on the application access panel.</span></span>

<span data-ttu-id="248bb-111">Ceci est un excellent moyen pour commencer à intégrer rapidement tout type d’application dans Azure AD et vous permet d’effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="248bb-111">This is a great way to get started integrating any kind of application into Azure AD quickly, and allows you to:</span></span>

-   <span data-ttu-id="248bb-112">intégrer **n’importe quelle application au monde** à votre client Azure AD, si elle affiche un champ d’entrée HTML de nom d’utilisateur et de mot de passe ;</span><span class="sxs-lookup"><span data-stu-id="248bb-112">Integrate **any application in the world** with your Azure AD tenant, so long as it renders an HTML username and password input field</span></span>

-   <span data-ttu-id="248bb-113">activer **l’authentification unique pour vos utilisateurs** par le stockage et la relecture en toute sécurité des noms d’utilisateur et mots de passe pour l’application que vous avez intégrée à Azure AD ;</span><span class="sxs-lookup"><span data-stu-id="248bb-113">Enable **Single Sign-on for your users** by securely storing and replaying usernames and passwords for the application you’ve integrated with Azure AD</span></span>

-   <span data-ttu-id="248bb-114">**détecter automatiquement les champs d’entrée** de n’importe quelle application et vous permettre de détecter manuellement ces champs à l’aide de l’extension de navigateur du volet d’accès, au cas où la détection automatique ne les trouve pas ;</span><span class="sxs-lookup"><span data-stu-id="248bb-114">**Auto-detect input** fields for any application and allow you to manually detect those fields using the Access Panel Browser Extension, in case auto-detection does not find them</span></span>

-   <span data-ttu-id="248bb-115">**prendre en charge les applications qui requièrent plusieurs champs de connexion** pour les applications qui requièrent plus que les champs de nom d’utilisateur et de mot de passe pour la connexion ;</span><span class="sxs-lookup"><span data-stu-id="248bb-115">**Support applications that require multiple sign-in fields** for applications that require more than just username and password fields to sign in</span></span>

-   <span data-ttu-id="248bb-116">**personnaliser les étiquettes** des champs d’entrée de nom d’utilisateur et de mot de passe que vos utilisateurs voient dans le [volet d’accès aux applications](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) lorsqu’ils entrent leurs informations d’identification ;</span><span class="sxs-lookup"><span data-stu-id="248bb-116">**Customize the labels** of the username and password input fields your users see on the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) when they enter their credentials</span></span>

-   <span data-ttu-id="248bb-117">autoriser vos **utilisateurs** à fournir leurs propres noms d’utilisateur et mots de passe de tout compte d’application existant qu’ils saisissent manuellement dans le [volet d’accès aux applications](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) ;</span><span class="sxs-lookup"><span data-stu-id="248bb-117">Allow your **users** to provide their own usernames and passwords for any existing application accounts they are typing in manually on the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span></span>

-   <span data-ttu-id="248bb-118">autoriser un **membre du groupe d’entreprise** à spécifier les noms d’utilisateur et mots de passe affectés à un utilisateur à l’aide de la fonctionnalité [Accès aux applications en libre-service](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) ;</span><span class="sxs-lookup"><span data-stu-id="248bb-118">Allow a **member of the business group** to specify the usernames and passwords assigned to a user by using the [Self-Service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) feature</span></span>

-   <span data-ttu-id="248bb-119">autoriser un **administrateur** à spécifier les noms d’utilisateur et mots de passe affectés à un utilisateur à l’aide de la fonctionnalité Mettre à jour les informations d'identification lors de [l’affectation d’un utilisateur à une application](#_How_to_configure_1) ;</span><span class="sxs-lookup"><span data-stu-id="248bb-119">Allow an **administrator** to specify the usernames and passwords assigned to a user by using the Update Credentials feature when [assigning a user to an application](#_How_to_configure_1)</span></span>

-   <span data-ttu-id="248bb-120">autoriser un **administrateur** à spécifier les noms d’utilisateur et mots de passe partagés utilisés par un groupe de personnes à l’aide de la fonctionnalité Mettre à jour les informations d'identification lors de [l’affectation d’un groupe à une application](#assign-an-application-to-a-group-directly).</span><span class="sxs-lookup"><span data-stu-id="248bb-120">Allow an **administrator** to specify the shared username or password used by a group of people by using the Update Credentials feature when [assigning a group to an application](#assign-an-application-to-a-group-directly)</span></span>

<span data-ttu-id="248bb-121">Vous trouverez ci-dessous les instructions pour activer [l’authentification unique par mot de passe](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) pour n’importe quelle application que vous ajoutez à l’aide de l’expérience **d’ajout d’une application ne relevant pas de la galerie**.</span><span class="sxs-lookup"><span data-stu-id="248bb-121">Below describes how you can enable [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) to any application that you add using the **add a non-gallery application** experience.</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="248bb-122">Vue d’ensemble des étapes requises</span><span class="sxs-lookup"><span data-stu-id="248bb-122">Overview of steps required</span></span>

<span data-ttu-id="248bb-123">Pour configurer une application à partir de la galerie Azure AD, vous devez effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="248bb-123">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="248bb-124">Ajouter une application ne figurant pas dans la galerie</span><span class="sxs-lookup"><span data-stu-id="248bb-124">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="248bb-125">Configurer l’application pour l’authentification unique avec mot de passe</span><span class="sxs-lookup"><span data-stu-id="248bb-125">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="248bb-126">Affecter l’application à un utilisateur ou à un groupe</span><span class="sxs-lookup"><span data-stu-id="248bb-126">Assign the application to a user or a group</span></span>](#assign-the-application-to-a-user-or-a-group)

    -   [<span data-ttu-id="248bb-127">Affecter un utilisateur directement à une application</span><span class="sxs-lookup"><span data-stu-id="248bb-127">Assign a user to an application directly</span></span>](#assign-a-user-to-an-application-directly)

    -   [<span data-ttu-id="248bb-128">Affecter une application directement à un groupe</span><span class="sxs-lookup"><span data-stu-id="248bb-128">Assign an application to a group directly</span></span>](#assign-an-application-to-a-group-directly)

## <a name="add-a-non-gallery-application"></a><span data-ttu-id="248bb-129">Ajouter une application ne relevant pas de la galerie</span><span class="sxs-lookup"><span data-stu-id="248bb-129">Add a non-gallery application</span></span>

<span data-ttu-id="248bb-130">Pour ajouter une application à partir de la galerie Azure AD, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="248bb-130">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="248bb-131">Ouvrez le [portail Azure](https://portal.azure.com) et connectez-vous en tant qu’**administrateur général** ou **coadministrateur**</span><span class="sxs-lookup"><span data-stu-id="248bb-131">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="248bb-132">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="248bb-132">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="248bb-133">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="248bb-133">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="248bb-134">Cliquez sur **Applications d’entreprise** dans le menu de navigation gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="248bb-134">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="248bb-135">Cliquez sur le bouton **Ajouter** dans le coin supérieur droit du panneau **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="248bb-135">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="248bb-136">Cliquez sur **Application ne figurant pas dans la galerie**.</span><span class="sxs-lookup"><span data-stu-id="248bb-136">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="248bb-137">Entrez le nom de votre application dans la zone de texte **Nom**.</span><span class="sxs-lookup"><span data-stu-id="248bb-137">Enter the name of your application in the **Name** textbox.</span></span> <span data-ttu-id="248bb-138">Sélectionnez **Ajouter.**</span><span class="sxs-lookup"><span data-stu-id="248bb-138">Select **Add.**</span></span>

<span data-ttu-id="248bb-139">Après une courte période, vous pourrez voir le panneau de configuration de l’application.</span><span class="sxs-lookup"><span data-stu-id="248bb-139">After a short period, you be able to see the application’s configuration blade.</span></span>

## <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="248bb-140">Configurer l’application pour l’authentification unique par mot de passe</span><span class="sxs-lookup"><span data-stu-id="248bb-140">Configure the application for password single sign-on</span></span>

<span data-ttu-id="248bb-141">Pour configurer l’authentification unique pour une application, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="248bb-141">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="248bb-142">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général** ou **coadministrateur**</span><span class="sxs-lookup"><span data-stu-id="248bb-142">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="248bb-143">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="248bb-143">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="248bb-144">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="248bb-144">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="248bb-145">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="248bb-145">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="248bb-146">Cliquez sur **Toutes les applications** pour afficher la liste complète de vos applications.</span><span class="sxs-lookup"><span data-stu-id="248bb-146">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="248bb-147">Si l’application que vous recherchez ne figure pas dans la liste, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications.**</span><span class="sxs-lookup"><span data-stu-id="248bb-147">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="248bb-148">Sélectionnez l’application pour laquelle vous souhaitez configurer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="248bb-148">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="248bb-149">Une fois l’application chargée, cliquez sur **Authentification unique** dans le menu de navigation de gauche de l’application.</span><span class="sxs-lookup"><span data-stu-id="248bb-149">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="248bb-150">Sélectionnez le mode **Authentification par mot de passe.**</span><span class="sxs-lookup"><span data-stu-id="248bb-150">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="248bb-151">Entrez **l’URL de connexion**.</span><span class="sxs-lookup"><span data-stu-id="248bb-151">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="248bb-152">Il s’agit de l’URL où les utilisateurs entrent leurs nom d’utilisateur et mot de passe pour se connecter.</span><span class="sxs-lookup"><span data-stu-id="248bb-152">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="248bb-153">Vérifiez que les champs de connexion sont visibles dans l’URL.</span><span class="sxs-lookup"><span data-stu-id="248bb-153">Ensure the sign in fields are visible at the URL.</span></span>

10. <span data-ttu-id="248bb-154">Affectez des utilisateurs à l’application.</span><span class="sxs-lookup"><span data-stu-id="248bb-154">Assign users to the application.</span></span>

11. <span data-ttu-id="248bb-155">En outre, vous pouvez également fournir des informations d’identification pour le compte de l’utilisateur en sélectionnant les lignes des utilisateurs, en cliquant sur **Mettre à jour les informations d’identification** et en entrant le nom d’utilisateur et le mot de passe à la place des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="248bb-155">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="248bb-156">Autrement, les utilisateurs doivent entrer les informations d’identification eux-mêmes lors du lancement.</span><span class="sxs-lookup"><span data-stu-id="248bb-156">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="assign-a-user-to-an-application-directly"></a><span data-ttu-id="248bb-157">Affecter un utilisateur directement à une application</span><span class="sxs-lookup"><span data-stu-id="248bb-157">Assign a user to an application directly</span></span>

<span data-ttu-id="248bb-158">Pour affecter un ou plusieurs utilisateurs directement à une application, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="248bb-158">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="248bb-159">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général.**</span><span class="sxs-lookup"><span data-stu-id="248bb-159">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="248bb-160">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="248bb-160">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="248bb-161">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="248bb-161">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="248bb-162">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="248bb-162">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="248bb-163">Cliquez sur **Toutes les applications** pour afficher la liste complète de vos applications.</span><span class="sxs-lookup"><span data-stu-id="248bb-163">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="248bb-164">Si l’application que vous recherchez ne figure pas dans la liste, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications.**</span><span class="sxs-lookup"><span data-stu-id="248bb-164">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="248bb-165">Dans la liste qui s’affiche, sélectionnez l’application à laquelle vous souhaitez affecter un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="248bb-165">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="248bb-166">Une fois l’application chargée, cliquez sur **Utilisateurs et groupes** dans le menu de navigation de gauche de l’application.</span><span class="sxs-lookup"><span data-stu-id="248bb-166">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="248bb-167">Cliquez sur le bouton **Ajouter** en haut de la liste **Utilisateurs et groupes** pour ouvrir le panneau **Ajouter une attribution**.</span><span class="sxs-lookup"><span data-stu-id="248bb-167">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="248bb-168">Cliquez sur le sélecteur **Utilisateurs et groupes** à partir du panneau **Ajouter une attribution**.</span><span class="sxs-lookup"><span data-stu-id="248bb-168">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="248bb-169">Tapez **le nom complet** ou **l’adresse de messagerie** de l’utilisateur souhaité pour l’attribution dans la zone de recherche **Rechercher par nom ou adresse de messagerie**.</span><span class="sxs-lookup"><span data-stu-id="248bb-169">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="248bb-170">Pointez sur **l’utilisateur** dans la liste pour afficher une **case à cocher**.</span><span class="sxs-lookup"><span data-stu-id="248bb-170">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="248bb-171">Cliquez sur la case à cocher en regard de la photo de profil ou du logo de l’utilisateur pour ajouter ce dernier à la liste **Sélectionné**.</span><span class="sxs-lookup"><span data-stu-id="248bb-171">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="248bb-172">**Facultatif :** si vous souhaitez **ajouter plusieurs utilisateurs**, entrez un autre **nom complet** ou une autre **adresse de messagerie** dans la zone de recherche **Rechercher par nom ou adresse de messagerie**, puis cliquez sur la case à cocher pour ajouter cet utilisateur à la liste **Sélectionné**.</span><span class="sxs-lookup"><span data-stu-id="248bb-172">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="248bb-173">Après avoir sélectionné les utilisateurs, cliquez sur le bouton **Sélectionner** pour les ajouter à la liste des utilisateurs et des groupes à affecter à l’application.</span><span class="sxs-lookup"><span data-stu-id="248bb-173">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="248bb-174">**Facultatif :** cliquez sur le sélecteur **Sélectionner un rôle** dans le panneau **Ajouter une attribution** pour sélectionner un rôle à affecter aux utilisateurs que vous avez sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="248bb-174">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="248bb-175">Cliquez sur le bouton **Attribuer** pour affecter l’application aux utilisateurs sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="248bb-175">Click the **Assign** button to assign the application to the selected users.</span></span>

## <a name="assign-an-application-to-a-group-directly"></a><span data-ttu-id="248bb-176">Affecter une application directement à un groupe</span><span class="sxs-lookup"><span data-stu-id="248bb-176">Assign an application to a group directly</span></span>

<span data-ttu-id="248bb-177">Pour affecter un ou plusieurs groupes directement à une application, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="248bb-177">To assign one or more groups to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="248bb-178">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant **qu’administrateur général**.</span><span class="sxs-lookup"><span data-stu-id="248bb-178">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="248bb-179">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="248bb-179">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="248bb-180">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="248bb-180">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="248bb-181">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="248bb-181">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="248bb-182">Cliquez sur **Toutes les applications** pour afficher la liste complète de vos applications.</span><span class="sxs-lookup"><span data-stu-id="248bb-182">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="248bb-183">Si l’application que vous recherchez ne figure pas dans la liste, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications.**</span><span class="sxs-lookup"><span data-stu-id="248bb-183">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="248bb-184">Dans la liste qui s’affiche, sélectionnez l’application à laquelle vous souhaitez affecter un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="248bb-184">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="248bb-185">Une fois l’application chargée, cliquez sur **Utilisateurs et groupes** dans le menu de navigation de gauche de l’application.</span><span class="sxs-lookup"><span data-stu-id="248bb-185">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="248bb-186">Cliquez sur le bouton **Ajouter** en haut de la liste **Utilisateurs et groupes** pour ouvrir le panneau **Ajouter une attribution**.</span><span class="sxs-lookup"><span data-stu-id="248bb-186">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="248bb-187">Cliquez sur le sélecteur **Utilisateurs et groupes** à partir du panneau **Ajouter une attribution**.</span><span class="sxs-lookup"><span data-stu-id="248bb-187">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="248bb-188">Tapez le **nom de groupe complet** du groupe souhaité pour l’attribution dans la zone de recherche **Rechercher par nom ou adresse de messagerie**.</span><span class="sxs-lookup"><span data-stu-id="248bb-188">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="248bb-189">Pointez sur le **groupe** dans la liste pour afficher une **case à cocher**.</span><span class="sxs-lookup"><span data-stu-id="248bb-189">Hover over the **group** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="248bb-190">Cliquez sur la case à cocher en regard de la photo de profil ou du logo du groupe pour ajouter ce dernier à la liste **Sélectionné**.</span><span class="sxs-lookup"><span data-stu-id="248bb-190">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="248bb-191">**Facultatif :** si vous souhaitez **ajouter plusieurs groupes**, entrez un autre **nom de groupe complet** dans la zone de recherche **Rechercher par nom ou adresse de messagerie**, puis cliquez sur la case à cocher pour ajouter ce groupe à la liste **Sélectionné**.</span><span class="sxs-lookup"><span data-stu-id="248bb-191">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span></span>

13. <span data-ttu-id="248bb-192">Lorsque vous avez fini de sélectionner les groupes, cliquez sur le bouton **Sélectionner** pour les ajouter à la liste des utilisateurs et des groupes à affecter à l’application.</span><span class="sxs-lookup"><span data-stu-id="248bb-192">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="248bb-193">**Facultatif :** cliquez sur le sélecteur **Sélectionner un rôle** dans le panneau **Ajouter une attribution** pour sélectionner un rôle à affecter aux groupes que vous avez sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="248bb-193">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span></span>

15. <span data-ttu-id="248bb-194">Cliquez sur le bouton **Attribuer** pour affecter l’application aux groupes sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="248bb-194">Click the **Assign** button to assign the application to the selected groups.</span></span>

<span data-ttu-id="248bb-195">Après une courte période, les utilisateurs que vous avez sélectionnés sont en mesure de lancer ces applications dans le panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="248bb-195">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="248bb-196">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="248bb-196">Next steps</span></span>
[<span data-ttu-id="248bb-197">Fournir une authentification unique à vos applications avec le proxy d’application</span><span class="sxs-lookup"><span data-stu-id="248bb-197">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
