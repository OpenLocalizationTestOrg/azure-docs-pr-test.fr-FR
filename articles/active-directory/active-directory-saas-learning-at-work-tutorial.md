---
title: "Didacticiel : Intégration d’Azure Active Directory avec Learning at Work | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et d’apprentissage au travail."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d607174-bea1-4f40-8233-54cabe02c66a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: jeedes
ms.openlocfilehash: fa09d585d57932a95cadba9a66029765d7df3694
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learning-at-work"></a><span data-ttu-id="378bf-103">Didacticiel : Intégration d’Azure Active Directory à Learning at Work</span><span class="sxs-lookup"><span data-stu-id="378bf-103">Tutorial: Azure Active Directory integration with Learning at Work</span></span>

<span data-ttu-id="378bf-104">Dans ce didacticiel, vous apprendrez comment toointegrate d’apprentissage au travail avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="378bf-104">In this tutorial, you learn how toointegrate Learning at Work with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="378bf-105">Intégration de formation au travail avec Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="378bf-105">Integrating Learning at Work with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="378bf-106">Vous pouvez contrôler dans Azure AD qui a accès tooLearning au travail</span><span class="sxs-lookup"><span data-stu-id="378bf-106">You can control in Azure AD who has access tooLearning at Work</span></span>
- <span data-ttu-id="378bf-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooLearning au travail (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="378bf-107">You can enable your users tooautomatically get signed-on tooLearning at Work (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="378bf-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="378bf-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="378bf-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="378bf-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="378bf-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="378bf-110">Prerequisites</span></span>

<span data-ttu-id="378bf-111">tooconfigure intégration d’Azure AD avec Learning au travail, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="378bf-111">tooconfigure Azure AD integration with Learning at Work, you need hello following items:</span></span>

- <span data-ttu-id="378bf-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="378bf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="378bf-113">Un abonnement Learning at Work pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="378bf-113">A Learning at Work single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="378bf-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="378bf-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="378bf-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="378bf-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="378bf-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="378bf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="378bf-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="378bf-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="378bf-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="378bf-118">Scenario description</span></span>
<span data-ttu-id="378bf-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="378bf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="378bf-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="378bf-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="378bf-121">Ajout d’apprentissage au travail à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="378bf-121">Adding Learning at Work from hello gallery</span></span>
2. <span data-ttu-id="378bf-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="378bf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learning-at-work-from-hello-gallery"></a><span data-ttu-id="378bf-123">Ajout d’apprentissage au travail à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="378bf-123">Adding Learning at Work from hello gallery</span></span>
<span data-ttu-id="378bf-124">intégration de hello tooconfigure d’apprentissage au travail dans Azure AD, vous devez tooadd au travail d’apprentissage à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="378bf-124">tooconfigure hello integration of Learning at Work into Azure AD, you need tooadd Learning at Work from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="378bf-125">**tooadd de formation au travail à partir de la galerie de hello, effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="378bf-125">**tooadd Learning at Work from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="378bf-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="378bf-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="378bf-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="378bf-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="378bf-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="378bf-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="378bf-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="378bf-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="378bf-133">Dans la zone de recherche de hello, tapez **d’apprentissage au travail**.</span><span class="sxs-lookup"><span data-stu-id="378bf-133">In hello search box, type **Learning at Work**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_search.png)

5. <span data-ttu-id="378bf-135">Dans le volet de résultats hello, sélectionnez **d’apprentissage au travail**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="378bf-135">In hello results panel, select **Learning at Work**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="378bf-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="378bf-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="378bf-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Learning at Work à l’aide d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="378bf-138">In this section, you configure and test Azure AD single sign-on with Learning at Work based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="378bf-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Learning au travail est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="378bf-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Learning at Work is tooa user in Azure AD.</span></span> <span data-ttu-id="378bf-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans l’apprentissage automatique au travail hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="378bf-140">In other words, a link relationship between an Azure AD user and hello related user in Learning at Work needs toobe established.</span></span>

