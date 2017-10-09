---
title: "Didacticiel : Intégration d’Azure Active Directory avec Pingboard | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Pingboard."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 0a916b1f9ef32d8124aa11284d2115bb4fc0bbc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pingboard"></a><span data-ttu-id="5ceb3-103">Didacticiel : Intégration d’Azure Active Directory avec Pingboard</span><span class="sxs-lookup"><span data-stu-id="5ceb3-103">Tutorial: Azure Active Directory integration with Pingboard</span></span>

<span data-ttu-id="5ceb3-104">Dans ce didacticiel, vous apprendrez comment toointegrate Pingboard avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5ceb3-104">In this tutorial, you learn how toointegrate Pingboard with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5ceb3-105">Intégration Pingboard à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="5ceb3-105">Integrating Pingboard with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5ceb3-106">Vous pouvez contrôler dans Azure AD qui a accès tooPingboard</span><span class="sxs-lookup"><span data-stu-id="5ceb3-106">You can control in Azure AD who has access tooPingboard</span></span>
- <span data-ttu-id="5ceb3-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooPingboard (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ceb3-107">You can enable your users tooautomatically get signed-on tooPingboard (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5ceb3-108">Vous pouvez gérer vos comptes dans un emplacement central - portail de gestion Azure hello</span><span class="sxs-lookup"><span data-stu-id="5ceb3-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="5ceb3-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5ceb3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5ceb3-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="5ceb3-110">Prerequisites</span></span>

<span data-ttu-id="5ceb3-111">tooconfigure intégration d’Azure AD avec Pingboard, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="5ceb3-111">tooconfigure Azure AD integration with Pingboard, you need hello following items:</span></span>

- <span data-ttu-id="5ceb3-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ceb3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5ceb3-113">Un abonnement Pingboard pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="5ceb3-113">A Pingboard single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5ceb3-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5ceb3-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="5ceb3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5ceb3-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="5ceb3-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5ceb3-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5ceb3-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="5ceb3-118">Scenario description</span></span>
<span data-ttu-id="5ceb3-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5ceb3-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="5ceb3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5ceb3-121">Ajout de Pingboard à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="5ceb3-121">Adding Pingboard from hello gallery</span></span>
2. <span data-ttu-id="5ceb3-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ceb3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pingboard-from-hello-gallery"></a><span data-ttu-id="5ceb3-123">Ajout de Pingboard à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="5ceb3-123">Adding Pingboard from hello gallery</span></span>
<span data-ttu-id="5ceb3-124">intégration de hello tooconfigure de Pingboard dans Azure AD, vous devez tooadd Pingboard à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-124">tooconfigure hello integration of Pingboard into Azure AD, you need tooadd Pingboard from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5ceb3-125">**tooadd Pingboard à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5ceb3-125">**tooadd Pingboard from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5ceb3-126">Bonjour  **[portail de gestion Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5ceb3-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5ceb3-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="5ceb3-131">Cliquez sur **ajouter** bouton en haut de hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="5ceb3-133">Dans la zone de recherche de hello, tapez **Pingboard**.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-133">In hello search box, type **Pingboard**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_search.png)

5. <span data-ttu-id="5ceb3-135">Dans le volet de résultats hello, sélectionnez **Pingboard**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-135">In hello results panel, select **Pingboard**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5ceb3-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ceb3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5ceb3-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Pingboard sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="5ceb3-138">In this section, you configure and test Azure AD single sign-on with Pingboard based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5ceb3-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Pingboard est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Pingboard is tooa user in Azure AD.</span></span> <span data-ttu-id="5ceb3-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Pingboard doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-140">In other words, a link relationship between an Azure AD user and hello related user in Pingboard needs toobe established.</span></span>

<span data-ttu-id="5ceb3-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans Pingboard.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Pingboard.</span></span>

<span data-ttu-id="5ceb3-142">tooconfigure et test Azure AD l’authentification unique avec Pingboard, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="5ceb3-142">tooconfigure and test Azure AD single sign-on with Pingboard, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5ceb3-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5ceb3-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5ceb3-145">**[Création d’un utilisateur de test Pingboard](#creating-a-pingboard-test-user)**  -toohave de Britta Simon dans Pingboard qui est la représentation sous forme de toohello lié Azure AD de sa contrepartie.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-145">**[Creating a Pingboard test user](#creating-a-pingboard-test-user)** - toohave a counterpart of Britta Simon in Pingboard that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="5ceb3-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5ceb3-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5ceb3-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ceb3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5ceb3-149">Dans cette section, vous activez Azure AD l’authentification unique dans le portail de gestion Azure hello et configurez l’authentification unique dans votre application Pingboard.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Pingboard application.</span></span>

<span data-ttu-id="5ceb3-150">**tooconfigure Azure AD single sign-on avec Pingboard, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5ceb3-150">**tooconfigure Azure AD single sign-on with Pingboard, perform hello following steps:**</span></span>

1. <span data-ttu-id="5ceb3-151">Dans le portail de gestion Azure hello, sur hello **Pingboard** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-151">In hello Azure Management portal, on hello **Pingboard** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="5ceb3-153">Sur hello **l’authentification unique** boîte de dialogue, en tant que **Mode** sélectionnez **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_samlbase.png)

3. <span data-ttu-id="5ceb3-155">Sur hello **Pingboard domaine et les URL** section, effectuer hello comme suit si vous le souhaitez application hello tooconfigure **IDP** en mode initié par :</span><span class="sxs-lookup"><span data-stu-id="5ceb3-155">On hello **Pingboard Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_url.png)

    <span data-ttu-id="5ceb3-157">a.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-157">a.</span></span> <span data-ttu-id="5ceb3-158">Bonjour **identificateur** valeur hello de type en tant que zone de texte :`http://<entity-id>.pingboard.com/sp`</span><span class="sxs-lookup"><span data-stu-id="5ceb3-158">In hello **Identifier** textbox, type hello value as: `http://<entity-id>.pingboard.com/sp`</span></span>

    <span data-ttu-id="5ceb3-159">b.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-159">b.</span></span> <span data-ttu-id="5ceb3-160">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<entity-id>.pingboard.com/auth/saml/consume`</span><span class="sxs-lookup"><span data-stu-id="5ceb3-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<entity-id>.pingboard.com/auth/saml/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5ceb3-161">Notez qu’il s’agit pas des valeurs réelles hello.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="5ceb3-162">Vous avez tooupdate ces valeurs avec hello URL d’identificateur et de réponse réelle.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="5ceb3-163">Ici, nous vous suggérons vous toouse hello unique valeur de chaîne Bonjour identificateur.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="5ceb3-164">Contact [équipe de support Client de Pingboard](https://support.pingboard.com/) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-164">Contact [Pingboard Client support team](https://support.pingboard.com/) tooget these values.</span></span> 

4. <span data-ttu-id="5ceb3-165">Vérifiez **afficher les paramètres d’URL avancés**, si vous le souhaitez application hello tooconfigure **SP** en mode initié par :</span><span class="sxs-lookup"><span data-stu-id="5ceb3-165">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_sp_initiated01.png)

    <span data-ttu-id="5ceb3-167">a.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-167">a.</span></span> <span data-ttu-id="5ceb3-168">Bonjour **URL de connexion** valeur hello de type en tant que zone de texte :`http://<sub-domain>.pingboard.com/sign_in`</span><span class="sxs-lookup"><span data-stu-id="5ceb3-168">In hello **Sign-on URL** textbox, type hello value as: `http://<sub-domain>.pingboard.com/sign_in`</span></span>
     
5. <span data-ttu-id="5ceb3-169">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier XML de hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_certificate.png) 

6. <span data-ttu-id="5ceb3-171">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="5ceb3-171">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-pingboard-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="5ceb3-173">tooconfigure SSO Pingboard côté, ouvrez une nouvelle fenêtre de navigateur et connectez-vous à tooyour Pingboard compte.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-173">tooconfigure SSO on Pingboard side, open a new browser window and log in tooyour Pingboard Account.</span></span> <span data-ttu-id="5ceb3-174">Vous devez être un tooset d’administration Pingboard d’authentification unique sur.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-174">You must be a Pingboard admin tooset up single sign on.</span></span>

8. <span data-ttu-id="5ceb3-175">Dans le menu du haut hello sélectionnez **applications > intégrations**</span><span class="sxs-lookup"><span data-stu-id="5ceb3-175">From hello top menu select **Apps > Integrations**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-pingboard-tutorial/Pingboard_integration.png)

