---
title: "Didacticiel : Intégration d’Azure Active Directory avec Klue | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Klue."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 08341008-980b-4111-adb2-97bbabbf1e47
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: bb9134a558d6c050f428690d57a3cea850b7dbee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-klue"></a><span data-ttu-id="0d4ce-103">Didacticiel : Intégration d’Azure Active Directory avec Klue</span><span class="sxs-lookup"><span data-stu-id="0d4ce-103">Tutorial: Azure Active Directory integration with Klue</span></span>

<span data-ttu-id="0d4ce-104">Dans ce didacticiel, vous apprendrez comment toointegrate Klue avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0d4ce-104">In this tutorial, you learn how toointegrate Klue with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0d4ce-105">Intégration Klue à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="0d4ce-105">Integrating Klue with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0d4ce-106">Vous pouvez contrôler dans Azure AD qui a accès tooKlue</span><span class="sxs-lookup"><span data-stu-id="0d4ce-106">You can control in Azure AD who has access tooKlue</span></span>
- <span data-ttu-id="0d4ce-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooKlue (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d4ce-107">You can enable your users tooautomatically get signed-on tooKlue (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0d4ce-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="0d4ce-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0d4ce-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0d4ce-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0d4ce-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="0d4ce-110">Prerequisites</span></span>

<span data-ttu-id="0d4ce-111">tooconfigure intégration d’Azure AD avec Klue, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="0d4ce-111">tooconfigure Azure AD integration with Klue, you need hello following items:</span></span>

- <span data-ttu-id="0d4ce-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d4ce-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0d4ce-113">Un abonnement Klue pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="0d4ce-113">A Klue single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0d4ce-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0d4ce-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="0d4ce-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0d4ce-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0d4ce-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0d4ce-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0d4ce-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="0d4ce-118">Scenario description</span></span>
<span data-ttu-id="0d4ce-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0d4ce-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="0d4ce-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0d4ce-121">Ajout de Klue à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="0d4ce-121">Adding Klue from hello gallery</span></span>
2. <span data-ttu-id="0d4ce-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d4ce-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-klue-from-hello-gallery"></a><span data-ttu-id="0d4ce-123">Ajout de Klue à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="0d4ce-123">Adding Klue from hello gallery</span></span>
<span data-ttu-id="0d4ce-124">intégration de hello tooconfigure de Klue dans Azure AD, vous devez tooadd Klue à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-124">tooconfigure hello integration of Klue into Azure AD, you need tooadd Klue from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0d4ce-125">**tooadd Klue à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0d4ce-125">**tooadd Klue from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0d4ce-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0d4ce-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0d4ce-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="0d4ce-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="0d4ce-133">Dans la zone de recherche de hello, tapez **Klue**.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-133">In hello search box, type **Klue**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-klue-tutorial/tutorial_klue_search.png)

5. <span data-ttu-id="0d4ce-135">Dans le volet de résultats hello, sélectionnez **Klue**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-135">In hello results panel, select **Klue**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-klue-tutorial/tutorial_klue_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0d4ce-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d4ce-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0d4ce-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Klue sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="0d4ce-138">In this section, you configure and test Azure AD single sign-on with Klue based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0d4ce-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Klue est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Klue is tooa user in Azure AD.</span></span> <span data-ttu-id="0d4ce-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Klue doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-140">In other words, a link relationship between an Azure AD user and hello related user in Klue needs toobe established.</span></span>

<span data-ttu-id="0d4ce-141">Dans Klue, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-141">In Klue, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0d4ce-142">tooconfigure et test Azure AD l’authentification unique avec Klue, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="0d4ce-142">tooconfigure and test Azure AD single sign-on with Klue, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0d4ce-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0d4ce-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0d4ce-145">**[Création d’un utilisateur de test Klue](#creating-a-klue-test-user)**  -toohave un équivalent de Britta Simon dans Klue est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-145">**[Creating a Klue test user](#creating-a-klue-test-user)** - toohave a counterpart of Britta Simon in Klue that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0d4ce-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0d4ce-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0d4ce-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d4ce-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0d4ce-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Klue.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Klue application.</span></span>

<span data-ttu-id="0d4ce-150">**tooconfigure Azure AD single sign-on avec Klue, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0d4ce-150">**tooconfigure Azure AD single sign-on with Klue, perform hello following steps:**</span></span>

1. <span data-ttu-id="0d4ce-151">Bonjour portail Azure, sur hello **Klue** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-151">In hello Azure portal, on hello **Klue** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="0d4ce-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-klue-tutorial/tutorial_klue_samlbase.png)

3. <span data-ttu-id="0d4ce-155">Sur hello **Klue domaine et les URL** section, si vous le souhaitez application hello tooconfigure **IDP** en mode initié par :</span><span class="sxs-lookup"><span data-stu-id="0d4ce-155">On hello **Klue Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-klue-tutorial/tutorial_klue_url1.png)

    <span data-ttu-id="0d4ce-157">a.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-157">a.</span></span> <span data-ttu-id="0d4ce-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`urn:klue:<Customer ID>`</span><span class="sxs-lookup"><span data-stu-id="0d4ce-158">In hello **Identifier** textbox, type a URL using hello following pattern: `urn:klue:<Customer ID>`</span></span>

    <span data-ttu-id="0d4ce-159">b.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-159">b.</span></span> <span data-ttu-id="0d4ce-160">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://app.klue.com/account/auth/saml/<Customer UUID>/callback`</span><span class="sxs-lookup"><span data-stu-id="0d4ce-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://app.klue.com/account/auth/saml/<Customer UUID>/callback`</span></span>

