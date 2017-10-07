---
title: "Didacticiel : Intégration d’Azure Active Directory à Clever | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Clever."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 069ff13a-310e-4366-a147-d6ec5cca12a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 24430e1e6c750efa5787561aa151201b1fe7d428
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clever"></a><span data-ttu-id="3826c-103">Didacticiel : Intégration d’Azure Active Directory à Clever</span><span class="sxs-lookup"><span data-stu-id="3826c-103">Tutorial: Azure Active Directory integration with Clever</span></span>

<span data-ttu-id="3826c-104">Dans ce didacticiel, vous apprendrez comment toointegrate Clever avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3826c-104">In this tutorial, you learn how toointegrate Clever with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3826c-105">Intégration Clever à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="3826c-105">Integrating Clever with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3826c-106">Vous pouvez contrôler dans Azure AD qui a accès tooClever.</span><span class="sxs-lookup"><span data-stu-id="3826c-106">You can control in Azure AD who has access tooClever.</span></span>
- <span data-ttu-id="3826c-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooClever (Single Sign-On) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3826c-107">You can enable your users tooautomatically get signed-on tooClever (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="3826c-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3826c-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="3826c-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3826c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3826c-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="3826c-110">Prerequisites</span></span>

<span data-ttu-id="3826c-111">tooconfigure intégration d’Azure AD avec Clever, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="3826c-111">tooconfigure Azure AD integration with Clever, you need hello following items:</span></span>

- <span data-ttu-id="3826c-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="3826c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3826c-113">Un abonnement Clever pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="3826c-113">A Clever single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3826c-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="3826c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3826c-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="3826c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3826c-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="3826c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3826c-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3826c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3826c-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="3826c-118">Scenario description</span></span>
<span data-ttu-id="3826c-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="3826c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3826c-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="3826c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3826c-121">Ajout de Clever à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="3826c-121">Adding Clever from hello gallery</span></span>
2. <span data-ttu-id="3826c-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="3826c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-clever-from-hello-gallery"></a><span data-ttu-id="3826c-123">Ajout de Clever à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="3826c-123">Adding Clever from hello gallery</span></span>
<span data-ttu-id="3826c-124">intégration de hello tooconfigure de Clever dans Azure AD, vous devez tooadd Clever à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="3826c-124">tooconfigure hello integration of Clever into Azure AD, you need tooadd Clever from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3826c-125">**tooadd Clever à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="3826c-125">**tooadd Clever from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3826c-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="3826c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="3826c-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="3826c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3826c-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="3826c-129">Then go too**All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="3826c-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="3826c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="3826c-133">Dans la zone de recherche de hello, tapez **Clever**, sélectionnez **Clever** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="3826c-133">In hello search box, type **Clever**, select **Clever** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Intelligente dans la liste des résultats hello](./media/active-directory-saas-clever-tutorial/tutorial_clever_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="3826c-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="3826c-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="3826c-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Clever avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="3826c-136">In this section, you configure and test Azure AD single sign-on with Clever based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3826c-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Clever est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3826c-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Clever is tooa user in Azure AD.</span></span> <span data-ttu-id="3826c-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Clever doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="3826c-138">In other words, a link relationship between an Azure AD user and hello related user in Clever needs toobe established.</span></span>

<span data-ttu-id="3826c-139">Dans Clever, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="3826c-139">In Clever, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3826c-140">tooconfigure et test Azure AD l’authentification unique avec Clever, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="3826c-140">tooconfigure and test Azure AD single sign-on with Clever, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3826c-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="3826c-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3826c-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3826c-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3826c-143">**[Créer un utilisateur test intelligent](#create-a-clever-test-user)**  -toohave un équivalent de Britta Simon dans Clever est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="3826c-143">**[Create a Clever test user](#create-a-clever-test-user)** - toohave a counterpart of Britta Simon in Clever that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3826c-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="3826c-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3826c-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="3826c-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="3826c-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="3826c-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="3826c-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application intelligente.</span><span class="sxs-lookup"><span data-stu-id="3826c-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Clever application.</span></span>

<span data-ttu-id="3826c-148">**tooconfigure Azure AD single sign-on avec Clever, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="3826c-148">**tooconfigure Azure AD single sign-on with Clever, perform hello following steps:**</span></span>

1. <span data-ttu-id="3826c-149">Bonjour portail Azure, sur hello **Clever** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="3826c-149">In hello Azure portal, on hello **Clever** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="3826c-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="3826c-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-clever-tutorial/tutorial_clever_samlbase.png)

