---
title: "Didacticiel : intégration d’Azure Active Directory à PostBeyond | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et PostBeyond."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 09992f08-ec50-4472-997f-ccbe719039e8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 38019fd24a603732e91a1b5f7bfed5ab4edb017f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-postbeyond"></a><span data-ttu-id="8284f-103">Didacticiel : Intégration d’Azure AD à PostBeyond</span><span class="sxs-lookup"><span data-stu-id="8284f-103">Tutorial: Azure Active Directory integration with PostBeyond</span></span>

<span data-ttu-id="8284f-104">Dans ce didacticiel, vous apprendrez comment toointegrate PostBeyond avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8284f-104">In this tutorial, you learn how toointegrate PostBeyond with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8284f-105">Intégration PostBeyond à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="8284f-105">Integrating PostBeyond with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8284f-106">Vous pouvez contrôler dans Azure AD qui a accès tooPostBeyond</span><span class="sxs-lookup"><span data-stu-id="8284f-106">You can control in Azure AD who has access tooPostBeyond</span></span>
- <span data-ttu-id="8284f-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooPostBeyond (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="8284f-107">You can enable your users tooautomatically get signed-on tooPostBeyond (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8284f-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="8284f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8284f-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8284f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8284f-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8284f-110">Prerequisites</span></span>

<span data-ttu-id="8284f-111">tooconfigure intégration d’Azure AD avec PostBeyond, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="8284f-111">tooconfigure Azure AD integration with PostBeyond, you need hello following items:</span></span>

- <span data-ttu-id="8284f-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="8284f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8284f-113">Un abonnement PostBeyond pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="8284f-113">A PostBeyond single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8284f-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="8284f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8284f-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="8284f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8284f-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="8284f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8284f-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8284f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8284f-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="8284f-118">Scenario description</span></span>
<span data-ttu-id="8284f-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="8284f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8284f-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="8284f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8284f-121">Ajout de PostBeyond à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="8284f-121">Adding PostBeyond from hello gallery</span></span>
2. <span data-ttu-id="8284f-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8284f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-postbeyond-from-hello-gallery"></a><span data-ttu-id="8284f-123">Ajout de PostBeyond à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="8284f-123">Adding PostBeyond from hello gallery</span></span>
<span data-ttu-id="8284f-124">intégration de hello tooconfigure de PostBeyond dans Azure AD, vous devez tooadd PostBeyond à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="8284f-124">tooconfigure hello integration of PostBeyond into Azure AD, you need tooadd PostBeyond from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8284f-125">**tooadd PostBeyond à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8284f-125">**tooadd PostBeyond from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8284f-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="8284f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8284f-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="8284f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8284f-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="8284f-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="8284f-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="8284f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="8284f-133">Dans la zone de recherche de hello, tapez **PostBeyond**.</span><span class="sxs-lookup"><span data-stu-id="8284f-133">In hello search box, type **PostBeyond**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_search.png)

5. <span data-ttu-id="8284f-135">Dans le volet de résultats hello, sélectionnez **PostBeyond**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="8284f-135">In hello results panel, select **PostBeyond**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8284f-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8284f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8284f-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec PostBeyond, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="8284f-138">In this section, you configure and test Azure AD single sign-on with PostBeyond based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8284f-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans PostBeyond est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8284f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PostBeyond is tooa user in Azure AD.</span></span> <span data-ttu-id="8284f-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans PostBeyond doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="8284f-140">In other words, a link relationship between an Azure AD user and hello related user in PostBeyond needs toobe established.</span></span>

<span data-ttu-id="8284f-141">Dans PostBeyond, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="8284f-141">In PostBeyond, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8284f-142">tooconfigure et test Azure AD l’authentification unique avec PostBeyond, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="8284f-142">tooconfigure and test Azure AD single sign-on with PostBeyond, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8284f-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="8284f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8284f-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8284f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8284f-145">**[Création d’un utilisateur test PostBeyond](#creating-a-postbeyond-test-user)**  -toohave un équivalent de Britta Simon dans PostBeyond est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8284f-145">**[Creating a PostBeyond test user](#creating-a-postbeyond-test-user)** - toohave a counterpart of Britta Simon in PostBeyond that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8284f-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="8284f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8284f-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="8284f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8284f-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8284f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8284f-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application PostBeyond.</span><span class="sxs-lookup"><span data-stu-id="8284f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your PostBeyond application.</span></span>

<span data-ttu-id="8284f-150">**tooconfigure Azure AD single sign-on avec PostBeyond, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8284f-150">**tooconfigure Azure AD single sign-on with PostBeyond, perform hello following steps:**</span></span>

1. <span data-ttu-id="8284f-151">Bonjour portail Azure, sur hello **PostBeyond** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="8284f-151">In hello Azure portal, on hello **PostBeyond** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="8284f-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="8284f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_samlbase.png)