<span data-ttu-id="378bf-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans l’apprentissage automatique au travail.</span><span class="sxs-lookup"><span data-stu-id="378bf-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Learning at Work.</span></span>

<span data-ttu-id="378bf-142">tooconfigure et test Azure AD l’authentification unique avec Learning au travail, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="378bf-142">tooconfigure and test Azure AD single sign-on with Learning at Work, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="378bf-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="378bf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="378bf-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="378bf-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="378bf-145">**[Création d’un apprentissage à l’utilisateur de test de travail](#creating-a-learning-at-work-test-user)**  -toohave un équivalent de Britta Simon dans Learning au travail qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="378bf-145">**[Creating a Learning at Work test user](#creating-a-learning-at-work-test-user)** - toohave a counterpart of Britta Simon in Learning at Work that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="378bf-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="378bf-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="378bf-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="378bf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="378bf-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="378bf-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="378bf-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre apprentissage au travail de votre application.</span><span class="sxs-lookup"><span data-stu-id="378bf-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Learning at Work application.</span></span>

<span data-ttu-id="378bf-150">**tooconfigure Azure AD single sign-on avec Learning au travail, effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="378bf-150">**tooconfigure Azure AD single sign-on with Learning at Work, perform hello following steps:**</span></span>

1. <span data-ttu-id="378bf-151">Bonjour portail Azure, sur hello **d’apprentissage au travail** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="378bf-151">In hello Azure portal, on hello **Learning at Work** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="378bf-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="378bf-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_samlbase.png)

3. <span data-ttu-id="378bf-155">Sur hello **d’apprentissage au domaine de travail et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="378bf-155">On hello **Learning at Work Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_url.png)

    <span data-ttu-id="378bf-157">a.</span><span class="sxs-lookup"><span data-stu-id="378bf-157">a.</span></span> <span data-ttu-id="378bf-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.sabacloud.com/Saba/Web/<company code>`</span><span class="sxs-lookup"><span data-stu-id="378bf-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.sabacloud.com/Saba/Web/<company code>`</span></span>

    <span data-ttu-id="378bf-159">b.</span><span class="sxs-lookup"><span data-stu-id="378bf-159">b.</span></span> <span data-ttu-id="378bf-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.sabacloud.com/Saba/saml/SSO/alias/<company name>`</span><span class="sxs-lookup"><span data-stu-id="378bf-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.sabacloud.com/Saba/saml/SSO/alias/<company name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="378bf-161">Ces valeurs ne sont pas hello réel.</span><span class="sxs-lookup"><span data-stu-id="378bf-161">These values are not hello real.</span></span> <span data-ttu-id="378bf-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="378bf-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="378bf-163">Contact [d’apprentissage à l’équipe de prise en charge de travail Client](https://www.learninga-z.com/site/contact/support) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="378bf-163">Contact [Learning at Work Client support team](https://www.learninga-z.com/site/contact/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="378bf-164">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="378bf-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_certificate.png) 

5. <span data-ttu-id="378bf-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="378bf-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="378bf-168">Sur hello **de formation à la Configuration du travail** , cliquez sur **configurer d’apprentissage au travail** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="378bf-168">On hello **Learning at Work Configuration** section, click **Configure Learning at Work** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="378bf-169">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="378bf-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_configure.png) 