3. <span data-ttu-id="3826c-153">Sur hello **domaine intelligent et URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="3826c-153">On hello **Clever Domain and URLs** section, perform hello following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL Clever](./media/active-directory-saas-clever-tutorial/tutorial_clever_url.png)

    <span data-ttu-id="3826c-155">a.</span><span class="sxs-lookup"><span data-stu-id="3826c-155">a.</span></span> <span data-ttu-id="3826c-156">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://clever.com/in/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="3826c-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://clever.com/in/<companyname>`</span></span>

    <span data-ttu-id="3826c-157">b.</span><span class="sxs-lookup"><span data-stu-id="3826c-157">b.</span></span> <span data-ttu-id="3826c-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://clever.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="3826c-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://clever.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3826c-159">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="3826c-159">These values are not real.</span></span> <span data-ttu-id="3826c-160">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="3826c-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="3826c-161">Contact [équipe de support Client intelligent](https://clever.com/about/contact/) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="3826c-161">Contact [Clever Client support team](https://clever.com/about/contact/) tooget these values.</span></span>

4. <span data-ttu-id="3826c-162">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="3826c-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-clever-tutorial/tutorial_clever_certificate.png)

5. <span data-ttu-id="3826c-164">Hello intelligente application attend les assertions SAML hello dans un format spécifique, ce qui vous oblige à tooyour de mappages d’attributs personnalisés tooadd **attributs du jeton SAML** configuration.</span><span class="sxs-lookup"><span data-stu-id="3826c-164">hello Clever application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **SAML Token Attributes** configuration.</span></span>

    <span data-ttu-id="3826c-165">Hello suivant capture d’écran montre un exemple de cela.</span><span class="sxs-lookup"><span data-stu-id="3826c-165">hello following screenshot shows an example for this.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-clever-tutorial/tutorial_clever_07.png) 

