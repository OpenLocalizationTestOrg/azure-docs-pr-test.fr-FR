---
title: "Didacticiel : intégration d’Azure Active Directory avec Learning Seat LMS | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et LMS, Learning siège."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bb056fcf-4135-478e-85b1-5015d1f07b85
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: jeedes
ms.openlocfilehash: dc08aa444b85f35a4458768ac560ec663baa1c95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learning-seat-lms"></a><span data-ttu-id="3fbba-103">Didacticiel : intégration d’Azure Active Directory à Learning Seat LMS</span><span class="sxs-lookup"><span data-stu-id="3fbba-103">Tutorial: Azure Active Directory integration with Learning Seat LMS</span></span>

<span data-ttu-id="3fbba-104">Dans ce didacticiel, vous apprendrez comment toointegrate LMS, Learning siège avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3fbba-104">In this tutorial, you learn how toointegrate Learning Seat LMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3fbba-105">Intégration LMS, Learning siège à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="3fbba-105">Integrating Learning Seat LMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3fbba-106">Vous pouvez contrôler dans Azure AD qui a accès tooLearning siège LMS</span><span class="sxs-lookup"><span data-stu-id="3fbba-106">You can control in Azure AD who has access tooLearning Seat LMS</span></span>
- <span data-ttu-id="3fbba-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooLearning LMS siège (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="3fbba-107">You can enable your users tooautomatically get signed-on tooLearning Seat LMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3fbba-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="3fbba-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3fbba-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez.</span><span class="sxs-lookup"><span data-stu-id="3fbba-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="3fbba-110">[Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3fbba-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3fbba-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="3fbba-111">Prerequisites</span></span>

<span data-ttu-id="3fbba-112">tooconfigure intégration d’Azure AD avec LMS, Learning siège, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="3fbba-112">tooconfigure Azure AD integration with Learning Seat LMS, you need hello following items:</span></span>

- <span data-ttu-id="3fbba-113">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="3fbba-113">An Azure AD subscription</span></span>
- <span data-ttu-id="3fbba-114">Un abonnement à Learning Seat LMS pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="3fbba-114">A Learning Seat LMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3fbba-115">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="3fbba-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3fbba-116">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="3fbba-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3fbba-117">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="3fbba-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3fbba-118">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3fbba-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3fbba-119">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="3fbba-119">Scenario description</span></span>
<span data-ttu-id="3fbba-120">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="3fbba-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3fbba-121">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="3fbba-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3fbba-122">Ajout de siège LMS, Learning à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="3fbba-122">Adding Learning Seat LMS from hello gallery</span></span>
2. <span data-ttu-id="3fbba-123">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="3fbba-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learning-seat-lms-from-hello-gallery"></a><span data-ttu-id="3fbba-124">Ajout de siège LMS, Learning à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="3fbba-124">Adding Learning Seat LMS from hello gallery</span></span>
<span data-ttu-id="3fbba-125">tooconfigure hello intégration de siège LMS, Learning dans Azure AD, vous devez tooadd LMS, Learning siège à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="3fbba-125">tooconfigure hello integration of Learning Seat LMS into Azure AD, you need tooadd Learning Seat LMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3fbba-126">**tooadd LMS, Learning siège à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="3fbba-126">**tooadd Learning Seat LMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3fbba-127">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="3fbba-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3fbba-129">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="3fbba-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3fbba-130">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="3fbba-130">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="3fbba-132">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="3fbba-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="3fbba-134">Dans la zone de recherche de hello, tapez **LMS, Learning siège**.</span><span class="sxs-lookup"><span data-stu-id="3fbba-134">In hello search box, type **Learning Seat LMS**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_search.png)

5. <span data-ttu-id="3fbba-136">Dans le volet de résultats hello, sélectionnez **LMS, Learning siège**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="3fbba-136">In hello results panel, select **Learning Seat LMS**, and then click **Add** button tooadd hello application.</span></span>


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3fbba-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="3fbba-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3fbba-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Learning Seat LMS avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="3fbba-138">In this section, you configure and test Azure AD single sign-on with Learning Seat LMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3fbba-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans LMS, Learning siège est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3fbba-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Learning Seat LMS is tooa user in Azure AD.</span></span> <span data-ttu-id="3fbba-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans LMS, Learning siège doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="3fbba-140">In other words, a link relationship between an Azure AD user and hello related user in Learning Seat LMS needs toobe established.</span></span>

