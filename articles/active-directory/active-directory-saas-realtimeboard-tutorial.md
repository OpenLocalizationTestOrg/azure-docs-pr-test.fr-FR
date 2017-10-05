---
title: "Didacticiel : Intégration d’Azure Active Directory à RealtimeBoard | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et RealtimeBoard."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: a37fc1c0-4bae-4173-989b-00de53a0076f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: jeedes
ms.openlocfilehash: d3ba8cb1f7e1d4332f7912848e8b6902d9acf909
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-realtimeboard"></a><span data-ttu-id="c1754-103">Didacticiel : Intégration d’Azure Active Directory à RealtimeBoard</span><span class="sxs-lookup"><span data-stu-id="c1754-103">Tutorial: Azure Active Directory integration with RealtimeBoard</span></span>

<span data-ttu-id="c1754-104">Dans ce didacticiel, vous allez apprendre à intégrer RealtimeBoard à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c1754-104">In this tutorial, you learn how to integrate RealtimeBoard with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c1754-105">L’intégration de RealtimeBoard à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="c1754-105">Integrating RealtimeBoard with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c1754-106">Dans Azure AD, vous pouvez contrôler qui a accès à RealtimeBoard.</span><span class="sxs-lookup"><span data-stu-id="c1754-106">You can control in Azure AD who has access to RealtimeBoard.</span></span>
- <span data-ttu-id="c1754-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à RealtimeBoard (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c1754-107">You can enable your users to automatically get signed-on to RealtimeBoard (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="c1754-108">Vous pouvez gérer vos comptes dans un emplacement central : le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c1754-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="c1754-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c1754-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c1754-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c1754-110">Prerequisites</span></span>

<span data-ttu-id="c1754-111">Pour configurer l’intégration d’Azure AD à RealtimeBoard, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="c1754-111">To configure Azure AD integration with RealtimeBoard, you need the following items:</span></span>

- <span data-ttu-id="c1754-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1754-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c1754-113">Un abonnement RealtimeBoard pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="c1754-113">A RealtimeBoard single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c1754-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="c1754-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c1754-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="c1754-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c1754-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="c1754-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c1754-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c1754-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c1754-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="c1754-118">Scenario description</span></span>
<span data-ttu-id="c1754-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="c1754-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c1754-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="c1754-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c1754-121">Ajout de RealtimeBoard à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="c1754-121">Adding RealtimeBoard from the gallery</span></span>
2. <span data-ttu-id="c1754-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1754-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-realtimeboard-from-the-gallery"></a><span data-ttu-id="c1754-123">Ajout de RealtimeBoard à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="c1754-123">Adding RealtimeBoard from the gallery</span></span>
<span data-ttu-id="c1754-124">Pour configurer l’intégration de RealtimeBoard à Azure AD, vous devez ajouter RealtimeBoard à votre liste d’applications SaaS gérées, depuis la galerie.</span><span class="sxs-lookup"><span data-stu-id="c1754-124">To configure the integration of RealtimeBoard into Azure AD, you need to add RealtimeBoard from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c1754-125">**Pour ajouter RealtimeBoard à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c1754-125">**To add RealtimeBoard from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c1754-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c1754-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Bouton Azure Active Directory][1]

2. <span data-ttu-id="c1754-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="c1754-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c1754-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="c1754-129">Then go to **All applications**.</span></span>

    ![Panneau Applications d’entreprise][2]
    
3. <span data-ttu-id="c1754-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="c1754-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Bouton Nouvelle application][3]

