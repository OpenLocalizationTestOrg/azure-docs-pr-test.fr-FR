---
title: "Didacticiel : Intégration d’Azure Active Directory à Land Gorilla Client | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et terrestres Gorilla."
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
ms.date: 03/13/2017
ms.author: jeedes
ms.openlocfilehash: e95a30551e636108fe22a7ab6d1827bc12d7f9a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-land-gorilla-client"></a><span data-ttu-id="69670-103">Didacticiel : Intégration d’Azure Active Directory à Land Gorilla Client</span><span class="sxs-lookup"><span data-stu-id="69670-103">Tutorial: Azure Active Directory integration with Land Gorilla Client</span></span>

<span data-ttu-id="69670-104">Dans ce didacticiel, vous apprendrez comment toointegrate Client de Gorilla terrestres avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="69670-104">In this tutorial, you learn how toointegrate Land Gorilla Client with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="69670-105">Intégrant terrestres Gorilla Client Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="69670-105">Integrating Land Gorilla Client with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="69670-106">Vous pouvez contrôler dans Azure AD qui a accès tooLand Gorilla Client</span><span class="sxs-lookup"><span data-stu-id="69670-106">You can control in Azure AD who has access tooLand Gorilla Client</span></span>
- <span data-ttu-id="69670-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooLand Client Gorilla (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="69670-107">You can enable your users tooautomatically get signed-on tooLand Gorilla Client (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="69670-108">Vous pouvez gérer vos comptes dans un emplacement central - portail de gestion Azure hello</span><span class="sxs-lookup"><span data-stu-id="69670-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="69670-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="69670-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="69670-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="69670-110">Prerequisites</span></span>

<span data-ttu-id="69670-111">tooconfigure intégration d’Azure AD avec terres Gorilla Client, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="69670-111">tooconfigure Azure AD integration with Land Gorilla Client, you need hello following items:</span></span>

- <span data-ttu-id="69670-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="69670-112">An Azure AD subscription</span></span>
- <span data-ttu-id="69670-113">Un abonnement Land Gorilla Client pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="69670-113">A Land Gorilla Client single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="69670-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="69670-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="69670-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="69670-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="69670-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="69670-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="69670-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="69670-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="69670-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="69670-118">Scenario description</span></span>
<span data-ttu-id="69670-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="69670-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="69670-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="69670-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="69670-121">Ajout du Client Gorilla terrestres à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="69670-121">Adding Land Gorilla Client from hello gallery</span></span>
2. <span data-ttu-id="69670-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="69670-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-land-gorilla-client-from-hello-gallery"></a><span data-ttu-id="69670-123">Ajout du Client Gorilla terrestres à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="69670-123">Adding Land Gorilla Client from hello gallery</span></span>
<span data-ttu-id="69670-124">tooconfigure hello intégration du Client de Gorilla terrestres dans Azure AD, vous devez le Client de Gorilla tooadd terrestres à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="69670-124">tooconfigure hello integration of Land Gorilla Client into Azure AD, you need tooadd Land Gorilla Client from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="69670-125">**tooadd Client de Gorilla terrestres à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="69670-125">**tooadd Land Gorilla Client from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="69670-126">Bonjour  **[portail de gestion Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="69670-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="69670-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="69670-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="69670-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="69670-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="69670-131">Cliquez sur **ajouter** bouton en haut de hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="69670-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="69670-133">Dans la zone de recherche de hello, tapez **terrestres Gorilla Client**.</span><span class="sxs-lookup"><span data-stu-id="69670-133">In hello search box, type **Land Gorilla Client**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_search.png)

5. <span data-ttu-id="69670-135">Dans le volet de résultats hello, sélectionnez **terrestres Gorilla Client**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="69670-135">In hello results panel, select **Land Gorilla Client**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_addfromgallery.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="69670-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="69670-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="69670-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Land Gorilla Client avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="69670-138">In this section, you configure and test Azure AD single sign-on with Land Gorilla Client based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="69670-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans terrestres Gorilla Client est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="69670-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Land Gorilla Client is tooa user in Azure AD.</span></span> <span data-ttu-id="69670-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans terrestres Gorilla Client doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="69670-140">In other words, a link relationship between an Azure AD user and hello related user in Land Gorilla Client needs toobe established.</span></span>

