---
title: "Didacticiel : Intégration d’Azure Active Directory à Boomi | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Boomi."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8e05afa9-2eda-4975-a0cc-6d408065860f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: ce64a4561697d311a8c7b1b244315bb552c5cfb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-boomi"></a><span data-ttu-id="7a6f2-103">Didacticiel : Intégration d’Azure Active Directory à Boomi</span><span class="sxs-lookup"><span data-stu-id="7a6f2-103">Tutorial: Azure Active Directory integration with Boomi</span></span>

<span data-ttu-id="7a6f2-104">Dans ce didacticiel, vous apprendrez comment toointegrate Boomi avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7a6f2-104">In this tutorial, you learn how toointegrate Boomi with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7a6f2-105">Intégration de Boomi à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="7a6f2-105">Integrating Boomi with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7a6f2-106">Vous pouvez contrôler dans Azure AD qui a accès tooBoomi</span><span class="sxs-lookup"><span data-stu-id="7a6f2-106">You can control in Azure AD who has access tooBoomi</span></span>
- <span data-ttu-id="7a6f2-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooBoomi (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="7a6f2-107">You can enable your users tooautomatically get signed-on tooBoomi (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7a6f2-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="7a6f2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7a6f2-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7a6f2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a6f2-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7a6f2-110">Prerequisites</span></span>

<span data-ttu-id="7a6f2-111">tooconfigure intégration d’Azure AD à Boomi, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="7a6f2-111">tooconfigure Azure AD integration with Boomi, you need hello following items:</span></span>

- <span data-ttu-id="7a6f2-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="7a6f2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7a6f2-113">Un abonnement Boomi pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="7a6f2-113">A Boomi single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7a6f2-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7a6f2-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="7a6f2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7a6f2-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7a6f2-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7a6f2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7a6f2-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="7a6f2-118">Scenario description</span></span>
<span data-ttu-id="7a6f2-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7a6f2-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="7a6f2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7a6f2-121">Ajout de Boomi à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="7a6f2-121">Adding Boomi from hello gallery</span></span>
2. <span data-ttu-id="7a6f2-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="7a6f2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-boomi-from-hello-gallery"></a><span data-ttu-id="7a6f2-123">Ajout de Boomi à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="7a6f2-123">Adding Boomi from hello gallery</span></span>
<span data-ttu-id="7a6f2-124">intégration de hello tooconfigure de Boomi dans Azure AD, vous devez tooadd Boomi à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-124">tooconfigure hello integration of Boomi into Azure AD, you need tooadd Boomi from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7a6f2-125">**tooadd Boomi à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7a6f2-125">**tooadd Boomi from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7a6f2-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7a6f2-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7a6f2-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="7a6f2-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="7a6f2-133">Dans la zone de recherche de hello, tapez **Boomi**.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-133">In hello search box, type **Boomi**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_search.png)

5. <span data-ttu-id="7a6f2-135">Dans le volet de résultats hello, sélectionnez **Boomi**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-135">In hello results panel, select **Boomi**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7a6f2-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="7a6f2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7a6f2-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Boomi avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="7a6f2-138">In this section, you configure and test Azure AD single sign-on with Boomi based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7a6f2-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Boomi est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Boomi is tooa user in Azure AD.</span></span> <span data-ttu-id="7a6f2-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Boomi doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-140">In other words, a link relationship between an Azure AD user and hello related user in Boomi needs toobe established.</span></span>

<span data-ttu-id="7a6f2-141">En l’occurrence, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-141">In Boomi, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7a6f2-142">tooconfigure et test Azure AD l’authentification unique à Boomi, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="7a6f2-142">tooconfigure and test Azure AD single sign-on with Boomi, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7a6f2-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7a6f2-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7a6f2-145">**[Création d’un utilisateur de test de Boomi](#creating-a-boomi-test-user)**  -toohave un équivalent de Britta Simon dans Boomi est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-145">**[Creating a Boomi test user](#creating-a-boomi-test-user)** - toohave a counterpart of Britta Simon in Boomi that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7a6f2-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7a6f2-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7a6f2-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="7a6f2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7a6f2-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de Boomi.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Boomi application.</span></span>

<span data-ttu-id="7a6f2-150">**tooconfigure Azure AD single sign-on avec Boomi, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7a6f2-150">**tooconfigure Azure AD single sign-on with Boomi, perform hello following steps:**</span></span>

1. <span data-ttu-id="7a6f2-151">Bonjour portail Azure, sur hello **Boomi** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-151">In hello Azure portal, on hello **Boomi** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="7a6f2-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_samlbase.png)