4. <span data-ttu-id="0d4ce-161">Cliquez sur **Afficher les paramètres d’URL avancés**.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="0d4ce-162">Si vous le souhaitez application hello tooconfigure **SP** en mode initié par :</span><span class="sxs-lookup"><span data-stu-id="0d4ce-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-klue-tutorial/tutorial_klue_url2.png)

    <span data-ttu-id="0d4ce-164">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://app.klue.com/account/auth/saml/<Customer UUID>/`</span><span class="sxs-lookup"><span data-stu-id="0d4ce-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://app.klue.com/account/auth/saml/<Customer UUID>/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="0d4ce-165">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-165">These values are not real.</span></span> <span data-ttu-id="0d4ce-166">Mettre à jour ces valeurs avec des URL de réponse réelle hello, identificateur et URL de connexion.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-166">Update these values with hello actual Reply URL, Identifier, and Sign-On URL.</span></span> <span data-ttu-id="0d4ce-167">Contact [équipe de support Client de Klue](mailto:support@klue.com) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-167">Contact [Klue Client support team](mailto:support@klue.com) tooget these values.</span></span>

5. <span data-ttu-id="0d4ce-168">Hello Klue application attend les assertions SAML hello dans un format spécifique, ce qui nécessite vous tooadd attribut personnalisé tooyour SAML attributs du jeton configuration des mappages.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-168">hello Klue application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="0d4ce-169">Vous pouvez gérer les valeurs de ces attributs hello depuis hello »**attributs utilisateur**« section sur la page d’intégration d’application.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-169">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-klue-tutorial/attribute.png)

6. <span data-ttu-id="0d4ce-171">Bonjour **attributs utilisateur** section hello **l’authentification unique** boîte de dialogue, configurer des attributs de jeton SAML comme indiqué dans hello précédant l’image et effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="0d4ce-171">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello preceding image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="0d4ce-172">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="0d4ce-172">Attribute Name</span></span>      | <span data-ttu-id="0d4ce-173">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="0d4ce-173">Attribute Value</span></span>      |
    | ------------------- | -------------------- |
    | <span data-ttu-id="0d4ce-174">first_name</span><span class="sxs-lookup"><span data-stu-id="0d4ce-174">first_name</span></span>          | <span data-ttu-id="0d4ce-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="0d4ce-175">user.givenname</span></span> |
    | <span data-ttu-id="0d4ce-176">last_name</span><span class="sxs-lookup"><span data-stu-id="0d4ce-176">last_name</span></span>           | <span data-ttu-id="0d4ce-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="0d4ce-177">user.surname</span></span> |
    | <span data-ttu-id="0d4ce-178">email</span><span class="sxs-lookup"><span data-stu-id="0d4ce-178">email</span></span>               | <span data-ttu-id="0d4ce-179">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="0d4ce-179">user.userprincipalname</span></span>|
    
    <span data-ttu-id="0d4ce-180">a.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-180">a.</span></span> <span data-ttu-id="0d4ce-181">Cliquez sur **ajouter un attribut** tooopen hello **ajouter un attribut** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-181">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-klue-tutorial/tutorial_attribute_04.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-klue-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="0d4ce-184">b.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-184">b.</span></span> <span data-ttu-id="0d4ce-185">Bonjour **nom** zone de texte, nom d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-185">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="0d4ce-186">c.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-186">c.</span></span> <span data-ttu-id="0d4ce-187">À partir de hello **valeur** liste, la valeur d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-187">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="0d4ce-188">d.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-188">d.</span></span> <span data-ttu-id="0d4ce-189">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-189">Click **Ok**.</span></span>

