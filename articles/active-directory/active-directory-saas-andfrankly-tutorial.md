---
title: "Didacticiel : Intégration d’Azure Active Directory dans &frankly | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et & franchement."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d702060-1b89-4e9d-9f01-ede4f1171c73
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 92677b6fcd8609ca31f82a30e85c7010b7bb3351
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-frankly"></a><span data-ttu-id="f1ac5-103">Didacticiel : Intégration d’Azure Active Directory dans &frankly</span><span class="sxs-lookup"><span data-stu-id="f1ac5-103">Tutorial: Azure Active Directory integration with &frankly</span></span>

<span data-ttu-id="f1ac5-104">Dans ce didacticiel, vous apprendrez comment toointegrate & franchement avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f1ac5-104">In this tutorial, you learn how toointegrate &frankly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f1ac5-105">Intégration & franchement avec Azure AD vous fournit hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="f1ac5-105">Integrating &frankly with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f1ac5-106">Vous pouvez contrôler dans Azure AD qui a accès trop & franchement</span><span class="sxs-lookup"><span data-stu-id="f1ac5-106">You can control in Azure AD who has access too&frankly</span></span>
- <span data-ttu-id="f1ac5-107">Vous pouvez activer vos utilisateurs tooautomatically obtenir connecté trop & franchement (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1ac5-107">You can enable your users tooautomatically get signed-on too&frankly (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f1ac5-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="f1ac5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f1ac5-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f1ac5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f1ac5-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f1ac5-110">Prerequisites</span></span>

<span data-ttu-id="f1ac5-111">intégration d’Azure AD tooconfigure avec & franchement, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f1ac5-111">tooconfigure Azure AD integration with &frankly, you need hello following items:</span></span>

- <span data-ttu-id="f1ac5-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1ac5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f1ac5-113">Un abonnement &frankly pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="f1ac5-113">A &frankly single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f1ac5-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f1ac5-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="f1ac5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f1ac5-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f1ac5-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f1ac5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f1ac5-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="f1ac5-118">Scenario description</span></span>
<span data-ttu-id="f1ac5-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f1ac5-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="f1ac5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f1ac5-121">Ajout & franchement à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="f1ac5-121">Adding &frankly from hello gallery</span></span>
2. <span data-ttu-id="f1ac5-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1ac5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-frankly-from-hello-gallery"></a><span data-ttu-id="f1ac5-123">Ajout & franchement à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="f1ac5-123">Adding &frankly from hello gallery</span></span>
<span data-ttu-id="f1ac5-124">intégration de hello tooconfigure & franchement dans Azure AD, vous devez tooadd & franchement à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-124">tooconfigure hello integration of &frankly into Azure AD, you need tooadd &frankly from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f1ac5-125">**tooadd & franchement à partir de la galerie hello, effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f1ac5-125">**tooadd &frankly from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1ac5-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f1ac5-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f1ac5-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="f1ac5-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="f1ac5-133">Dans la zone de recherche de hello, tapez **& franchement**.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-133">In hello search box, type **&frankly**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_search.png)

5. <span data-ttu-id="f1ac5-135">Dans le volet de résultats hello, sélectionnez **& franchement**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-135">In hello results panel, select **&frankly**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f1ac5-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1ac5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f1ac5-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec &frankly, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="f1ac5-138">In this section, you configure and test Azure AD single sign-on with &frankly based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f1ac5-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel hello utilisateur équivalent dans & franchement est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in &frankly is tooa user in Azure AD.</span></span> <span data-ttu-id="f1ac5-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et utilisateur hello dans & franchement toobe besoins établie.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-140">In other words, a link relationship between an Azure AD user and hello related user in &frankly needs toobe established.</span></span>

<span data-ttu-id="f1ac5-141">Dans le & franchement, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-141">In &frankly, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f1ac5-142">tooconfigure et Azure AD l’authentification unique avec & test franchement, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="f1ac5-142">tooconfigure and test Azure AD single sign-on with &frankly, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f1ac5-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f1ac5-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f1ac5-145">**[Créer un & franchement utilisateur test](#creating-a-frankly-test-user)**  -toohave un équivalent de Britta Simon dans & franchement qui est lié toohello la représentation sous forme de Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-145">**[Creating a &frankly test user](#creating-a-frankly-test-user)** - toohave a counterpart of Britta Simon in &frankly that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f1ac5-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f1ac5-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f1ac5-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1ac5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f1ac5-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurer l’authentification unique dans votre & franchement application.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your &frankly application.</span></span>

<span data-ttu-id="f1ac5-150">**tooconfigure Azure AD unique authentification avec & franchement, effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f1ac5-150">**tooconfigure Azure AD single sign-on with &frankly, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1ac5-151">Bonjour portail Azure, sur hello **& franchement** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-151">In hello Azure portal, on hello **&frankly** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="f1ac5-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_samlbase.png)

3. <span data-ttu-id="f1ac5-155">Sur hello **& franchement domaine et les URL** section, si vous le souhaitez application hello tooconfigure **IDP** en mode initié par :</span><span class="sxs-lookup"><span data-stu-id="f1ac5-155">On hello **&frankly Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_url.png)

    <span data-ttu-id="f1ac5-157">a.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-157">a.</span></span> <span data-ttu-id="f1ac5-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/metadata.php/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="f1ac5-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/metadata.php/<tenant id>`</span></span>

    <span data-ttu-id="f1ac5-159">b.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-159">b.</span></span> <span data-ttu-id="f1ac5-160">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/saml2-acs.php/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="f1ac5-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/saml2-acs.php/<tenant id>`</span></span>

4. <span data-ttu-id="f1ac5-161">Cliquez sur **Afficher les paramètres d’URL avancés**.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="f1ac5-162">Si vous le souhaitez application hello tooconfigure **SP** en mode initié par :</span><span class="sxs-lookup"><span data-stu-id="f1ac5-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_url1.png)

    <span data-ttu-id="f1ac5-164">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://andfrankly.com/saml/okta/?saml_sso=<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="f1ac5-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://andfrankly.com/saml/okta/?saml_sso=<tenant id>`</span></span>
    > [!NOTE] 
    > <span data-ttu-id="f1ac5-165">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-165">These values are not real.</span></span> <span data-ttu-id="f1ac5-166">Mettre à jour ces valeurs avec hello identificateur réel, l’authentification et l’URL de réponse.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-166">Update these values with hello actual Identifier, Sign-on, and Reply URL.</span></span> <span data-ttu-id="f1ac5-167">Contact [équipe de support andfrankly](mailto:help@andfrankly.com) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-167">Contact [andfrankly support team](mailto:help@andfrankly.com) tooget these values.</span></span>

