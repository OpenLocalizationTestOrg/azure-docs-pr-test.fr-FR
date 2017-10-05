---
title: "Didacticiel : Intégrer Azure Active Directory dans vxMaintain | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et vxMaintain."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 841a1066-593c-4603-9abe-f48496d73d10
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: ad87534af448356b8cc80d8ddd278bfb8a9165e7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-vxmaintain"></a><span data-ttu-id="18e31-103">Didacticiel : Intégrer Azure Active Directory dans vxMaintain</span><span class="sxs-lookup"><span data-stu-id="18e31-103">Tutorial: Integrate Azure Active Directory with vxMaintain</span></span>

<span data-ttu-id="18e31-104">Dans ce didacticiel, vous allez apprendre à intégrer vxMaintain à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="18e31-104">In this tutorial, you learn how to integrate vxMaintain with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="18e31-105">Cette intégration offre plusieurs avantages importants.</span><span class="sxs-lookup"><span data-stu-id="18e31-105">This integration provides several important benefits.</span></span> <span data-ttu-id="18e31-106">Vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="18e31-106">You can:</span></span>

- <span data-ttu-id="18e31-107">Contrôler qui a accès à vxMaintain dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="18e31-107">Control in Azure AD who has access to vxMaintain.</span></span>
- <span data-ttu-id="18e31-108">Autoriser vos utilisateurs à se connecter automatiquement à vxMaintain par le biais de l’authentification unique, avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="18e31-108">Enable your users to automatically sign in to vxMaintain with single sign-on (SSO) by using their Azure AD accounts.</span></span>
- <span data-ttu-id="18e31-109">Gérer vos comptes à un emplacement central : le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="18e31-109">Manage your accounts in one central location: the Azure portal.</span></span>

<span data-ttu-id="18e31-110">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="18e31-110">To learn more about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18e31-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="18e31-111">Prerequisites</span></span>

<span data-ttu-id="18e31-112">Pour configurer l’intégration d’Azure AD à vxMaintain, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="18e31-112">To configure Azure AD integration with vxMaintain, you need the following items:</span></span>

- <span data-ttu-id="18e31-113">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="18e31-113">An Azure AD subscription</span></span>
- <span data-ttu-id="18e31-114">Un abonnement vxMaintain dans lequel l’authentification unique (SSO) est incluse</span><span class="sxs-lookup"><span data-stu-id="18e31-114">A vxMaintain SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="18e31-115">Lorsque vous testez les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="18e31-115">When you test the steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="18e31-116">Pour tester la procédure de ce didacticiel, suivez les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="18e31-116">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="18e31-117">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="18e31-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="18e31-118">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="18e31-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="18e31-119">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="18e31-119">Scenario description</span></span>
<span data-ttu-id="18e31-120">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="18e31-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="18e31-121">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="18e31-121">The scenario that this tutorial outlines consists of two main building blocks:</span></span>

* <span data-ttu-id="18e31-122">Ajout de vxMaintain à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="18e31-122">Adding vxMaintain from the gallery</span></span>
* <span data-ttu-id="18e31-123">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="18e31-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="add-vxmaintain-from-the-gallery"></a><span data-ttu-id="18e31-124">Ajouter vxMaintain à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="18e31-124">Add vxMaintain from the gallery</span></span>
<span data-ttu-id="18e31-125">Pour configurer l’intégration de vxMaintain dans Azure AD, vous devez ajouter vxMaintain à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="18e31-125">To configure the integration of vxMaintain with Azure AD, you need to add vxMaintain from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="18e31-126">Pour ajouter vxMaintain à partir de la galerie, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="18e31-126">To add vxMaintain from the gallery, do the following:</span></span>

