---
title: "Didacticiel : Intégration d’Azure Active Directory à Direct | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Direct."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7c2cd1f0-d14c-42f0-94a8-9b800008b285
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: ac663070b39e55eade2c43814b63a9d0374c7316
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-direct"></a><span data-ttu-id="9b854-103">Didacticiel : Intégration d’Azure Active Directory à Direct</span><span class="sxs-lookup"><span data-stu-id="9b854-103">Tutorial: Azure Active Directory integration with Direct</span></span>

<span data-ttu-id="9b854-104">Dans ce didacticiel, vous apprendrez comment toointegrate directe avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9b854-104">In this tutorial, you learn how toointegrate Direct with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9b854-105">Intégration directe avec Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="9b854-105">Integrating Direct with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9b854-106">Vous pouvez contrôler dans Azure AD qui a accès tooDirect</span><span class="sxs-lookup"><span data-stu-id="9b854-106">You can control in Azure AD who has access tooDirect</span></span>
- <span data-ttu-id="9b854-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooDirect (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="9b854-107">You can enable your users tooautomatically get signed-on tooDirect (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9b854-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="9b854-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9b854-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9b854-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9b854-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9b854-110">Prerequisites</span></span>

<span data-ttu-id="9b854-111">tooconfigure intégration d’Azure AD avec Direct, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="9b854-111">tooconfigure Azure AD integration with Direct, you need hello following items:</span></span>

- <span data-ttu-id="9b854-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="9b854-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9b854-113">Un abonnement Direct pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="9b854-113">A Direct single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9b854-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="9b854-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9b854-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="9b854-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9b854-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="9b854-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9b854-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9b854-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9b854-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="9b854-118">Scenario description</span></span>
<span data-ttu-id="9b854-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="9b854-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9b854-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="9b854-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9b854-121">L’ajout Direct de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="9b854-121">Adding Direct from hello gallery</span></span>
2. <span data-ttu-id="9b854-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9b854-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-direct-from-hello-gallery"></a><span data-ttu-id="9b854-123">L’ajout Direct de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="9b854-123">Adding Direct from hello gallery</span></span>
<span data-ttu-id="9b854-124">intégration de hello tooconfigure de Direct dans Azure AD, vous devez tooadd Direct à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="9b854-124">tooconfigure hello integration of Direct into Azure AD, you need tooadd Direct from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9b854-125">**tooadd Direct à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9b854-125">**tooadd Direct from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9b854-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="9b854-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9b854-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="9b854-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9b854-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="9b854-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="9b854-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="9b854-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="9b854-133">Dans la zone de recherche de hello, tapez **Direct**.</span><span class="sxs-lookup"><span data-stu-id="9b854-133">In hello search box, type **Direct**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-direct-tutorial/tutorial_direct_search.png)

5. <span data-ttu-id="9b854-135">Dans le volet de résultats hello, sélectionnez **Direct**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="9b854-135">In hello results panel, select **Direct**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-direct-tutorial/tutorial_direct_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9b854-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9b854-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9b854-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Direct, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="9b854-138">In this section, you configure and test Azure AD single sign-on with Direct based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9b854-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello est Direct tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9b854-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Direct is tooa user in Azure AD.</span></span> <span data-ttu-id="9b854-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans toobe besoins Direct établie.</span><span class="sxs-lookup"><span data-stu-id="9b854-140">In other words, a link relationship between an Azure AD user and hello related user in Direct needs toobe established.</span></span>

