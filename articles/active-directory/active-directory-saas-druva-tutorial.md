---
title: "Didacticiel : intégration d’Azure Active Directory à Druva | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Druva."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ab92b600-1fea-4905-b1c7-ef8e4d8c495c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: a1c36c06d6d005e0aa363fbf34efe630e4cca1ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-druva"></a><span data-ttu-id="18cfe-103">Didacticiel : Intégration d’Azure Active Directory à Druva</span><span class="sxs-lookup"><span data-stu-id="18cfe-103">Tutorial: Azure Active Directory integration with Druva</span></span>

<span data-ttu-id="18cfe-104">Dans ce didacticiel, vous apprendrez comment toointegrate Druva avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="18cfe-104">In this tutorial, you learn how toointegrate Druva with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="18cfe-105">Intégration de Druva à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="18cfe-105">Integrating Druva with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="18cfe-106">Vous pouvez contrôler dans Azure AD qui a accès tooDruva.</span><span class="sxs-lookup"><span data-stu-id="18cfe-106">You can control in Azure AD who has access tooDruva.</span></span>
- <span data-ttu-id="18cfe-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooDruva (Single Sign-On) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="18cfe-107">You can enable your users tooautomatically get signed-on tooDruva (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="18cfe-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="18cfe-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="18cfe-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="18cfe-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18cfe-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="18cfe-110">Prerequisites</span></span>

<span data-ttu-id="18cfe-111">tooconfigure intégration d’Azure AD à Druva, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="18cfe-111">tooconfigure Azure AD integration with Druva, you need hello following items:</span></span>

- <span data-ttu-id="18cfe-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="18cfe-112">An Azure AD subscription</span></span>
- <span data-ttu-id="18cfe-113">Un abonnement Druva pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="18cfe-113">A Druva single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="18cfe-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="18cfe-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="18cfe-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="18cfe-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="18cfe-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="18cfe-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="18cfe-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="18cfe-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="18cfe-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="18cfe-118">Scenario description</span></span>
<span data-ttu-id="18cfe-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="18cfe-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="18cfe-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="18cfe-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="18cfe-121">Ajout de Druva à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="18cfe-121">Adding Druva from hello gallery</span></span>
2. <span data-ttu-id="18cfe-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="18cfe-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-druva-from-hello-gallery"></a><span data-ttu-id="18cfe-123">Ajout de Druva à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="18cfe-123">Adding Druva from hello gallery</span></span>
<span data-ttu-id="18cfe-124">intégration de hello tooconfigure de Druva dans Azure AD, vous devez tooadd Druva à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="18cfe-124">tooconfigure hello integration of Druva into Azure AD, you need tooadd Druva from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="18cfe-125">**tooadd Druva à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="18cfe-125">**tooadd Druva from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="18cfe-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="18cfe-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="18cfe-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="18cfe-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="18cfe-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="18cfe-129">Then go too**All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="18cfe-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="18cfe-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="18cfe-133">Dans la zone de recherche de hello, tapez **Druva**, sélectionnez **Druva** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="18cfe-133">In hello search box, type **Druva**, select **Druva** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Liste des résultats de Druva Bonjour](./media/active-directory-saas-druva-tutorial/tutorial_druva_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="18cfe-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="18cfe-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="18cfe-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Druva, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="18cfe-136">In this section, you configure and test Azure AD single sign-on with Druva based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="18cfe-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Druva est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="18cfe-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Druva is tooa user in Azure AD.</span></span> <span data-ttu-id="18cfe-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Druva doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="18cfe-138">In other words, a link relationship between an Azure AD user and hello related user in Druva needs toobe established.</span></span>