9.  <span data-ttu-id="5ceb3-177">Sur hello **intégrations** page, recherche hello **« Azure Active Directory »** vignette, puis cliquez dessus.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-177">On hello **Integrations** page, find hello **"Azure Active Directory"** tile, and click it.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-pingboard-tutorial/Pingboard_aad.png)

10. <span data-ttu-id="5ceb3-179">Bonjour modale qui suit cliquez **« Configurer »**</span><span class="sxs-lookup"><span data-stu-id="5ceb3-179">In hello modal that follows click **"Configure"**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-pingboard-tutorial/Pingboard_configure.png)

11. <span data-ttu-id="5ceb3-181">Sur hello après page, vous remarquerez que « intégration d’Azure SSO est activée. ».</span><span class="sxs-lookup"><span data-stu-id="5ceb3-181">On hello following page, you will notice that "Azure SSO Integration is enabled.".</span></span> <span data-ttu-id="5ceb3-182">Ouvrez hello téléchargé un fichier Metadata XML dans un Bonjour le bloc-notes et collez le contenu des **IDP Metadata**.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-182">Open hello downloaded Metadata XML file in a notepad and paste hello content in **IDP Metadata**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-pingboard-tutorial/Pingboard_sso_configure.png)

12. <span data-ttu-id="5ceb3-184">fichier de Hello sera validé, et si tout est correct, l’authentification unique est maintenant activée</span><span class="sxs-lookup"><span data-stu-id="5ceb3-184">hello file will be validated, and if everything is correct, single sign on will now be enabled</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5ceb3-185">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ceb3-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="5ceb3-186">objectif Hello de cette section est toocreate un utilisateur de test dans le portail de gestion Azure hello appelé Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-186">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="5ceb3-188">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5ceb3-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5ceb3-189">Bonjour **portail de gestion Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-189">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5ceb3-191">Accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs** liste de hello toodisplay des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-191">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5ceb3-193">En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-193">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5ceb3-195">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5ceb3-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5ceb3-197">a.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-197">a.</span></span> <span data-ttu-id="5ceb3-198">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5ceb3-199">b.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-199">b.</span></span> <span data-ttu-id="5ceb3-200">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-200">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5ceb3-201">c.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-201">c.</span></span> <span data-ttu-id="5ceb3-202">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5ceb3-203">d.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-203">d.</span></span> <span data-ttu-id="5ceb3-204">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-204">Click **Create**.</span></span>
 
