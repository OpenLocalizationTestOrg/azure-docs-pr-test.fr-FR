---
title: "Didacticiel : Intégration d’Azure Active Directory à ZIVVER | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et ZIVVER."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 64cb7ea0-df6c-4963-84d8-6f435980e2de
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 0928abcc4dcbd97b892298f4919c8d44e1a058a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zivver"></a><span data-ttu-id="c15d1-103">Didacticiel : Intégration d’Azure Active Directory à ZIVVER</span><span class="sxs-lookup"><span data-stu-id="c15d1-103">Tutorial: Azure Active Directory integration with ZIVVER</span></span>

<span data-ttu-id="c15d1-104">Dans ce didacticiel, vous apprendrez comment toointegrate ZIVVER avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c15d1-104">In this tutorial, you learn how toointegrate ZIVVER with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c15d1-105">Intégration ZIVVER à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="c15d1-105">Integrating ZIVVER with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c15d1-106">Vous pouvez contrôler dans Azure AD qui a accès tooZIVVER.</span><span class="sxs-lookup"><span data-stu-id="c15d1-106">You can control in Azure AD who has access tooZIVVER.</span></span>
- <span data-ttu-id="c15d1-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooZIVVER (Single Sign-On) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c15d1-107">You can enable your users tooautomatically get signed-on tooZIVVER (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="c15d1-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c15d1-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="c15d1-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c15d1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c15d1-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c15d1-110">Prerequisites</span></span>

<span data-ttu-id="c15d1-111">tooconfigure intégration d’Azure AD avec ZIVVER, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="c15d1-111">tooconfigure Azure AD integration with ZIVVER, you need hello following items:</span></span>

- <span data-ttu-id="c15d1-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="c15d1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c15d1-113">Un abonnement ZIVVER pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="c15d1-113">A ZIVVER single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c15d1-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="c15d1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c15d1-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="c15d1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c15d1-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="c15d1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c15d1-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c15d1-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c15d1-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="c15d1-118">Scenario description</span></span>
<span data-ttu-id="c15d1-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="c15d1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c15d1-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="c15d1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c15d1-121">Ajout de ZIVVER à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="c15d1-121">Adding ZIVVER from hello gallery</span></span>
2. <span data-ttu-id="c15d1-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c15d1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zivver-from-hello-gallery"></a><span data-ttu-id="c15d1-123">Ajout de ZIVVER à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="c15d1-123">Adding ZIVVER from hello gallery</span></span>
<span data-ttu-id="c15d1-124">intégration de hello tooconfigure de ZIVVER dans Azure AD, vous devez tooadd ZIVVER à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="c15d1-124">tooconfigure hello integration of ZIVVER into Azure AD, you need tooadd ZIVVER from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c15d1-125">**tooadd ZIVVER à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c15d1-125">**tooadd ZIVVER from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c15d1-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="c15d1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="c15d1-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="c15d1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c15d1-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="c15d1-129">Then go too**All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="c15d1-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="c15d1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="c15d1-133">Dans la zone de recherche de hello, tapez **ZIVVER**, sélectionnez **ZIVVER** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="c15d1-133">In hello search box, type **ZIVVER**, select **ZIVVER** from result panel then click **Add** button tooadd hello application.</span></span>

    ![ZIVVER dans la liste des résultats hello](./media/active-directory-saas-zivver-tutorial/tutorial_zivver_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c15d1-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c15d1-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="c15d1-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec ZIVVER, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="c15d1-136">In this section, you configure and test Azure AD single sign-on with ZIVVER based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c15d1-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans ZIVVER est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c15d1-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ZIVVER is tooa user in Azure AD.</span></span> <span data-ttu-id="c15d1-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans ZIVVER doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="c15d1-138">In other words, a link relationship between an Azure AD user and hello related user in ZIVVER needs toobe established.</span></span>

<span data-ttu-id="c15d1-139">Dans ZIVVER, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="c15d1-139">In ZIVVER, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c15d1-140">tooconfigure et test Azure AD l’authentification unique avec ZIVVER, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="c15d1-140">tooconfigure and test Azure AD single sign-on with ZIVVER, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c15d1-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="c15d1-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c15d1-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c15d1-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c15d1-143">**[Créer un utilisateur de test ZIVVER](#create-a-zivver-test-user)**  -toohave un équivalent de Britta Simon dans ZIVVER est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c15d1-143">**[Create a ZIVVER test user](#create-a-zivver-test-user)** - toohave a counterpart of Britta Simon in ZIVVER that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c15d1-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c15d1-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c15d1-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="c15d1-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="c15d1-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c15d1-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="c15d1-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application ZIVVER.</span><span class="sxs-lookup"><span data-stu-id="c15d1-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ZIVVER application.</span></span>

<span data-ttu-id="c15d1-148">**tooconfigure Azure AD single sign-on avec ZIVVER, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c15d1-148">**tooconfigure Azure AD single sign-on with ZIVVER, perform hello following steps:**</span></span>

1. <span data-ttu-id="c15d1-149">Bonjour portail Azure, sur hello **ZIVVER** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="c15d1-149">In hello Azure portal, on hello **ZIVVER** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="c15d1-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c15d1-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-zivver-tutorial/tutorial_zivver_samlbase.png)

3. <span data-ttu-id="c15d1-153">Sur hello **ZIVVER domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c15d1-153">On hello **ZIVVER Domain and URLs** section, perform hello following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL ZIVVER](./media/active-directory-saas-zivver-tutorial/tutorial_zivver_url.png)

    <span data-ttu-id="c15d1-155">Bonjour **identificateur** zone de texte, tapez l’URL hello :`https://app.zivver.com/SAML/Zivver`</span><span class="sxs-lookup"><span data-stu-id="c15d1-155">In hello **Identifier** textbox, type hello URL: `https://app.zivver.com/SAML/Zivver`</span></span>

4. <span data-ttu-id="c15d1-156">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="c15d1-156">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-zivver-tutorial/tutorial_zivver_certificate.png) 

5. <span data-ttu-id="c15d1-158">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="c15d1-158">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-zivver-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c15d1-160">tooconfigure l’authentification unique sur **ZIVVER** côté, vous devez hello toosend téléchargé **Metadata XML** trop[ZIVVER l’équipe de support](https://support.zivver.com).</span><span class="sxs-lookup"><span data-stu-id="c15d1-160">tooconfigure single sign-on on **ZIVVER** side, you need toosend hello downloaded **Metadata XML** too[ZIVVER support team](https://support.zivver.com).</span></span> <span data-ttu-id="c15d1-161">Ils définir ce hello toohave de paramètre connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="c15d1-161">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="c15d1-162">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="c15d1-162">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c15d1-163">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="c15d1-163">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c15d1-164">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c15d1-164">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c15d1-165">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="c15d1-165">Create an Azure AD test user</span></span>

<span data-ttu-id="c15d1-166">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="c15d1-166">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="c15d1-168">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c15d1-168">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c15d1-169">Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.</span><span class="sxs-lookup"><span data-stu-id="c15d1-169">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-zivver-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="c15d1-171">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="c15d1-171">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-zivver-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="c15d1-173">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="c15d1-173">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![bouton Ajouter de Hello](./media/active-directory-saas-zivver-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="c15d1-175">Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c15d1-175">In hello **User** dialog box, perform hello following steps:</span></span>

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-zivver-tutorial/create_aaduser_04.png)

    <span data-ttu-id="c15d1-177">a.</span><span class="sxs-lookup"><span data-stu-id="c15d1-177">a.</span></span> <span data-ttu-id="c15d1-178">Bonjour **nom** , tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c15d1-178">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c15d1-179">b.</span><span class="sxs-lookup"><span data-stu-id="c15d1-179">b.</span></span> <span data-ttu-id="c15d1-180">Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c15d1-180">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="c15d1-181">c.</span><span class="sxs-lookup"><span data-stu-id="c15d1-181">c.</span></span> <span data-ttu-id="c15d1-182">Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.</span><span class="sxs-lookup"><span data-stu-id="c15d1-182">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="c15d1-183">d.</span><span class="sxs-lookup"><span data-stu-id="c15d1-183">d.</span></span> <span data-ttu-id="c15d1-184">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="c15d1-184">Click **Create**.</span></span>
  
### <a name="create-a-zivver-test-user"></a><span data-ttu-id="c15d1-185">Créer un utilisateur de test ZIVVER</span><span class="sxs-lookup"><span data-stu-id="c15d1-185">Create a ZIVVER test user</span></span>

<span data-ttu-id="c15d1-186">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans ZIVVER.</span><span class="sxs-lookup"><span data-stu-id="c15d1-186">In this section, you create a user called Britta Simon in ZIVVER.</span></span> <span data-ttu-id="c15d1-187">Travailler avec [ZIVVER l’équipe de support](https://support.zivver.com) utilisateurs hello tooadd plate-forme ZIVVER hello.</span><span class="sxs-lookup"><span data-stu-id="c15d1-187">Work with [ZIVVER support team](https://support.zivver.com) tooadd hello users in hello ZIVVER platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="c15d1-188">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c15d1-188">Assign hello Azure AD test user</span></span>

<span data-ttu-id="c15d1-189">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooZIVVER.</span><span class="sxs-lookup"><span data-stu-id="c15d1-189">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZIVVER.</span></span>

![Attribuer le rôle d’utilisateur hello][200] 

<span data-ttu-id="c15d1-191">**tooassign Britta Simon tooZIVVER, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c15d1-191">**tooassign Britta Simon tooZIVVER, perform hello following steps:**</span></span>

1. <span data-ttu-id="c15d1-192">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="c15d1-192">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="c15d1-194">Dans la liste des applications hello, sélectionnez **ZIVVER**.</span><span class="sxs-lookup"><span data-stu-id="c15d1-194">In hello applications list, select **ZIVVER**.</span></span>

    ![lien ZIVVER Hello dans la liste des Applications hello](./media/active-directory-saas-zivver-tutorial/tutorial_zivver_app.png)  

3. <span data-ttu-id="c15d1-196">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="c15d1-196">In hello menu on hello left, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202]

4. <span data-ttu-id="c15d1-198">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="c15d1-198">Click **Add** button.</span></span> <span data-ttu-id="c15d1-199">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="c15d1-199">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="c15d1-201">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="c15d1-201">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c15d1-202">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="c15d1-202">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c15d1-203">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="c15d1-203">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="c15d1-204">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="c15d1-204">Test single sign-on</span></span>

<span data-ttu-id="c15d1-205">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="c15d1-205">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c15d1-206">Lorsque vous cliquez sur hello ZIVVER vignette dans le volet d’accès de hello, vous devez obtenir l’application de ZIVVER tooyour automatiquement signé sur.</span><span class="sxs-lookup"><span data-stu-id="c15d1-206">When you click hello ZIVVER tile in hello Access Panel, you should get automatically signed-on tooyour ZIVVER application.</span></span>
<span data-ttu-id="c15d1-207">Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c15d1-207">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c15d1-208">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="c15d1-208">Additional resources</span></span>

* [<span data-ttu-id="c15d1-209">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c15d1-209">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c15d1-210">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="c15d1-210">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_203.png