4. <span data-ttu-id="c1754-133">Dans la zone de recherche, tapez **RealtimeBoard**, sélectionnez **RealtimeBoard** dans le volet de résultats, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="c1754-133">In the search box, type **RealtimeBoard**, select **RealtimeBoard** from result panel then click **Add** button to add the application.</span></span>

    ![RealtimeBoard dans la liste des résultats](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c1754-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1754-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="c1754-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec RealtimeBoard via un utilisateur de test, appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="c1754-136">In this section, you configure and test Azure AD single sign-on with RealtimeBoard based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c1754-137">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur RealtimeBoard équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c1754-137">For single sign-on to work, Azure AD needs to know what the counterpart user in RealtimeBoard is to a user in Azure AD.</span></span> <span data-ttu-id="c1754-138">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur RealtimeBoard associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="c1754-138">In other words, a link relationship between an Azure AD user and the related user in RealtimeBoard needs to be established.</span></span>

<span data-ttu-id="c1754-139">Dans RealtimeBoard, assignez la valeur de **nom d’utilisateur** dans Azure AD comme valeur **Nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="c1754-139">In RealtimeBoard, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c1754-140">Pour configurer et tester l’authentification unique Azure AD avec RealtimeBoard, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="c1754-140">To configure and test Azure AD single sign-on with RealtimeBoard, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c1754-141">**[Configurer l’authentification unique Azure AD](#configure-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="c1754-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c1754-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c1754-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c1754-143">**[Créer un utilisateur de test RealtimeBoard](#create-a-realtimeboard-test-user)** pour avoir un équivalent de Britta Simon dans RealtimeBoard, lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c1754-143">**[Create a RealtimeBoard test user](#create-a-realtimeboard-test-user)** - to have a counterpart of Britta Simon in RealtimeBoard that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c1754-144">**[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c1754-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c1754-145">**[Tester l’authentification unique](#test-single-sign-on)** : pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="c1754-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="c1754-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1754-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="c1754-147">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application RealtimeBoard.</span><span class="sxs-lookup"><span data-stu-id="c1754-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your RealtimeBoard application.</span></span>

<span data-ttu-id="c1754-148">**Pour configurer l'authentification unique Azure AD avec RealtimeBoard, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c1754-148">**To configure Azure AD single sign-on with RealtimeBoard, perform the following steps:**</span></span>

1. <span data-ttu-id="c1754-149">Dans le portail Azure, sur la page d’intégration de l’application **RealtimeBoard**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="c1754-149">In the Azure portal, on the **RealtimeBoard** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="c1754-151">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c1754-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_samlbase.png)

3. <span data-ttu-id="c1754-153">Dans la section **Domaines et URL RealtimeBoard**, si vous souhaitez configurer l’application en mode initié par **IDP**, suivez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="c1754-153">On the **RealtimeBoard Domain and URLs** section, if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Informations d’authentification unique dans Domaine et URL RealtimeBoard](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_url.png)

    <span data-ttu-id="c1754-155">Dans la zone de texte **Identificateur**, tapez une URL comme : `https://realtimeboard.com/`</span><span class="sxs-lookup"><span data-stu-id="c1754-155">In the **Identifier** textbox, type a URL as: `https://realtimeboard.com/`</span></span>

4. <span data-ttu-id="c1754-156">Cochez **Afficher les paramètres d’URL avancés** si vous souhaitez configurer l’application en mode lancé par le **fournisseur de service** :</span><span class="sxs-lookup"><span data-stu-id="c1754-156">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_url2.png)

    <span data-ttu-id="c1754-158">Dans la zone de texte **URL d’authentification**, tapez l’URL : `https://realtimeboard.com/sso/saml`</span><span class="sxs-lookup"><span data-stu-id="c1754-158">In the **Sign-on URL** textbox, type a URL as: `https://realtimeboard.com/sso/saml`</span></span>

5. <span data-ttu-id="c1754-159">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="c1754-159">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Lien Téléchargement de certificat](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_certificate.png) 

6. <span data-ttu-id="c1754-161">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="c1754-161">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="c1754-163">Pour configurer l’authentification unique côté **RealtimeBoard**, vous devez envoyer le fichier **XML de métadonnées** téléchargé à [l’équipe de support technique de RealtimeBoard](mailto:support@realtimeboard.com).</span><span class="sxs-lookup"><span data-stu-id="c1754-163">To configure single sign-on on **RealtimeBoard** side, you need to send the downloaded **Metadata XML** to [RealtimeBoard support team](mailto:support@realtimeboard.com).</span></span> <span data-ttu-id="c1754-164">Celles-ci configurent ensuite ce paramètre pour que la connexion SSO SAML soit définie correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="c1754-164">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="c1754-165">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="c1754-165">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c1754-166">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="c1754-166">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c1754-167">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c1754-167">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c1754-168">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1754-168">Create an Azure AD test user</span></span>

