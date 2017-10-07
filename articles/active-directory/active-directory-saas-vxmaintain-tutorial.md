---
title: "Didacticiel : Intégrer Azure Active Directory dans vxMaintain | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et vxMaintain."
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
ms.openlocfilehash: 937ea276d898986fc5a953c96fddabdc8940309f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-vxmaintain"></a><span data-ttu-id="b0c2f-103">Didacticiel : Intégrer Azure Active Directory dans vxMaintain</span><span class="sxs-lookup"><span data-stu-id="b0c2f-103">Tutorial: Integrate Azure Active Directory with vxMaintain</span></span>

<span data-ttu-id="b0c2f-104">Dans ce didacticiel, vous apprendrez comment vxMaintain toointegrate avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b0c2f-104">In this tutorial, you learn how toointegrate vxMaintain with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b0c2f-105">Cette intégration offre plusieurs avantages importants.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-105">This integration provides several important benefits.</span></span> <span data-ttu-id="b0c2f-106">Vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="b0c2f-106">You can:</span></span>

- <span data-ttu-id="b0c2f-107">Contrôle dans Azure AD qui a accès toovxMaintain.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-107">Control in Azure AD who has access toovxMaintain.</span></span>
- <span data-ttu-id="b0c2f-108">Activer vos informations d’identification tooautomatically utilisateurs toovxMaintain avec l’authentification unique (SSO) à l’aide de leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-108">Enable your users tooautomatically sign in toovxMaintain with single sign-on (SSO) by using their Azure AD accounts.</span></span>
- <span data-ttu-id="b0c2f-109">Gérer vos comptes dans un emplacement central : hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-109">Manage your accounts in one central location: hello Azure portal.</span></span>

<span data-ttu-id="b0c2f-110">toolearn en savoir plus sur l’intégration de l’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b0c2f-110">toolearn more about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b0c2f-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b0c2f-111">Prerequisites</span></span>

<span data-ttu-id="b0c2f-112">tooconfigure intégration d’Azure AD avec vxMaintain, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="b0c2f-112">tooconfigure Azure AD integration with vxMaintain, you need hello following items:</span></span>

- <span data-ttu-id="b0c2f-113">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0c2f-113">An Azure AD subscription</span></span>
- <span data-ttu-id="b0c2f-114">Un abonnement vxMaintain dans lequel l’authentification unique (SSO) est incluse</span><span class="sxs-lookup"><span data-stu-id="b0c2f-114">A vxMaintain SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b0c2f-115">Lorsque vous testez les étapes hello dans ce didacticiel, nous vous recommandons de ne pas utiliser un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-115">When you test hello steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="b0c2f-116">étapes de hello tootest dans ce didacticiel, suivez ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="b0c2f-116">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="b0c2f-117">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b0c2f-118">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b0c2f-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b0c2f-119">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="b0c2f-119">Scenario description</span></span>
<span data-ttu-id="b0c2f-120">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="b0c2f-121">scénario Hello décrivant ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="b0c2f-121">hello scenario that this tutorial outlines consists of two main building blocks:</span></span>

* <span data-ttu-id="b0c2f-122">Ajout de vxMaintain à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="b0c2f-122">Adding vxMaintain from hello gallery</span></span>
* <span data-ttu-id="b0c2f-123">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0c2f-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="add-vxmaintain-from-hello-gallery"></a><span data-ttu-id="b0c2f-124">Ajouter des vxMaintain à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="b0c2f-124">Add vxMaintain from hello gallery</span></span>
<span data-ttu-id="b0c2f-125">intégration de hello tooconfigure de vxMaintain avec Azure AD, vous devez vxMaintain tooadd à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-125">tooconfigure hello integration of vxMaintain with Azure AD, you need tooadd vxMaintain from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b0c2f-126">vxMaintain tooadd à partir de la galerie hello, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="b0c2f-126">tooadd vxMaintain from hello gallery, do hello following:</span></span>