1. <span data-ttu-id="18e31-127">Dans le volet gauche du [portail Azure](https://portal.azure.com), cliquez sur le bouton **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="18e31-127">In the [Azure portal](https://portal.azure.com), in the left pane, select the **Azure Active Directory** button.</span></span> 

    ![Bouton Azure Active Directory][1]

2. <span data-ttu-id="18e31-129">Sélectionnez **Applications d’entreprise** > **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="18e31-129">Select **Enterprise applications** > **All applications**.</span></span>

    ![Volet Applications d’entreprise][2]
    
3. <span data-ttu-id="18e31-131">Pour ajouter une application, dans la boîte de dialogue **Toutes les applications**, sélectionnez **Nouvelle application**.</span><span class="sxs-lookup"><span data-stu-id="18e31-131">To add an application, in the **All applications** dialog box, select **New application**.</span></span>

    ![Bouton Nouvelle application][3]

4. <span data-ttu-id="18e31-133">Dans la zone de recherche, tapez **vxMaintain**.</span><span class="sxs-lookup"><span data-stu-id="18e31-133">In the search box, type **vxMaintain**.</span></span>

    ![Liste déroulante Mode](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_search.png)

5. <span data-ttu-id="18e31-135">Dans la liste des résultats, sélectionnez **vxMaintain**, puis **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="18e31-135">In the results list, select **vxMaintain**, and then select **Add**.</span></span>

    ![Lien vxMaintain](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="18e31-137">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="18e31-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="18e31-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec vxMaintain au moyen d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="18e31-138">In this section, you configure and test Azure AD SSO by using vxMaintain, based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="18e31-139">Pour que l’authentification unique fonctionne, Azure AD doit connaître l’équivalent de vxMaintain pour l’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="18e31-139">For SSO to work, Azure AD needs to know the vxMaintain counterpart to the Azure AD user.</span></span> <span data-ttu-id="18e31-140">Autrement dit, vous devez établir une relation entre l’utilisateur Azure AD et l’utilisateur vxMaintain correspondant.</span><span class="sxs-lookup"><span data-stu-id="18e31-140">That is, you must establish a link relationship between the Azure AD user and the corresponding vxMaintain user.</span></span>

<span data-ttu-id="18e31-141">Pour établir cette relation, assignez la valeur du **nom d’utilisateur** vxMaintain en tant que valeur de **nom d’utilisateur** Azure AD.</span><span class="sxs-lookup"><span data-stu-id="18e31-141">To establish the link relationship, assign the vxMaintain **user name** value as the Azure AD **Username** value.</span></span>

<span data-ttu-id="18e31-142">Pour configurer et tester l’authentification unique Azure AD avec vxMaintain, suivez les indications des sections ci-après :</span><span class="sxs-lookup"><span data-stu-id="18e31-142">To configure and test Azure AD SSO by using vxMaintain, complete the following building blocks.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="18e31-143">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="18e31-143">Configure Azure AD SSO</span></span>

<span data-ttu-id="18e31-144">Dans cette section, vous allez activer l’authentification unique (SSO) Azure AD dans le portail Azure et la configurer dans votre application vxMaintain en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="18e31-144">In this section, you can both enable Azure AD SSO in the Azure portal and configure SSO in your vxMaintain application by doing the following:</span></span>

1. <span data-ttu-id="18e31-145">Dans la page d’intégration de l’application **vxMaintain** sur le portail Azure, sélectionnez **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="18e31-145">In the Azure portal, on the **vxMaintain** application integration page, select **Single sign-on**.</span></span>

    ![Commande Authentification unique][4]

2. <span data-ttu-id="18e31-147">Pour activer l’authentification unique, dans la liste déroulante **Mode**, sélectionnez **Authentification basée sur SAML**.</span><span class="sxs-lookup"><span data-stu-id="18e31-147">To enable SSO, in the **Single Sign-on Mode** drop-down list, select **SAML-based Sign-on**.</span></span>
 
    ![Commande Authentification basée sur SAML](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_samlbase.png)

3. <span data-ttu-id="18e31-149">Sous **Domaine et URL vxMaintain**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="18e31-149">Under **vxMaintain Domain and URLs**, do the following:</span></span>

    ![Section Domaine et URL vxMaintain](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_url.png)

    <span data-ttu-id="18e31-151">a.</span><span class="sxs-lookup"><span data-stu-id="18e31-151">a.</span></span> <span data-ttu-id="18e31-152">Dans la zone de texte **Identificateur**, tapez une URL dont la syntaxe est la suivante : `https://<company name>.verisae.com`</span><span class="sxs-lookup"><span data-stu-id="18e31-152">In the **Identifier** box, type a URL that has the following syntax: `https://<company name>.verisae.com`</span></span>

    <span data-ttu-id="18e31-153">b.</span><span class="sxs-lookup"><span data-stu-id="18e31-153">b.</span></span> <span data-ttu-id="18e31-154">Dans la zone de texte **URL de réponse**, tapez une URL dont la syntaxe est la suivante : `https://<company name>.verisae.com/DataNett/action/ssoConsume/mobile?_log=true`</span><span class="sxs-lookup"><span data-stu-id="18e31-154">In the **Reply URL** box, type a URL that has the following syntax: `https://<company name>.verisae.com/DataNett/action/ssoConsume/mobile?_log=true`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="18e31-155">Les valeurs ci-dessus ne sont pas réelles.</span><span class="sxs-lookup"><span data-stu-id="18e31-155">The preceding values are not real.</span></span> <span data-ttu-id="18e31-156">Mettez-les à jour avec l’identificateur et l’URL de réponse réels.</span><span class="sxs-lookup"><span data-stu-id="18e31-156">Update them with the actual identifier and reply URL.</span></span> <span data-ttu-id="18e31-157">Pour obtenir les valeurs, contactez l’[équipe de support vxMaintain](http://www.verisae.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="18e31-157">To obtain the values, contact the [vxMaintain support team](http://www.verisae.com/contact-us).</span></span>
 
4. <span data-ttu-id="18e31-158">Sous **Certificat de signature SAML**, sélectionnez **XML des métadonnées** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="18e31-158">Under **SAML Signing Certificate**, select **Metadata XML**, and then save the metadata file to your computer.</span></span>

    ![Section Certificat de signature SAML](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_certificate.png) 

5. <span data-ttu-id="18e31-160">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="18e31-160">Select **Save**.</span></span>

    ![Bouton Enregistrer](./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="18e31-162">Pour configurer l’authentification unique **vxMaintain**, envoyez le fichier **XML des métadonnées** téléchargé à l’[équipe de support vxMaintain](http://www.verisae.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="18e31-162">To configure **vxMaintain** SSO, send the downloaded **Metadata XML** file to the [vxMaintain support team](http://www.verisae.com/contact-us).</span></span>

> [!TIP]
> <span data-ttu-id="18e31-163">Lors de la configuration de l’application, vous pouvez lire une version abrégée des instructions précédentes sur le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="18e31-163">As you set up the app, you can read a concise version of the preceding instructions in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="18e31-164">Après avoir ajouté cette application à partir de la section **Active Directory** > **Applications d’entreprise**, sélectionnez l’onglet **Authentification unique** et accédez à la documentation incorporée à partir de la section **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="18e31-164">After you add the app from the **Active Directory** > **Enterprise Applications** section, select the **Single Sign-On** tab, and then access the embedded documentation from the **Configuration** section.</span></span> 
>
><span data-ttu-id="18e31-165">Pour en savoir plus sur la fonctionnalité de documentation incorporée, consultez [Gestion de l’authentification unique pour les applications d’entreprise](https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="18e31-165">To learn more about the embedded documentation feature, see [Managing single sign-on for enterprise apps](https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="18e31-166">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="18e31-166">Create an Azure AD test user</span></span>
<span data-ttu-id="18e31-167">Dans cette section, vous allez créer un utilisateur de test nommé Britta Simon dans le portail Azure en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="18e31-167">In this section, you create test user Britta Simon in the Azure portal by doing the following:</span></span>

![Utilisateur de test Azure AD][100]

1. <span data-ttu-id="18e31-169">Dans le volet gauche du **portail Azure**, cliquez sur le bouton **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="18e31-169">In the **Azure portal**, in the left pane, select the **Azure Active Directory** button.</span></span>

    ![Le bouton « Azure Active Directory »](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="18e31-171">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes** > **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="18e31-171">To display a list of users, go to **Users and groups** > **All users**.</span></span>
    
    <span data-ttu-id="18e31-172">![Lien Tous les utilisateurs](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_02.png)</span><span class="sxs-lookup"><span data-stu-id="18e31-172">![The "All users" link](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_02.png)</span></span>  
    <span data-ttu-id="18e31-173">La boîte de dialogue **Tous les utilisateurs** s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="18e31-173">The **All users** dialog box opens.</span></span> 

3. <span data-ttu-id="18e31-174">Pour ouvrir la boîte de dialogue **Utilisateur**, sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="18e31-174">To open the **User** dialog box, select **Add**.</span></span>
 
    ![Bouton Ajouter](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="18e31-176">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="18e31-176">In the **User** dialog box, do the following:</span></span>
 
    ![Boîte de dialogue Utilisateur](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="18e31-178">a.</span><span class="sxs-lookup"><span data-stu-id="18e31-178">a.</span></span> <span data-ttu-id="18e31-179">Dans la zone **Nom**, tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="18e31-179">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="18e31-180">b.</span><span class="sxs-lookup"><span data-stu-id="18e31-180">b.</span></span> <span data-ttu-id="18e31-181">Dans la zone **Nom d’utilisateur** , tapez l’adresse e-mail de l’utilisateur de test Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="18e31-181">In the **User name** box, type the email address of test user Britta Simon.</span></span>

    <span data-ttu-id="18e31-182">c.</span><span class="sxs-lookup"><span data-stu-id="18e31-182">c.</span></span> <span data-ttu-id="18e31-183">Cochez la case **Afficher le mot de passe**, puis notez la valeur générée dans la zone **Mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="18e31-183">Select the **Show Password** check box, and then note the value that was generated in the **Password** box.</span></span>

    <span data-ttu-id="18e31-184">d.</span><span class="sxs-lookup"><span data-stu-id="18e31-184">d.</span></span> <span data-ttu-id="18e31-185">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="18e31-185">Select **Create**.</span></span>
 
### <a name="create-a-vxmaintain-test-user"></a><span data-ttu-id="18e31-186">Créer un utilisateur de test vxMaintain</span><span class="sxs-lookup"><span data-stu-id="18e31-186">Create a vxMaintain test user</span></span>

<span data-ttu-id="18e31-187">Dans cette section, vous allez créer un utilisateur de test appelé Britta Simon dans vxMaintain.</span><span class="sxs-lookup"><span data-stu-id="18e31-187">In this section, you create test user Britta Simon in vxMaintain.</span></span> <span data-ttu-id="18e31-188">Pour ajouter des utilisateurs dans la plateforme vxMaintain, collaborez avec l’[équipe du support technique de vxMaintain](http://www.verisae.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="18e31-188">To add users in the vxMaintain platform, work with the [vxMaintain support team](http://www.verisae.com/contact-us).</span></span> <span data-ttu-id="18e31-189">Avant d’utiliser l’authentification unique, créez et activez les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="18e31-189">Before you use SSO, create and activate the users.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="18e31-190">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="18e31-190">Assign the Azure AD test user</span></span>

<span data-ttu-id="18e31-191">Dans cette section, vous allez autoriser l’utilisateur de test Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à vxMaintain.</span><span class="sxs-lookup"><span data-stu-id="18e31-191">In this section, you enable test user Britta Simon to use Azure SSO by granting access to vxMaintain.</span></span> <span data-ttu-id="18e31-192">Pour ce faire, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="18e31-192">To do so, do the following:</span></span>

![Utilisateur de test dans la liste Nom affiché][200] 

1. <span data-ttu-id="18e31-194">Dans la vue **Applications** du portail Azure, accédez à la vue **Répertoire** >**Applications d’entreprise** > **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="18e31-194">In the Azure portal **Applications** view, go to **Directory** view > **Enterprise applications** > **All applications**.</span></span>

    ![Lien Toutes les applications][201] 

2. <span data-ttu-id="18e31-196">Dans la liste **Applications**, sélectionnez **vxMaintain**.</span><span class="sxs-lookup"><span data-stu-id="18e31-196">In the **Applications** list, select **vxMaintain**.</span></span>

    ![Lien vxMaintain](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_app.png) 

3. <span data-ttu-id="18e31-198">Dans le volet gauche, sélectionnez **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="18e31-198">In the left pane, select **Users and groups**.</span></span>

    ![Lien « Utilisateurs et groupes »][202] 

4. <span data-ttu-id="18e31-200">Sélectionnez **Ajouter** puis, dans le volet **Ajouter une attribution**, sélectionnez **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="18e31-200">Select **Add** and then, in the **Add Assignment** pane, select **Users and groups**.</span></span>

    ![Lien « Utilisateurs et groupes »][203]

5. <span data-ttu-id="18e31-202">Dans la boîte de dialogue **Utilisateurs et groupes** de la liste **Utilisateurs**, sélectionnez **Britta Simon**, puis sélectionnez le bouton **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="18e31-202">In the **Users and groups** dialog box, in the **Users** list, select **Britta Simon**, and then select the **Select** button.</span></span>

7. <span data-ttu-id="18e31-203">Dans la boîte de dialogue **Ajouter une attribution**, sélectionnez **Affecter**.</span><span class="sxs-lookup"><span data-stu-id="18e31-203">In the **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-your-azure-ad-single-sign-on"></a><span data-ttu-id="18e31-204">Tester votre authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="18e31-204">Test your Azure AD single sign-on</span></span>

<span data-ttu-id="18e31-205">Dans cette section, vous allez tester la configuration SSO Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="18e31-205">In this section, you test your Azure AD SSO configuration by using the Access Panel.</span></span>

<span data-ttu-id="18e31-206">Quand vous cliquez sur la vignette **vxMaintain** dans le panneau d’accès, vous devez être connecté automatiquement à votre application vxMaintain.</span><span class="sxs-lookup"><span data-stu-id="18e31-206">Selecting the **vxMaintain** tile in the Access Panel should sign you in to your vxMaintain application automatically.</span></span>

<span data-ttu-id="18e31-207">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="18e31-207">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="18e31-208">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="18e31-208">Next steps</span></span>

* [<span data-ttu-id="18e31-209">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="18e31-209">List of tutorials on integrating SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="18e31-210">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="18e31-210">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_203.png

