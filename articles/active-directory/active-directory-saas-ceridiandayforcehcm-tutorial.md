---
title: "Didacticiel : Intégration d’Azure Active Directory à Ceridian Dayforce HCM | Microsoft docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Ceridian Dayforce HCM."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 7adf1eb3-d063-45d6-96a8-fd53b329b3f3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 4d72f29b4e5e30ef8881806d789f6676fc541e2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ceridian-dayforce-hcm"></a><span data-ttu-id="493c1-103">Didacticiel : Intégration d’Azure Active Directory à Ceridian Dayforce HCM</span><span class="sxs-lookup"><span data-stu-id="493c1-103">Tutorial: Azure Active Directory integration with Ceridian Dayforce HCM</span></span>

<span data-ttu-id="493c1-104">Dans ce didacticiel, vous apprendrez comment toointegrate HCM de Dayforce Ceridian avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="493c1-104">In this tutorial, you learn how toointegrate Ceridian Dayforce HCM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="493c1-105">Intégration Ceridian Dayforce HCM à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="493c1-105">Integrating Ceridian Dayforce HCM with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="493c1-106">Vous pouvez contrôler dans Azure AD qui a accès tooCeridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="493c1-106">You can control in Azure AD who has access tooCeridian Dayforce HCM.</span></span>
- <span data-ttu-id="493c1-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooCeridian HCM Dayforce (Single Sign-On) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="493c1-107">You can enable your users tooautomatically get signed-on tooCeridian Dayforce HCM (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="493c1-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="493c1-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="493c1-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="493c1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="493c1-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="493c1-110">Prerequisites</span></span>

<span data-ttu-id="493c1-111">tooconfigure intégration d’Azure AD avec Ceridian Dayforce HCM, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="493c1-111">tooconfigure Azure AD integration with Ceridian Dayforce HCM, you need hello following items:</span></span>

- <span data-ttu-id="493c1-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="493c1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="493c1-113">Un abonnement Ceridian Dayforce HCM pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="493c1-113">A Ceridian Dayforce HCM single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="493c1-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="493c1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="493c1-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="493c1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="493c1-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="493c1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="493c1-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="493c1-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="493c1-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="493c1-118">Scenario description</span></span>
<span data-ttu-id="493c1-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="493c1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="493c1-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="493c1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="493c1-121">Ajout de Ceridian Dayforce HCM à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="493c1-121">Adding Ceridian Dayforce HCM from hello gallery</span></span>
2. <span data-ttu-id="493c1-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="493c1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ceridian-dayforce-hcm-from-hello-gallery"></a><span data-ttu-id="493c1-123">Ajout de Ceridian Dayforce HCM à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="493c1-123">Adding Ceridian Dayforce HCM from hello gallery</span></span>
<span data-ttu-id="493c1-124">intégration de hello tooconfigure de Ceridian Dayforce HCM dans Azure AD, vous devez tooadd Ceridian Dayforce HCM à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="493c1-124">tooconfigure hello integration of Ceridian Dayforce HCM into Azure AD, you need tooadd Ceridian Dayforce HCM from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="493c1-125">**tooadd HCM de Dayforce Ceridian à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="493c1-125">**tooadd Ceridian Dayforce HCM from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="493c1-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="493c1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="493c1-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="493c1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="493c1-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="493c1-129">Then go too**All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="493c1-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="493c1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="493c1-133">Dans la zone de recherche de hello, tapez **Ceridian Dayforce HCM**, sélectionnez **Ceridian Dayforce HCM** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="493c1-133">In hello search box, type **Ceridian Dayforce HCM**, select **Ceridian Dayforce HCM** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Liste des résultats de HCM de Dayforce Ceridian Bonjour](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="493c1-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="493c1-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="493c1-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Ceridian Dayforce HCM, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="493c1-136">In this section, you configure and test Azure AD single sign-on with Ceridian Dayforce HCM based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="493c1-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Ceridian Dayforce HCM est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="493c1-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Ceridian Dayforce HCM is tooa user in Azure AD.</span></span> <span data-ttu-id="493c1-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Ceridian Dayforce HCM doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="493c1-138">In other words, a link relationship between an Azure AD user and hello related user in Ceridian Dayforce HCM needs toobe established.</span></span>

