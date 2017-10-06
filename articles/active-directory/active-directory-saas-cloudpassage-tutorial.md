---
title: "Didacticiel : Intégration d’Azure Active Directory avec CloudPassage | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et CloudPassage."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bfe1f14e-74e4-4680-ac9e-f7355e1c94cc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 32fb007b90f071626c9b40fb5afc341dd3c1ae99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cloudpassage"></a><span data-ttu-id="5b112-103">Didacticiel : Intégration d’Azure Active Directory avec CloudPassage</span><span class="sxs-lookup"><span data-stu-id="5b112-103">Tutorial: Azure Active Directory integration with CloudPassage</span></span>

<span data-ttu-id="5b112-104">Dans ce didacticiel, vous apprendrez comment toointegrate CloudPassage avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5b112-104">In this tutorial, you learn how toointegrate CloudPassage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5b112-105">Intégration CloudPassage à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="5b112-105">Integrating CloudPassage with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5b112-106">Vous pouvez contrôler dans Azure AD qui a accès tooCloudPassage</span><span class="sxs-lookup"><span data-stu-id="5b112-106">You can control in Azure AD who has access tooCloudPassage</span></span>
- <span data-ttu-id="5b112-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooCloudPassage (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b112-107">You can enable your users tooautomatically get signed-on tooCloudPassage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5b112-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="5b112-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5b112-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5b112-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b112-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="5b112-110">Prerequisites</span></span>

<span data-ttu-id="5b112-111">tooconfigure intégration d’Azure AD avec CloudPassage, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="5b112-111">tooconfigure Azure AD integration with CloudPassage, you need hello following items:</span></span>

- <span data-ttu-id="5b112-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b112-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5b112-113">Un abonnement CloudPassage pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="5b112-113">A CloudPassage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5b112-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="5b112-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5b112-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="5b112-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5b112-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="5b112-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5b112-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5b112-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5b112-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="5b112-118">Scenario description</span></span>
<span data-ttu-id="5b112-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="5b112-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5b112-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="5b112-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5b112-121">Ajout de CloudPassage à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="5b112-121">Adding CloudPassage from hello gallery</span></span>
2. <span data-ttu-id="5b112-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b112-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cloudpassage-from-hello-gallery"></a><span data-ttu-id="5b112-123">Ajout de CloudPassage à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="5b112-123">Adding CloudPassage from hello gallery</span></span>
<span data-ttu-id="5b112-124">intégration de hello tooconfigure de CloudPassage dans Azure AD, vous devez tooadd CloudPassage à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="5b112-124">tooconfigure hello integration of CloudPassage into Azure AD, you need tooadd CloudPassage from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5b112-125">**tooadd CloudPassage à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5b112-125">**tooadd CloudPassage from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b112-126">Bonjour ** [portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="5b112-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5b112-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="5b112-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5b112-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5b112-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="5b112-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="5b112-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="5b112-133">Dans la zone de recherche de hello, tapez **CloudPassage**.</span><span class="sxs-lookup"><span data-stu-id="5b112-133">In hello search box, type **CloudPassage**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_search.png)

5. <span data-ttu-id="5b112-135">Dans le volet de résultats hello, sélectionnez **CloudPassage**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="5b112-135">In hello results panel, select **CloudPassage**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5b112-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b112-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5b112-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec CloudPassage avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="5b112-138">In this section, you configure and test Azure AD single sign-on with CloudPassage based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5b112-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans CloudPassage est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5b112-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in CloudPassage is tooa user in Azure AD.</span></span> <span data-ttu-id="5b112-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans CloudPassage doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="5b112-140">In other words, a link relationship between an Azure AD user and hello related user in CloudPassage needs toobe established.</span></span>