<span data-ttu-id="18cfe-139">Dans Druva, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="18cfe-139">In Druva, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="18cfe-140">tooconfigure et test Azure AD l’authentification unique à Druva, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="18cfe-140">tooconfigure and test Azure AD single sign-on with Druva, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="18cfe-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="18cfe-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="18cfe-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="18cfe-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="18cfe-143">**[Créer un utilisateur de test de Druva](#create-a-druva-test-user)**  -toohave un équivalent de Britta Simon dans Druva est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="18cfe-143">**[Create a Druva test user](#create-a-druva-test-user)** - toohave a counterpart of Britta Simon in Druva that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="18cfe-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="18cfe-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="18cfe-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="18cfe-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="18cfe-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="18cfe-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="18cfe-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Druva.</span><span class="sxs-lookup"><span data-stu-id="18cfe-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Druva application.</span></span>

<span data-ttu-id="18cfe-148">**tooconfigure Azure AD single sign-on avec Druva, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="18cfe-148">**tooconfigure Azure AD single sign-on with Druva, perform hello following steps:**</span></span>

1. <span data-ttu-id="18cfe-149">Bonjour portail Azure, sur hello **Druva** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="18cfe-149">In hello Azure portal, on hello **Druva** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="18cfe-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="18cfe-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-druva-tutorial/tutorial_druva_samlbase.png)

3. <span data-ttu-id="18cfe-153">Sur hello **Druva domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="18cfe-153">On hello **Druva Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-druva-tutorial/tutorial_druva_url.png)

    <span data-ttu-id="18cfe-155">Bonjour **URL de connexion** zone de texte, tapez l’URL hello :`https://cloud.druva.com/home`</span><span class="sxs-lookup"><span data-stu-id="18cfe-155">In hello **Sign-on URL** textbox, type hello URL: `https://cloud.druva.com/home`</span></span>

4. <span data-ttu-id="18cfe-156">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="18cfe-156">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-druva-tutorial/tutorial_druva_certificate.png) 

5. <span data-ttu-id="18cfe-158">Votre application Druva attend les assertions SAML hello dans un format spécifique, ce qui vous oblige à tooyour de mappages d’attributs personnalisés tooadd **attributs du jeton SAML** configuration.</span><span class="sxs-lookup"><span data-stu-id="18cfe-158">Your Druva application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **SAML Token Attributes** configuration.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-druva-tutorial/tutorial_druva_attribute.png)

6. <span data-ttu-id="18cfe-160">Bonjour **attributs utilisateur** section hello **l’authentification unique** boîte de dialogue, configurer des attributs de jeton SAML comme indiqué dans hello précédant l’image et effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="18cfe-160">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello preceding image and perform hello following steps:</span></span>

    | <span data-ttu-id="18cfe-161">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="18cfe-161">Attribute Name</span></span>      | <span data-ttu-id="18cfe-162">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="18cfe-162">Attribute Value</span></span>      |
    | ------------------- | -------------------- |
    | <span data-ttu-id="18cfe-163">insync\_auth\_token</span><span class="sxs-lookup"><span data-stu-id="18cfe-163">insync\_auth\_token</span></span> |<span data-ttu-id="18cfe-164">Entrez la valeur générée de jeton de hello</span><span class="sxs-lookup"><span data-stu-id="18cfe-164">Enter hello token generated value</span></span> |
    
    <span data-ttu-id="18cfe-165">a.</span><span class="sxs-lookup"><span data-stu-id="18cfe-165">a.</span></span> <span data-ttu-id="18cfe-166">Cliquez sur **ajouter un attribut** tooopen hello **ajouter un attribut** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="18cfe-166">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-druva-tutorial/tutorial_attribute_04.png)
    
    ![Configurer l’authentification unique](./media/active-directory-saas-druva-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="18cfe-169">b.</span><span class="sxs-lookup"><span data-stu-id="18cfe-169">b.</span></span> <span data-ttu-id="18cfe-170">Bonjour **nom** zone de texte, nom d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="18cfe-170">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="18cfe-171">c.</span><span class="sxs-lookup"><span data-stu-id="18cfe-171">c.</span></span> <span data-ttu-id="18cfe-172">À partir de hello **valeur** liste, la valeur d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="18cfe-172">From hello **Value** list, type hello attribute value shown for that row.</span></span> <span data-ttu-id="18cfe-173">valeur générée du jeton Hello est expliquée plus loin dans le didacticiel.</span><span class="sxs-lookup"><span data-stu-id="18cfe-173">hello token generated value is explained later in tutorial.</span></span>
    
    <span data-ttu-id="18cfe-174">d.</span><span class="sxs-lookup"><span data-stu-id="18cfe-174">d.</span></span> <span data-ttu-id="18cfe-175">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="18cfe-175">Click **Ok**.</span></span>    

7. <span data-ttu-id="18cfe-176">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="18cfe-176">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-druva-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="18cfe-178">Sur hello **Druva Configuration** , cliquez sur **configurer de Druva** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="18cfe-178">On hello **Druva Configuration** section, click **Configure Druva** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="18cfe-179">Hello de copie **URL de déconnexion et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="18cfe-179">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-druva-tutorial/tutorial_druva_configure.png) 