<span data-ttu-id="3fbba-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans LMS, Learning siège.</span><span class="sxs-lookup"><span data-stu-id="3fbba-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Learning Seat LMS.</span></span>

<span data-ttu-id="3fbba-142">tooconfigure et test Azure AD l’authentification unique avec LMS, Learning siège, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="3fbba-142">tooconfigure and test Azure AD single sign-on with Learning Seat LMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3fbba-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="3fbba-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3fbba-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3fbba-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3fbba-145">**[Création d’un utilisateur de test LMS, Learning siège](#creating-a-learnconnect-test-user)**  -toohave un équivalent de Britta Simon dans LMS, Learning siège qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="3fbba-145">**[Creating a Learning Seat LMS test user](#creating-a-learnconnect-test-user)** - toohave a counterpart of Britta Simon in Learning Seat LMS that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3fbba-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="3fbba-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3fbba-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="3fbba-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3fbba-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="3fbba-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3fbba-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application LMS, Learning siège.</span><span class="sxs-lookup"><span data-stu-id="3fbba-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Learning Seat LMS application.</span></span>

<span data-ttu-id="3fbba-150">**tooconfigure Azure AD l’authentification unique avec LMS, Learning siège, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="3fbba-150">**tooconfigure Azure AD single sign-on with Learning Seat LMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="3fbba-151">Bonjour portail Azure, sur hello **LMS, Learning siège** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="3fbba-151">In hello Azure portal, on hello **Learning Seat LMS** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="3fbba-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="3fbba-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_samlbase.png)

3. <span data-ttu-id="3fbba-155">Sur hello **Learning siège LMS domaine et les URL** section, effectuer hello comme suit si vous le souhaitez application hello tooconfigure **IDP** en mode initié par :</span><span class="sxs-lookup"><span data-stu-id="3fbba-155">On hello **Learning Seat LMS Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_url.png)

    <span data-ttu-id="3fbba-157">a.</span><span class="sxs-lookup"><span data-stu-id="3fbba-157">a.</span></span> <span data-ttu-id="3fbba-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.learningseatlms.com`</span><span class="sxs-lookup"><span data-stu-id="3fbba-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.learningseatlms.com`</span></span>

    <span data-ttu-id="3fbba-159">b.</span><span class="sxs-lookup"><span data-stu-id="3fbba-159">b.</span></span> <span data-ttu-id="3fbba-160">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.learningseatlms.com/Account/AssertionConsumerService`</span><span class="sxs-lookup"><span data-stu-id="3fbba-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.learningseatlms.com/Account/AssertionConsumerService`</span></span>

4. <span data-ttu-id="3fbba-161">Vérifiez **afficher les paramètres d’URL avancés**, si vous le souhaitez application hello tooconfigure **SP** en mode initié par :</span><span class="sxs-lookup"><span data-stu-id="3fbba-161">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_url2.png)

    <span data-ttu-id="3fbba-163">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.learningseatlms.com`</span><span class="sxs-lookup"><span data-stu-id="3fbba-163">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.learningseatlms.com`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="3fbba-164">Ces valeurs ne sont pas des valeurs réelles hello.</span><span class="sxs-lookup"><span data-stu-id="3fbba-164">These values are not hello real values.</span></span> <span data-ttu-id="3fbba-165">Mettre à jour les valeurs de hello réel identificateur, les URL de réponse et les URL de connexion.</span><span class="sxs-lookup"><span data-stu-id="3fbba-165">Update these values with hello actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="3fbba-166">Contact [équipe de support technique d’apprentissage siège](http://help.learningseatlms.com/help) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="3fbba-166">Contact [Learning Seat support team](http://help.learningseatlms.com/help) tooget these values.</span></span> 

5. <span data-ttu-id="3fbba-167">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="3fbba-167">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_certificate.png) 

