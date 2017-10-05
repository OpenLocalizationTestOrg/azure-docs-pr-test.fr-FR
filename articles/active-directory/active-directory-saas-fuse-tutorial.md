---
title: "Didacticiel : Intégration d’Azure AD à Fuse | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Fuse."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 5ef34f58-863a-4b37-875c-e8efa3e18bb3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 9a91e22faced9e126043bebefd85c307dbdf933d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fuse"></a><span data-ttu-id="d0d0f-103">Didacticiel : Intégration d’Azure Active Directory avec Fuse</span><span class="sxs-lookup"><span data-stu-id="d0d0f-103">Tutorial: Azure Active Directory integration with Fuse</span></span>

<span data-ttu-id="d0d0f-104">Dans ce didacticiel, vous allez apprendre à intégrer Fuse dans Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d0d0f-104">In this tutorial, you learn how to integrate Fuse with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d0d0f-105">L’intégration de Fuse dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="d0d0f-105">Integrating Fuse with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d0d0f-106">Dans Azure AD, vous pouvez contrôler qui a accès à Fuse.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-106">You can control in Azure AD who has access to Fuse.</span></span>
- <span data-ttu-id="d0d0f-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Fuse (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-107">You can enable your users to automatically get signed-on to Fuse (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="d0d0f-108">Vous pouvez gérer vos comptes dans un emplacement central : le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="d0d0f-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d0d0f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d0d0f-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d0d0f-110">Prerequisites</span></span>

<span data-ttu-id="d0d0f-111">Pour configurer l’intégration d’Azure AD avec Fuse, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="d0d0f-111">To configure Azure AD integration with Fuse, you need the following items:</span></span>

- <span data-ttu-id="d0d0f-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0d0f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d0d0f-113">Un abonnement Fuse pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="d0d0f-113">A Fuse single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d0d0f-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d0d0f-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="d0d0f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d0d0f-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d0d0f-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d0d0f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d0d0f-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="d0d0f-118">Scenario description</span></span>
<span data-ttu-id="d0d0f-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d0d0f-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="d0d0f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d0d0f-121">Ajouter Fuse depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="d0d0f-121">Add Fuse from the gallery</span></span>
2. <span data-ttu-id="d0d0f-122">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0d0f-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-fuse-from-the-gallery"></a><span data-ttu-id="d0d0f-123">Ajouter Fuse depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="d0d0f-123">Add Fuse from the gallery</span></span>
<span data-ttu-id="d0d0f-124">Pour configurer l’intégration de Fuse avec Azure AD, vous devez ajouter Fuse disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-124">To configure the integration of Fuse into Azure AD, you need to add Fuse from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d0d0f-125">**Pour ajouter Fuse à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d0d0f-125">**To add Fuse from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d0d0f-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Bouton Azure Active Directory][1]

2. <span data-ttu-id="d0d0f-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d0d0f-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-129">Then go to **All applications**.</span></span>

    ![Panneau Applications d’entreprise][2]
    
3. <span data-ttu-id="d0d0f-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Bouton Nouvelle application][3]

4. <span data-ttu-id="d0d0f-133">Dans la zone de recherche, tapez **Fuse**, sélectionnez **Fuse** dans le volet de résultats, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-133">In the search box, type **Fuse**, select **Fuse** from result panel then click **Add** button to add the application.</span></span>

    ![Fuse dans la liste des résultats](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d0d0f-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0d0f-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="d0d0f-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Fuse, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="d0d0f-136">In this section, you configure and test Azure AD single sign-on with Fuse based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d0d0f-137">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Fuse correspondant dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Fuse is to a user in Azure AD.</span></span> <span data-ttu-id="d0d0f-138">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Fuse associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-138">In other words, a link relationship between an Azure AD user and the related user in Fuse needs to be established.</span></span>

<span data-ttu-id="d0d0f-139">Dans Fuse, assignez la valeur du **nom d’utilisateur** d’Azure AD comme valeur de **Username** (Nom d’utilisateur) pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-139">In Fuse, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d0d0f-140">Pour configurer et tester l’authentification unique Azure AD avec Fuse, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="d0d0f-140">To configure and test Azure AD single sign-on with Fuse, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d0d0f-141">**[Configurer l’authentification unique Azure AD](#configure-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d0d0f-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d0d0f-143">**[Créer un utilisateur de test Fuse](#create-a-fuse-test-user)** pour avoir dans Fuse un équivalent de Britta Simon lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-143">**[Create a Fuse test user](#create-a-fuse-test-user)** - to have a counterpart of Britta Simon in Fuse that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d0d0f-144">**[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d0d0f-145">**[Tester l’authentification unique](#test-single-sign-on)** : pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="d0d0f-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0d0f-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="d0d0f-147">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Fuse.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Fuse application.</span></span>

<span data-ttu-id="d0d0f-148">**Pour configurer l’authentification unique Azure AD avec Fuse, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d0d0f-148">**To configure Azure AD single sign-on with Fuse, perform the following steps:**</span></span>

1. <span data-ttu-id="d0d0f-149">Dans le portail Azure, dans la page d’intégration de l’application **Fuse**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-149">In the Azure portal, on the **Fuse** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="d0d0f-151">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_samlbase.png)

3. <span data-ttu-id="d0d0f-153">Dans la section **Domaine et URL Fuse**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="d0d0f-153">On the **Fuse Domain and URLs** section, perform the following steps:</span></span>

    ![Informations d’authentification unique dans Fuse Domain and URLs (Domaine et URL Fuse)](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_url.png)
    
    <span data-ttu-id="d0d0f-155">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<tenant name>.fusion-universal.com/`</span><span class="sxs-lookup"><span data-stu-id="d0d0f-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant name>.fusion-universal.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d0d0f-156">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-156">This value is not real.</span></span> <span data-ttu-id="d0d0f-157">Mettez à jour cette valeur avec l’URL de connexion réelle.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-157">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="d0d0f-158">Pour obtenir cette valeur, contactez l’[équipe de support client Fuse](mailto:support@fusion-universal.com).</span><span class="sxs-lookup"><span data-stu-id="d0d0f-158">Contact [Fuse Client support team](mailto:support@fusion-universal.com) to get this value.</span></span> 
 
4. <span data-ttu-id="d0d0f-159">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (brut)**, puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-159">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span></span>

    ![Lien Téléchargement de certificat](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_certificate.png) 

5. <span data-ttu-id="d0d0f-161">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="d0d0f-161">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-fuse-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d0d0f-163">Dans la section **Configuration de Fuse** , cliquez sur **Configurer Fuse** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-163">On the **Fuse Configuration** section, click **Configure Fuse** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d0d0f-164">Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="d0d0f-164">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuration de Fuse](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_configure.png) 

7. <span data-ttu-id="d0d0f-166">Pour configurer l’authentification unique de votre application, contactez l’[équipe de support Fuse](mailto:support@fusion-universal.com) et fournissez-lui les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="d0d0f-166">To get SSO configured for your application, contact [Fuse support team](mailto:support@fusion-universal.com) and provide them with the following:</span></span>

    * <span data-ttu-id="d0d0f-167">Le **fichier de certificat (brut)** téléchargé</span><span class="sxs-lookup"><span data-stu-id="d0d0f-167">The downloaded **Certificate (Raw) file**</span></span>
    * <span data-ttu-id="d0d0f-168">L’**URL du service d’authentification unique SAML**</span><span class="sxs-lookup"><span data-stu-id="d0d0f-168">The **SAML Single Sign-On Service URL**</span></span>
    * <span data-ttu-id="d0d0f-169">L’**ID d’entité SAML**</span><span class="sxs-lookup"><span data-stu-id="d0d0f-169">The **SAML Entity ID**</span></span>
    * <span data-ttu-id="d0d0f-170">L’**URL de déconnexion**</span><span class="sxs-lookup"><span data-stu-id="d0d0f-170">The **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="d0d0f-171">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d0d0f-172">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d0d0f-173">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d0d0f-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d0d0f-174">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0d0f-174">Create an Azure AD test user</span></span>

<span data-ttu-id="d0d0f-175">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="d0d0f-177">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d0d0f-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d0d0f-178">Dans le volet gauche du Portail Azure, cliquez sur le bouton **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Bouton Azure Active Directory](./media/active-directory-saas-fuse-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="d0d0f-180">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Liens « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/active-directory-saas-fuse-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="d0d0f-182">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Bouton Ajouter](./media/active-directory-saas-fuse-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="d0d0f-184">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="d0d0f-184">In the **User** dialog box, perform the following steps:</span></span>

    ![Boîte de dialogue Utilisateur](./media/active-directory-saas-fuse-tutorial/create_aaduser_04.png)

    <span data-ttu-id="d0d0f-186">a.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-186">a.</span></span> <span data-ttu-id="d0d0f-187">Dans la zone **Nom**, tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-187">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d0d0f-188">b.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-188">b.</span></span> <span data-ttu-id="d0d0f-189">Dans la zone **Nom d’utilisateur** , tapez l’adresse e-mail de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-189">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="d0d0f-190">c.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-190">c.</span></span> <span data-ttu-id="d0d0f-191">Cochez la case **Afficher le mot de passe**, puis notez la valeur affichée dans le champ **Mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="d0d0f-192">d.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-192">d.</span></span> <span data-ttu-id="d0d0f-193">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-193">Click **Create**.</span></span>
 
### <a name="create-a-fuse-test-user"></a><span data-ttu-id="d0d0f-194">Créer un utilisateur de test Fuse</span><span class="sxs-lookup"><span data-stu-id="d0d0f-194">Create a Fuse test user</span></span>

<span data-ttu-id="d0d0f-195">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Fuse.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-195">In this section, you create a user called Britta Simon in Fuse.</span></span> <span data-ttu-id="d0d0f-196">Collaborez avec l’[équipe du support technique Fuse](mailto:support@fusion-universal.com) pour ajouter des utilisateurs dans la plate-forme Fuse.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-196">Please work with [Fuse support team](mailto:support@fusion-universal.com) to add the users in the Fuse platform.</span></span>


### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="d0d0f-197">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0d0f-197">Assign the Azure AD test user</span></span>

<span data-ttu-id="d0d0f-198">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Fuse.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Fuse.</span></span>

![Attribuer le rôle d’utilisateur][200] 

<span data-ttu-id="d0d0f-200">**Pour affecter Britta Simon à Fuse, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d0d0f-200">**To assign Britta Simon to Fuse, perform the following steps:**</span></span>

1. <span data-ttu-id="d0d0f-201">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="d0d0f-203">Dans la liste des applications, sélectionnez **Fuse**.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-203">In the applications list, select **Fuse**.</span></span>

    ![Lien Fuse dans la liste des applications](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_app.png)  

3. <span data-ttu-id="d0d0f-205">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Lien « Utilisateurs et groupes »][202]

4. <span data-ttu-id="d0d0f-207">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-207">Click **Add** button.</span></span> <span data-ttu-id="d0d0f-208">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Volet Ajouter une attribution][203]

5. <span data-ttu-id="d0d0f-210">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d0d0f-211">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d0d0f-212">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="d0d0f-213">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="d0d0f-213">Test single sign-on</span></span>

<span data-ttu-id="d0d0f-214">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d0d0f-215">Lorsque vous cliquez sur la vignette Fuse dans le volet d’accès, vous devez être connecté automatiquement à votre application Fuse.</span><span class="sxs-lookup"><span data-stu-id="d0d0f-215">When you click the Fuse tile in the Access Panel, you should get automatically signed-on to your Fuse application.</span></span>
<span data-ttu-id="d0d0f-216">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d0d0f-216">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d0d0f-217">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="d0d0f-217">Additional resources</span></span>

* [<span data-ttu-id="d0d0f-218">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d0d0f-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d0d0f-219">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="d0d0f-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_203.png

