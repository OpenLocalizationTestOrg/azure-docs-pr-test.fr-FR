---
title: "Didacticiel : Intégration d’Azure Active Directory à Fuze | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et AUTODESTRUCTEUR de fusée."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9780b4bf-1fd1-48c1-9ceb-f750225ae08a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeedes
ms.openlocfilehash: d0ea8c6456824e348301ed8bf1f5e00f4bfa8121
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fuze"></a><span data-ttu-id="831b5-103">Didacticiel : Intégration d’Azure Active Directory avec Fuze</span><span class="sxs-lookup"><span data-stu-id="831b5-103">Tutorial: Azure Active Directory integration with Fuze</span></span>

<span data-ttu-id="831b5-104">Dans ce didacticiel, vous apprendrez comment toointegrate AUTODESTRUCTEUR de fusée avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="831b5-104">In this tutorial, you learn how toointegrate Fuze with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="831b5-105">Intégration AUTODESTRUCTEUR de fusée à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="831b5-105">Integrating Fuze with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="831b5-106">Vous pouvez contrôler dans Azure AD qui a accès tooFuze</span><span class="sxs-lookup"><span data-stu-id="831b5-106">You can control in Azure AD who has access tooFuze</span></span>
- <span data-ttu-id="831b5-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooFuze (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="831b5-107">You can enable your users tooautomatically get signed-on tooFuze (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="831b5-108">Vous pouvez gérer vos comptes dans un emplacement central - portail de gestion Azure hello</span><span class="sxs-lookup"><span data-stu-id="831b5-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="831b5-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="831b5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="831b5-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="831b5-110">Prerequisites</span></span>

<span data-ttu-id="831b5-111">tooconfigure intégration d’Azure AD avec AUTODESTRUCTEUR de fusée, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="831b5-111">tooconfigure Azure AD integration with Fuze, you need hello following items:</span></span>

- <span data-ttu-id="831b5-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="831b5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="831b5-113">Un abonnement Fuze pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="831b5-113">A Fuze single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="831b5-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="831b5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="831b5-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="831b5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="831b5-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="831b5-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="831b5-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="831b5-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="831b5-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="831b5-118">Scenario description</span></span>
<span data-ttu-id="831b5-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="831b5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="831b5-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="831b5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="831b5-121">Ajout d’AUTODESTRUCTEUR de fusée à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="831b5-121">Adding Fuze from hello gallery</span></span>
2. <span data-ttu-id="831b5-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="831b5-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-fuze-from-hello-gallery"></a><span data-ttu-id="831b5-123">Ajout d’AUTODESTRUCTEUR de fusée à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="831b5-123">Adding Fuze from hello gallery</span></span>
<span data-ttu-id="831b5-124">intégration de hello tooconfigure d’AUTODESTRUCTEUR de fusée dans Azure AD, vous devez tooadd AUTODESTRUCTEUR de fusée à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="831b5-124">tooconfigure hello integration of Fuze into Azure AD, you need tooadd Fuze from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="831b5-125">**tooadd AUTODESTRUCTEUR de fusée à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="831b5-125">**tooadd Fuze from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="831b5-126">Bonjour  **[portail de gestion Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="831b5-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="831b5-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="831b5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="831b5-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="831b5-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="831b5-131">Cliquez sur **ajouter** bouton en haut de hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="831b5-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="831b5-133">Dans la zone de recherche de hello, tapez **AUTODESTRUCTEUR de fusée**.</span><span class="sxs-lookup"><span data-stu-id="831b5-133">In hello search box, type **Fuze**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_000.png)

5. <span data-ttu-id="831b5-135">Dans le volet de résultats hello, sélectionnez **AUTODESTRUCTEUR de fusée**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="831b5-135">In hello results panel, select **Fuze**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="831b5-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="831b5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="831b5-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Fuze avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="831b5-138">In this section, you configure and test Azure AD single sign-on with Fuze based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="831b5-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans AUTODESTRUCTEUR de fusée est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="831b5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Fuze is tooa user in Azure AD.</span></span> <span data-ttu-id="831b5-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans AUTODESTRUCTEUR de fusée doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="831b5-140">In other words, a link relationship between an Azure AD user and hello related user in Fuze needs toobe established.</span></span>