3. <span data-ttu-id="8284f-155">Sur hello **PostBeyond domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="8284f-155">On hello **PostBeyond Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_url.png)

    <span data-ttu-id="8284f-157">a.</span><span class="sxs-lookup"><span data-stu-id="8284f-157">a.</span></span> <span data-ttu-id="8284f-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.postbeyond.com`</span><span class="sxs-lookup"><span data-stu-id="8284f-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.postbeyond.com`</span></span>

    <span data-ttu-id="8284f-159">b.</span><span class="sxs-lookup"><span data-stu-id="8284f-159">b.</span></span> <span data-ttu-id="8284f-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.postbeyond.com`</span><span class="sxs-lookup"><span data-stu-id="8284f-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.postbeyond.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8284f-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="8284f-161">These values are not real.</span></span> <span data-ttu-id="8284f-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="8284f-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8284f-163">Contact [équipe de support Client de PostBeyond](mailto:sso@postbeyond.com) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="8284f-163">Contact [PostBeyond Client support team](mailto:sso@postbeyond.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="8284f-164">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="8284f-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_certificate.png) 

5. <span data-ttu-id="8284f-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="8284f-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-postbeyond-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8284f-168">Sur hello **PostBeyond Configuration** , cliquez sur **PostBeyond de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="8284f-168">On hello **PostBeyond Configuration** section, click **Configure PostBeyond** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8284f-169">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="8284f-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_configure.png) 

7. <span data-ttu-id="8284f-171">tooconfigure l’authentification unique sur **PostBeyond** côté, vous devez hello toosend téléchargé **Certificate(Base64)**, **ID d’entité SAML**, **SAML Single Sign-On URL du service** et **URL de déconnexion** trop[équipe de support PostBeyond](mailto:sso@postbeyond.com).</span><span class="sxs-lookup"><span data-stu-id="8284f-171">tooconfigure single sign-on on **PostBeyond** side, you need toosend hello downloaded **Certificate(Base64)**, **SAML Entity ID**, **SAML Single Sign-On Service URL** and **Sign-Out URL** too[PostBeyond support team](mailto:sso@postbeyond.com).</span></span> <span data-ttu-id="8284f-172">Ils définir ce hello toohave de paramètre connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="8284f-172">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="8284f-173">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="8284f-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8284f-174">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="8284f-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8284f-175">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8284f-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8284f-176">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="8284f-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="8284f-177">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="8284f-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="8284f-179">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8284f-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8284f-180">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="8284f-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-postbeyond-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8284f-182">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="8284f-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-postbeyond-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8284f-184">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="8284f-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-postbeyond-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8284f-186">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="8284f-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-postbeyond-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8284f-188">a.</span><span class="sxs-lookup"><span data-stu-id="8284f-188">a.</span></span> <span data-ttu-id="8284f-189">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8284f-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8284f-190">b.</span><span class="sxs-lookup"><span data-stu-id="8284f-190">b.</span></span> <span data-ttu-id="8284f-191">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8284f-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8284f-192">c.</span><span class="sxs-lookup"><span data-stu-id="8284f-192">c.</span></span> <span data-ttu-id="8284f-193">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="8284f-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8284f-194">d.</span><span class="sxs-lookup"><span data-stu-id="8284f-194">d.</span></span> <span data-ttu-id="8284f-195">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="8284f-195">Click **Create**.</span></span>
 
### <a name="creating-a-postbeyond-test-user"></a><span data-ttu-id="8284f-196">Création d’un utilisateur de test PostBeyond</span><span class="sxs-lookup"><span data-stu-id="8284f-196">Creating a PostBeyond test user</span></span>

<span data-ttu-id="8284f-197">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans PostBeyond.</span><span class="sxs-lookup"><span data-stu-id="8284f-197">In this section, you create a user called Britta Simon in PostBeyond.</span></span> <span data-ttu-id="8284f-198">Si vous ne savez pas comment tooadd Britta Simon dans PostBeyond, collaborez avec [équipe de support PostBeyond](mailto:sso@postbeyond.com) tooadd hello utilisateur de test et activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="8284f-198">If you don't know how tooadd Britta Simon in PostBeyond, please work with [PostBeyond support team](mailto:sso@postbeyond.com) tooadd hello test user and enable SSO.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8284f-199">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8284f-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8284f-200">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooPostBeyond.</span><span class="sxs-lookup"><span data-stu-id="8284f-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPostBeyond.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="8284f-202">**tooassign Britta Simon tooPostBeyond, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8284f-202">**tooassign Britta Simon tooPostBeyond, perform hello following steps:**</span></span>

1. <span data-ttu-id="8284f-203">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="8284f-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="8284f-205">Dans la liste des applications hello, sélectionnez **PostBeyond**.</span><span class="sxs-lookup"><span data-stu-id="8284f-205">In hello applications list, select **PostBeyond**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_app.png) 

3. <span data-ttu-id="8284f-207">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="8284f-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="8284f-209">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="8284f-209">Click **Add** button.</span></span> <span data-ttu-id="8284f-210">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="8284f-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="8284f-212">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="8284f-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8284f-213">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="8284f-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8284f-214">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="8284f-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8284f-215">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="8284f-215">Testing single sign-on</span></span>

<span data-ttu-id="8284f-216">objectif Hello de cette section est tootest votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="8284f-216">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="8284f-217">Lorsque vous cliquez sur la vignette de PostBeyond hello dans hello volet d’accès, vous devez obtenir l’authentification PostBeyond toohello dans la page.</span><span class="sxs-lookup"><span data-stu-id="8284f-217">When you click hello PostBeyond tile in hello Access Panel, you should get toohello PostBeyond sign in page.</span></span> <span data-ttu-id="8284f-218">Cliquez sur **Sign in with Office 365**(Se connecter avec Office 365), entrez vos informations d’identification Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8284f-218">Click on **Sign in with Office 365**, enter your Azure AD credentials.</span></span> <span data-ttu-id="8284f-219">Vous devriez maintenant être connecté à PostBeyond.</span><span class="sxs-lookup"><span data-stu-id="8284f-219">Then, you should be logged in into PostBeyond.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8284f-220">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="8284f-220">Additional resources</span></span>

* [<span data-ttu-id="8284f-221">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8284f-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8284f-222">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="8284f-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_203.png