1. <span data-ttu-id="b0c2f-127">Bonjour [portail Azure](https://portal.azure.com)hello du volet gauche, dans Sélectionnez hello **Azure Active Directory** bouton.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-127">In hello [Azure portal](https://portal.azure.com), in hello left pane, select hello **Azure Active Directory** button.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="b0c2f-129">Sélectionnez **Applications d’entreprise** > **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-129">Select **Enterprise applications** > **All applications**.</span></span>

    ![volet de « Applications d’entreprise » Hello][2]
    
3. <span data-ttu-id="b0c2f-131">tooadd une application, Bonjour **toutes les applications** boîte de dialogue, sélectionnez **nouvelle application**.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-131">tooadd an application, in hello **All applications** dialog box, select **New application**.</span></span>

    ![Hello « Nouvelle application » bouton][3]

4. <span data-ttu-id="b0c2f-133">Dans la zone de recherche de hello, tapez **vxMaintain**.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-133">In hello search box, type **vxMaintain**.</span></span>

    ![liste déroulante de « Seul Mode d’authentification » Hello](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_search.png)

5. <span data-ttu-id="b0c2f-135">Dans la liste des résultats hello, sélectionnez **vxMaintain**, puis sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-135">In hello results list, select **vxMaintain**, and then select **Add**.</span></span>

    ![lien de vxMaintain Hello](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b0c2f-137">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0c2f-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="b0c2f-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec vxMaintain au moyen d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="b0c2f-138">In this section, you configure and test Azure AD SSO by using vxMaintain, based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b0c2f-139">Pour l’authentification unique toowork, Azure AD doit utilisateur d’Azure AD toohello tooknow hello vxMaintain équivalent.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-139">For SSO toowork, Azure AD needs tooknow hello vxMaintain counterpart toohello Azure AD user.</span></span> <span data-ttu-id="b0c2f-140">Autrement dit, vous devez établir une relation de lien entre hello correspondant vxMaintain utilisateur et Azure AD hello.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-140">That is, you must establish a link relationship between hello Azure AD user and hello corresponding vxMaintain user.</span></span>

<span data-ttu-id="b0c2f-141">relation de lien de hello tooestablish, affecter hello vxMaintain **nom d’utilisateur** valeur comme hello Azure AD **nom d’utilisateur** valeur.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-141">tooestablish hello link relationship, assign hello vxMaintain **user name** value as hello Azure AD **Username** value.</span></span>

<span data-ttu-id="b0c2f-142">tooconfigure et test de l’authentification unique de Azure AD à l’aide de vxMaintain, hello terminée après les blocs de construction.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-142">tooconfigure and test Azure AD SSO by using vxMaintain, complete hello following building blocks.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="b0c2f-143">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0c2f-143">Configure Azure AD SSO</span></span>

<span data-ttu-id="b0c2f-144">Dans cette section, vous pouvez les activer l’authentification unique de Azure AD Bonjour portail Azure et configurer l’authentification unique dans votre application vxMaintain de manière hello suivante :</span><span class="sxs-lookup"><span data-stu-id="b0c2f-144">In this section, you can both enable Azure AD SSO in hello Azure portal and configure SSO in your vxMaintain application by doing hello following:</span></span>

1. <span data-ttu-id="b0c2f-145">Bonjour portail Azure, sur hello **vxMaintain** page d’intégration d’application, sélectionnez **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-145">In hello Azure portal, on hello **vxMaintain** application integration page, select **Single sign-on**.</span></span>

    ![Hello « Sur l’authentification unique » de commande][4]

2. <span data-ttu-id="b0c2f-147">tooenable SSO, Bonjour **Mode d’authentification unique** la liste déroulante, sélectionnez **SAML-authentification**.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-147">tooenable SSO, in hello **Single Sign-on Mode** drop-down list, select **SAML-based Sign-on**.</span></span>
 
    ![Hello commande « SAML-authentification »](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_samlbase.png)

3. <span data-ttu-id="b0c2f-149">Sous **vxMaintain domaine et les URL**, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="b0c2f-149">Under **vxMaintain Domain and URLs**, do hello following:</span></span>

    ![Hello vxMaintain section URL et de domaine](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_url.png)

    <span data-ttu-id="b0c2f-151">a.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-151">a.</span></span> <span data-ttu-id="b0c2f-152">Bonjour **identificateur** zone, tapez une URL qui a hello selon la syntaxe :`https://<company name>.verisae.com`</span><span class="sxs-lookup"><span data-stu-id="b0c2f-152">In hello **Identifier** box, type a URL that has hello following syntax: `https://<company name>.verisae.com`</span></span>

    <span data-ttu-id="b0c2f-153">b.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-153">b.</span></span> <span data-ttu-id="b0c2f-154">Bonjour **URL de réponse** zone, tapez une URL qui a hello selon la syntaxe :`https://<company name>.verisae.com/DataNett/action/ssoConsume/mobile?_log=true`</span><span class="sxs-lookup"><span data-stu-id="b0c2f-154">In hello **Reply URL** box, type a URL that has hello following syntax: `https://<company name>.verisae.com/DataNett/action/ssoConsume/mobile?_log=true`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b0c2f-155">Hello les valeurs précédentes ne sont pas réelles.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-155">hello preceding values are not real.</span></span> <span data-ttu-id="b0c2f-156">Mettre à jour avec l’identificateur de réel hello et URL de réponse.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-156">Update them with hello actual identifier and reply URL.</span></span> <span data-ttu-id="b0c2f-157">les valeurs hello tooobtain, contact hello [équipe de support vxMaintain](http://www.verisae.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="b0c2f-157">tooobtain hello values, contact hello [vxMaintain support team](http://www.verisae.com/contact-us).</span></span>
 
4. <span data-ttu-id="b0c2f-158">Sous **le certificat de signature SAML**, sélectionnez **Metadata XML**, puis enregistrez ordinateur de tooyour de fichier de métadonnées hello.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-158">Under **SAML Signing Certificate**, select **Metadata XML**, and then save hello metadata file tooyour computer.</span></span>

    ![Hello section « Certificat de signature SAML »](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_certificate.png) 

5. <span data-ttu-id="b0c2f-160">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-160">Select **Save**.</span></span>

    ![bouton Enregistrer de Hello](./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b0c2f-162">tooconfigure **vxMaintain** SSO, hello envoi téléchargé **Metadata XML** toohello de fichiers [équipe de support vxMaintain](http://www.verisae.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="b0c2f-162">tooconfigure **vxMaintain** SSO, send hello downloaded **Metadata XML** file toohello [vxMaintain support team](http://www.verisae.com/contact-us).</span></span>

> [!TIP]
> <span data-ttu-id="b0c2f-163">Lorsque vous définissez application hello, vous pouvez lire une version concise de hello précédant les instructions dans hello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b0c2f-163">As you set up hello app, you can read a concise version of hello preceding instructions in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="b0c2f-164">Après avoir ajouté l’application hello de hello **Active Directory** > **des Applications d’entreprise** section, sélectionnez hello **Single Sign-On** onglet, puis hello d’accès incorporé documentation hello **Configuration** section.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-164">After you add hello app from hello **Active Directory** > **Enterprise Applications** section, select hello **Single Sign-On** tab, and then access hello embedded documentation from hello **Configuration** section.</span></span> 
>
><span data-ttu-id="b0c2f-165">toolearn en savoir plus sur la fonctionnalité de documentation embedded hello, consultez [la gestion de l’authentification unique pour les applications d’entreprise](https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="b0c2f-165">toolearn more about hello embedded documentation feature, see [Managing single sign-on for enterprise apps](https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b0c2f-166">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0c2f-166">Create an Azure AD test user</span></span>
<span data-ttu-id="b0c2f-167">Dans cette section, vous créez utilisateur test Britta Simon Bonjour portail Azure en procédant comme suit de hello :</span><span class="sxs-lookup"><span data-stu-id="b0c2f-167">In this section, you create test user Britta Simon in hello Azure portal by doing hello following:</span></span>

![utilisateur de test Hello Azure AD][100]

1. <span data-ttu-id="b0c2f-169">Bonjour **portail Azure**hello du volet gauche, dans Sélectionnez hello **Azure Active Directory** bouton.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-169">In hello **Azure portal**, in hello left pane, select hello **Azure Active Directory** button.</span></span>

    ![bouton de « Azure Active Directory » Hello](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b0c2f-171">toodisplay une liste des utilisateurs, accédez trop**utilisateurs et groupes** > **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-171">toodisplay a list of users, go too**Users and groups** > **All users**.</span></span>
    
    <span data-ttu-id="b0c2f-172">![lien Hello « Tous les utilisateurs »](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_02.png)</span><span class="sxs-lookup"><span data-stu-id="b0c2f-172">![hello "All users" link](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_02.png)</span></span>  
    <span data-ttu-id="b0c2f-173">Hello **tous les utilisateurs** boîte de dialogue s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-173">hello **All users** dialog box opens.</span></span> 

3. <span data-ttu-id="b0c2f-174">tooopen hello **utilisateur** boîte de dialogue, sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-174">tooopen hello **User** dialog box, select **Add**.</span></span>
 
    ![bouton Ajouter de Hello](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b0c2f-176">Bonjour **utilisateur** boîte de dialogue zone, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="b0c2f-176">In hello **User** dialog box, do hello following:</span></span>
 
    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b0c2f-178">a.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-178">a.</span></span> <span data-ttu-id="b0c2f-179">Bonjour **nom** , tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-179">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b0c2f-180">b.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-180">b.</span></span> <span data-ttu-id="b0c2f-181">Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur de test Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-181">In hello **User name** box, type hello email address of test user Britta Simon.</span></span>

    <span data-ttu-id="b0c2f-182">c.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-182">c.</span></span> <span data-ttu-id="b0c2f-183">Sélectionnez hello **afficher le mot de passe** case à cocher, puis sur valeur hello Remarque qui a été générée dans hello **mot de passe** boîte.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-183">Select hello **Show Password** check box, and then note hello value that was generated in hello **Password** box.</span></span>

    <span data-ttu-id="b0c2f-184">d.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-184">d.</span></span> <span data-ttu-id="b0c2f-185">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-185">Select **Create**.</span></span>
 
### <a name="create-a-vxmaintain-test-user"></a><span data-ttu-id="b0c2f-186">Créer un utilisateur de test vxMaintain</span><span class="sxs-lookup"><span data-stu-id="b0c2f-186">Create a vxMaintain test user</span></span>

<span data-ttu-id="b0c2f-187">Dans cette section, vous allez créer un utilisateur de test appelé Britta Simon dans vxMaintain.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-187">In this section, you create test user Britta Simon in vxMaintain.</span></span> <span data-ttu-id="b0c2f-188">utilisateurs tooadd dans la plate-forme vxMaintain hello, travailler avec les [équipe de support vxMaintain](http://www.verisae.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="b0c2f-188">tooadd users in hello vxMaintain platform, work with the [vxMaintain support team](http://www.verisae.com/contact-us).</span></span> <span data-ttu-id="b0c2f-189">Avant d’utiliser l’authentification unique, créer et activer les utilisateurs de hello.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-189">Before you use SSO, create and activate hello users.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="b0c2f-190">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0c2f-190">Assign hello Azure AD test user</span></span>

<span data-ttu-id="b0c2f-191">Dans cette section, vous activez l’utilisateur de test Britta Simon toouse Azure SSO en accordant l’accès toovxMaintain.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-191">In this section, you enable test user Britta Simon toouse Azure SSO by granting access toovxMaintain.</span></span> <span data-ttu-id="b0c2f-192">Par conséquent, toodo hello suivant :</span><span class="sxs-lookup"><span data-stu-id="b0c2f-192">toodo so, do hello following:</span></span>

![Utilisateur de test dans la liste nom complet de hello][200] 

1. <span data-ttu-id="b0c2f-194">Bonjour Azure portal **Applications** afficher, accédez trop**active** vue > **des applications d’entreprise** > **detouteslesapplications**.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-194">In hello Azure portal **Applications** view, go too**Directory** view > **Enterprise applications** > **All applications**.</span></span>

    ![lient Hello « Toutes les applications »][201] 

2. <span data-ttu-id="b0c2f-196">Bonjour **Applications** liste, sélectionnez **vxMaintain**.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-196">In hello **Applications** list, select **vxMaintain**.</span></span>

    ![lien de vxMaintain Hello](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_app.png) 

3. <span data-ttu-id="b0c2f-198">Dans le volet gauche de hello, sélectionnez **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-198">In hello left pane, select **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202] 

4. <span data-ttu-id="b0c2f-200">Sélectionnez **ajouter** , puis, dans hello **ajouter l’affectation** volet, sélectionnez **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-200">Select **Add** and then, in hello **Add Assignment** pane, select **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][203]

5. <span data-ttu-id="b0c2f-202">Bonjour **utilisateurs et groupes** la boîte de dialogue hello **utilisateurs** liste, sélectionnez **Britta Simon**, puis sélectionnez hello **sélectionnez** bouton.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-202">In hello **Users and groups** dialog box, in hello **Users** list, select **Britta Simon**, and then select hello **Select** button.</span></span>

7. <span data-ttu-id="b0c2f-203">Bonjour **ajouter l’affectation** boîte de dialogue, sélectionnez **affecter**.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-203">In hello **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-your-azure-ad-single-sign-on"></a><span data-ttu-id="b0c2f-204">Tester votre authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0c2f-204">Test your Azure AD single sign-on</span></span>

<span data-ttu-id="b0c2f-205">Dans cette section, vous testez votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-205">In this section, you test your Azure AD SSO configuration by using hello Access Panel.</span></span>

<span data-ttu-id="b0c2f-206">En sélectionnant hello **vxMaintain** vignette dans le volet d’accès de hello doit connecter tooyour vxMaintain application automatiquement.</span><span class="sxs-lookup"><span data-stu-id="b0c2f-206">Selecting hello **vxMaintain** tile in hello Access Panel should sign you in tooyour vxMaintain application automatically.</span></span>

<span data-ttu-id="b0c2f-207">Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b0c2f-207">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b0c2f-208">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b0c2f-208">Next steps</span></span>

* [<span data-ttu-id="b0c2f-209">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b0c2f-209">List of tutorials on integrating SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b0c2f-210">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="b0c2f-210">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

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