### <a name="creating-a-pingboard-test-user"></a><span data-ttu-id="5ceb3-205">Création d’un utilisateur de test Pingboard</span><span class="sxs-lookup"><span data-stu-id="5ceb3-205">Creating a Pingboard test user</span></span>

<span data-ttu-id="5ceb3-206">Dans l’ordre tooenable Azure AD les utilisateurs toolog dans Pingboard, ils doivent être configurés dans Pingboard.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-206">In order tooenable Azure AD users toolog into Pingboard, they must be provisioned into Pingboard.</span></span>  
<span data-ttu-id="5ceb3-207">Dans les cas de hello de Pingboard, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-207">In hello case of Pingboard, provisioning is a manual task.</span></span>

<span data-ttu-id="5ceb3-208">**effectuer des comptes d’utilisateur, tooprovision hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5ceb3-208">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="5ceb3-209">Ouvrez une session dans tooyour Pingboard site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-209">Log in tooyour Pingboard company site as an administrator.</span></span>

2. <span data-ttu-id="5ceb3-210">Cliquez sur le bouton **« Ajouter un employé »** sur la page **Annuaire**.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-210">Click **“Add Employee”** button on **Directory** page.</span></span>

    ![Ajouter un employé](./media/active-directory-saas-pingboard-tutorial/create_testuser_add.png)