<span data-ttu-id="493c1-139">Dans Ceridian Dayforce HCM, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="493c1-139">In Ceridian Dayforce HCM, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="493c1-140">tooconfigure et test Azure AD l’authentification unique avec Ceridian Dayforce HCM, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="493c1-140">tooconfigure and test Azure AD single sign-on with Ceridian Dayforce HCM, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="493c1-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="493c1-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="493c1-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="493c1-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="493c1-143">**[Créer un utilisateur de test Ceridian Dayforce HCM](#create-a-ceridian-dayforce-hcm-test-user)**  -toohave un équivalent de Britta Simon dans Ceridian Dayforce HCM qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="493c1-143">**[Create a Ceridian Dayforce HCM test user](#create-a-ceridian-dayforce-hcm-test-user)** - toohave a counterpart of Britta Simon in Ceridian Dayforce HCM that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="493c1-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="493c1-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="493c1-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="493c1-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="493c1-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="493c1-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="493c1-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="493c1-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Ceridian Dayforce HCM application.</span></span>

<span data-ttu-id="493c1-148">**tooconfigure Azure AD l’authentification unique avec Ceridian Dayforce HCM, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="493c1-148">**tooconfigure Azure AD single sign-on with Ceridian Dayforce HCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="493c1-149">Bonjour portail Azure, sur hello **Ceridian Dayforce HCM** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="493c1-149">In hello Azure portal, on hello **Ceridian Dayforce HCM** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="493c1-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="493c1-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_samlbase.png)

3. <span data-ttu-id="493c1-153">Sur hello **Ceridian Dayforce HCM domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="493c1-153">On hello **Ceridian Dayforce HCM Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_url.png)
    
    <span data-ttu-id="493c1-155">a.</span><span class="sxs-lookup"><span data-stu-id="493c1-155">a.</span></span> <span data-ttu-id="493c1-156">Bonjour **URL de connexion** zone de texte, tapez l’URL hello utilisée par vos utilisateurs sur toosign tooyour application de Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="493c1-156">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour Ceridian Dayforce HCM application.</span></span>
    
    | <span data-ttu-id="493c1-157">Environnement</span><span class="sxs-lookup"><span data-stu-id="493c1-157">Environment</span></span> | <span data-ttu-id="493c1-158">URL</span><span class="sxs-lookup"><span data-stu-id="493c1-158">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="493c1-159">Production</span><span class="sxs-lookup"><span data-stu-id="493c1-159">For production</span></span> | `https://sso.dayforcehcm.com/<DayforcehcmNamespace>` |
    | <span data-ttu-id="493c1-160">Test</span><span class="sxs-lookup"><span data-stu-id="493c1-160">For test</span></span> | `https://ssotest.dayforcehcm.com/<DayforcehcmNamespace>` |
    
    <span data-ttu-id="493c1-161">b.</span><span class="sxs-lookup"><span data-stu-id="493c1-161">b.</span></span> <span data-ttu-id="493c1-162">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :</span><span class="sxs-lookup"><span data-stu-id="493c1-162">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    
    | <span data-ttu-id="493c1-163">Environnement</span><span class="sxs-lookup"><span data-stu-id="493c1-163">Environment</span></span> | <span data-ttu-id="493c1-164">URL</span><span class="sxs-lookup"><span data-stu-id="493c1-164">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="493c1-165">Production</span><span class="sxs-lookup"><span data-stu-id="493c1-165">For production</span></span> | `https://ncpingfederate.dayforcehcm.com/sp` |
    | <span data-ttu-id="493c1-166">Test</span><span class="sxs-lookup"><span data-stu-id="493c1-166">For test</span></span> | `https://fs-test.dayforcehcm.com/sp` |
    
    <span data-ttu-id="493c1-167">c.</span><span class="sxs-lookup"><span data-stu-id="493c1-167">c.</span></span> <span data-ttu-id="493c1-168">Bonjour **URL de réponse** zone de texte, tapez l’URL hello utilisée par Azure AD toopost hello réponse.</span><span class="sxs-lookup"><span data-stu-id="493c1-168">In hello **Reply URL** textbox, type hello URL used by Azure AD toopost hello response.</span></span>
    
    | <span data-ttu-id="493c1-169">Environnement</span><span class="sxs-lookup"><span data-stu-id="493c1-169">Environment</span></span> | <span data-ttu-id="493c1-170">URL</span><span class="sxs-lookup"><span data-stu-id="493c1-170">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="493c1-171">Production</span><span class="sxs-lookup"><span data-stu-id="493c1-171">For production</span></span> | `https://ncpingfederate.dayforcehcm.com/sp/ACS.saml2` |
    | <span data-ttu-id="493c1-172">Test</span><span class="sxs-lookup"><span data-stu-id="493c1-172">For test</span></span> | `https://fs-test.dayforcehcm.com/sp/ACS.saml2` |
    
    > [!NOTE] 
    > <span data-ttu-id="493c1-173">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="493c1-173">These values are not real.</span></span> <span data-ttu-id="493c1-174">Mettre à jour les valeurs de hello réel identificateur, les URL de réponse et les URL de connexion.</span><span class="sxs-lookup"><span data-stu-id="493c1-174">Update these values with hello actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="493c1-175">Contact [équipe de support Client de HCM Ceridian Dayforce](https://www.ceridian.com/contact-us/index.html) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="493c1-175">Contact [Ceridian Dayforce HCM Client support team](https://www.ceridian.com/contact-us/index.html) tooget these values.</span></span>

4. <span data-ttu-id="493c1-176">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="493c1-176">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_certificate.png) 