<span data-ttu-id="69670-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans terrestres Gorilla Client.</span><span class="sxs-lookup"><span data-stu-id="69670-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Land Gorilla Client.</span></span>

<span data-ttu-id="69670-142">tooconfigure et test Azure AD l’authentification unique avec terres Gorilla Client, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="69670-142">tooconfigure and test Azure AD single sign-on with Land Gorilla Client, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="69670-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="69670-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="69670-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec groupe limité.</span><span class="sxs-lookup"><span data-stu-id="69670-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with limited group.</span></span>
3. <span data-ttu-id="69670-145">**[Création d’un utilisateur de test terrestres Gorilla](#creating-a-land-gorilla-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="69670-145">**[Creating a Land Gorilla test user](#creating-a-land-gorilla-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="69670-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="69670-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="69670-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="69670-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="69670-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="69670-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="69670-149">Dans cette section, vous activez Azure AD l’authentification unique dans le portail de gestion Azure hello et configurez l’authentification unique dans votre application cliente de Gorilla terrestres.</span><span class="sxs-lookup"><span data-stu-id="69670-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Land Gorilla Client application.</span></span>

<span data-ttu-id="69670-150">**tooconfigure Azure AD l’authentification unique avec terres Gorilla Client, exécutez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="69670-150">**tooconfigure Azure AD single sign-on with Land Gorilla Client, perform hello following steps:**</span></span>

1. <span data-ttu-id="69670-151">Dans le portail de gestion Azure hello, sur hello **terrestres Gorilla Client** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="69670-151">In hello Azure Management portal, on hello **Land Gorilla Client** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="69670-153">Sur hello **l’authentification unique** boîte de dialogue, en tant que **Mode** sélectionnez **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="69670-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_samlbase.png)

3. <span data-ttu-id="69670-155">Sur hello **URL et domaine de Client Gorilla terrestres** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="69670-155">On hello **Land Gorilla Client Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_url_02.png)

    <span data-ttu-id="69670-157">a.</span><span class="sxs-lookup"><span data-stu-id="69670-157">a.</span></span> <span data-ttu-id="69670-158">Bonjour **identificateur** zone de texte, valeur hello du type à l’aide de hello modèle :</span><span class="sxs-lookup"><span data-stu-id="69670-158">In hello **Identifier** textbox, type hello value using one of hello following pattern:</span></span> 
    
    `https://<customer domain>.landgorilla.com/` 
    
    `https://www.<customer domain>.landgorilla.com`

    <span data-ttu-id="69670-159">b.</span><span class="sxs-lookup"><span data-stu-id="69670-159">b.</span></span> <span data-ttu-id="69670-160">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide d’une des hello modèle :</span><span class="sxs-lookup"><span data-stu-id="69670-160">In hello **Reply URL** textbox, type a URL using one of hello following pattern:</span></span>

    `https://<customer domain>.landgorilla.com/simplesaml/module.php/core/authenticate.php`

    `https://www.<customer domain>.landgorilla.com/simplesaml/module.php/core/authenticate.php`

    `https://<customer domain>.landgorilla.com/simplesaml/module.php/saml/sp/saml2-acs.php/default-sp`
    
    `https://www.<customer domain>.landgorilla.com/simplesaml/module.php/saml/sp/saml2-acs.php/default-sp`

    > [!NOTE] 
    > <span data-ttu-id="69670-161">Notez qu’il s’agit pas des valeurs réelles hello.</span><span class="sxs-lookup"><span data-stu-id="69670-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="69670-162">Vous avez tooupdate ces valeurs avec hello URL d’identificateur et de réponse réelle.</span><span class="sxs-lookup"><span data-stu-id="69670-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="69670-163">Ici, nous vous suggérons vous toouse hello unique valeur de chaîne Bonjour identificateur.</span><span class="sxs-lookup"><span data-stu-id="69670-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="69670-164">Contact [équipe terrestres Gorilla Client](https://www.landgorilla.com/support/) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="69670-164">Contact [Land Gorilla Client team](https://www.landgorilla.com/support/) tooget these values.</span></span> 

4. <span data-ttu-id="69670-165">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier XML de hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="69670-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_certificate.png) 

