---
title: "Didacticiel : Intégration d’Azure Active Directory à WORKS MOBILE | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et WORKS MOBILE."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 725f32fd-d0ad-49c7-b137-1cc246bf85d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 80192218a2e99a921834bb53e708d5e4fab413f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-works-mobile"></a><span data-ttu-id="29ca6-103">Didacticiel : Intégration d’Azure Active Directory à WORKS MOBILE</span><span class="sxs-lookup"><span data-stu-id="29ca6-103">Tutorial: Azure Active Directory integration with WORKS MOBILE</span></span>

<span data-ttu-id="29ca6-104">Dans ce didacticiel, vous découvrez le fonctionnement de toointegrate MOBILE avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="29ca6-104">In this tutorial, you learn how toointegrate WORKS MOBILE with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="29ca6-105">Intégration WORKS MOBILE auprès d’Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="29ca6-105">Integrating WORKS MOBILE with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="29ca6-106">Vous pouvez contrôler dans Azure AD qui a accès tooWORKS MOBILE</span><span class="sxs-lookup"><span data-stu-id="29ca6-106">You can control in Azure AD who has access tooWORKS MOBILE</span></span>
- <span data-ttu-id="29ca6-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooWORKS MOBILE (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="29ca6-107">You can enable your users tooautomatically get signed-on tooWORKS MOBILE (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="29ca6-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="29ca6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="29ca6-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="29ca6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="29ca6-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="29ca6-110">Prerequisites</span></span>

<span data-ttu-id="29ca6-111">tooconfigure intégration d’Azure AD avec WORKS MOBILE, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="29ca6-111">tooconfigure Azure AD integration with WORKS MOBILE, you need hello following items:</span></span>

- <span data-ttu-id="29ca6-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="29ca6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="29ca6-113">Un abonnement WORKS MOBILE pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="29ca6-113">A WORKS MOBILE single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="29ca6-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="29ca6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="29ca6-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="29ca6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="29ca6-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="29ca6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="29ca6-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="29ca6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="29ca6-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="29ca6-118">Scenario description</span></span>
<span data-ttu-id="29ca6-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="29ca6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="29ca6-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="29ca6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="29ca6-121">Ajout de WORKS MOBILE à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="29ca6-121">Adding WORKS MOBILE from hello gallery</span></span>
2. <span data-ttu-id="29ca6-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="29ca6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-works-mobile-from-hello-gallery"></a><span data-ttu-id="29ca6-123">Ajout de WORKS MOBILE à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="29ca6-123">Adding WORKS MOBILE from hello gallery</span></span>
<span data-ttu-id="29ca6-124">intégration de hello tooconfigure de WORKS MOBILE dans Azure AD, vous devez tooadd WORKS MOBILE à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="29ca6-124">tooconfigure hello integration of WORKS MOBILE into Azure AD, you need tooadd WORKS MOBILE from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="29ca6-125">**tooadd MOBILE fonctionne à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="29ca6-125">**tooadd WORKS MOBILE from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="29ca6-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="29ca6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="29ca6-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="29ca6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="29ca6-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="29ca6-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="29ca6-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="29ca6-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="29ca6-133">Dans la zone de recherche de hello, tapez **WORKS MOBILE**.</span><span class="sxs-lookup"><span data-stu-id="29ca6-133">In hello search box, type **WORKS MOBILE**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_search.png)

5. <span data-ttu-id="29ca6-135">Dans le volet de résultats hello, sélectionnez **WORKS MOBILE**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="29ca6-135">In hello results panel, select **WORKS MOBILE**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="29ca6-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="29ca6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="29ca6-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec WORKS MOBILE grâce à un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="29ca6-138">In this section, you configure and test Azure AD single sign-on with WORKS MOBILE based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="29ca6-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans WORKS MOBILE est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29ca6-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in WORKS MOBILE is tooa user in Azure AD.</span></span> <span data-ttu-id="29ca6-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans WORKS MOBILE doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="29ca6-140">In other words, a link relationship between an Azure AD user and hello related user in WORKS MOBILE needs toobe established.</span></span>

<span data-ttu-id="29ca6-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans WORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="29ca6-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in WORKS MOBILE.</span></span>