7. <span data-ttu-id="0d4ce-190">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-190">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-klue-tutorial/tutorial_klue_certificate.png) 

8. <span data-ttu-id="0d4ce-192">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="0d4ce-192">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-klue-tutorial/tutorial_general_400.png)
    
9. <span data-ttu-id="0d4ce-194">Sur hello **Klue Configuration** , cliquez sur **Klue de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-194">On hello **Klue Configuration** section, click **Configure Klue** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0d4ce-195">Hello de copie **ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="0d4ce-195">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-klue-tutorial/tutorial_klue_configure.png) 

10. <span data-ttu-id="0d4ce-197">tooconfigure l’authentification unique sur **Klue** côté, vous devez hello toosend téléchargé **Certificate(Base64), SAML Sign-On URL du Service unique et ID d’entité SAML** trop[équipe de support Klue](mailto:support@klue.com).</span><span class="sxs-lookup"><span data-stu-id="0d4ce-197">tooconfigure single sign-on on **Klue** side, you need toosend hello downloaded **Certificate(Base64), SAML Single Sign-On Service URL, and SAML Entity ID** too[Klue support team](mailto:support@klue.com).</span></span>

> [!TIP]
> <span data-ttu-id="0d4ce-198">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="0d4ce-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0d4ce-199">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0d4ce-200">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0d4ce-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0d4ce-201">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d4ce-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="0d4ce-202">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="0d4ce-204">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0d4ce-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0d4ce-205">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-klue-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0d4ce-207">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-klue-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0d4ce-209">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-klue-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0d4ce-211">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="0d4ce-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-klue-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0d4ce-213">a.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-213">a.</span></span> <span data-ttu-id="0d4ce-214">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0d4ce-215">b.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-215">b.</span></span> <span data-ttu-id="0d4ce-216">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0d4ce-217">c.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-217">c.</span></span> <span data-ttu-id="0d4ce-218">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0d4ce-219">d.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-219">d.</span></span> <span data-ttu-id="0d4ce-220">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-220">Click **Create**.</span></span>
 
### <a name="creating-a-klue-test-user"></a><span data-ttu-id="0d4ce-221">Création d’un utilisateur de test Klue</span><span class="sxs-lookup"><span data-stu-id="0d4ce-221">Creating a Klue test user</span></span>

<span data-ttu-id="0d4ce-222">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans Klue.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-222">hello objective of this section is toocreate a user called Britta Simon in Klue.</span></span> <span data-ttu-id="0d4ce-223">Klue prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-223">Klue supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="0d4ce-224">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-224">There is no action item for you in this section.</span></span> <span data-ttu-id="0d4ce-225">Un nouvel utilisateur est créé au cours d’une tentative de tooaccess Klue s’il n’existe pas encore.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-225">A new user is created during an attempt tooaccess Klue if it doesn't exist yet.</span></span>

>[!Note]
><span data-ttu-id="0d4ce-226">Si vous avez besoin de toocreate un utilisateur manuellement, contactez [équipe de support Klue](mailto:support@klue.com).</span><span class="sxs-lookup"><span data-stu-id="0d4ce-226">If you need toocreate a user manually, Contact [Klue support team](mailto:support@klue.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0d4ce-227">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d4ce-227">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0d4ce-228">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooKlue.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKlue.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="0d4ce-230">**tooassign Britta Simon tooKlue, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0d4ce-230">**tooassign Britta Simon tooKlue, perform hello following steps:**</span></span>

1. <span data-ttu-id="0d4ce-231">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-231">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="0d4ce-233">Dans la liste des applications hello, sélectionnez **Klue**.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-233">In hello applications list, select **Klue**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-klue-tutorial/tutorial_klue_app.png) 

3. <span data-ttu-id="0d4ce-235">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="0d4ce-237">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-237">Click **Add** button.</span></span> <span data-ttu-id="0d4ce-238">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="0d4ce-240">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0d4ce-241">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0d4ce-242">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0d4ce-243">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="0d4ce-243">Testing single sign-on</span></span>

<span data-ttu-id="0d4ce-244">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-244">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0d4ce-245">Lorsque vous cliquez sur mosaïque Klue hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Klue application.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-245">When you click hello Klue tile in hello Access Panel, you should get automatically signed-on tooyour Klue application.</span></span>
<span data-ttu-id="0d4ce-246">Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0d4ce-246">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="0d4ce-247">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="0d4ce-247">Additional resources</span></span>

* [<span data-ttu-id="0d4ce-248">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0d4ce-248">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0d4ce-249">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="0d4ce-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-klue-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-klue-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-klue-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-klue-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-klue-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-klue-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-klue-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-klue-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-klue-tutorial/tutorial_general_203.png

