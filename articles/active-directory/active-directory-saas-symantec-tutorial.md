---
title: "Didacticiel : Intégration d’Azure Active Directory à Symantec Web Security Service (WSS) | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et le Service de sécurité Web Symantec (WSS)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d6e4d893-1f14-4522-ac20-0c73b18c72a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 9f02b3d4ce2073110c55af4b567b0e3b5a88404f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-symantec-web-security-service-wss"></a><span data-ttu-id="ca609-103">Didacticiel : Intégration d’Azure Active Directory à Symantec Web Security Service (WSS)</span><span class="sxs-lookup"><span data-stu-id="ca609-103">Tutorial: Azure Active Directory integration with Symantec Web Security Service (WSS)</span></span>

<span data-ttu-id="ca609-104">Dans ce didacticiel, vous allez apprendre comment toointegrate votre Service de sécurité Web Symantec (WSS) compte avec votre compte Azure Active Directory (Azure AD) afin de WSS peut authentifier un utilisateur final configuré Bonjour Azure AD à l’aide de l’authentification SAML et appliquer l’utilisateur ou règles de stratégie de groupe.</span><span class="sxs-lookup"><span data-stu-id="ca609-104">In this tutorial, you will learn how toointegrate your Symantec Web Security Service (WSS) account with your Azure Active Directory (Azure AD) account so that WSS can authenticate an end user provisioned in hello Azure AD using SAML authentication and enforce user or group level policy rules.</span></span>

<span data-ttu-id="ca609-105">Intégration de Service de sécurité Web Symantec (WSS) avec Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="ca609-105">Integrating Symantec Web Security Service (WSS) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ca609-106">Gérez tous les utilisateurs finaux de hello et les groupes utilisés par votre compte WSS à partir de votre portail Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ca609-106">Manage all of hello end users and groups used by your WSS account from your Azure AD portal.</span></span> 

- <span data-ttu-id="ca609-107">Autoriser le hello fin utilisateurs tooauthenticate eux-mêmes dans WSS à l’aide de leurs informations d’identification Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ca609-107">Allow hello end users tooauthenticate themselves in WSS using their Azure AD credentials.</span></span>

- <span data-ttu-id="ca609-108">Activer la mise en œuvre hello d’utilisateur et groupe de règles de stratégie de niveau définis dans votre compte WSS.</span><span class="sxs-lookup"><span data-stu-id="ca609-108">Enable hello enforcement of user and group level policy rules defined in your WSS account.</span></span>

<span data-ttu-id="ca609-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ca609-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ca609-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ca609-110">Prerequisites</span></span>

<span data-ttu-id="ca609-111">tooconfigure intégration d’Azure AD avec Symantec Security Service WSS (Web), vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="ca609-111">tooconfigure Azure AD integration with Symantec Web Security Service (WSS), you need hello following items:</span></span>

- <span data-ttu-id="ca609-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="ca609-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ca609-113">Un compte Symantec Web Security Service (WSS)</span><span class="sxs-lookup"><span data-stu-id="ca609-113">A Symantec Web Security Service (WSS) account</span></span>

> [!NOTE]
> <span data-ttu-id="ca609-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un compte WSS est actuellement utilisé à des fins de production.</span><span class="sxs-lookup"><span data-stu-id="ca609-114">tootest hello steps in this tutorial, we do not recommend using a WSS account that is currently being used for production purpose.</span></span>