<span data-ttu-id="831b5-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans AUTODESTRUCTEUR de fusée.</span><span class="sxs-lookup"><span data-stu-id="831b5-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Fuze.</span></span>

<span data-ttu-id="831b5-142">tooconfigure et test Azure AD l’authentification unique avec AUTODESTRUCTEUR de fusée, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="831b5-142">tooconfigure and test Azure AD single sign-on with Fuze, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="831b5-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="831b5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="831b5-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="831b5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="831b5-145">**[Création d’un utilisateur de test AUTODESTRUCTEUR de fusée](#creating-a-fuze-test-user)**  -toohave de Britta Simon dans AUTODESTRUCTEUR de fusée qui est la représentation sous forme de toohello lié Azure AD de sa contrepartie.</span><span class="sxs-lookup"><span data-stu-id="831b5-145">**[Creating a Fuze test user](#creating-a-fuze-test-user)** - toohave a counterpart of Britta Simon in Fuze that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="831b5-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="831b5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="831b5-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="831b5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="831b5-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="831b5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="831b5-149">Dans cette section, vous activez Azure AD l’authentification unique dans le portail de gestion Azure hello et configurez l’authentification unique dans votre application AUTODESTRUCTEUR de fusée.</span><span class="sxs-lookup"><span data-stu-id="831b5-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Fuze application.</span></span>

<span data-ttu-id="831b5-150">**tooconfigure Azure AD single sign-on avec AUTODESTRUCTEUR de fusée, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="831b5-150">**tooconfigure Azure AD single sign-on with Fuze, perform hello following steps:**</span></span>

1. <span data-ttu-id="831b5-151">Dans le portail de gestion Azure hello, sur hello **AUTODESTRUCTEUR de fusée** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="831b5-151">In hello Azure Management portal, on hello **Fuze** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="831b5-153">Sur hello **l’authentification unique** boîte de dialogue, en tant que **Mode** sélectionnez **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="831b5-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_01.png)

3. <span data-ttu-id="831b5-155">Sur hello **AUTODESTRUCTEUR de fusée domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="831b5-155">On hello **Fuze Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_020.png)
    
    <span data-ttu-id="831b5-157">Bonjour **URL de connexion** zone de texte, tapez l’URL hello ouverture de session en tant que :`https://www.thinkingphones.com/jetspeed/portal/`</span><span class="sxs-lookup"><span data-stu-id="831b5-157">In hello **Sign on URL** textbox, type hello Sign-on URL as: `https://www.thinkingphones.com/jetspeed/portal/`</span></span>

4.  <span data-ttu-id="831b5-158">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="831b5-158">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-fuze-tutorial/tutorial_general_400.png)

5. <span data-ttu-id="831b5-160">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier xml de hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="831b5-160">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello xml file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_05.png) 