<span data-ttu-id="29ca6-142">tooconfigure et test Azure AD l’authentification unique avec WORKS MOBILE, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="29ca6-142">tooconfigure and test Azure AD single sign-on with WORKS MOBILE, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="29ca6-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="29ca6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="29ca6-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="29ca6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="29ca6-145">**[Création d’un utilisateur de test fonctionne MOBILE](#creating-a-works-mobile-test-user)**  -toohave un équivalent de Britta Simon dans WORKS MOBILE qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="29ca6-145">**[Creating a WORKS MOBILE test user](#creating-a-works-mobile-test-user)** - toohave a counterpart of Britta Simon in WORKS MOBILE that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="29ca6-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="29ca6-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="29ca6-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="29ca6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="29ca6-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="29ca6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="29ca6-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application MOBILE de fonctionnement.</span><span class="sxs-lookup"><span data-stu-id="29ca6-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your WORKS MOBILE application.</span></span>

<span data-ttu-id="29ca6-150">**tooconfigure Azure AD single sign-on avec WORKS MOBILE, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="29ca6-150">**tooconfigure Azure AD single sign-on with WORKS MOBILE, perform hello following steps:**</span></span>

1. <span data-ttu-id="29ca6-151">Bonjour portail Azure, sur hello **WORKS MOBILE** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="29ca6-151">In hello Azure portal, on hello **WORKS MOBILE** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="29ca6-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="29ca6-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_samlbase.png)

3. <span data-ttu-id="29ca6-155">Sur hello **WORKS MOBILE domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="29ca6-155">On hello **WORKS MOBILE Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_url.png)

    <span data-ttu-id="29ca6-157">a.</span><span class="sxs-lookup"><span data-stu-id="29ca6-157">a.</span></span> <span data-ttu-id="29ca6-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.worksmobile.com/jp/myservice`</span><span class="sxs-lookup"><span data-stu-id="29ca6-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.worksmobile.com/jp/myservice`</span></span>

    <span data-ttu-id="29ca6-159">b.</span><span class="sxs-lookup"><span data-stu-id="29ca6-159">b.</span></span> <span data-ttu-id="29ca6-160">Bonjour **identificateur** valeur hello de type en tant que zone de texte`worksmobile.com`</span><span class="sxs-lookup"><span data-stu-id="29ca6-160">In hello **Identifier** textbox, type hello value as `worksmobile.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="29ca6-161">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="29ca6-161">This value is not real.</span></span> <span data-ttu-id="29ca6-162">Mettre à jour de cette valeur avec hello URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="29ca6-162">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="29ca6-163">Contact [équipe de support technique WORKS MOBILE Client](mailto:dl_ssoinfo@worksmobile.com) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="29ca6-163">Contact [WORKS MOBILE Client support team](mailto:dl_ssoinfo@worksmobile.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="29ca6-164">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Raw)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="29ca6-164">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_certificate.png) 

5. <span data-ttu-id="29ca6-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="29ca6-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-worksmobile-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="29ca6-168">Sur hello **WORKS MOBILE Configuration** , cliquez sur **MOBILE de WORKS configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="29ca6-168">On hello **WORKS MOBILE Configuration** section, click **Configure WORKS MOBILE** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="29ca6-169">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="29ca6-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_configure.png) 