<span data-ttu-id="ca609-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="ca609-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ca609-116">N’utilisez pas le compte WSS qui est actuellement utilisé à des fins de production pour ce test, sauf si c’est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="ca609-116">Do not use your WSS account that is currently being used for production purpose for this test unless it is necessary.</span></span>
- <span data-ttu-id="ca609-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ca609-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ca609-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="ca609-118">Scenario description</span></span>
<span data-ttu-id="ca609-119">Dans ce didacticiel, vous allez configurer votre Azure AD tooenable unique authentification tooWSS à l’aide des informations d’identification de l’utilisateur final hello définies dans votre compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ca609-119">In this tutorial, you will configure your Azure AD tooenable single sign-on tooWSS using hello end user credentials defined in your Azure AD account.</span></span>
<span data-ttu-id="ca609-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="ca609-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ca609-121">Ajout d’application de Service de sécurité Web Symantec (WSS) hello à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="ca609-121">Adding hello Symantec Web Security Service (WSS) app from hello gallery</span></span>
2. <span data-ttu-id="ca609-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ca609-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-symantec-web-security-service-wss-from-hello-gallery"></a><span data-ttu-id="ca609-123">Ajout de Service de sécurité Web Symantec (WSS) à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="ca609-123">Adding Symantec Web Security Service (WSS) from hello gallery</span></span>
<span data-ttu-id="ca609-124">intégration de hello tooconfigure de Symantec Security Service WSS (Web) dans Azure AD, vous devez tooadd Symantec Security Service WSS (Web) à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="ca609-124">tooconfigure hello integration of Symantec Web Security Service (WSS) into Azure AD, you need tooadd Symantec Web Security Service (WSS) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ca609-125">**tooadd Symantec Security Service WSS (Web) à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ca609-125">**tooadd Symantec Web Security Service (WSS) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ca609-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="ca609-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="ca609-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="ca609-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ca609-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="ca609-129">Then go too**All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="ca609-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="ca609-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="ca609-133">Dans la zone de recherche de hello, tapez **Symantec Web sécurité Service (WSS)**, sélectionnez **Symantec Web sécurité Service (WSS)** à partir du volet de résultats, puis sur **ajouter** hello tooadd de bouton application.</span><span class="sxs-lookup"><span data-stu-id="ca609-133">In hello search box, type **Symantec Web Security Service (WSS)**, select **Symantec Web Security Service (WSS)** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Symantec Security Service WSS (Web) dans la liste des résultats hello](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ca609-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ca609-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="ca609-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD auprès de Symantec Web Security Service (WSS) avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="ca609-136">In this section, you configure and test Azure AD single sign-on with Symantec Web Security Service (WSS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ca609-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Symantec Web sécurité Service (WSS) est tooa dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ca609-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Symantec Web Security Service (WSS) is tooa user in Azure AD.</span></span> <span data-ttu-id="ca609-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Symantec Security Service WSS (Web) doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="ca609-138">In other words, a link relationship between an Azure AD user and hello related user in Symantec Web Security Service (WSS) needs toobe established.</span></span>

<span data-ttu-id="ca609-139">Dans Symantec Web sécurité Service (WSS), affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="ca609-139">In Symantec Web Security Service (WSS), assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ca609-140">tooconfigure et test Azure AD l’authentification unique avec Symantec Security Service WSS (Web), vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="ca609-140">tooconfigure and test Azure AD single sign-on with Symantec Web Security Service (WSS), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ca609-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="ca609-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ca609-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ca609-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ca609-143">**[Créer un utilisateur de test du Service de sécurité Web Symantec (WSS)](#create-a-symantec-web-security-service-wss-test-user)**  -toohave un équivalent de Britta Simon dans Symantec Security Service WSS (Web) qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ca609-143">**[Create a Symantec Web Security Service (WSS) test user](#create-a-symantec-web-security-service-wss-test-user)** - toohave a counterpart of Britta Simon in Symantec Web Security Service (WSS) that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ca609-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="ca609-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ca609-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="ca609-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="ca609-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ca609-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="ca609-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de Service de sécurité Web Symantec (WSS).</span><span class="sxs-lookup"><span data-stu-id="ca609-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Symantec Web Security Service (WSS) application.</span></span>

<span data-ttu-id="ca609-148">**tooconfigure Azure AD l’authentification unique avec Symantec Web sécurité Service (WSS), effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ca609-148">**tooconfigure Azure AD single sign-on with Symantec Web Security Service (WSS), perform hello following steps:**</span></span>

1. <span data-ttu-id="ca609-149">Bonjour portail Azure, sur hello **Symantec Web sécurité Service (WSS)** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="ca609-149">In hello Azure portal, on hello **Symantec Web Security Service (WSS)** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="ca609-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="ca609-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_samlbase.png)

3. <span data-ttu-id="ca609-153">Sur hello **URL et le domaine de Service (WSS) de sécurité Web Symantec** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="ca609-153">On hello **Symantec Web Security Service (WSS) Domain and URLs** section, perform hello following steps:</span></span>

    ![Informations d’authentification unique Domaine et URL Symantec Web Security Service (WSS)](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_url.png)

    <span data-ttu-id="ca609-155">a.</span><span class="sxs-lookup"><span data-stu-id="ca609-155">a.</span></span> <span data-ttu-id="ca609-156">Bonjour **identificateur** zone de texte, tapez l’URL hello :`https://saml.threatpulse.net:8443/saml/saml_realm`</span><span class="sxs-lookup"><span data-stu-id="ca609-156">In hello **Identifier** textbox, type hello URL: `https://saml.threatpulse.net:8443/saml/saml_realm`</span></span>

    <span data-ttu-id="ca609-157">b.</span><span class="sxs-lookup"><span data-stu-id="ca609-157">b.</span></span> <span data-ttu-id="ca609-158">Bonjour **URL de réponse** zone de texte, tapez l’URL hello :`https://saml.threatpulse.net:8443/saml/saml_realm/bcsamlpost`</span><span class="sxs-lookup"><span data-stu-id="ca609-158">In hello **Reply URL** textbox, type hello URL: `https://saml.threatpulse.net:8443/saml/saml_realm/bcsamlpost`</span></span>

    > [!NOTE]
    > <span data-ttu-id="ca609-159">Veuillez contacter hello [équipe de support Client de Service de sécurité Web Symantec (WSS)](https://www.symantec.com/contact-us) si des valeurs hello hello **identificateur** et **URL de réponse** ne fonctionnent pas pour une raison quelconque.</span><span class="sxs-lookup"><span data-stu-id="ca609-159">Please contact hello [Symantec Web Security Service (WSS) Client support team](https://www.symantec.com/contact-us) if hello values for hello **Identifier** and **Reply URL** are not working for some reason.</span></span>

4. <span data-ttu-id="ca609-160">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="ca609-160">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_certificate.png) 

5. <span data-ttu-id="ca609-162">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="ca609-162">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-symantec-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="ca609-164">tooconfigure l’authentification unique sur hello au niveau de Service de sécurité Web Symantec (WSS), consultez la documentation en ligne de toohello WSS.</span><span class="sxs-lookup"><span data-stu-id="ca609-164">tooconfigure single sign-on on hello Symantec Web Security Service (WSS) side, refer toohello WSS online documentation.</span></span> <span data-ttu-id="ca609-165">Hello téléchargé **Metadata XML** fichier devez toobe importé dans le portail WSS hello.</span><span class="sxs-lookup"><span data-stu-id="ca609-165">hello downloaded **Metadata XML** file will need toobe imported into hello WSS portal.</span></span> <span data-ttu-id="ca609-166">Contact hello [équipe de support du Service de sécurité Web Symantec (WSS)](https://www.symantec.com/contact-us) si vous avez besoin d’assistance à la configuration de hello sur le portail WSS hello.</span><span class="sxs-lookup"><span data-stu-id="ca609-166">Contact hello [Symantec Web Security Service (WSS) support team](https://www.symantec.com/contact-us) if you need assistance with hello configuration on hello WSS portal.</span></span>

> [!TIP]
> <span data-ttu-id="ca609-167">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="ca609-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ca609-168">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="ca609-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ca609-169">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ca609-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ca609-170">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="ca609-170">Create an Azure AD test user</span></span>

<span data-ttu-id="ca609-171">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="ca609-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="ca609-173">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ca609-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ca609-174">Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.</span><span class="sxs-lookup"><span data-stu-id="ca609-174">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-symantec-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="ca609-176">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="ca609-176">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-symantec-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="ca609-178">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="ca609-178">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![bouton Ajouter de Hello](./media/active-directory-saas-symantec-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="ca609-180">Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="ca609-180">In hello **User** dialog box, perform hello following steps:</span></span>

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-symantec-tutorial/create_aaduser_04.png)

    <span data-ttu-id="ca609-182">a.</span><span class="sxs-lookup"><span data-stu-id="ca609-182">a.</span></span> <span data-ttu-id="ca609-183">Bonjour **nom** , tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ca609-183">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ca609-184">b.</span><span class="sxs-lookup"><span data-stu-id="ca609-184">b.</span></span> <span data-ttu-id="ca609-185">Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ca609-185">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="ca609-186">c.</span><span class="sxs-lookup"><span data-stu-id="ca609-186">c.</span></span> <span data-ttu-id="ca609-187">Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.</span><span class="sxs-lookup"><span data-stu-id="ca609-187">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="ca609-188">d.</span><span class="sxs-lookup"><span data-stu-id="ca609-188">d.</span></span> <span data-ttu-id="ca609-189">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="ca609-189">Click **Create**.</span></span>
 
### <a name="create-a-symantec-web-security-service-wss-test-user"></a><span data-ttu-id="ca609-190">Créer un utilisateur de test Symantec Web Security Service (WSS)</span><span class="sxs-lookup"><span data-stu-id="ca609-190">Create a Symantec Web Security Service (WSS) test user</span></span>

<span data-ttu-id="ca609-191">Dans cette section, vous créez un utilisateur appelé Britta Simon dans Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="ca609-191">In this section, you create a user called Britta Simon in Symantec Web Security Service (WSS).</span></span> <span data-ttu-id="ca609-192">nom d’utilisateur de fin correspondante Hello peut être créée manuellement dans le portail WSS hello ou vous pouvez attendre hello utilisateurs/groupes configurés dans le portail WSS toohello hello Azure AD toobe synchronisé après quelques minutes (environ 15 minutes).</span><span class="sxs-lookup"><span data-stu-id="ca609-192">hello corresponding end username can be manually created in hello WSS portal or you can wait for hello users/groups provisioned in hello Azure AD toobe synchronized toohello WSS portal after a few minutes (~15 minutes).</span></span> <span data-ttu-id="ca609-193">Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="ca609-193">Users must be created and activated before you use single sign-on.</span></span> <span data-ttu-id="ca609-194">Hello adresse IP publique de machine hello utilisateur final, qui sera utilisé toobrowse des sites Web a également besoin toobe configuré dans le portail du Service de sécurité Web Symantec (WSS) hello.</span><span class="sxs-lookup"><span data-stu-id="ca609-194">hello public IP address of hello end user machine, which will be used toobrowse websites also need toobe provisioned in hello Symantec Web Security Service (WSS) portal.</span></span>

> [!NOTE]
> <span data-ttu-id="ca609-195">Veuillez [cliquez ici](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) tooget votre machine de publique IPaddress.</span><span class="sxs-lookup"><span data-stu-id="ca609-195">Please [click here](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) tooget your machine's public IPaddress.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="ca609-196">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ca609-196">Assign hello Azure AD test user</span></span>

<span data-ttu-id="ca609-197">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooSymantec sécurité Service WSS (Web).</span><span class="sxs-lookup"><span data-stu-id="ca609-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSymantec Web Security Service (WSS).</span></span>

![Attribuer le rôle d’utilisateur hello][200] 

<span data-ttu-id="ca609-199">**tooassign Britta Simon tooSymantec Web sécurité Service (WSS), effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ca609-199">**tooassign Britta Simon tooSymantec Web Security Service (WSS), perform hello following steps:**</span></span>

1. <span data-ttu-id="ca609-200">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="ca609-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="ca609-202">Dans la liste des applications hello, sélectionnez **Symantec Web sécurité Service (WSS)**.</span><span class="sxs-lookup"><span data-stu-id="ca609-202">In hello applications list, select **Symantec Web Security Service (WSS)**.</span></span>

    ![lien de Service de sécurité Web Symantec (WSS) Hello dans la liste des Applications hello](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_app.png)  

3. <span data-ttu-id="ca609-204">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="ca609-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202]

4. <span data-ttu-id="ca609-206">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="ca609-206">Click **Add** button.</span></span> <span data-ttu-id="ca609-207">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="ca609-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="ca609-209">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="ca609-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ca609-210">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="ca609-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ca609-211">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="ca609-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="ca609-212">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="ca609-212">Test single sign-on</span></span>

<span data-ttu-id="ca609-213">Dans cette section, vous testerez fonctionnalité d’authentification unique hello maintenant que vous avez configuré votre toouse de compte WSS votre Azure AD pour l’authentification SAML.</span><span class="sxs-lookup"><span data-stu-id="ca609-213">In this section, you'll test hello single sign-on functionality now that you've configured your WSS account toouse your Azure AD for SAML authentication.</span></span>

<span data-ttu-id="ca609-214">Après avoir configuré votre trafic tooproxy de navigateur web tooWSS, lorsque vous ouvrez votre navigateur web et que vous essayez toobrowse tooa site, puis vous allez être redirigé toohello authentification Azure page.</span><span class="sxs-lookup"><span data-stu-id="ca609-214">After you have configured your web browser tooproxy traffic tooWSS, when you open your web browser and try toobrowse tooa site then you'll be redirected toohello Azure sign-on page.</span></span> <span data-ttu-id="ca609-215">Entrez des informations d’identification de hello de l’utilisateur final de test hello qui a été configuré Bonjour Azure AD (autrement dit, BrittaSimon) et le mot de passe correspondant.</span><span class="sxs-lookup"><span data-stu-id="ca609-215">Enter hello credentials of hello test end user that has been provisioned in hello Azure AD (that is, BrittaSimon) and associated password.</span></span> <span data-ttu-id="ca609-216">Une fois authentifié, vous serez en mesure de toobrowse toohello site que vous avez choisi.</span><span class="sxs-lookup"><span data-stu-id="ca609-216">Once authenticated, you'll be able toobrowse toohello website that you chose.</span></span> <span data-ttu-id="ca609-217">Devez-vous créer une règle de stratégie sur hello WSS côté tooblock BrittaSimon de parcourir le site particulier de tooa puis de la page de bloc WSS hello doit s’afficher lorsque vous essayez de toobrowse toothat site en tant qu’utilisateur BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ca609-217">Should you create a policy rule on hello WSS side tooblock BrittaSimon from browsing tooa particular site then you should see hello WSS block page when you attempt toobrowse toothat site as user BrittaSimon.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ca609-218">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="ca609-218">Additional resources</span></span>

* [<span data-ttu-id="ca609-219">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ca609-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ca609-220">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="ca609-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_203.png