5. <span data-ttu-id="493c1-178">Votre application Ceridian Dayforce HCM attend les assertions SAML hello dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="493c1-178">Your Ceridian Dayforce HCM application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="493c1-179">Travailler avec [équipe de support Ceridian Dayforce HCM](https://www.ceridian.com/contact-us/index.html) premier identificateur d’utilisateur corrects de hello tooidentify.</span><span class="sxs-lookup"><span data-stu-id="493c1-179">Work with [Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html) first tooidentify hello correct user identifier.</span></span> <span data-ttu-id="493c1-180">Microsoft recommande d’utiliser hello **« name »** attribut sous la forme d’identificateur de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="493c1-180">Microsoft recommends using hello **"name"** attribute as user identifier.</span></span> <span data-ttu-id="493c1-181">Vous pouvez gérer les valeurs de ces attributs hello depuis hello **attributs utilisateur** section sur la page d’intégration d’application.</span><span class="sxs-lookup"><span data-stu-id="493c1-181">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span> <span data-ttu-id="493c1-182">Hello suivant capture d’écran montre un exemple de cela.</span><span class="sxs-lookup"><span data-stu-id="493c1-182">hello following screenshot shows an example for this.</span></span>  

    ![Configurer l’authentification unique](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_07.png)

6. <span data-ttu-id="493c1-184">Bonjour **attributs utilisateur** section hello **l’authentification unique** boîte de dialogue, configurer des attributs de jeton SAML comme indiqué dans l’image ci-dessus hello et effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="493c1-184">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="493c1-185">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="493c1-185">Attribute Name</span></span>  | <span data-ttu-id="493c1-186">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="493c1-186">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    | <span data-ttu-id="493c1-187">name</span><span class="sxs-lookup"><span data-stu-id="493c1-187">name</span></span>  | <span data-ttu-id="493c1-188">user.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="493c1-188">user.extensionattribute2</span></span> |    

    <span data-ttu-id="493c1-189">a.</span><span class="sxs-lookup"><span data-stu-id="493c1-189">a.</span></span> <span data-ttu-id="493c1-190">Cliquez sur **ajouter un attribut** tooopen hello **ajouter un attribut** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="493c1-190">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_attribute_04.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="493c1-193">b.</span><span class="sxs-lookup"><span data-stu-id="493c1-193">b.</span></span> <span data-ttu-id="493c1-194">Bonjour **nom** zone de texte, nom d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="493c1-194">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="493c1-195">c.</span><span class="sxs-lookup"><span data-stu-id="493c1-195">c.</span></span> <span data-ttu-id="493c1-196">Bonjour **valeur** liste, sélectionnez hello utilisateur attribut toouse pour votre implémentation.</span><span class="sxs-lookup"><span data-stu-id="493c1-196">In hello **Value** list, select hello user attribute you want toouse for your implementation.</span></span>
    <span data-ttu-id="493c1-197">Par exemple, si vous voulez toouse hello EmployeeID comme identificateur d’utilisateur unique et si vous avez stocké la valeur de l’attribut hello Bonjour ExtensionAttribute2, puis sélectionnez **user.extensionattribute2**.</span><span class="sxs-lookup"><span data-stu-id="493c1-197">For example, if you want toouse hello EmployeeID as unique user identifier and you have stored hello attribute value in hello ExtensionAttribute2, then select **user.extensionattribute2**.</span></span>
    
    <span data-ttu-id="493c1-198">d.</span><span class="sxs-lookup"><span data-stu-id="493c1-198">d.</span></span> <span data-ttu-id="493c1-199">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="493c1-199">Click **Ok**.</span></span>

7. <span data-ttu-id="493c1-200">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="493c1-200">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="493c1-202">Sur hello **Ceridian Dayforce HCM Configuration** , cliquez sur **configurer HCM de Dayforce Ceridian** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="493c1-202">On hello **Ceridian Dayforce HCM Configuration** section, click **Configure Ceridian Dayforce HCM** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="493c1-203">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="493c1-203">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuration de Ceridian Dayforce HCM](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_configure.png) 