7. <span data-ttu-id="378bf-171">tooconfigure l’authentification unique sur **d’apprentissage au travail** côté, vous devez hello toosend téléchargé **Metadata XML**, **ID d’entité SAML**, **SAML Single Sign-On URL du service**, et **URL de déconnexion** trop[de formation à la prise en charge de travail](https://www.learninga-z.com/site/contact/support).</span><span class="sxs-lookup"><span data-stu-id="378bf-171">tooconfigure single sign-on on **Learning at Work** side, you need toosend hello downloaded **Metadata XML**, **SAML Entity ID**, **SAML Single Sign-On Service URL**, and **Sign-Out URL** too[Learning at Work support](https://www.learninga-z.com/site/contact/support).</span></span>

> [!TIP]
> <span data-ttu-id="378bf-172">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="378bf-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="378bf-173">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="378bf-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="378bf-174">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="378bf-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="378bf-175">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="378bf-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="378bf-176">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="378bf-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="378bf-178">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="378bf-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="378bf-179">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="378bf-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="378bf-181">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="378bf-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="378bf-183">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="378bf-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="378bf-185">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="378bf-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="378bf-187">a.</span><span class="sxs-lookup"><span data-stu-id="378bf-187">a.</span></span> <span data-ttu-id="378bf-188">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="378bf-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="378bf-189">b.</span><span class="sxs-lookup"><span data-stu-id="378bf-189">b.</span></span> <span data-ttu-id="378bf-190">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="378bf-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="378bf-191">c.</span><span class="sxs-lookup"><span data-stu-id="378bf-191">c.</span></span> <span data-ttu-id="378bf-192">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="378bf-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="378bf-193">d.</span><span class="sxs-lookup"><span data-stu-id="378bf-193">d.</span></span> <span data-ttu-id="378bf-194">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="378bf-194">Click **Create**.</span></span>
 
### <a name="creating-a-learning-at-work-test-user"></a><span data-ttu-id="378bf-195">Création d’un utilisateur de test Learning at Work</span><span class="sxs-lookup"><span data-stu-id="378bf-195">Creating a Learning at Work test user</span></span>

<span data-ttu-id="378bf-196">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Learning at Work.</span><span class="sxs-lookup"><span data-stu-id="378bf-196">In this section, you create a user called Britta Simon in Learning at Work.</span></span> <span data-ttu-id="378bf-197">Travailler avec [prise en charge de travail de formation](https://www.learninga-z.com/site/contact/support) utilisateurs hello tooadd hello formation à la plate-forme de travail.</span><span class="sxs-lookup"><span data-stu-id="378bf-197">Work with [Learning at Work support](https://www.learninga-z.com/site/contact/support) tooadd hello users in hello Learning at Work platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="378bf-198">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="378bf-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="378bf-199">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant tooLearning d’accès au travail.</span><span class="sxs-lookup"><span data-stu-id="378bf-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLearning at Work.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="378bf-201">**tooassign tooLearning Britta Simon au travail, effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="378bf-201">**tooassign Britta Simon tooLearning at Work, perform hello following steps:**</span></span>

1. <span data-ttu-id="378bf-202">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="378bf-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="378bf-204">Dans la liste des applications hello, sélectionnez **d’apprentissage au travail**.</span><span class="sxs-lookup"><span data-stu-id="378bf-204">In hello applications list, select **Learning at Work**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_app.png) 

3. <span data-ttu-id="378bf-206">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="378bf-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="378bf-208">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="378bf-208">Click **Add** button.</span></span> <span data-ttu-id="378bf-209">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="378bf-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="378bf-211">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="378bf-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="378bf-212">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="378bf-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="378bf-213">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="378bf-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="378bf-214">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="378bf-214">Testing single sign-on</span></span>

<span data-ttu-id="378bf-215">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="378bf-215">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="378bf-216">Lorsque vous cliquez sur hello apprentissage de la vignette de travail dans hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour d’apprentissage au travail de votre application.</span><span class="sxs-lookup"><span data-stu-id="378bf-216">When you click hello Learning at Work tile in hello Access Panel, you should get automatically signed-on tooyour Learning at Work application.</span></span>
<span data-ttu-id="378bf-217">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="378bf-217">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="378bf-218">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="378bf-218">Additional resources</span></span>

* [<span data-ttu-id="378bf-219">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="378bf-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="378bf-220">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="378bf-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_203.png