<span data-ttu-id="9b854-141">Directe, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="9b854-141">In Direct, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9b854-142">tooconfigure et test Azure AD sur l’authentification unique avec Direct, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="9b854-142">tooconfigure and test Azure AD single sign-on with Direct, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9b854-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="9b854-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9b854-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9b854-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9b854-145">**[Création d’un utilisateur test Direct](#creating-a-direct-test-user)**  -toohave un équivalent de Britta Simon directe est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9b854-145">**[Creating a Direct test user](#creating-a-direct-test-user)** - toohave a counterpart of Britta Simon in Direct that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9b854-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="9b854-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9b854-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="9b854-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9b854-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9b854-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9b854-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application directe.</span><span class="sxs-lookup"><span data-stu-id="9b854-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Direct application.</span></span>

<span data-ttu-id="9b854-150">**tooconfigure Azure AD l’authentification unique avec Direct, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9b854-150">**tooconfigure Azure AD single sign-on with Direct, perform hello following steps:**</span></span>

1. <span data-ttu-id="9b854-151">Bonjour portail Azure, sur hello **Direct** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="9b854-151">In hello Azure portal, on hello **Direct** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="9b854-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="9b854-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-direct-tutorial/tutorial_direct_samlbase.png)

3. <span data-ttu-id="9b854-155">Sur hello **Direct de domaine et les URL** section, si vous le souhaitez application hello tooconfigure **IDP** en mode initié par :</span><span class="sxs-lookup"><span data-stu-id="9b854-155">On hello **Direct Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-direct-tutorial/tutorial_direct_url.png)

    <span data-ttu-id="9b854-157">Bonjour **identificateur** zone de texte, tapez l’URL hello :`https://direct4b.com/`</span><span class="sxs-lookup"><span data-stu-id="9b854-157">In hello **Identifier** textbox, type hello URL: `https://direct4b.com/`</span></span>

4. <span data-ttu-id="9b854-158">Vérifiez **afficher les paramètres d’URL avancés**, si vous le souhaitez application hello tooconfigure **SP** en mode initié par :</span><span class="sxs-lookup"><span data-stu-id="9b854-158">Check **Show advanced URL settings**, If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-direct-tutorial/tutorial_direct_url1.png)

     <span data-ttu-id="9b854-160">Bonjour **URL de connexion** zone de texte, tapez l’URL hello :`https://direct4b.com/sso`</span><span class="sxs-lookup"><span data-stu-id="9b854-160">In hello **Sign-on URL** textbox, type hello URL: `https://direct4b.com/sso`</span></span> 
    
5. <span data-ttu-id="9b854-161">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="9b854-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-direct-tutorial/tutorial_direct_certificate.png) 