3. <span data-ttu-id="7a6f2-155">Sur hello **Boomi domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="7a6f2-155">On hello **Boomi Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_url.png)

    <span data-ttu-id="7a6f2-157">a.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-157">a.</span></span> <span data-ttu-id="7a6f2-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://platform.boomi.com/sso/<accountname>/saml`</span><span class="sxs-lookup"><span data-stu-id="7a6f2-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://platform.boomi.com/sso/<accountname>/saml`</span></span>

    <span data-ttu-id="7a6f2-159">b.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-159">b.</span></span> <span data-ttu-id="7a6f2-160">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://platform.boomi.com/sso/<accountname>/saml`</span><span class="sxs-lookup"><span data-stu-id="7a6f2-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://platform.boomi.com/sso/<accountname>/saml`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7a6f2-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-161">These values are not real.</span></span> <span data-ttu-id="7a6f2-162">Mettre à jour ces valeurs hello URL d’identificateur et de réponse réelle.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="7a6f2-163">Contact [équipe de support technique de Boomi](https://boomi.com/company/contact/) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-163">Contact [Boomi support team](https://boomi.com/company/contact/) tooget these values.</span></span>

4. <span data-ttu-id="7a6f2-164">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_certificate.png)

4. <span data-ttu-id="7a6f2-166">Application de Boomi attend les assertions SAML hello dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-166">Boomi application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="7a6f2-167">Veuillez configurer hello suivant des revendications pour cette application.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-167">Please configure hello following claims for this application.</span></span> <span data-ttu-id="7a6f2-168">Vous pouvez gérer les valeurs de ces attributs hello depuis hello »**attributs utilisateur**« section sur la page d’intégration d’application.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-168">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="7a6f2-169">Hello suivant capture d’écran montre un exemple de cela.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-169">hello following screenshot shows an example for this.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-boomi-tutorial/tutorial_attribute.png)

5. <span data-ttu-id="7a6f2-171">Bonjour **attributs utilisateur** section hello **l’authentification unique** boîte de dialogue, pour chaque ligne de la table hello ci-dessous, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="7a6f2-171">In hello **User Attributes** section on hello **Single sign-on** dialog, for each row shown in hello table below, perform hello following steps:</span></span>

    | <span data-ttu-id="7a6f2-172">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="7a6f2-172">Attribute Name</span></span> | <span data-ttu-id="7a6f2-173">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="7a6f2-173">Attribute Value</span></span> |
    | -------------- | --------------- |
    | <span data-ttu-id="7a6f2-174">FEDERATION_ID</span><span class="sxs-lookup"><span data-stu-id="7a6f2-174">FEDERATION_ID</span></span> | <span data-ttu-id="7a6f2-175">user.mail</span><span class="sxs-lookup"><span data-stu-id="7a6f2-175">user.mail</span></span> |
    
    <span data-ttu-id="7a6f2-176">a.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-176">a.</span></span> <span data-ttu-id="7a6f2-177">Cliquez sur **ajouter un attribut** tooopen hello **ajouter un attribut** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-177">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_04.png)
    
    ![Configurer l’authentification unique](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="7a6f2-180">b.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-180">b.</span></span> <span data-ttu-id="7a6f2-181">Bonjour **nom** zone de texte, nom d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-181">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="7a6f2-182">c.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-182">c.</span></span> <span data-ttu-id="7a6f2-183">À partir de hello **valeur** liste, la valeur d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-183">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="7a6f2-184">d.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-184">d.</span></span> <span data-ttu-id="7a6f2-185">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-185">Click **Ok**.</span></span>

6. <span data-ttu-id="7a6f2-186">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="7a6f2-186">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-boomi-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="7a6f2-188">Sur hello **Boomi Configuration** , cliquez sur **configurer de Boomi** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-188">On hello **Boomi Configuration** section, click **Configure Boomi** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7a6f2-189">Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="7a6f2-189">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_configure.png) 

8. <span data-ttu-id="7a6f2-191">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Boomi en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-191">In a different web browser window, log into your Boomi company site as an administrator.</span></span> 

9. <span data-ttu-id="7a6f2-192">Accédez trop**nom de la société** et accédez trop**configurer**.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-192">Navigate too**Company Name** and go too**Set up**.</span></span>

