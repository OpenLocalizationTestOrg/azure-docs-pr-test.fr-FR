---
title: "Didacticiel : Intégration d’Azure Active Directory à Nomadic | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Nomadic."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 13d02b1c-d98a-40b1-824f-afa45a2deb6a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 1817a1395c2ffa7268abfff268d9d041f7f21a57
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-nomadic"></a><span data-ttu-id="f7e1f-103">Didacticiel : Intégration d’Azure Active Directory à Nomadic</span><span class="sxs-lookup"><span data-stu-id="f7e1f-103">Tutorial: Azure Active Directory integration with Nomadic</span></span>

<span data-ttu-id="f7e1f-104">Dans ce didacticiel, vous découvrez comment intégrer Nomadic à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f7e1f-104">In this tutorial, you learn how to integrate Nomadic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f7e1f-105">L’intégration de Nomadic à Azure AD vous procure les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="f7e1f-105">Integrating Nomadic with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f7e1f-106">Dans Azure AD, vous pouvez contrôler qui a accès à Nomadic.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-106">You can control in Azure AD who has access to Nomadic.</span></span>
- <span data-ttu-id="f7e1f-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Nomadic (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-107">You can enable your users to automatically get signed-on to Nomadic (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="f7e1f-108">Vous pouvez gérer vos comptes dans un emplacement central : le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="f7e1f-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f7e1f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f7e1f-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f7e1f-110">Prerequisites</span></span>

<span data-ttu-id="f7e1f-111">Pour configurer l’intégration d’Azure AD à Nomadic, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f7e1f-111">To configure Azure AD integration with Nomadic, you need the following items:</span></span>

- <span data-ttu-id="f7e1f-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="f7e1f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f7e1f-113">Un abonnement Nomadic pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="f7e1f-113">A Nomadic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f7e1f-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f7e1f-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="f7e1f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f7e1f-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f7e1f-117">Si vous ne disposez pas d’un environnement d’essai Azure AD, vous pouvez [vous inscrire pour un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f7e1f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f7e1f-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="f7e1f-118">Scenario description</span></span>
<span data-ttu-id="f7e1f-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f7e1f-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="f7e1f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f7e1f-121">Ajouter Nomadic depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="f7e1f-121">Add Nomadic from the gallery</span></span>
2. <span data-ttu-id="f7e1f-122">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f7e1f-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-nomadic-from-the-gallery"></a><span data-ttu-id="f7e1f-123">Ajouter Nomadic depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="f7e1f-123">Add Nomadic from the gallery</span></span>
<span data-ttu-id="f7e1f-124">Pour configurer l’intégration de Nomadic dans Azure AD, vous devez ajouter Nomadic depuis la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-124">To configure the integration of Nomadic into Azure AD, you need to add Nomadic from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f7e1f-125">**Pour ajouter Nomadic à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f7e1f-125">**To add Nomadic from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f7e1f-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Bouton Azure Active Directory][1]

2. <span data-ttu-id="f7e1f-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f7e1f-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-129">Then go to **All applications**.</span></span>

    ![Panneau Applications d’entreprise][2]
    
3. <span data-ttu-id="f7e1f-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Bouton Nouvelle application][3]

4. <span data-ttu-id="f7e1f-133">Dans la zone de recherche, tapez **Nomadic**, sélectionnez **Nomadic** dans le volet de résultats, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-133">In the search box, type **Nomadic**, select **Nomadic** from result panel then click **Add** button to add the application.</span></span>

    ![Nomadic dans la liste des résultats](./media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f7e1f-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f7e1f-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="f7e1f-136">Dans cette section, vous configurez et vous testez l’authentification unique Azure AD avec Nomadic, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="f7e1f-136">In this section, you configure and test Azure AD single sign-on with Nomadic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f7e1f-137">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Nomadic équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Nomadic is to a user in Azure AD.</span></span> <span data-ttu-id="f7e1f-138">En d’autres termes, une relation de liaison entre un utilisateur Azure AD et l’utilisateur Nomadic associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-138">In other words, a link relationship between an Azure AD user and the related user in Nomadic needs to be established.</span></span>

<span data-ttu-id="f7e1f-139">Dans Nomadic, assignez la valeur du **nom d’utilisateur** d’Azure AD comme valeur de **Username** (Nom d’utilisateur) pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-139">In Nomadic, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f7e1f-140">Pour configurer et tester l’authentification unique Azure AD avec Nomadic, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="f7e1f-140">To configure and test Azure AD single sign-on with Nomadic, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f7e1f-141">**[Configurer l’authentification unique Azure AD](#configure-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f7e1f-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f7e1f-143">**[Créer un utilisateur de test Nomadic](#create-a-nomadic-test-user)** pour avoir dans Nomadic un équivalent de Britta Simon lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-143">**[Create a Nomadic test user](#create-a-nomadic-test-user)** - to have a counterpart of Britta Simon in Nomadic that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f7e1f-144">**[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f7e1f-145">**[Tester l’authentification unique](#test-single-sign-on)** : pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="f7e1f-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f7e1f-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="f7e1f-147">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Nomadic.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Nomadic application.</span></span>

<span data-ttu-id="f7e1f-148">**Pour configurer l’authentification unique Azure AD avec Nomadic, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f7e1f-148">**To configure Azure AD single sign-on with Nomadic, perform the following steps:**</span></span>

1. <span data-ttu-id="f7e1f-149">Dans le portail Azure, dans la page d’intégration de l’application **Nomadic**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-149">In the Azure portal, on the **Nomadic** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="f7e1f-151">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_samlbase.png)

3. <span data-ttu-id="f7e1f-153">Dans la section **Nomadic Domain and URLs** (Domaine et URL Nomadic), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f7e1f-153">On the **Nomadic Domain and URLs** section, perform the following steps:</span></span>

    ![Informations d’authentification unique dans Nomadic Domain and URLs (Domaine et URL Nomadic)](./media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_url.png)

    <span data-ttu-id="f7e1f-155">a.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-155">a.</span></span> <span data-ttu-id="f7e1f-156">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<company name>.nomadic.fm/signin`</span><span class="sxs-lookup"><span data-stu-id="f7e1f-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.nomadic.fm/signin`</span></span>

    <span data-ttu-id="f7e1f-157">b.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-157">b.</span></span> <span data-ttu-id="f7e1f-158">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<company name>.nomadic.fm/auth/saml2/sp`, `https://<company name>.staging.nomadic.fm/auth/saml2/sp`</span><span class="sxs-lookup"><span data-stu-id="f7e1f-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.nomadic.fm/auth/saml2/sp`, `https://<company name>.staging.nomadic.fm/auth/saml2/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f7e1f-159">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-159">These values are not real.</span></span> <span data-ttu-id="f7e1f-160">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f7e1f-161">Pour obtenir ces valeurs, contactez l’[équipe de support client Nomadic](mailto:help@nomadic.fm).</span><span class="sxs-lookup"><span data-stu-id="f7e1f-161">Contact [Nomadic Client support team](mailto:help@nomadic.fm) to get these values.</span></span> 
 


4. <span data-ttu-id="f7e1f-162">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Lien Téléchargement de certificat](./media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_certificate.png) 

5. <span data-ttu-id="f7e1f-164">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="f7e1f-164">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-nomadic-tutorial/tutorial_general_400.png)

6.  <span data-ttu-id="f7e1f-166">Pour obtenir la configuration de l’authentification unique pour votre application, contactez l’[équipe de support Nomadic](mailto:help@nomadic.fm) en lui fournissant les **métadonnées** téléchargées.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-166">To get SSO configured for your application, contact [Nomadic support team](mailto:help@nomadic.fm) and provide them with the downloaded **metadata**.</span></span>

> [!TIP]
> <span data-ttu-id="f7e1f-167">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f7e1f-168">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f7e1f-169">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f7e1f-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f7e1f-170">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="f7e1f-170">Create an Azure AD test user</span></span>

<span data-ttu-id="f7e1f-171">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="f7e1f-173">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f7e1f-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f7e1f-174">Dans le volet gauche du Portail Azure, cliquez sur le bouton **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-174">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Bouton Azure Active Directory](./media/active-directory-saas-nomadic-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="f7e1f-176">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-176">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Liens « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/active-directory-saas-nomadic-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="f7e1f-178">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-178">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Bouton Ajouter](./media/active-directory-saas-nomadic-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="f7e1f-180">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f7e1f-180">In the **User** dialog box, perform the following steps:</span></span>

    ![Boîte de dialogue Utilisateur](./media/active-directory-saas-nomadic-tutorial/create_aaduser_04.png)

    <span data-ttu-id="f7e1f-182">a.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-182">a.</span></span> <span data-ttu-id="f7e1f-183">Dans la zone **Nom**, tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-183">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f7e1f-184">b.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-184">b.</span></span> <span data-ttu-id="f7e1f-185">Dans la zone **Nom d’utilisateur** , tapez l’adresse e-mail de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-185">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="f7e1f-186">c.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-186">c.</span></span> <span data-ttu-id="f7e1f-187">Cochez la case **Afficher le mot de passe**, puis notez la valeur affichée dans le champ **Mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-187">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="f7e1f-188">d.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-188">d.</span></span> <span data-ttu-id="f7e1f-189">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-189">Click **Create**.</span></span>
 
### <a name="create-a-nomadic-test-user"></a><span data-ttu-id="f7e1f-190">Créer un utilisateur de test Nomadic</span><span class="sxs-lookup"><span data-stu-id="f7e1f-190">Create a Nomadic test user</span></span>

<span data-ttu-id="f7e1f-191">Dans cette section, vous créez un utilisateur nommé Britta Simon dans Nomadic.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-191">In this section, you create a user called Britta Simon in Nomadic.</span></span> <span data-ttu-id="f7e1f-192">Collaborez avec [l’équipe du support technique Nomadic](mailto:help@nomadic.fm) pour ajouter des utilisateurs dans la plateforme Nomadic.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-192">Please work with [Nomadic support team](mailto:help@nomadic.fm) to add the users in the Nomadic platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="f7e1f-193">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="f7e1f-193">Assign the Azure AD test user</span></span>

<span data-ttu-id="f7e1f-194">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Nomadic.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Nomadic.</span></span>

![Attribuer le rôle d’utilisateur][200] 

<span data-ttu-id="f7e1f-196">**Pour affecter Britta Simon à Nomadic, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f7e1f-196">**To assign Britta Simon to Nomadic, perform the following steps:**</span></span>

1. <span data-ttu-id="f7e1f-197">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="f7e1f-199">Dans la liste des applications, sélectionnez **Nomadic**.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-199">In the applications list, select **Nomadic**.</span></span>

    ![Lien Nomadic dans la liste des applications](./media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_app.png)  

3. <span data-ttu-id="f7e1f-201">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-201">In the menu on the left, click **Users and groups**.</span></span>

    ![Lien « Utilisateurs et groupes »][202]

4. <span data-ttu-id="f7e1f-203">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-203">Click **Add** button.</span></span> <span data-ttu-id="f7e1f-204">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Volet Ajouter une attribution][203]

5. <span data-ttu-id="f7e1f-206">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f7e1f-207">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f7e1f-208">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="f7e1f-209">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="f7e1f-209">Test single sign-on</span></span>

<span data-ttu-id="f7e1f-210">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f7e1f-211">Quand vous cliquez sur la vignette Nomadic dans le panneau d’accès, vous devez être connecté automatiquement à votre application Nomadic.</span><span class="sxs-lookup"><span data-stu-id="f7e1f-211">When you click the Nomadic tile in the Access Panel, you should get automatically signed-on to your Nomadic application.</span></span>
<span data-ttu-id="f7e1f-212">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f7e1f-212">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f7e1f-213">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="f7e1f-213">Additional resources</span></span>

* [<span data-ttu-id="f7e1f-214">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f7e1f-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f7e1f-215">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="f7e1f-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_203.png