6. <span data-ttu-id="831b5-162">tooconfigure l’authentification unique sur **AUTODESTRUCTEUR de fusée** côté, vous devez hello toosend téléchargé **Metadata XML** trop[équipe de support AUTODESTRUCTEUR de fusée](https://www.fuze.com/support).</span><span class="sxs-lookup"><span data-stu-id="831b5-162">tooconfigure single sign-on on **Fuze** side, you need toosend hello downloaded **Metadata XML** too[Fuze support team](https://www.fuze.com/support).</span></span> <span data-ttu-id="831b5-163">Ils seront configurer Bonjour de toohave commande connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="831b5-163">They will set this up in order toohave hello SAML SSO connection set properly on both sides.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="831b5-164">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="831b5-164">Creating an Azure AD test user</span></span>
<span data-ttu-id="831b5-165">objectif Hello de cette section est toocreate un utilisateur de test dans le portail de gestion Azure hello appelé Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="831b5-165">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="831b5-167">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="831b5-167">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="831b5-168">Bonjour **portail de gestion Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="831b5-168">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-fuze-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="831b5-170">Accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs** liste de hello toodisplay des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="831b5-170">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-fuze-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="831b5-172">En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="831b5-172">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-fuze-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="831b5-174">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="831b5-174">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-fuze-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="831b5-176">a.</span><span class="sxs-lookup"><span data-stu-id="831b5-176">a.</span></span> <span data-ttu-id="831b5-177">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="831b5-177">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="831b5-178">b.</span><span class="sxs-lookup"><span data-stu-id="831b5-178">b.</span></span> <span data-ttu-id="831b5-179">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="831b5-179">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="831b5-180">c.</span><span class="sxs-lookup"><span data-stu-id="831b5-180">c.</span></span> <span data-ttu-id="831b5-181">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="831b5-181">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="831b5-182">d.</span><span class="sxs-lookup"><span data-stu-id="831b5-182">d.</span></span> <span data-ttu-id="831b5-183">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="831b5-183">Click **Create**.</span></span> 


### <a name="creating-a-fuze-test-user"></a><span data-ttu-id="831b5-184">Création d’un utilisateur de test Fuze</span><span class="sxs-lookup"><span data-stu-id="831b5-184">Creating a Fuze test user</span></span>

<span data-ttu-id="831b5-185">L’application Fuze prend en charge la configuration juste-à-temps complète. Ainsi, les utilisateurs sont créés automatiquement lors de leur connexion.</span><span class="sxs-lookup"><span data-stu-id="831b5-185">Fuze application supports full Just in time user provision, so users will get created automatically when they sign-in.</span></span> <span data-ttu-id="831b5-186">Pour toute autre précision, contactez le [support technique](https://www.fuze.com/support) de Fuze.</span><span class="sxs-lookup"><span data-stu-id="831b5-186">For any other clarification, please contact Fuze [support](https://www.fuze.com/support).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="831b5-187">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="831b5-187">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="831b5-188">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant tooFuze de son accès.</span><span class="sxs-lookup"><span data-stu-id="831b5-188">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooFuze.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="831b5-190">**tooassign Britta Simon tooFuze, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="831b5-190">**tooassign Britta Simon tooFuze, perform hello following steps:**</span></span>

1. <span data-ttu-id="831b5-191">Dans le portail de gestion Azure hello, ouvrez la vue des applications hello, puis naviguez toohello les vue de répertoire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="831b5-191">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="831b5-193">Dans la liste des applications hello, sélectionnez **AUTODESTRUCTEUR de fusée**.</span><span class="sxs-lookup"><span data-stu-id="831b5-193">In hello applications list, select **Fuze**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_50.png) 

3. <span data-ttu-id="831b5-195">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="831b5-195">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="831b5-197">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="831b5-197">Click **Add** button.</span></span> <span data-ttu-id="831b5-198">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="831b5-198">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="831b5-200">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="831b5-200">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="831b5-201">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="831b5-201">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="831b5-202">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="831b5-202">Click **Assign** button on **Add Assignment** dialog.</span></span>
    

### <a name="testing-single-sign-on"></a><span data-ttu-id="831b5-203">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="831b5-203">Testing single sign-on</span></span>

<span data-ttu-id="831b5-204">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="831b5-204">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="831b5-205">Lorsque vous cliquez sur mosaïque AUTODESTRUCTEUR de fusée hello hello volet d’accès, vous devez obtenir l’application d’AUTODESTRUCTEUR de fusée automatiquement signé sur tooyour.</span><span class="sxs-lookup"><span data-stu-id="831b5-205">When you click hello Fuze tile in hello Access Panel, you should get automatically signed-on tooyour Fuze application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="831b5-206">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="831b5-206">Additional resources</span></span>

* [<span data-ttu-id="831b5-207">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="831b5-207">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="831b5-208">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="831b5-208">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_203.png