7. <span data-ttu-id="29ca6-171">tooget l’authentification unique configurée pour votre application, contactez [équipe de support technique WORKS MOBILE](mailto:dl_ssoinfo@worksmobile.com) et fournissez-leur hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="29ca6-171">tooget SSO configured for your application, contact [WORKS MOBILE support team](mailto:dl_ssoinfo@worksmobile.com) and provide them with hello following information:</span></span> 

    <span data-ttu-id="29ca6-172">hello • téléchargé **fichier de certificat**</span><span class="sxs-lookup"><span data-stu-id="29ca6-172">• hello downloaded **Certificate file**</span></span>

    <span data-ttu-id="29ca6-173">• hello **SAML Sign-On URL du Service unique**</span><span class="sxs-lookup"><span data-stu-id="29ca6-173">• hello **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="29ca6-174">• hello **ID d’entité SAML**</span><span class="sxs-lookup"><span data-stu-id="29ca6-174">• hello **SAML Entity ID**</span></span>

    <span data-ttu-id="29ca6-175">• hello **URL de déconnexion**</span><span class="sxs-lookup"><span data-stu-id="29ca6-175">• hello **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="29ca6-176">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="29ca6-176">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="29ca6-177">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="29ca6-177">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="29ca6-178">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="29ca6-178">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="29ca6-179">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="29ca6-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="29ca6-180">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="29ca6-180">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="29ca6-182">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="29ca6-182">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="29ca6-183">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="29ca6-183">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="29ca6-185">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="29ca6-185">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="29ca6-187">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="29ca6-187">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="29ca6-189">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="29ca6-189">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="29ca6-191">a.</span><span class="sxs-lookup"><span data-stu-id="29ca6-191">a.</span></span> <span data-ttu-id="29ca6-192">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="29ca6-192">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="29ca6-193">b.</span><span class="sxs-lookup"><span data-stu-id="29ca6-193">b.</span></span> <span data-ttu-id="29ca6-194">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="29ca6-194">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="29ca6-195">c.</span><span class="sxs-lookup"><span data-stu-id="29ca6-195">c.</span></span> <span data-ttu-id="29ca6-196">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="29ca6-196">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="29ca6-197">d.</span><span class="sxs-lookup"><span data-stu-id="29ca6-197">d.</span></span> <span data-ttu-id="29ca6-198">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="29ca6-198">Click **Create**.</span></span>
 
### <a name="creating-a-works-mobile-test-user"></a><span data-ttu-id="29ca6-199">Création d’un utilisateur de test WORKS MOBILE</span><span class="sxs-lookup"><span data-stu-id="29ca6-199">Creating a WORKS MOBILE test user</span></span>

 <span data-ttu-id="29ca6-200">Dans cette section, vous créez un utilisateur appelé Britta Simon dans WORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="29ca6-200">In this section, you create a user called Britta Simon in WORKS MOBILE.</span></span> <span data-ttu-id="29ca6-201">Collaborez avec [équipe de support technique WORKS MOBILE](mailto:dl_ssoinfo@worksmobile.com) tooadd les utilisateurs de hello dans la plateforme MOBILE de fonctionnement de hello.</span><span class="sxs-lookup"><span data-stu-id="29ca6-201">Please work with [WORKS MOBILE support team](mailto:dl_ssoinfo@worksmobile.com) tooadd hello users in hello WORKS MOBILE platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="29ca6-202">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="29ca6-202">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="29ca6-203">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooWORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="29ca6-203">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWORKS MOBILE.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="29ca6-205">**tooassign Britta Simon tooWORKS MOBILE, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="29ca6-205">**tooassign Britta Simon tooWORKS MOBILE, perform hello following steps:**</span></span>

1. <span data-ttu-id="29ca6-206">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="29ca6-206">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="29ca6-208">Dans la liste des applications hello, sélectionnez **WORKS MOBILE**.</span><span class="sxs-lookup"><span data-stu-id="29ca6-208">In hello applications list, select **WORKS MOBILE**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_app.png) 

3. <span data-ttu-id="29ca6-210">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="29ca6-210">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="29ca6-212">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="29ca6-212">Click **Add** button.</span></span> <span data-ttu-id="29ca6-213">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="29ca6-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="29ca6-215">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="29ca6-215">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="29ca6-216">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="29ca6-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="29ca6-217">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="29ca6-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="29ca6-218">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="29ca6-218">Testing single sign-on</span></span>

<span data-ttu-id="29ca6-219">Dans cette section, vous tester votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="29ca6-219">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="29ca6-220">Lorsque vous cliquez sur mosaïque fonctionne MOBILE hello hello volet d’accès, vous devez obtenir l’application MOBILE de fonctionnement de tooyour automatiquement signé sur.</span><span class="sxs-lookup"><span data-stu-id="29ca6-220">When you click hello WORKS MOBILE tile in hello Access Panel, you should get automatically signed-on tooyour WORKS MOBILE application.</span></span>
<span data-ttu-id="29ca6-221">Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="29ca6-221">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="29ca6-222">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="29ca6-222">Additional resources</span></span>

* [<span data-ttu-id="29ca6-223">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="29ca6-223">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="29ca6-224">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="29ca6-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_203.png