10. <span data-ttu-id="7a6f2-193">Cliquez sur hello **Options SSO** onglet et suivez les étapes ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-193">Click hello **SSO Options** tab and perform below steps.</span></span>

    ![Configurer l’authentification unique côté application](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_11.png)

    <span data-ttu-id="7a6f2-195">a.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-195">a.</span></span> <span data-ttu-id="7a6f2-196">Cochez la case **Enable SAML Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-196">Check **Enable SAML Single Sign-On** checkbox.</span></span>

    <span data-ttu-id="7a6f2-197">b.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-197">b.</span></span> <span data-ttu-id="7a6f2-198">Cliquez sur **importation** hello de tooupload téléchargé certificat auprès d’Azure AD trop**certificat de fournisseur d’identité**.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-198">Click **Import** tooupload hello downloaded certificate from Azure AD too**Identity Provider Certificate**.</span></span>
    
    <span data-ttu-id="7a6f2-199">c.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-199">c.</span></span> <span data-ttu-id="7a6f2-200">Bonjour **Identity Provider Login URL** zone de texte, placez la valeur hello **SAML Sign-On URL du Service unique** à partir de la fenêtre de configuration d’application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-200">In hello **Identity Provider Login URL** textbox, put hello value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="7a6f2-201">d.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-201">d.</span></span> <span data-ttu-id="7a6f2-202">Dans **Federation Id Location** (Emplacement ID de fédération), sélectionnez le bouton radio **Federation Id is in FEDERATION_ID Attribute element** (L’ID de fédération se trouve dans l’élément d’attribut FEDERATION_ID).</span><span class="sxs-lookup"><span data-stu-id="7a6f2-202">As **Federation Id Location**, select **Federation Id is in FEDERATION_ID Attribute element** radio button.</span></span> 

    <span data-ttu-id="7a6f2-203">e.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-203">e.</span></span> <span data-ttu-id="7a6f2-204">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="7a6f2-204">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="7a6f2-205">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="7a6f2-205">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7a6f2-206">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-206">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7a6f2-207">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7a6f2-207">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7a6f2-208">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="7a6f2-208">Creating an Azure AD test user</span></span>
<span data-ttu-id="7a6f2-209">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-209">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="7a6f2-211">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7a6f2-211">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7a6f2-212">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-212">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7a6f2-214">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-214">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7a6f2-216">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-216">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7a6f2-218">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="7a6f2-218">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7a6f2-220">a.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-220">a.</span></span> <span data-ttu-id="7a6f2-221">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-221">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7a6f2-222">b.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-222">b.</span></span> <span data-ttu-id="7a6f2-223">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-223">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7a6f2-224">c.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-224">c.</span></span> <span data-ttu-id="7a6f2-225">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-225">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7a6f2-226">d.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-226">d.</span></span> <span data-ttu-id="7a6f2-227">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-227">Click **Create**.</span></span>
 
### <a name="creating-a-boomi-test-user"></a><span data-ttu-id="7a6f2-228">Création d’un utilisateur de test Boomi</span><span class="sxs-lookup"><span data-stu-id="7a6f2-228">Creating a Boomi test user</span></span>

<span data-ttu-id="7a6f2-229">Dans l’ordre tooenable Azure AD les utilisateurs toolog dans tooBoomi, vous devez les configurer dans Boomi.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-229">In order tooenable Azure AD users toolog in tooBoomi, they must be provisioned into Boomi.</span></span> <span data-ttu-id="7a6f2-230">Dans les cas de hello d’occurrence, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-230">In hello case of Boomi, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="7a6f2-231">tooprovision un compte d’utilisateur, effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="7a6f2-231">tooprovision a user account, perform hello following steps:</span></span>

1. <span data-ttu-id="7a6f2-232">Ouvrez une session dans tooyour site d’entreprise Boomi en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-232">Log in tooyour Boomi company site as an administrator.</span></span>