6. <span data-ttu-id="9b854-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="9b854-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-direct-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="9b854-165">tooconfigure l’authentification unique sur **Direct** côté, vous devez hello toosend téléchargé **Metadata XML** trop[prise en charge directe équipe](https://direct4b.com/ja/support.html#inquiry).</span><span class="sxs-lookup"><span data-stu-id="9b854-165">tooconfigure single sign-on on **Direct** side, you need toosend hello downloaded **Metadata XML** too[Direct support team](https://direct4b.com/ja/support.html#inquiry).</span></span> 

> [!TIP]
> <span data-ttu-id="9b854-166">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="9b854-166">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9b854-167">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="9b854-167">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9b854-168">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9b854-168">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9b854-169">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="9b854-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="9b854-170">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="9b854-170">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="9b854-172">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9b854-172">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9b854-173">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="9b854-173">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-direct-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9b854-175">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="9b854-175">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-direct-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9b854-177">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="9b854-177">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-direct-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9b854-179">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="9b854-179">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-direct-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9b854-181">a.</span><span class="sxs-lookup"><span data-stu-id="9b854-181">a.</span></span> <span data-ttu-id="9b854-182">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9b854-182">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9b854-183">b.</span><span class="sxs-lookup"><span data-stu-id="9b854-183">b.</span></span> <span data-ttu-id="9b854-184">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9b854-184">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9b854-185">c.</span><span class="sxs-lookup"><span data-stu-id="9b854-185">c.</span></span> <span data-ttu-id="9b854-186">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="9b854-186">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9b854-187">d.</span><span class="sxs-lookup"><span data-stu-id="9b854-187">d.</span></span> <span data-ttu-id="9b854-188">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="9b854-188">Click **Create**.</span></span>
 
### <a name="creating-a-direct-test-user"></a><span data-ttu-id="9b854-189">Création d’un utilisateur de test Direct</span><span class="sxs-lookup"><span data-stu-id="9b854-189">Creating a Direct test user</span></span>

<span data-ttu-id="9b854-190">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Direct.</span><span class="sxs-lookup"><span data-stu-id="9b854-190">In this section, you create a user called Britta Simon in Direct.</span></span> <span data-ttu-id="9b854-191">Travailler avec [prise en charge directe équipe](https://direct4b.com/ja/support.html#inquiry) pour ajouter des utilisateurs de hello de plate-forme Direct de hello.</span><span class="sxs-lookup"><span data-stu-id="9b854-191">Work with [Direct support team](https://direct4b.com/ja/support.html#inquiry) to add hello users in hello Direct platform.</span></span> <span data-ttu-id="9b854-192">Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="9b854-192">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9b854-193">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="9b854-193">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9b854-194">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooDirect.</span><span class="sxs-lookup"><span data-stu-id="9b854-194">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDirect.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="9b854-196">**tooassign Britta Simon tooDirect, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9b854-196">**tooassign Britta Simon tooDirect, perform hello following steps:**</span></span>

1. <span data-ttu-id="9b854-197">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="9b854-197">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="9b854-199">Dans la liste des applications hello, sélectionnez **Direct**.</span><span class="sxs-lookup"><span data-stu-id="9b854-199">In hello applications list, select **Direct**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-direct-tutorial/tutorial_direct_app.png) 

3. <span data-ttu-id="9b854-201">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="9b854-201">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="9b854-203">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="9b854-203">Click **Add** button.</span></span> <span data-ttu-id="9b854-204">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="9b854-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="9b854-206">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="9b854-206">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9b854-207">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="9b854-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9b854-208">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="9b854-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9b854-209">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="9b854-209">Testing single sign-on</span></span>

<span data-ttu-id="9b854-210">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="9b854-210">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

1. <span data-ttu-id="9b854-211">Si vous le souhaitez tootest dans **IDP initiée par le Mode**:</span><span class="sxs-lookup"><span data-stu-id="9b854-211">If you wish tootest in **IDP Initiated Mode**:</span></span>

    <span data-ttu-id="9b854-212">Lorsque vous cliquez sur hello **Direct** vignette dans hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour **Direct** application.</span><span class="sxs-lookup"><span data-stu-id="9b854-212">When you click hello **Direct** tile in hello Access Panel, you should get automatically signed-on tooyour **Direct** application.</span></span>

2. <span data-ttu-id="9b854-213">Si vous le souhaitez tootest dans **SP initiée par le Mode**:</span><span class="sxs-lookup"><span data-stu-id="9b854-213">If you wish tootest in **SP Initiated Mode**:</span></span>
    
    <span data-ttu-id="9b854-214">a.</span><span class="sxs-lookup"><span data-stu-id="9b854-214">a.</span></span> <span data-ttu-id="9b854-215">Cliquez sur hello **Direct** vignette dans le volet d’accès de hello et vous serez redirigé toohello application page authentification.</span><span class="sxs-lookup"><span data-stu-id="9b854-215">Click on hello **Direct** tile in hello Access Panel and you will be redirected toohello application sign-on page.</span></span>

    <span data-ttu-id="9b854-216">b.</span><span class="sxs-lookup"><span data-stu-id="9b854-216">b.</span></span> <span data-ttu-id="9b854-217">Entrez votre `subdomain` dans la zone de texte hello affichée, puis appuyez sur « 次へ (suivant) » et que vous devez obtenir automatiquement signé sur tooyour **Direct** application.</span><span class="sxs-lookup"><span data-stu-id="9b854-217">Input your `subdomain` in hello textbox displayed and press '次へ (Next)' and you should get automatically signed-on tooyour **Direct** application .</span></span>
    
<span data-ttu-id="9b854-218">Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9b854-218">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9b854-219">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="9b854-219">Additional resources</span></span>

* [<span data-ttu-id="9b854-220">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9b854-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9b854-221">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="9b854-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-direct-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-direct-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-direct-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-direct-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-direct-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-direct-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-direct-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-direct-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-direct-tutorial/tutorial_general_203.png

