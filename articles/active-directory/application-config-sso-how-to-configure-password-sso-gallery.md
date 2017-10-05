---
title: "Configurer l’authentification unique par mot de passe pour une application de la galerie Azure AD | Microsoft Docs"
description: "Comment configurer une application pour l’authentification unique par mot de passe lorsqu’elle est répertoriée dans la galerie d’applications Azure AD"
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
ms.openlocfilehash: d4dc110eb25c3e550ac4663d28e626a696b58f62
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="f6cdd-103">Comment configurer l’authentification unique par mot de passe pour une application de la galerie Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6cdd-103">How to configure password single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="f6cdd-104">Lorsque vous ajoutez une application à partir de la [Galerie d’applications Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery), vous pouvez choisir la façon dont vous souhaitez que vos utilisateurs s’y connectent.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-104">When you add an application from the [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery), you have the choice of how you want your users to sign in to that application.</span></span> <span data-ttu-id="f6cdd-105">Vous pouvez configurer ce choix à tout moment en sélectionnant l’élément de navigation **Authentification unique** sur une application d’entreprise dans le [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f6cdd-105">You can configure this choice at any time by selecting the **Single Sign-on** navigation item on an Enterprise Application in the [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="f6cdd-106">L’une des méthodes d’authentification unique disponibles est l’option [Authentification unique par mot de passe](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work).</span><span class="sxs-lookup"><span data-stu-id="f6cdd-106">One of the single sign-on methods available to you is the [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) option.</span></span> <span data-ttu-id="f6cdd-107">Ceci est un excellent moyen pour commencer à intégrer rapidement des applications dans Azure AD et vous permet d’effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="f6cdd-107">This is a great way to get started integrating applications into Azure AD quickly, and allows you to:</span></span>

-   <span data-ttu-id="f6cdd-108">activer **l’authentification unique pour vos utilisateurs** par le stockage et la relecture en toute sécurité des noms d’utilisateur et mots de passe pour l’application que vous avez intégrée à Azure AD ;</span><span class="sxs-lookup"><span data-stu-id="f6cdd-108">Enable **Single Sign-on for your users** by securely storing and replaying usernames and passwords for the application you’ve integrated with Azure AD</span></span>

-   <span data-ttu-id="f6cdd-109">**prendre en charge les applications qui requièrent plusieurs champs de connexion** pour les applications qui requièrent plus que les champs de nom d’utilisateur et de mot de passe pour la connexion ;</span><span class="sxs-lookup"><span data-stu-id="f6cdd-109">**Support applications that require multiple sign-in fields** for applications that require more than just username and password fields to sign in</span></span>

-   <span data-ttu-id="f6cdd-110">**personnaliser les étiquettes** des champs d’entrée de nom d’utilisateur et de mot de passe que vos utilisateurs voient dans le [volet d’accès aux applications](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) lorsqu’ils entrent leurs informations d’identification ;</span><span class="sxs-lookup"><span data-stu-id="f6cdd-110">**Customize the labels** of the username and password input fields your users see on the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) when they enter their credentials</span></span>

-   <span data-ttu-id="f6cdd-111">autoriser vos **utilisateurs** à fournir leurs propres noms d’utilisateur et mots de passe de tout compte d’application existant qu’ils saisissent manuellement dans le [volet d’accès aux applications](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) ;</span><span class="sxs-lookup"><span data-stu-id="f6cdd-111">Allow your **users** to provide their own usernames and passwords for any existing application accounts they are typing in manually on the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span></span>

-   <span data-ttu-id="f6cdd-112">autoriser un **membre du groupe d’entreprise** à spécifier les noms d’utilisateur et mots de passe affectés à un utilisateur à l’aide de la fonctionnalité [Accès aux applications en libre-service](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) ;</span><span class="sxs-lookup"><span data-stu-id="f6cdd-112">Allow a **member of the business group** to specify the usernames and passwords assigned to a user by using the [Self-Service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) feature</span></span>