2. <span data-ttu-id="7a6f2-233">Une fois connecté, accédez trop**gestion des utilisateurs** et accédez trop**utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-233">After logging in, navigate too**User Management** and go too**Users**.</span></span>

    <span data-ttu-id="7a6f2-234">![Utilisateurs](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "Utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="7a6f2-234">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "Users")</span></span>

3. <span data-ttu-id="7a6f2-235">Cliquez sur  **+**  icône et hello **rôles d’utilisateur Ajouter/Mettre à jour** boîte de dialogue s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-235">Click **+**  icon and hello **Add/Maintain User Roles** dialog opens.</span></span>

    <span data-ttu-id="7a6f2-236">![Utilisateurs](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "Utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="7a6f2-236">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "Users")</span></span>

    <span data-ttu-id="7a6f2-237">![Utilisateurs](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "Utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="7a6f2-237">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "Users")</span></span>

    <span data-ttu-id="7a6f2-238">a.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-238">a.</span></span> <span data-ttu-id="7a6f2-239">Bonjour **adresse de messagerie utilisateur** par courrier électronique de type hello d’utilisateur de zone de texte, comme BrittaSimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-239">In hello **User e-mail address** textbox, type hello email of user like BrittaSimon@contoso.com.</span></span>
    
    <span data-ttu-id="7a6f2-240">b.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-240">b.</span></span> <span data-ttu-id="7a6f2-241">Bonjour **prénom** type hello premier nom d’utilisateur comme Brian zone de texte.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-241">In hello **First name** textbox, type hello First name of user like Britta.</span></span>

    <span data-ttu-id="7a6f2-242">c.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-242">c.</span></span> <span data-ttu-id="7a6f2-243">Bonjour **nom** zone de texte, type hello nom d’utilisateur comme Simon.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-243">In hello **Last name** textbox, type hello Last name of user like Simon.</span></span>
    
    <span data-ttu-id="7a6f2-244">d.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-244">d.</span></span> <span data-ttu-id="7a6f2-245">Entrez l’utilisateur hello **ID de fédération**.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-245">Enter hello user's **Federation ID**.</span></span> <span data-ttu-id="7a6f2-246">Chaque utilisateur doit avoir un ID de fédération qui identifie de façon unique utilisateur hello dans le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-246">Each user must have a Federation ID that uniquely identifies hello user within hello account.</span></span>
    
    <span data-ttu-id="7a6f2-247">e.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-247">e.</span></span> <span data-ttu-id="7a6f2-248">Affecter hello **utilisateur Standard** utilisateur toohello de rôle.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-248">Assign hello **Standard User** role toohello user.</span></span> <span data-ttu-id="7a6f2-249">N’attribuez pas le rôle d’administrateur hello car qui lui donnent accès atmosphère normal, ainsi que des accès de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-249">Do not assign hello Administrator role because that would give him normal Atmosphere access as well as single sign-on access.</span></span>
    
    <span data-ttu-id="7a6f2-250">f.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-250">f.</span></span> <span data-ttu-id="7a6f2-251">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-251">Click **OK**.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="7a6f2-252">utilisateur de Hello pas reçoit un message de notification accueil contenant un mot de passe qui peut être utilisé toolog dans toohello AtomSphere compte, car son mot de passe est géré via le fournisseur d’identité hello.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-252">hello user will not receive a welcome notification email containing a password that can be used toolog in toohello AtomSphere account because his password is managed through hello identity provider.</span></span> <span data-ttu-id="7a6f2-253">Vous pouvez utiliser n’importe quel autre Boomi utilisateur compte outil de création ou API fournie par Boomi tooprovision des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-253">You may use any other Boomi user account creation tools or APIs provided by Boomi tooprovision AAD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7a6f2-254">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="7a6f2-254">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7a6f2-255">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooBoomi.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-255">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBoomi.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="7a6f2-257">**tooassign Britta Simon tooBoomi, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7a6f2-257">**tooassign Britta Simon tooBoomi, perform hello following steps:**</span></span>

1. <span data-ttu-id="7a6f2-258">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-258">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="7a6f2-260">Dans la liste des applications hello, sélectionnez **Boomi**.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-260">In hello applications list, select **Boomi**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_app.png) 

3. <span data-ttu-id="7a6f2-262">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-262">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="7a6f2-264">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-264">Click **Add** button.</span></span> <span data-ttu-id="7a6f2-265">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-265">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="7a6f2-267">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-267">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7a6f2-268">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-268">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7a6f2-269">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-269">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7a6f2-270">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="7a6f2-270">Testing single sign-on</span></span>

<span data-ttu-id="7a6f2-271">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-271">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7a6f2-272">Lorsque vous cliquez sur mosaïque Boomi hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Boomi application.</span><span class="sxs-lookup"><span data-stu-id="7a6f2-272">When you click hello Boomi tile in hello Access Panel, you should get automatically signed-on tooyour Boomi application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7a6f2-273">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="7a6f2-273">Additional resources</span></span>

* [<span data-ttu-id="7a6f2-274">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7a6f2-274">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7a6f2-275">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="7a6f2-275">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_203.png