5. <span data-ttu-id="69670-167">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="69670-167">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-landgorilla-tutorial/tutorial_general_400.png) 

6. <span data-ttu-id="69670-169">configuration de SSO tooget complète pour votre application à fin terrestres Gorilla, contactez [équipe de support Client de Gorilla terrestres](https://www.landgorilla.com/support/) et fournissez-leur hello téléchargé **» Metadata XML** fichier.</span><span class="sxs-lookup"><span data-stu-id="69670-169">tooget SSO configuration complete for your application at Land Gorilla end, Contact [Land Gorilla Client support team](https://www.landgorilla.com/support/) and provide them with hello downloaded **“Metadata XML** file.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="69670-170">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="69670-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="69670-171">objectif Hello de cette section est toocreate un utilisateur de test dans le portail de gestion Azure hello appelé Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="69670-171">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="69670-173">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="69670-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="69670-174">Bonjour **portail de gestion Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="69670-174">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="69670-176">Accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs** liste de hello toodisplay des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="69670-176">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="69670-178">En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="69670-178">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="69670-180">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="69670-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="69670-182">a.</span><span class="sxs-lookup"><span data-stu-id="69670-182">a.</span></span> <span data-ttu-id="69670-183">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="69670-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="69670-184">b.</span><span class="sxs-lookup"><span data-stu-id="69670-184">b.</span></span> <span data-ttu-id="69670-185">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="69670-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="69670-186">c.</span><span class="sxs-lookup"><span data-stu-id="69670-186">c.</span></span> <span data-ttu-id="69670-187">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="69670-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="69670-188">d.</span><span class="sxs-lookup"><span data-stu-id="69670-188">d.</span></span> <span data-ttu-id="69670-189">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="69670-189">Click **Create**.</span></span> 

### <a name="creating-a-land-gorilla-test-user"></a><span data-ttu-id="69670-190">Création d’un utilisateur de test Land Gorilla</span><span class="sxs-lookup"><span data-stu-id="69670-190">Creating a Land Gorilla test user</span></span>

<span data-ttu-id="69670-191">Collaborez avec [équipe de support terrestres Gorilla](https://www.landgorilla.com/support/) tooadd les utilisateurs de hello dans la plateforme de terrains Gorilla hello.</span><span class="sxs-lookup"><span data-stu-id="69670-191">Please work with [Land Gorilla support team](https://www.landgorilla.com/support/) tooadd hello users in hello Land Gorilla platform.</span></span>
    
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="69670-192">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="69670-192">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="69670-193">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant son tooLand accès Gorilla Client.</span><span class="sxs-lookup"><span data-stu-id="69670-193">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooLand Gorilla Client.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="69670-195">**tooassign Britta Simon tooLand Gorilla Client, exécutez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="69670-195">**tooassign Britta Simon tooLand Gorilla Client, perform hello following steps:**</span></span>

1. <span data-ttu-id="69670-196">Dans le portail de gestion Azure hello, ouvrez la vue des applications hello, puis naviguez toohello les vue de répertoire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="69670-196">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="69670-198">Dans la liste des applications hello, sélectionnez **terrestres Gorilla Client**.</span><span class="sxs-lookup"><span data-stu-id="69670-198">In hello applications list, select **Land Gorilla Client**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_app.png) 

3. <span data-ttu-id="69670-200">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="69670-200">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="69670-202">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="69670-202">Click **Add** button.</span></span> <span data-ttu-id="69670-203">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="69670-203">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="69670-205">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="69670-205">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="69670-206">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="69670-206">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="69670-207">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="69670-207">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="69670-208">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="69670-208">Testing single sign-on</span></span>

<span data-ttu-id="69670-209">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="69670-209">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="69670-210">Lorsque vous cliquez sur mosaïque terrestres Gorilla Client hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour application terrestres Gorilla cliente.</span><span class="sxs-lookup"><span data-stu-id="69670-210">When you click hello Land Gorilla Client tile in hello Access Panel, you should get automatically signed-on tooyour Land Gorilla Client application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="69670-211">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="69670-211">Additional resources</span></span>

* [<span data-ttu-id="69670-212">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="69670-212">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="69670-213">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="69670-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_203.png