6. <span data-ttu-id="3fbba-169">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="3fbba-169">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-learnconnect-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="3fbba-171">tooconfigure l’authentification unique sur **LMS, Learning siège** côté, vous devez hello toosend téléchargé **Metadata XML** trop[équipe de support technique d’apprentissage siège](http://help.learningseatlms.com/help).</span><span class="sxs-lookup"><span data-stu-id="3fbba-171">tooconfigure single sign-on on **Learning Seat LMS** side, you need toosend hello downloaded **Metadata XML** too[Learning Seat support team](http://help.learningseatlms.com/help).</span></span>

> [!TIP]
> <span data-ttu-id="3fbba-172">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="3fbba-172">You can now read a concise version of these instructions inside hello [Azure  portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3fbba-173">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="3fbba-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3fbba-174">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation](https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3fbba-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3fbba-175">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="3fbba-175">Creating an Azure AD test user</span></span>

<span data-ttu-id="3fbba-176">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="3fbba-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="3fbba-178">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="3fbba-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3fbba-179">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="3fbba-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3fbba-181">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="3fbba-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3fbba-183">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="3fbba-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3fbba-185">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="3fbba-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3fbba-187">a.</span><span class="sxs-lookup"><span data-stu-id="3fbba-187">a.</span></span> <span data-ttu-id="3fbba-188">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3fbba-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3fbba-189">b.</span><span class="sxs-lookup"><span data-stu-id="3fbba-189">b.</span></span> <span data-ttu-id="3fbba-190">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3fbba-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3fbba-191">c.</span><span class="sxs-lookup"><span data-stu-id="3fbba-191">c.</span></span> <span data-ttu-id="3fbba-192">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="3fbba-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3fbba-193">d.</span><span class="sxs-lookup"><span data-stu-id="3fbba-193">d.</span></span> <span data-ttu-id="3fbba-194">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="3fbba-194">Click **Create**.</span></span>
 
### <a name="creating-a-learning-seat-lms-test-user"></a><span data-ttu-id="3fbba-195">Création d’un utilisateur de test Learning Seat LMS</span><span class="sxs-lookup"><span data-stu-id="3fbba-195">Creating a Learning Seat LMS test user</span></span>

<span data-ttu-id="3fbba-196">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Learning Seat LMS.</span><span class="sxs-lookup"><span data-stu-id="3fbba-196">In this section, you create a user called Britta Simon in Learning Seat LMS.</span></span> <span data-ttu-id="3fbba-197">Contact [équipe de support technique d’apprentissage siège](http://help.learningseatlms.com/help) avec tous les hello utilisateur informations tooadd hello utilisateurs Bonjour application de LMS, Learning siège.</span><span class="sxs-lookup"><span data-stu-id="3fbba-197">Contact [Learning Seat support team](http://help.learningseatlms.com/help) with all hello user information tooadd hello users in hello Learning Seat LMS application.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3fbba-198">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="3fbba-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3fbba-199">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooLearning siège LMS.</span><span class="sxs-lookup"><span data-stu-id="3fbba-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLearning Seat LMS.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="3fbba-201">**tooassign Britta Simon tooLearning siège LMS, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="3fbba-201">**tooassign Britta Simon tooLearning Seat LMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="3fbba-202">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="3fbba-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="3fbba-204">Dans la liste des applications hello, sélectionnez **LMS, Learning siège**.</span><span class="sxs-lookup"><span data-stu-id="3fbba-204">In hello applications list, select **Learning Seat LMS**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_app.png) 

3. <span data-ttu-id="3fbba-206">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="3fbba-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="3fbba-208">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="3fbba-208">Click **Add** button.</span></span> <span data-ttu-id="3fbba-209">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="3fbba-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="3fbba-211">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="3fbba-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3fbba-212">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="3fbba-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3fbba-213">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="3fbba-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3fbba-214">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="3fbba-214">Testing single sign-on</span></span>

<span data-ttu-id="3fbba-215">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="3fbba-215">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span> 

<span data-ttu-id="3fbba-216">Cliquez sur hello LMS, Learning siège vignette Bonjour volet d’accès, vous sera automatiquement signé sur tooyour LMS, Learning siège.</span><span class="sxs-lookup"><span data-stu-id="3fbba-216">Click hello Learning Seat LMS tile in hello Access Panel, you will be automatically signed-on tooyour Learning Seat LMS application.</span></span> <span data-ttu-id="3fbba-217">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="3fbba-217">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3fbba-218">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="3fbba-218">Additional resources</span></span>

* [<span data-ttu-id="3fbba-219">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3fbba-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3fbba-220">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="3fbba-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_203.png