<span data-ttu-id="c1754-169">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c1754-169">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="c1754-171">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c1754-171">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c1754-172">Dans le volet gauche du Portail Azure, cliquez sur le bouton **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c1754-172">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Bouton Azure Active Directory](./media/active-directory-saas-realtimeboard-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="c1754-174">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="c1754-174">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Liens « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/active-directory-saas-realtimeboard-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="c1754-176">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="c1754-176">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Bouton Ajouter](./media/active-directory-saas-realtimeboard-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="c1754-178">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c1754-178">In the **User** dialog box, perform the following steps:</span></span>

    ![Boîte de dialogue Utilisateur](./media/active-directory-saas-realtimeboard-tutorial/create_aaduser_04.png)

    <span data-ttu-id="c1754-180">a.</span><span class="sxs-lookup"><span data-stu-id="c1754-180">a.</span></span> <span data-ttu-id="c1754-181">Dans la zone **Nom**, tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c1754-181">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c1754-182">b.</span><span class="sxs-lookup"><span data-stu-id="c1754-182">b.</span></span> <span data-ttu-id="c1754-183">Dans la zone **Nom d’utilisateur** , tapez l’adresse e-mail de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c1754-183">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="c1754-184">c.</span><span class="sxs-lookup"><span data-stu-id="c1754-184">c.</span></span> <span data-ttu-id="c1754-185">Cochez la case **Afficher le mot de passe**, puis notez la valeur affichée dans le champ **Mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="c1754-185">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="c1754-186">d.</span><span class="sxs-lookup"><span data-stu-id="c1754-186">d.</span></span> <span data-ttu-id="c1754-187">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="c1754-187">Click **Create**.</span></span>
 
### <a name="create-a-realtimeboard-test-user"></a><span data-ttu-id="c1754-188">Créer un utilisateur RealtimeBoard de test</span><span class="sxs-lookup"><span data-stu-id="c1754-188">Create a RealtimeBoard test user</span></span>

<span data-ttu-id="c1754-189">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans RealtimeBoard.</span><span class="sxs-lookup"><span data-stu-id="c1754-189">The objective of this section is to create a user called Britta Simon in RealtimeBoard.</span></span> <span data-ttu-id="c1754-190">RealtimeBoard prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="c1754-190">RealtimeBoard supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="c1754-191">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="c1754-191">There is no action item for you in this section.</span></span> <span data-ttu-id="c1754-192">S’il n’y a pas déjà un utilisateur dans RealtimeBoard, un utilisateur est créé lorsque vous tentez d’y accéder.</span><span class="sxs-lookup"><span data-stu-id="c1754-192">If a user doesn't already exist in RealtimeBoard, a new one is created when you attempt to access RealtimeBoard.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="c1754-193">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1754-193">Assign the Azure AD test user</span></span>

<span data-ttu-id="c1754-194">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à RealtimeBoard.</span><span class="sxs-lookup"><span data-stu-id="c1754-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to RealtimeBoard.</span></span>

![Assigner le rôle d’utilisateur][200] 

<span data-ttu-id="c1754-196">**Pour affecter Britta Simon à RealtimeBoard, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c1754-196">**To assign Britta Simon to RealtimeBoard, perform the following steps:**</span></span>

1. <span data-ttu-id="c1754-197">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="c1754-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="c1754-199">Dans la liste des applications, sélectionnez **RealtimeBoard**.</span><span class="sxs-lookup"><span data-stu-id="c1754-199">In the applications list, select **RealtimeBoard**.</span></span>

    ![Lien correspondant à RealtimeBoard dans la liste Applications](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_app.png)  

3. <span data-ttu-id="c1754-201">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="c1754-201">In the menu on the left, click **Users and groups**.</span></span>

    ![Lien « Utilisateurs et groupes »][202]

4. <span data-ttu-id="c1754-203">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="c1754-203">Click **Add** button.</span></span> <span data-ttu-id="c1754-204">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="c1754-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Volet Ajouter une attribution][203]

5. <span data-ttu-id="c1754-206">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="c1754-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c1754-207">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="c1754-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c1754-208">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="c1754-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="c1754-209">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="c1754-209">Test single sign-on</span></span>

<span data-ttu-id="c1754-210">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="c1754-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c1754-211">Lorsque vous cliquez sur la vignette RealtimeBoard dans le volet d’accès, vous êtes connecté automatiquement à votre application RealtimeBoard.</span><span class="sxs-lookup"><span data-stu-id="c1754-211">When you click the RealtimeBoard tile in the Access Panel, you should get automatically signed-on to your RealtimeBoard application.</span></span>
<span data-ttu-id="c1754-212">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c1754-212">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c1754-213">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="c1754-213">Additional resources</span></span>

* [<span data-ttu-id="c1754-214">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c1754-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c1754-215">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="c1754-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_203.png