3. <span data-ttu-id="5ceb3-212">Sur hello **« Ajouter un employé »** boîte de dialogue de page, effectuer hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-212">On hello **“Add Employee”** dialog page, perform hello following steps.</span></span>

    ![Inviter des personnes](./media/active-directory-saas-pingboard-tutorial/create_testuser_name.png)

    <span data-ttu-id="5ceb3-214">a.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-214">a.</span></span> <span data-ttu-id="5ceb3-215">Bonjour **nom complet** zone de texte, nom complet de type hello de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-215">In hello **Full Name** textbox, type hello full name of Britta Simon.</span></span>

    <span data-ttu-id="5ceb3-216">b.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-216">b.</span></span> <span data-ttu-id="5ceb3-217">Bonjour **messagerie** zone de texte, tapez Bonjour adresse de messagerie du compte de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-217">In hello **Email** textbox, type hello email address of Britta Simon account.</span></span>

    <span data-ttu-id="5ceb3-218">c.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-218">c.</span></span> <span data-ttu-id="5ceb3-219">Bonjour **fonction** zone de texte, fonction de Britta Simon type hello.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-219">In hello **Job Title** textbox, type hello job title of Britta Simon.</span></span>

    <span data-ttu-id="5ceb3-220">d.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-220">d.</span></span> <span data-ttu-id="5ceb3-221">Bonjour **emplacement** liste déroulante, emplacement sélectionnez hello de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-221">In hello **Location** dropdown, select hello location  of Britta Simon.</span></span>
    
    <span data-ttu-id="5ceb3-222">e.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-222">e.</span></span> <span data-ttu-id="5ceb3-223">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-223">Click **Add**.</span></span>   

4. <span data-ttu-id="5ceb3-224">Ajout de hello tooconfirm d’utilisateur s’un écran de confirmation.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-224">A confirmation screen will come up tooconfirm hello addition of user.</span></span>
    
    ![Confirmer](./media/active-directory-saas-pingboard-tutorial/create_testuser_confirm.png)
        
    > [!NOTE]
    > <span data-ttu-id="5ceb3-226">titulaire du compte Azure Active Directory Hello sera reçoivent un e-mail et suivez les leur compte d’un tooconfirm lien avant son activation.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-226">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5ceb3-227">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ceb3-227">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5ceb3-228">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant tooPingboard de son accès.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooPingboard.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="5ceb3-230">**tooassign Britta Simon tooPingboard, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5ceb3-230">**tooassign Britta Simon tooPingboard, perform hello following steps:**</span></span>

1. <span data-ttu-id="5ceb3-231">Dans le portail de gestion Azure hello, ouvrez la vue des applications hello, puis naviguez toohello les vue de répertoire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-231">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="5ceb3-233">Dans la liste des applications hello, sélectionnez **Pingboard**.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-233">In hello applications list, select **Pingboard**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_app.png) 

3. <span data-ttu-id="5ceb3-235">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="5ceb3-237">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-237">Click **Add** button.</span></span> <span data-ttu-id="5ceb3-238">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="5ceb3-240">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5ceb3-241">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5ceb3-242">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5ceb3-243">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="5ceb3-243">Testing single sign-on</span></span>

<span data-ttu-id="5ceb3-244">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-244">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5ceb3-245">Lorsque vous cliquez sur mosaïque Pingboard hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Pingboard application.</span><span class="sxs-lookup"><span data-stu-id="5ceb3-245">When you click hello Pingboard tile in hello Access Panel, you should get automatically signed-on tooyour Pingboard application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5ceb3-246">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="5ceb3-246">Additional resources</span></span>

* [<span data-ttu-id="5ceb3-247">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5ceb3-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5ceb3-248">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="5ceb3-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_203.png