6. <span data-ttu-id="3826c-167">Bonjour **attributs utilisateur** section hello **l’authentification unique** boîte de dialogue, configurer des attributs de jeton SAML comme indiqué dans l’image ci-dessus hello et effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="3826c-167">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="3826c-168">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="3826c-168">Attribute Name</span></span>  | <span data-ttu-id="3826c-169">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="3826c-169">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    | <span data-ttu-id="3826c-170">clever.student.credentials.district\_username</span><span class="sxs-lookup"><span data-stu-id="3826c-170">clever.student.credentials.district\_username</span></span>  | <span data-ttu-id="3826c-171">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="3826c-171">user.userprincipalname</span></span> |
    | <span data-ttu-id="3826c-172">Firstname</span><span class="sxs-lookup"><span data-stu-id="3826c-172">Firstname</span></span>  | <span data-ttu-id="3826c-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="3826c-173">user.givenname</span></span> |
    | <span data-ttu-id="3826c-174">Lastname</span><span class="sxs-lookup"><span data-stu-id="3826c-174">Lastname</span></span>  | <span data-ttu-id="3826c-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="3826c-175">user.surname</span></span> |    

    <span data-ttu-id="3826c-176">a.</span><span class="sxs-lookup"><span data-stu-id="3826c-176">a.</span></span> <span data-ttu-id="3826c-177">Cliquez sur **ajouter un attribut** tooopen hello **ajouter un attribut** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="3826c-177">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-clever-tutorial/tutorial_attribute_04.png)
    
    ![Configurer l’authentification unique](./media/active-directory-saas-clever-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="3826c-180">b.</span><span class="sxs-lookup"><span data-stu-id="3826c-180">b.</span></span> <span data-ttu-id="3826c-181">Bonjour **nom** zone de texte, nom d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="3826c-181">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="3826c-182">c.</span><span class="sxs-lookup"><span data-stu-id="3826c-182">c.</span></span> <span data-ttu-id="3826c-183">À partir de hello **valeur** liste, la valeur d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="3826c-183">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="3826c-184">d.</span><span class="sxs-lookup"><span data-stu-id="3826c-184">d.</span></span> <span data-ttu-id="3826c-185">Laissez hello **Namespace** zone de texte vide.</span><span class="sxs-lookup"><span data-stu-id="3826c-185">Leave hello **Namespace** textbox blank.</span></span>
    
    <span data-ttu-id="3826c-186">d.</span><span class="sxs-lookup"><span data-stu-id="3826c-186">d.</span></span> <span data-ttu-id="3826c-187">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="3826c-187">Click **Ok**.</span></span>     

5. <span data-ttu-id="3826c-188">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="3826c-188">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-clever-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="3826c-190">toogenerate hello **métadonnées** url, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="3826c-190">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="3826c-191">a.</span><span class="sxs-lookup"><span data-stu-id="3826c-191">a.</span></span> <span data-ttu-id="3826c-192">Cliquez sur **Inscriptions des applications**.</span><span class="sxs-lookup"><span data-stu-id="3826c-192">Click **App registrations**.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-clever-tutorial/tutorial_clever_appregistrations.png)
   
    <span data-ttu-id="3826c-194">b.</span><span class="sxs-lookup"><span data-stu-id="3826c-194">b.</span></span> <span data-ttu-id="3826c-195">Cliquez sur **points de terminaison** tooopen **points de terminaison** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="3826c-195">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Configurer l’authentification unique](./media/active-directory-saas-clever-tutorial/tutorial_clever_endpointicon.png)

    <span data-ttu-id="3826c-197">c.</span><span class="sxs-lookup"><span data-stu-id="3826c-197">c.</span></span> <span data-ttu-id="3826c-198">Cliquez sur hello copie bouton toocopy **DOCUMENT de métadonnées de fédération** url et collez-le dans le bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="3826c-198">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-clever-tutorial/tutorial_clever_endpoint.png)
     
    <span data-ttu-id="3826c-200">d.</span><span class="sxs-lookup"><span data-stu-id="3826c-200">d.</span></span> <span data-ttu-id="3826c-201">Maintenant accédez toohello page de propriétés de **Clever** et copie Bonjour **Id d’Application** à l’aide de **copie** bouton et collez-le dans le bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="3826c-201">Now go toohello property page of **Clever** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-clever-tutorial/tutorial_clever_appid.png)

    <span data-ttu-id="3826c-203">e.</span><span class="sxs-lookup"><span data-stu-id="3826c-203">e.</span></span> <span data-ttu-id="3826c-204">Générer hello **URL de métadonnées** hello suivant le modèle à l’aide de :`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="3826c-204">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>   

9. <span data-ttu-id="3826c-205">Dans une fenêtre de navigateur web, ouvrez une session dans le site d’entreprise intelligente tooyour en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="3826c-205">In a different web browser window, log in tooyour Clever company site as an administrator.</span></span>

10. <span data-ttu-id="3826c-206">Dans la barre d’outils de hello, cliquez sur **connexion instantanée**.</span><span class="sxs-lookup"><span data-stu-id="3826c-206">In hello toolbar, click **Instant Login**.</span></span>

    <span data-ttu-id="3826c-207">![Instant Login](./media/active-directory-saas-clever-tutorial/ic798984.png "Instant Login")</span><span class="sxs-lookup"><span data-stu-id="3826c-207">![Instant Login](./media/active-directory-saas-clever-tutorial/ic798984.png "Instant Login")</span></span>

11. <span data-ttu-id="3826c-208">Sur hello **connexion instantanée** page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="3826c-208">On hello **Instant Login** page, perform hello following steps:</span></span>
      
      <span data-ttu-id="3826c-209">![Instant Login](./media/active-directory-saas-clever-tutorial/ic798985.png "Instant Login")</span><span class="sxs-lookup"><span data-stu-id="3826c-209">![Instant Login](./media/active-directory-saas-clever-tutorial/ic798985.png "Instant Login")</span></span>
      
      <span data-ttu-id="3826c-210">a.</span><span class="sxs-lookup"><span data-stu-id="3826c-210">a.</span></span> <span data-ttu-id="3826c-211">Hello de type **URL de connexion**.</span><span class="sxs-lookup"><span data-stu-id="3826c-211">Type hello **Login URL**.</span></span>
      
      >[!NOTE]
      ><span data-ttu-id="3826c-212">Hello **URL de connexion** est une valeur personnalisée.</span><span class="sxs-lookup"><span data-stu-id="3826c-212">hello **Login URL** is a custom value.</span></span> <span data-ttu-id="3826c-213">Contact [équipe de support Client intelligent](https://clever.com/about/contact/) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="3826c-213">Contact [Clever Client support team](https://clever.com/about/contact/) tooget this value.</span></span>
      
      <span data-ttu-id="3826c-214">b.</span><span class="sxs-lookup"><span data-stu-id="3826c-214">b.</span></span> <span data-ttu-id="3826c-215">Sous **Identity System**, sélectionnez **ADFS**.</span><span class="sxs-lookup"><span data-stu-id="3826c-215">As **Identity System**, select **ADFS**.</span></span>

      <span data-ttu-id="3826c-216">c.</span><span class="sxs-lookup"><span data-stu-id="3826c-216">c.</span></span> <span data-ttu-id="3826c-217">Hello de type **URL de métadonnées** Bonjour **URL de métadonnées** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="3826c-217">Type hello **Metadata URL** in hello **Metadata URL** textbox.</span></span>
      
      <span data-ttu-id="3826c-218">d.</span><span class="sxs-lookup"><span data-stu-id="3826c-218">d.</span></span> <span data-ttu-id="3826c-219">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="3826c-219">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="3826c-220">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="3826c-220">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3826c-221">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="3826c-221">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3826c-222">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3826c-222">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="3826c-223">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="3826c-223">Create an Azure AD test user</span></span>

<span data-ttu-id="3826c-224">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="3826c-224">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="3826c-226">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="3826c-226">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3826c-227">Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.</span><span class="sxs-lookup"><span data-stu-id="3826c-227">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-clever-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="3826c-229">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="3826c-229">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-clever-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="3826c-231">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="3826c-231">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![bouton Ajouter de Hello](./media/active-directory-saas-clever-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="3826c-233">Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="3826c-233">In hello **User** dialog box, perform hello following steps:</span></span>

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-clever-tutorial/create_aaduser_04.png)

    <span data-ttu-id="3826c-235">a.</span><span class="sxs-lookup"><span data-stu-id="3826c-235">a.</span></span> <span data-ttu-id="3826c-236">Bonjour **nom** , tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3826c-236">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3826c-237">b.</span><span class="sxs-lookup"><span data-stu-id="3826c-237">b.</span></span> <span data-ttu-id="3826c-238">Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3826c-238">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="3826c-239">c.</span><span class="sxs-lookup"><span data-stu-id="3826c-239">c.</span></span> <span data-ttu-id="3826c-240">Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.</span><span class="sxs-lookup"><span data-stu-id="3826c-240">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="3826c-241">d.</span><span class="sxs-lookup"><span data-stu-id="3826c-241">d.</span></span> <span data-ttu-id="3826c-242">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="3826c-242">Click **Create**.</span></span>
 
### <a name="create-a-clever-test-user"></a><span data-ttu-id="3826c-243">Créer un utilisateur de test Clever</span><span class="sxs-lookup"><span data-stu-id="3826c-243">Create a Clever test user</span></span>

<span data-ttu-id="3826c-244">tooenable Azure AD les utilisateurs toolog dans tooClever, vous devez les configurer dans Clever.</span><span class="sxs-lookup"><span data-stu-id="3826c-244">tooenable Azure AD users toolog in tooClever, they must be provisioned into Clever.</span></span>

<span data-ttu-id="3826c-245">En cas de Clever, travailler avec [équipe de support Client intelligent](https://clever.com/about/contact/) pour ajouter des utilisateurs de hello de plateforme intelligente de hello.</span><span class="sxs-lookup"><span data-stu-id="3826c-245">In case of Clever, Work with [Clever Client support team](https://clever.com/about/contact/) to add hello users in hello Clever platform.</span></span> <span data-ttu-id="3826c-246">Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="3826c-246">Users must be created and activated before you use single sign-on.</span></span> 

>[!NOTE]
><span data-ttu-id="3826c-247">Vous pouvez utiliser n’importe quel autre outil de création de compte utilisateur intelligent ou API fournie par tooprovision des comptes d’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3826c-247">You can use any other Clever user account creation tools or APIs provided by Clever tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="3826c-248">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="3826c-248">Assign hello Azure AD test user</span></span>

<span data-ttu-id="3826c-249">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooClever.</span><span class="sxs-lookup"><span data-stu-id="3826c-249">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooClever.</span></span>

![Attribuer le rôle d’utilisateur hello][200] 

<span data-ttu-id="3826c-251">**tooassign Britta Simon tooClever, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="3826c-251">**tooassign Britta Simon tooClever, perform hello following steps:**</span></span>

1. <span data-ttu-id="3826c-252">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="3826c-252">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="3826c-254">Dans la liste des applications hello, sélectionnez **Clever**.</span><span class="sxs-lookup"><span data-stu-id="3826c-254">In hello applications list, select **Clever**.</span></span>

    ![Hello Clever lien dans la liste des Applications hello](./media/active-directory-saas-clever-tutorial/tutorial_clever_app.png)  

3. <span data-ttu-id="3826c-256">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="3826c-256">In hello menu on hello left, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202]

4. <span data-ttu-id="3826c-258">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="3826c-258">Click **Add** button.</span></span> <span data-ttu-id="3826c-259">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="3826c-259">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="3826c-261">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="3826c-261">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3826c-262">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="3826c-262">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3826c-263">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="3826c-263">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="3826c-264">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="3826c-264">Test single sign-on</span></span>

<span data-ttu-id="3826c-265">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="3826c-265">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="3826c-266">Lorsque vous cliquez sur la vignette d’intelligent hello dans hello volet d’accès, vous devez obtenir application intelligente de tooyour automatiquement signé sur.</span><span class="sxs-lookup"><span data-stu-id="3826c-266">When you click hello Clever tile in hello Access Panel, you should get automatically signed-on tooyour Clever application.</span></span>
<span data-ttu-id="3826c-267">Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3826c-267">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3826c-268">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="3826c-268">Additional resources</span></span>

* [<span data-ttu-id="3826c-269">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3826c-269">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3826c-270">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="3826c-270">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clever-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clever-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clever-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clever-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clever-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clever-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clever-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clever-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clever-tutorial/tutorial_general_203.png