5. <span data-ttu-id="f1ac5-168">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_certificate.png) 

6. <span data-ttu-id="f1ac5-170">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="f1ac5-170">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-andfrankly-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="f1ac5-172">tooconfigure l’authentification unique sur **& franchement** côté, vous devez hello toosend téléchargé **Metadata XML** trop[équipe de support andfrankly](mailto:help@andfrankly.com).</span><span class="sxs-lookup"><span data-stu-id="f1ac5-172">tooconfigure single sign-on on **&frankly** side, you need toosend hello downloaded **Metadata XML** too[andfrankly support team](mailto:help@andfrankly.com).</span></span> 

> [!TIP]
> <span data-ttu-id="f1ac5-173">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="f1ac5-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f1ac5-174">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f1ac5-175">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f1ac5-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f1ac5-176">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1ac5-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="f1ac5-177">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="f1ac5-179">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f1ac5-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1ac5-180">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f1ac5-182">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f1ac5-184">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f1ac5-186">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f1ac5-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f1ac5-188">a.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-188">a.</span></span> <span data-ttu-id="f1ac5-189">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f1ac5-190">b.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-190">b.</span></span> <span data-ttu-id="f1ac5-191">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f1ac5-192">c.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-192">c.</span></span> <span data-ttu-id="f1ac5-193">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f1ac5-194">d.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-194">d.</span></span> <span data-ttu-id="f1ac5-195">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-195">Click **Create**.</span></span>
 
### <a name="creating-a-frankly-test-user"></a><span data-ttu-id="f1ac5-196">Création d’un utilisateur de test dans &frankly</span><span class="sxs-lookup"><span data-stu-id="f1ac5-196">Creating a &frankly test user</span></span>

<span data-ttu-id="f1ac5-197">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans &frankly.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-197">In this section, you create a user called Britta Simon in &frankly.</span></span> <span data-ttu-id="f1ac5-198">Travailler avec [équipe de support andfrankly](mailto:help@andfrankly.com) utilisateurs hello tooadd hello & franchement platform.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-198">Work with  [andfrankly support team](mailto:help@andfrankly.com) tooadd hello users in hello &frankly platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f1ac5-199">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1ac5-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f1ac5-200">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès trop & franchement.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too&frankly.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="f1ac5-202">**tooassign Britta Simon trop & franchement, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f1ac5-202">**tooassign Britta Simon too&frankly, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1ac5-203">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="f1ac5-205">Dans la liste des applications hello, sélectionnez **& franchement**.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-205">In hello applications list, select **&frankly**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_app.png) 

3. <span data-ttu-id="f1ac5-207">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="f1ac5-209">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-209">Click **Add** button.</span></span> <span data-ttu-id="f1ac5-210">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="f1ac5-212">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f1ac5-213">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f1ac5-214">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f1ac5-215">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="f1ac5-215">Testing single sign-on</span></span>

<span data-ttu-id="f1ac5-216">objectif Hello de cette section est tootest votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="f1ac5-216">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="f1ac5-217">Lorsque vous cliquez sur hello & franchement vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour & franchement application</span><span class="sxs-lookup"><span data-stu-id="f1ac5-217">When you click hello &frankly tile in hello Access Panel, you should get automatically signed-on tooyour &frankly application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f1ac5-218">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="f1ac5-218">Additional resources</span></span>

* [<span data-ttu-id="f1ac5-219">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f1ac5-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f1ac5-220">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="f1ac5-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_203.png