9. <span data-ttu-id="493c1-205">tooconfigure l’authentification unique sur **Ceridian Dayforce HCM** côté, vous devez hello toosend téléchargé **Metadata XML** et **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** trop[équipe de support Ceridian Dayforce HCM](https://www.ceridian.com/contact-us/index.html).</span><span class="sxs-lookup"><span data-stu-id="493c1-205">tooconfigure single sign-on on **Ceridian Dayforce HCM** side, you need toosend hello downloaded **Metadata XML** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html).</span></span>

> [!TIP]
> <span data-ttu-id="493c1-206">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="493c1-206">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="493c1-207">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="493c1-207">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="493c1-208">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="493c1-208">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="493c1-209">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="493c1-209">Create an Azure AD test user</span></span>

<span data-ttu-id="493c1-210">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="493c1-210">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="493c1-212">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="493c1-212">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="493c1-213">Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.</span><span class="sxs-lookup"><span data-stu-id="493c1-213">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="493c1-215">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="493c1-215">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="493c1-217">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="493c1-217">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![bouton Ajouter de Hello](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="493c1-219">Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="493c1-219">In hello **User** dialog box, perform hello following steps:</span></span>

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_04.png)

    <span data-ttu-id="493c1-221">a.</span><span class="sxs-lookup"><span data-stu-id="493c1-221">a.</span></span> <span data-ttu-id="493c1-222">Bonjour **nom** , tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="493c1-222">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="493c1-223">b.</span><span class="sxs-lookup"><span data-stu-id="493c1-223">b.</span></span> <span data-ttu-id="493c1-224">Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="493c1-224">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="493c1-225">c.</span><span class="sxs-lookup"><span data-stu-id="493c1-225">c.</span></span> <span data-ttu-id="493c1-226">Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.</span><span class="sxs-lookup"><span data-stu-id="493c1-226">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="493c1-227">d.</span><span class="sxs-lookup"><span data-stu-id="493c1-227">d.</span></span> <span data-ttu-id="493c1-228">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="493c1-228">Click **Create**.</span></span>
 
### <a name="create-a-ceridian-dayforce-hcm-test-user"></a><span data-ttu-id="493c1-229">Créer un utilisateur de test Ceridian Dayforce HCM</span><span class="sxs-lookup"><span data-stu-id="493c1-229">Create a Ceridian Dayforce HCM test user</span></span>

<span data-ttu-id="493c1-230">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="493c1-230">hello objective of this section is toocreate a user called Britta Simon in Ceridian Dayforce HCM.</span></span> <span data-ttu-id="493c1-231">Travailler avec hello [équipe de support Ceridian Dayforce HCM](https://www.ceridian.com/contact-us/index.html) utilisateurs tooget ajoutés Bonjour application de Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="493c1-231">Work with hello [Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html) tooget users added in hello Ceridian Dayforce HCM application.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="493c1-232">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="493c1-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="493c1-233">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooCeridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="493c1-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCeridian Dayforce HCM.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="493c1-235">**tooassign Britta Simon tooCeridian Dayforce HCM, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="493c1-235">**tooassign Britta Simon tooCeridian Dayforce HCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="493c1-236">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="493c1-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="493c1-238">Dans la liste des applications hello, sélectionnez **Ceridian Dayforce HCM**.</span><span class="sxs-lookup"><span data-stu-id="493c1-238">In hello applications list, select **Ceridian Dayforce HCM**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png) 

3. <span data-ttu-id="493c1-240">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="493c1-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="493c1-242">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="493c1-242">Click **Add** button.</span></span> <span data-ttu-id="493c1-243">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="493c1-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="493c1-245">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="493c1-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="493c1-246">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="493c1-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="493c1-247">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="493c1-247">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="493c1-248">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="493c1-248">Assign hello Azure AD test user</span></span>

<span data-ttu-id="493c1-249">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooCeridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="493c1-249">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCeridian Dayforce HCM.</span></span>

![Attribuer le rôle d’utilisateur hello][200] 

<span data-ttu-id="493c1-251">**tooassign Britta Simon tooCeridian Dayforce HCM, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="493c1-251">**tooassign Britta Simon tooCeridian Dayforce HCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="493c1-252">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="493c1-252">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="493c1-254">Dans la liste des applications hello, sélectionnez **Ceridian Dayforce HCM**.</span><span class="sxs-lookup"><span data-stu-id="493c1-254">In hello applications list, select **Ceridian Dayforce HCM**.</span></span>

    ![lien de Ceridian Dayforce HCM Hello dans la liste des Applications hello](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png)  

3. <span data-ttu-id="493c1-256">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="493c1-256">In hello menu on hello left, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202]

4. <span data-ttu-id="493c1-258">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="493c1-258">Click **Add** button.</span></span> <span data-ttu-id="493c1-259">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="493c1-259">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="493c1-261">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="493c1-261">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="493c1-262">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="493c1-262">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="493c1-263">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="493c1-263">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="493c1-264">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="493c1-264">Test single sign-on</span></span>

<span data-ttu-id="493c1-265">objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="493c1-265">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="493c1-266">Lorsque vous cliquez sur mosaïque Ceridian Dayforce HCM hello hello volet d’accès, vous devez obtenir l’application de Ceridian Dayforce HCM automatiquement signé sur tooyour.</span><span class="sxs-lookup"><span data-stu-id="493c1-266">When you click hello Ceridian Dayforce HCM tile in hello Access Panel, you should get automatically signed-on tooyour Ceridian Dayforce HCM application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="493c1-267">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="493c1-267">Additional resources</span></span>

* [<span data-ttu-id="493c1-268">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="493c1-268">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="493c1-269">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="493c1-269">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_203.png