<span data-ttu-id="5b112-141">Dans CloudPassage, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="5b112-141">In CloudPassage, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5b112-142">tooconfigure et test Azure AD l’authentification unique avec CloudPassage, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="5b112-142">tooconfigure and test Azure AD single sign-on with CloudPassage, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5b112-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="5b112-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5b112-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user) ** -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5b112-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5b112-145">**[Création d’un utilisateur de test CloudPassage](#creating-a-cloudpassage-test-user) ** -toohave un équivalent de Britta Simon dans CloudPassage est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5b112-145">**[Creating a CloudPassage test user](#creating-a-cloudpassage-test-user)** - toohave a counterpart of Britta Simon in CloudPassage that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5b112-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5b112-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5b112-147">**[Test de l’authentification unique sur](#testing-single-sign-on) ** -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="5b112-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5b112-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b112-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5b112-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="5b112-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your CloudPassage application.</span></span>

<span data-ttu-id="5b112-150">**tooconfigure Azure AD single sign-on avec CloudPassage, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5b112-150">**tooconfigure Azure AD single sign-on with CloudPassage, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b112-151">Bonjour portail Azure, sur hello **CloudPassage** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="5b112-151">In hello Azure portal, on hello **CloudPassage** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="5b112-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5b112-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_samlbase.png)

3. <span data-ttu-id="5b112-155">Sur hello **CloudPassage domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5b112-155">On hello **CloudPassage Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_url.png)

    <span data-ttu-id="5b112-157">a.</span><span class="sxs-lookup"><span data-stu-id="5b112-157">a.</span></span> <span data-ttu-id="5b112-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://portal.cloudpassage.com/saml/init/accountid`</span><span class="sxs-lookup"><span data-stu-id="5b112-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://portal.cloudpassage.com/saml/init/accountid`</span></span>

    <span data-ttu-id="5b112-159">b.</span><span class="sxs-lookup"><span data-stu-id="5b112-159">b.</span></span> <span data-ttu-id="5b112-160">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle : `https://portal.cloudpassage.com/saml/consume/accountid`.</span><span class="sxs-lookup"><span data-stu-id="5b112-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://portal.cloudpassage.com/saml/consume/accountid`.</span></span> <span data-ttu-id="5b112-161">Vous pouvez obtenir la valeur de cet attribut en cliquant sur **documentation d’installation de l’authentification unique** Bonjour **paramètres d’authentification unique** section de votre portail CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="5b112-161">You can get your value for this attribute by clicking **SSO Setup documentation** in hello **Single Sign-on Settings** section of your CloudPassage portal.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_05.png)
     
    > [!NOTE] 
    > <span data-ttu-id="5b112-163">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="5b112-163">These values are not real.</span></span> <span data-ttu-id="5b112-164">Mettre à jour ces valeurs avec l’URL de réponse réelle hello et URL de connexion.</span><span class="sxs-lookup"><span data-stu-id="5b112-164">Update these values with hello actual Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="5b112-165">Contact [équipe de support Client de CloudPassage](https://www.cloudpassage.com/company/contact/) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="5b112-165">Contact [CloudPassage Client support team](https://www.cloudpassage.com/company/contact/) tooget these values.</span></span> 

4. <span data-ttu-id="5b112-166">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="5b112-166">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_certificate.png) 

5. <span data-ttu-id="5b112-168">Votre application CloudPassage attend les assertions SAML hello dans un format spécifique, ce qui nécessite vous tooadd attribut personnalisé tooyour SAML attributs du jeton configuration des mappages.</span><span class="sxs-lookup"><span data-stu-id="5b112-168">Your CloudPassage application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span>   
<span data-ttu-id="5b112-169">Hello suivant capture d’écran montre un exemple de cela.</span><span class="sxs-lookup"><span data-stu-id="5b112-169">hello following screenshot shows an example for this.</span></span>
   
   ![Configurer l’authentification unique](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_25.png) 

6. <span data-ttu-id="5b112-171">Bonjour **attributs utilisateur** section hello **l’authentification unique** boîte de dialogue, configurer des attributs de jeton SAML comme indiqué dans l’image ci-dessus hello et effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5b112-171">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>

    | <span data-ttu-id="5b112-172">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="5b112-172">Attribute Name</span></span> | <span data-ttu-id="5b112-173">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="5b112-173">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="5b112-174">firstname</span><span class="sxs-lookup"><span data-stu-id="5b112-174">firstname</span></span> |<span data-ttu-id="5b112-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="5b112-175">user.givenname</span></span> |
    | <span data-ttu-id="5b112-176">lastname</span><span class="sxs-lookup"><span data-stu-id="5b112-176">lastname</span></span> |<span data-ttu-id="5b112-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="5b112-177">user.surname</span></span> |
    | <span data-ttu-id="5b112-178">email</span><span class="sxs-lookup"><span data-stu-id="5b112-178">email</span></span> |<span data-ttu-id="5b112-179">user.mail</span><span class="sxs-lookup"><span data-stu-id="5b112-179">user.mail</span></span> |
    
    <span data-ttu-id="5b112-180">a.</span><span class="sxs-lookup"><span data-stu-id="5b112-180">a.</span></span> <span data-ttu-id="5b112-181">Cliquez sur **ajouter un attribut** tooopen hello **ajouter un attribut** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="5b112-181">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cloudpassage-tutorial/tutorial_attribute_04.png)
    
    ![Configurer l’authentification unique](./media/active-directory-saas-cloudpassage-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="5b112-184">b.</span><span class="sxs-lookup"><span data-stu-id="5b112-184">b.</span></span> <span data-ttu-id="5b112-185">Bonjour **nom** zone de texte, nom d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="5b112-185">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="5b112-186">c.</span><span class="sxs-lookup"><span data-stu-id="5b112-186">c.</span></span> <span data-ttu-id="5b112-187">À partir de hello **valeur** liste, la valeur d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="5b112-187">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="5b112-188">d.</span><span class="sxs-lookup"><span data-stu-id="5b112-188">d.</span></span> <span data-ttu-id="5b112-189">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="5b112-189">Click **Ok**.</span></span>

7. <span data-ttu-id="5b112-190">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="5b112-190">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="5b112-192">Sur hello **CloudPassage Configuration** , cliquez sur **CloudPassage de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="5b112-192">On hello **CloudPassage Configuration** section, click **Configure CloudPassage** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5b112-193">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="5b112-193">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_configure.png) 

9. <span data-ttu-id="5b112-195">Dans une autre fenêtre de navigateur, site d’entreprise CloudPassage tooyour ouverture de session en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="5b112-195">In a different browser window, sign-on tooyour CloudPassage company site as administrator.</span></span>

10. <span data-ttu-id="5b112-196">Dans le menu hello haut de hello, cliquez sur **paramètres**, puis cliquez sur **Site Administration**.</span><span class="sxs-lookup"><span data-stu-id="5b112-196">In hello menu on hello top, click **Settings**, and then click **Site Administration**.</span></span> 
   
    ![Configurer l’authentification unique][12]

11. <span data-ttu-id="5b112-198">Cliquez sur hello **les paramètres d’authentification** onglet.</span><span class="sxs-lookup"><span data-stu-id="5b112-198">Click hello **Authentication Settings** tab.</span></span> 
   
    ![Configurer l’authentification unique][13]

12. <span data-ttu-id="5b112-200">Bonjour **paramètres d’authentification unique** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5b112-200">In hello **Single Sign-on Settings** section, perform hello following steps:</span></span> 
   
    ![Configurer l’authentification unique][14]

    <span data-ttu-id="5b112-202">a.</span><span class="sxs-lookup"><span data-stu-id="5b112-202">a.</span></span> <span data-ttu-id="5b112-203">Cochez la case **Activer l’authentification unique (SSO) (Documentation de configuration de l’authentification unique)**.</span><span class="sxs-lookup"><span data-stu-id="5b112-203">Select **Enable Single sign-on(SSO)(SSO Setup Documentation)** checkbox.</span></span>
    
    <span data-ttu-id="5b112-204">b.</span><span class="sxs-lookup"><span data-stu-id="5b112-204">b.</span></span> <span data-ttu-id="5b112-205">Coller **ID d’entité SAML** dans hello **URL de l’émetteur SAML** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="5b112-205">Paste **SAML Entity ID** into hello **SAML issuer URL** textbox.</span></span>
  
    <span data-ttu-id="5b112-206">c.</span><span class="sxs-lookup"><span data-stu-id="5b112-206">c.</span></span> <span data-ttu-id="5b112-207">Coller **SAML Sign-On URL du Service unique** dans hello **URL de point de terminaison SAML** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="5b112-207">Paste **SAML Single Sign-On Service URL** into hello **SAML endpoint URL** textbox.</span></span>
  
    <span data-ttu-id="5b112-208">d.</span><span class="sxs-lookup"><span data-stu-id="5b112-208">d.</span></span> <span data-ttu-id="5b112-209">Coller **URL de déconnexion** dans hello **page d’accueil de déconnexion** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="5b112-209">Paste **Sign-Out URL** into hello **Logout landing page** textbox.</span></span>
  
    <span data-ttu-id="5b112-210">e.</span><span class="sxs-lookup"><span data-stu-id="5b112-210">e.</span></span> <span data-ttu-id="5b112-211">Ouvrez votre certificat téléchargé dans le bloc-notes, hello copie le contenu des certificats téléchargés dans le Presse-papiers et le coller ensuite dans hello **certificat x 509** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="5b112-211">Open your downloaded certificate in notepad, copy hello content of downloaded certificate into your clipboard, and then paste it into hello **x 509 certificate** textbox.</span></span>
  
    <span data-ttu-id="5b112-212">f.</span><span class="sxs-lookup"><span data-stu-id="5b112-212">f.</span></span> <span data-ttu-id="5b112-213">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="5b112-213">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="5b112-214">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="5b112-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5b112-215">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello ** Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="5b112-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5b112-216">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5b112-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5b112-217">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b112-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="5b112-218">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="5b112-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="5b112-220">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5b112-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b112-221">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="5b112-221">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5b112-223">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="5b112-223">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5b112-225">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="5b112-225">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5b112-227">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5b112-227">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5b112-229">a.</span><span class="sxs-lookup"><span data-stu-id="5b112-229">a.</span></span> <span data-ttu-id="5b112-230">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5b112-230">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5b112-231">b.</span><span class="sxs-lookup"><span data-stu-id="5b112-231">b.</span></span> <span data-ttu-id="5b112-232">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5b112-232">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5b112-233">c.</span><span class="sxs-lookup"><span data-stu-id="5b112-233">c.</span></span> <span data-ttu-id="5b112-234">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="5b112-234">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5b112-235">d.</span><span class="sxs-lookup"><span data-stu-id="5b112-235">d.</span></span> <span data-ttu-id="5b112-236">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="5b112-236">Click **Create**.</span></span>
 
### <a name="creating-a-cloudpassage-test-user"></a><span data-ttu-id="5b112-237">Création d’un utilisateur de test CloudPassage</span><span class="sxs-lookup"><span data-stu-id="5b112-237">Creating a CloudPassage test user</span></span>

<span data-ttu-id="5b112-238">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="5b112-238">hello objective of this section is toocreate a user called Britta Simon in CloudPassage.</span></span>

<span data-ttu-id="5b112-239">**toocreate un utilisateur appelé Britta Simon dans CloudPassage, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5b112-239">**toocreate a user called Britta Simon in CloudPassage, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b112-240">Authentification tooyour **CloudPassage** site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="5b112-240">Sign-on tooyour **CloudPassage** company site as an administrator.</span></span> 

2. <span data-ttu-id="5b112-241">Dans la barre d’outils de hello en haut de hello, cliquez sur **paramètres**, puis cliquez sur **Site Administration**.</span><span class="sxs-lookup"><span data-stu-id="5b112-241">In hello toolbar on hello top, click **Settings**, and then click **Site Administration**.</span></span> 
   
   ![Création d’un utilisateur de test CloudPassage][22] 

3. <span data-ttu-id="5b112-243">Cliquez sur hello **utilisateurs** onglet, puis cliquez sur **ajouter un nouvel utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="5b112-243">Click hello **Users** tab, and then click **Add New User**.</span></span> 
   
   ![Création d’un utilisateur de test CloudPassage][23]

4. <span data-ttu-id="5b112-245">Bonjour **ajouter un nouvel utilisateur** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5b112-245">In hello **Add New User** section, perform hello following steps:</span></span> 
   
   ![Création d’un utilisateur de test CloudPassage][24]
    
    <span data-ttu-id="5b112-247">a.</span><span class="sxs-lookup"><span data-stu-id="5b112-247">a.</span></span> <span data-ttu-id="5b112-248">Bonjour **prénom** zone de texte, tapez Brian.</span><span class="sxs-lookup"><span data-stu-id="5b112-248">In hello **First Name** textbox, type Britta.</span></span> 
  
    <span data-ttu-id="5b112-249">b.</span><span class="sxs-lookup"><span data-stu-id="5b112-249">b.</span></span> <span data-ttu-id="5b112-250">Bonjour **nom** zone de texte, tapez Simon.</span><span class="sxs-lookup"><span data-stu-id="5b112-250">In hello **Last Name** textbox, type Simon.</span></span>
  
    <span data-ttu-id="5b112-251">c.</span><span class="sxs-lookup"><span data-stu-id="5b112-251">c.</span></span> <span data-ttu-id="5b112-252">Bonjour **nom d’utilisateur** zone de texte, hello **messagerie** zone de texte et hello **retapez le courrier électronique** zone de texte, tapez le nom d’utilisateur de Brian dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5b112-252">In hello **Username** textbox, hello **Email** textbox and hello **Retype Email** textbox, type Britta's user name in Azure AD.</span></span>
  
    <span data-ttu-id="5b112-253">d.</span><span class="sxs-lookup"><span data-stu-id="5b112-253">d.</span></span> <span data-ttu-id="5b112-254">En tant que **Type d’accès**, sélectionnez **Activer l’accès portail Halo**.</span><span class="sxs-lookup"><span data-stu-id="5b112-254">As **Access Type**, select **Enable Halo Portal Access**.</span></span>
  
    <span data-ttu-id="5b112-255">e.</span><span class="sxs-lookup"><span data-stu-id="5b112-255">e.</span></span> <span data-ttu-id="5b112-256">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="5b112-256">Click **Add**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5b112-257">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b112-257">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5b112-258">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooCloudPassage.</span><span class="sxs-lookup"><span data-stu-id="5b112-258">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCloudPassage.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="5b112-260">**tooassign Britta Simon tooCloudPassage, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5b112-260">**tooassign Britta Simon tooCloudPassage, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b112-261">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5b112-261">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="5b112-263">Dans la liste des applications hello, sélectionnez **CloudPassage**.</span><span class="sxs-lookup"><span data-stu-id="5b112-263">In hello applications list, select **CloudPassage**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_app.png) 

3. <span data-ttu-id="5b112-265">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5b112-265">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="5b112-267">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="5b112-267">Click **Add** button.</span></span> <span data-ttu-id="5b112-268">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5b112-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="5b112-270">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="5b112-270">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5b112-271">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5b112-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5b112-272">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5b112-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5b112-273">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="5b112-273">Testing single sign-on</span></span>

<span data-ttu-id="5b112-274">objectif Hello de cette section est tootest votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="5b112-274">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="5b112-275">Lorsque vous cliquez sur mosaïque CloudPassage hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour CloudPassage application.</span><span class="sxs-lookup"><span data-stu-id="5b112-275">When you click hello CloudPassage tile in hello Access Panel, you should get automatically signed-on tooyour CloudPassage application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5b112-276">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="5b112-276">Additional resources</span></span>

* [<span data-ttu-id="5b112-277">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5b112-277">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5b112-278">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="5b112-278">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_04.png
[12]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_07.png
[13]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_08.png
[14]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_09.png
[15]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_10.png
[22]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_15.png
[23]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_16.png
[24]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_17.png

[100]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_203.png