9. <span data-ttu-id="18cfe-181">Dans une fenêtre de navigateur web, ouvrez une session dans le site de société Druva tooyour en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="18cfe-181">In a different web browser window, log in tooyour Druva company site as an administrator.</span></span>

10. <span data-ttu-id="18cfe-182">Accédez trop**gérer \> paramètres**.</span><span class="sxs-lookup"><span data-stu-id="18cfe-182">Go too**Manage \> Settings**.</span></span>

    <span data-ttu-id="18cfe-183">![Paramètres](./media/active-directory-saas-druva-tutorial/ic795091.png "Paramètres")</span><span class="sxs-lookup"><span data-stu-id="18cfe-183">![Settings](./media/active-directory-saas-druva-tutorial/ic795091.png "Settings")</span></span>

11. <span data-ttu-id="18cfe-184">Dans la boîte de dialogue Paramètres d’authentification unique hello, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="18cfe-184">On hello Single Sign-On Settings dialog, perform hello following steps:</span></span>

    <span data-ttu-id="18cfe-185">![Paramètres d’authentification unique](./media/active-directory-saas-druva-tutorial/ic795092.png "paramètres d’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="18cfe-185">![Single Sign-On Settings](./media/active-directory-saas-druva-tutorial/ic795092.png "Single Sign-On Settings")</span></span>
    
    <span data-ttu-id="18cfe-186">a.</span><span class="sxs-lookup"><span data-stu-id="18cfe-186">a.</span></span> <span data-ttu-id="18cfe-187">Coller **SAML Sign-On URL du Service unique** valeur, ce qui vous avez copié à partir de hello portail Azure en hello **ID Provider Login URL** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="18cfe-187">Paste **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **ID Provider Login URL** textbox.</span></span>
    
    <span data-ttu-id="18cfe-188">b.</span><span class="sxs-lookup"><span data-stu-id="18cfe-188">b.</span></span> <span data-ttu-id="18cfe-189">Coller **URL de déconnexion** valeur, ce qui vous avez copié à partir de hello portail Azure en hello **ID Provider Logout URL** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="18cfe-189">Paste **Sign-Out URL** value, which you have copied from hello Azure portal into hello **ID Provider Logout URL** textbox.</span></span>
    
     <span data-ttu-id="18cfe-190">c.</span><span class="sxs-lookup"><span data-stu-id="18cfe-190">c.</span></span> <span data-ttu-id="18cfe-191">Ouvrez votre certificat codé en base 64 dans le bloc-notes, hello copie contenu de celui-ci dans le Presse-papiers et le coller ensuite toohello **ID fournisseur certificat** zone de texte</span><span class="sxs-lookup"><span data-stu-id="18cfe-191">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **ID Provider Certificate** textbox</span></span>
     
     <span data-ttu-id="18cfe-192">d.</span><span class="sxs-lookup"><span data-stu-id="18cfe-192">d.</span></span> <span data-ttu-id="18cfe-193">tooopen hello **paramètres** , cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="18cfe-193">tooopen hello **Settings** page, click **Save**.</span></span>

12. <span data-ttu-id="18cfe-194">Sur hello **paramètres** , cliquez sur **générer un jeton SSO**.</span><span class="sxs-lookup"><span data-stu-id="18cfe-194">On hello **Settings** page, click **Generate SSO Token**.</span></span>

    <span data-ttu-id="18cfe-195">![Paramètres](./media/active-directory-saas-druva-tutorial/ic795093.png "Paramètres")</span><span class="sxs-lookup"><span data-stu-id="18cfe-195">![Settings](./media/active-directory-saas-druva-tutorial/ic795093.png "Settings")</span></span>

13. <span data-ttu-id="18cfe-196">Sur hello **unique authentification jeton d’authentification** boîte de dialogue, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="18cfe-196">On hello **Single Sign-on Authentication Token** dialog, perform hello following steps:</span></span>

    <span data-ttu-id="18cfe-197">![SSO Token](./media/active-directory-saas-druva-tutorial/ic795094.png "SSO Token")</span><span class="sxs-lookup"><span data-stu-id="18cfe-197">![SSO Token](./media/active-directory-saas-druva-tutorial/ic795094.png "SSO Token")</span></span>
    
    <span data-ttu-id="18cfe-198">a.</span><span class="sxs-lookup"><span data-stu-id="18cfe-198">a.</span></span> <span data-ttu-id="18cfe-199">Cliquez sur **copie**, coller copié la valeur Bonjour **valeur** textbox Bonjour **ajouter un attribut** section.</span><span class="sxs-lookup"><span data-stu-id="18cfe-199">Click **Copy**, Paste copied value in hello **Value** textbox in hello **Add Attribute** section.</span></span>
    
    <span data-ttu-id="18cfe-200">b.</span><span class="sxs-lookup"><span data-stu-id="18cfe-200">b.</span></span> <span data-ttu-id="18cfe-201">Cliquez sur **Fermer**.</span><span class="sxs-lookup"><span data-stu-id="18cfe-201">Click **Close**.</span></span>

> [!TIP]
> <span data-ttu-id="18cfe-202">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="18cfe-202">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="18cfe-203">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="18cfe-203">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="18cfe-204">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="18cfe-204">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="18cfe-205">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="18cfe-205">Create an Azure AD test user</span></span>

<span data-ttu-id="18cfe-206">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="18cfe-206">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="18cfe-208">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="18cfe-208">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="18cfe-209">Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.</span><span class="sxs-lookup"><span data-stu-id="18cfe-209">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-druva-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="18cfe-211">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="18cfe-211">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-druva-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="18cfe-213">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="18cfe-213">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![bouton Ajouter de Hello](./media/active-directory-saas-druva-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="18cfe-215">Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="18cfe-215">In hello **User** dialog box, perform hello following steps:</span></span>

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-druva-tutorial/create_aaduser_04.png)

    <span data-ttu-id="18cfe-217">a.</span><span class="sxs-lookup"><span data-stu-id="18cfe-217">a.</span></span> <span data-ttu-id="18cfe-218">Bonjour **nom** , tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="18cfe-218">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="18cfe-219">b.</span><span class="sxs-lookup"><span data-stu-id="18cfe-219">b.</span></span> <span data-ttu-id="18cfe-220">Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="18cfe-220">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="18cfe-221">c.</span><span class="sxs-lookup"><span data-stu-id="18cfe-221">c.</span></span> <span data-ttu-id="18cfe-222">Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.</span><span class="sxs-lookup"><span data-stu-id="18cfe-222">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="18cfe-223">d.</span><span class="sxs-lookup"><span data-stu-id="18cfe-223">d.</span></span> <span data-ttu-id="18cfe-224">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="18cfe-224">Click **Create**.</span></span>
 
### <a name="create-a-druva-test-user"></a><span data-ttu-id="18cfe-225">Créer un utilisateur de test Druva</span><span class="sxs-lookup"><span data-stu-id="18cfe-225">Create a Druva test user</span></span>

<span data-ttu-id="18cfe-226">Dans l’ordre tooenable Azure AD les utilisateurs toolog dans tooDruva, vous devez les configurer dans Druva.</span><span class="sxs-lookup"><span data-stu-id="18cfe-226">In order tooenable Azure AD users toolog in tooDruva, they must be provisioned into Druva.</span></span> <span data-ttu-id="18cfe-227">Dans les cas de hello de Druva, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="18cfe-227">In hello case of Druva, provisioning is a manual task.</span></span>

<span data-ttu-id="18cfe-228">**configuration, de l’utilisateur tooconfigure effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="18cfe-228">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="18cfe-229">Connectez-vous à tooyour **Druva** site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="18cfe-229">Log in tooyour **Druva** company site as administrator.</span></span>

2. <span data-ttu-id="18cfe-230">Accédez trop**gérer \> utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="18cfe-230">Go too**Manage \> Users**.</span></span>
   
   <span data-ttu-id="18cfe-231">![Gestion des utilisateurs](./media/active-directory-saas-druva-tutorial/ic795097.png "Gestion des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="18cfe-231">![Manage Users](./media/active-directory-saas-druva-tutorial/ic795097.png "Manage Users")</span></span>

3. <span data-ttu-id="18cfe-232">Cliquez sur **Create New**.</span><span class="sxs-lookup"><span data-stu-id="18cfe-232">Click **Create New**.</span></span>
   
   <span data-ttu-id="18cfe-233">![Gestion des utilisateurs](./media/active-directory-saas-druva-tutorial/ic795098.png "Gestion des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="18cfe-233">![Manage Users](./media/active-directory-saas-druva-tutorial/ic795098.png "Manage Users")</span></span>

4. <span data-ttu-id="18cfe-234">Dans la boîte de dialogue Créer un nouvel utilisateur hello, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="18cfe-234">On hello Create New User dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="18cfe-235">![Create NewUser](./media/active-directory-saas-druva-tutorial/ic795099.png "Create NewUser")</span><span class="sxs-lookup"><span data-stu-id="18cfe-235">![Create NewUser](./media/active-directory-saas-druva-tutorial/ic795099.png "Create NewUser")</span></span>
   
   <span data-ttu-id="18cfe-236">a.</span><span class="sxs-lookup"><span data-stu-id="18cfe-236">a.</span></span> <span data-ttu-id="18cfe-237">Bonjour **adresse de messagerie** zone de texte, entrez hello adresse de messagerie de l’utilisateur comme  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="18cfe-237">In hello **Email address** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>
   
   <span data-ttu-id="18cfe-238">b.</span><span class="sxs-lookup"><span data-stu-id="18cfe-238">b.</span></span> <span data-ttu-id="18cfe-239">Bonjour **nom** zone de texte, entrez hello les nom d’utilisateur comme **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="18cfe-239">In hello **Name** textbox, enter hello name of user like **BrittaSimon**.</span></span>
   
   <span data-ttu-id="18cfe-240">c.</span><span class="sxs-lookup"><span data-stu-id="18cfe-240">c.</span></span> <span data-ttu-id="18cfe-241">Cliquez sur **Create User**.</span><span class="sxs-lookup"><span data-stu-id="18cfe-241">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="18cfe-242">Vous pouvez utiliser n’importe quel autre Druva utilisateur compte outil de création ou API fournie par Druva tooprovision comptes d’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="18cfe-242">You can use any other Druva user account creation tools or APIs provided by Druva tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="18cfe-243">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="18cfe-243">Assign hello Azure AD test user</span></span>

<span data-ttu-id="18cfe-244">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooDruva.</span><span class="sxs-lookup"><span data-stu-id="18cfe-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDruva.</span></span>

![Attribuer le rôle d’utilisateur hello][200] 

<span data-ttu-id="18cfe-246">**tooassign Britta Simon tooDruva, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="18cfe-246">**tooassign Britta Simon tooDruva, perform hello following steps:**</span></span>

1. <span data-ttu-id="18cfe-247">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="18cfe-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="18cfe-249">Dans la liste des applications hello, sélectionnez **Druva**.</span><span class="sxs-lookup"><span data-stu-id="18cfe-249">In hello applications list, select **Druva**.</span></span>

    ![lien de Druva Hello dans la liste des Applications hello](./media/active-directory-saas-druva-tutorial/tutorial_druva_app.png)  

3. <span data-ttu-id="18cfe-251">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="18cfe-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202]

4. <span data-ttu-id="18cfe-253">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="18cfe-253">Click **Add** button.</span></span> <span data-ttu-id="18cfe-254">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="18cfe-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="18cfe-256">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="18cfe-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="18cfe-257">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="18cfe-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="18cfe-258">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="18cfe-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="18cfe-259">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="18cfe-259">Test single sign-on</span></span>

<span data-ttu-id="18cfe-260">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="18cfe-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="18cfe-261">Lorsque vous cliquez sur mosaïque Druva hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Druva application.</span><span class="sxs-lookup"><span data-stu-id="18cfe-261">When you click hello Druva tile in hello Access Panel, you should get automatically signed-on tooyour Druva application.</span></span>
<span data-ttu-id="18cfe-262">Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="18cfe-262">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="18cfe-263">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="18cfe-263">Additional resources</span></span>

* [<span data-ttu-id="18cfe-264">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="18cfe-264">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="18cfe-265">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="18cfe-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-druva-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-druva-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-druva-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-druva-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-druva-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-druva-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-druva-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-druva-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-druva-tutorial/tutorial_general_203.png