-   <span data-ttu-id="f6cdd-113">autoriser un **administrateur** à spécifier les noms d’utilisateur et mots de passe affectés à un utilisateur à l’aide de la fonctionnalité Mettre à jour les informations d'identification lors de [l’affectation d’un utilisateur à une application](#assign-a-user-to-an-application-directly) ;</span><span class="sxs-lookup"><span data-stu-id="f6cdd-113">Allow an **administrator** to specify the usernames and passwords assigned to a user by using the Update Credentials feature when [assigning a user to an application](#assign-a-user-to-an-application-directly)</span></span>

-   <span data-ttu-id="f6cdd-114">autoriser un **administrateur** à spécifier les noms d’utilisateur et mots de passe partagés utilisés par un groupe de personnes à l’aide de la fonctionnalité Mettre à jour les informations d'identification lors de [l’affectation d’un groupe à une application](#assign-an-application-to-a-group-directly).</span><span class="sxs-lookup"><span data-stu-id="f6cdd-114">Allow an **administrator** to specify the shared username or password used by a group of people by using the Update Credentials feature when [assigning a group to an application](#assign-an-application-to-a-group-directly)</span></span>

<span data-ttu-id="f6cdd-115">Vous trouverez ci-dessous les instructions pour activer [l’authentification unique par mot de passe](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) pour une application qui a déjà été ajoutée à la [galerie d’applications Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span><span class="sxs-lookup"><span data-stu-id="f6cdd-115">Below describes how you can enable [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) to an application that is already in the [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="f6cdd-116">Vue d’ensemble des étapes requises</span><span class="sxs-lookup"><span data-stu-id="f6cdd-116">Overview of steps required</span></span>
<span data-ttu-id="f6cdd-117">Pour configurer une application à partir de la galerie Azure AD, vous devez effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="f6cdd-117">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="f6cdd-118">Ajouter une application à partir de la galerie Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6cdd-118">Add an application from the Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="f6cdd-119">Configurer l’application pour l’authentification unique basée sur un mot de passe</span><span class="sxs-lookup"><span data-stu-id="f6cdd-119">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="f6cdd-120">Affecter l’application à un utilisateur ou à un groupe</span><span class="sxs-lookup"><span data-stu-id="f6cdd-120">Assign the application to a user or a group</span></span>](#assign-the-application-to-a-user-or-a-group)

    -   [<span data-ttu-id="f6cdd-121">Affecter un utilisateur directement à une application</span><span class="sxs-lookup"><span data-stu-id="f6cdd-121">Assign a user to an application directly</span></span>](#assign-a-user-to-an-application-directly)

    -   [<span data-ttu-id="f6cdd-122">Affecter une application directement à un groupe</span><span class="sxs-lookup"><span data-stu-id="f6cdd-122">Assign an application to a group directly</span></span>](#assign-an-application-to-a-group-directly)

## <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="f6cdd-123">Ajouter une application à partir de la galerie Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6cdd-123">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="f6cdd-124">Pour ajouter une application à partir de la galerie Azure AD, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="f6cdd-124">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="f6cdd-125">Ouvrez le [portail Azure](https://portal.azure.com) et connectez-vous en tant qu’**administrateur général** ou **coadministrateur**</span><span class="sxs-lookup"><span data-stu-id="f6cdd-125">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="f6cdd-126">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-126">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f6cdd-127">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-127">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f6cdd-128">Cliquez sur **Applications d’entreprise** dans le menu de navigation gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-128">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="f6cdd-129">Cliquez sur le bouton **Ajouter** dans le coin supérieur droit du panneau **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-129">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="f6cdd-130">Dans la zone de texte **Entrer un nom** de la section **Ajouter à partir de la galerie**, tapez le nom de l’application.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-130">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application</span></span>

7.  <span data-ttu-id="f6cdd-131">Sélectionnez l’application pour laquelle vous souhaitez configurer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-131">Select the application you want to configure for single sign-on</span></span>

8.  <span data-ttu-id="f6cdd-132">Avant d’ajouter l’application, vous pouvez la renommer dans la zone de texte **Nom**.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-132">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="f6cdd-133">Pour ajouter l’application, cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-133">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="f6cdd-134">Après une courte période, vous pouvez voir le panneau de configuration de l’application.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-134">After a short period, you be able to see the application’s configuration blade.</span></span>

## <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="f6cdd-135">Configurer l’application pour l’authentification unique par mot de passe</span><span class="sxs-lookup"><span data-stu-id="f6cdd-135">Configure the application for password single sign-on</span></span>

<span data-ttu-id="f6cdd-136">Pour configurer l’authentification unique pour une application, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="f6cdd-136">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="f6cdd-137">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général** ou **coadministrateur**</span><span class="sxs-lookup"><span data-stu-id="f6cdd-137">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="f6cdd-138">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-138">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f6cdd-139">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-139">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f6cdd-140">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-140">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="f6cdd-141">Cliquez sur **Toutes les applications** pour afficher la liste complète de vos applications.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-141">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="f6cdd-142">Si l’application que vous recherchez ne figure pas dans la liste, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-142">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="f6cdd-143">Sélectionnez l’application pour laquelle vous souhaitez configurer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-143">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="f6cdd-144">Une fois l’application chargée, cliquez sur **Authentification unique** dans le menu de navigation gauche de l’application.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-144">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="f6cdd-145">Sélectionnez le mode **Authentification par mot de passe.**</span><span class="sxs-lookup"><span data-stu-id="f6cdd-145">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="f6cdd-146">[Affectez des utilisateurs à l’application](#assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="f6cdd-146">[Assign users to the application](#assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="f6cdd-147">En outre, vous pouvez également fournir des informations d’identification pour le compte de l’utilisateur en sélectionnant les lignes des utilisateurs, en cliquant sur **Mettre à jour les informations d’identification** et en entrant le nom d’utilisateur et le mot de passe à la place des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-147">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="f6cdd-148">Autrement, les utilisateurs doivent entrer les informations d’identification eux-mêmes lors du lancement.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-148">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="assign-a-user-to-an-application-directly"></a><span data-ttu-id="f6cdd-149">Affecter un utilisateur directement à une application</span><span class="sxs-lookup"><span data-stu-id="f6cdd-149">Assign a user to an application directly</span></span>

<span data-ttu-id="f6cdd-150">Pour affecter un ou plusieurs utilisateurs directement à une application, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f6cdd-150">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="f6cdd-151">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général.**</span><span class="sxs-lookup"><span data-stu-id="f6cdd-151">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="f6cdd-152">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-152">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f6cdd-153">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-153">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f6cdd-154">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-154">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="f6cdd-155">Cliquez sur **Toutes les applications** pour afficher la liste complète de vos applications.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-155">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="f6cdd-156">Si l’application que vous recherchez ne figure pas dans la liste, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications.**</span><span class="sxs-lookup"><span data-stu-id="f6cdd-156">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="f6cdd-157">Dans la liste qui s’affiche, sélectionnez l’application à laquelle vous souhaitez affecter un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-157">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="f6cdd-158">Une fois l’application chargée, cliquez sur **Utilisateurs et groupes** dans le menu de navigation de gauche de l’application.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-158">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="f6cdd-159">Cliquez sur le bouton **Ajouter** en haut de la liste **Utilisateurs et groupes** pour ouvrir le panneau **Ajouter une attribution**.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-159">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="f6cdd-160">Cliquez sur le sélecteur **Utilisateurs et groupes** à partir du panneau **Ajouter une attribution**.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-160">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="f6cdd-161">Tapez **le nom complet** ou **l’adresse de messagerie** de l’utilisateur souhaité pour l’attribution dans la zone de recherche **Rechercher par nom ou adresse de messagerie**.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-161">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="f6cdd-162">Pointez sur **l’utilisateur** dans la liste pour afficher une **case à cocher**.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-162">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="f6cdd-163">Cliquez sur la case à cocher en regard de la photo de profil ou du logo de l’utilisateur pour ajouter ce dernier à la liste **Sélectionné**.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-163">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="f6cdd-164">**Facultatif :** si vous souhaitez **ajouter plusieurs utilisateurs**, entrez un autre **nom complet** ou une autre **adresse de messagerie** dans la zone de recherche **Rechercher par nom ou adresse de messagerie**, puis cliquez sur la case à cocher pour ajouter cet utilisateur à la liste **Sélectionné**.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-164">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="f6cdd-165">Après avoir sélectionné les utilisateurs, cliquez sur le bouton **Sélectionner** pour les ajouter à la liste des utilisateurs et des groupes à affecter à l’application.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-165">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="f6cdd-166">**Facultatif :** cliquez sur le sélecteur **Sélectionner un rôle** dans le panneau **Ajouter une attribution** pour sélectionner un rôle à affecter aux utilisateurs que vous avez sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-166">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="f6cdd-167">Cliquez sur le bouton **Attribuer** pour affecter l’application aux utilisateurs sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-167">Click the **Assign** button to assign the application to the selected users.</span></span>

## <a name="assign-an-application-to-a-group-directly"></a><span data-ttu-id="f6cdd-168">Affecter une application directement à un groupe</span><span class="sxs-lookup"><span data-stu-id="f6cdd-168">Assign an application to a group directly</span></span>

<span data-ttu-id="f6cdd-169">Pour affecter un ou plusieurs groupes directement à une application, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f6cdd-169">To assign one or more groups to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="f6cdd-170">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant **qu’administrateur général**.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-170">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="f6cdd-171">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-171">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f6cdd-172">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-172">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f6cdd-173">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-173">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="f6cdd-174">Cliquez sur **Toutes les applications** pour afficher la liste complète de vos applications.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-174">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="f6cdd-175">Si l’application que vous recherchez ne figure pas dans la liste, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications.**</span><span class="sxs-lookup"><span data-stu-id="f6cdd-175">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="f6cdd-176">Dans la liste qui s’affiche, sélectionnez l’application à laquelle vous souhaitez affecter un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-176">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="f6cdd-177">Une fois l’application chargée, cliquez sur **Utilisateurs et groupes** dans le menu de navigation de gauche de l’application.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-177">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="f6cdd-178">Cliquez sur le bouton **Ajouter** en haut de la liste **Utilisateurs et groupes** pour ouvrir le panneau **Ajouter une attribution**.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-178">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="f6cdd-179">Cliquez sur le sélecteur **Utilisateurs et groupes** à partir du panneau **Ajouter une attribution**.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-179">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="f6cdd-180">Tapez le **nom de groupe complet** du groupe souhaité pour l’attribution dans la zone de recherche **Rechercher par nom ou adresse de messagerie**.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-180">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="f6cdd-181">Pointez sur le **groupe** dans la liste pour afficher une **case à cocher**.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-181">Hover over the **group** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="f6cdd-182">Cliquez sur la case à cocher en regard de la photo de profil ou du logo du groupe pour ajouter ce dernier à la liste **Sélectionné**.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-182">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="f6cdd-183">**Facultatif :** si vous souhaitez **ajouter plusieurs groupes**, entrez un autre **nom de groupe complet** dans la zone de recherche **Rechercher par nom ou adresse de messagerie**, puis cliquez sur la case à cocher pour ajouter ce groupe à la liste **Sélectionné**.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-183">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span></span>

13. <span data-ttu-id="f6cdd-184">Lorsque vous avez fini de sélectionner les groupes, cliquez sur le bouton **Sélectionner** pour les ajouter à la liste des utilisateurs et des groupes à affecter à l’application.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-184">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="f6cdd-185">**Facultatif :** cliquez sur le sélecteur **Sélectionner un rôle** dans le panneau **Ajouter une attribution** pour sélectionner un rôle à affecter aux groupes que vous avez sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-185">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span></span>

15. <span data-ttu-id="f6cdd-186">Cliquez sur le bouton **Attribuer** pour affecter l’application aux groupes sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-186">Click the **Assign** button to assign the application to the selected groups.</span></span>

<span data-ttu-id="f6cdd-187">Après une courte période, les utilisateurs que vous avez sélectionnés sont en mesure de lancer ces applications dans le panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="f6cdd-187">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6cdd-188">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f6cdd-188">Next steps</span></span>
[<span data-ttu-id="f6cdd-189">Fournir une authentification unique à vos applications avec le proxy d’application</span><span class="sxs-lookup"><span data-stu-id="f6cdd-189">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
