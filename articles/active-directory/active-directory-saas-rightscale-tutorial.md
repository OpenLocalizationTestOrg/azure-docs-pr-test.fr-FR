---
title: "Didacticiel : Intégration d’Azure Active Directory avec RightScale | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Rightscale."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3a8d376d-95fb-4dd7-832a-4fdd4dd7c87c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 53b927804a1e0f895778a164386459a4ea816f98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rightscale"></a><span data-ttu-id="b9d4b-103">Didacticiel : Intégration d’Azure Active Directory avec RightScale</span><span class="sxs-lookup"><span data-stu-id="b9d4b-103">Tutorial: Azure Active Directory integration with Rightscale</span></span>

<span data-ttu-id="b9d4b-104">Dans ce didacticiel, vous apprendrez comment toointegrate Rightscale avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b9d4b-104">In this tutorial, you learn how toointegrate Rightscale with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b9d4b-105">Intégration Rightscale à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="b9d4b-105">Integrating Rightscale with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b9d4b-106">Vous pouvez contrôler dans Azure AD qui a accès tooRightscale</span><span class="sxs-lookup"><span data-stu-id="b9d4b-106">You can control in Azure AD who has access tooRightscale</span></span>
- <span data-ttu-id="b9d4b-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooRightscale (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9d4b-107">You can enable your users tooautomatically get signed-on tooRightscale (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b9d4b-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="b9d4b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b9d4b-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b9d4b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9d4b-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b9d4b-110">Prerequisites</span></span>

<span data-ttu-id="b9d4b-111">tooconfigure intégration d’Azure AD avec Rightscale, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="b9d4b-111">tooconfigure Azure AD integration with Rightscale, you need hello following items:</span></span>

- <span data-ttu-id="b9d4b-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9d4b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b9d4b-113">Un abonnement RightScale pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="b9d4b-113">A Rightscale single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b9d4b-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b9d4b-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="b9d4b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b9d4b-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b9d4b-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b9d4b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b9d4b-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="b9d4b-118">Scenario description</span></span>
<span data-ttu-id="b9d4b-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b9d4b-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="b9d4b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b9d4b-121">Ajout de Rightscale à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="b9d4b-121">Adding Rightscale from hello gallery</span></span>
2. <span data-ttu-id="b9d4b-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9d4b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rightscale-from-hello-gallery"></a><span data-ttu-id="b9d4b-123">Ajout de Rightscale à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="b9d4b-123">Adding Rightscale from hello gallery</span></span>
<span data-ttu-id="b9d4b-124">intégration de hello tooconfigure de Rightscale dans Azure AD, vous devez tooadd Rightscale à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-124">tooconfigure hello integration of Rightscale into Azure AD, you need tooadd Rightscale from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b9d4b-125">**tooadd Rightscale à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b9d4b-125">**tooadd Rightscale from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9d4b-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b9d4b-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b9d4b-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="b9d4b-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="b9d4b-133">Dans la zone de recherche de hello, tapez **Rightscale**.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-133">In hello search box, type **Rightscale**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_search.png)

5. <span data-ttu-id="b9d4b-135">Dans le volet de résultats hello, sélectionnez **Rightscale**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-135">In hello results panel, select **Rightscale**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b9d4b-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9d4b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b9d4b-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec RightScale sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="b9d4b-138">In this section, you configure and test Azure AD single sign-on with Rightscale based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b9d4b-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Rightscale est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Rightscale is tooa user in Azure AD.</span></span> <span data-ttu-id="b9d4b-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Rightscale doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-140">In other words, a link relationship between an Azure AD user and hello related user in Rightscale needs toobe established.</span></span>

<span data-ttu-id="b9d4b-141">Dans Rightscale, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-141">In Rightscale, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b9d4b-142">tooconfigure et test Azure AD l’authentification unique avec Rightscale, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="b9d4b-142">tooconfigure and test Azure AD single sign-on with Rightscale, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b9d4b-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b9d4b-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b9d4b-145">**[Création d’un utilisateur de test Rightscale](#creating-a-rightscale-test-user)**  -toohave un équivalent de Britta Simon dans Rightscale est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-145">**[Creating a Rightscale test user](#creating-a-rightscale-test-user)** - toohave a counterpart of Britta Simon in Rightscale that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b9d4b-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b9d4b-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b9d4b-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9d4b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b9d4b-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Rightscale.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Rightscale application.</span></span>

<span data-ttu-id="b9d4b-150">**tooconfigure Azure AD single sign-on avec Rightscale, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b9d4b-150">**tooconfigure Azure AD single sign-on with Rightscale, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9d4b-151">Bonjour portail Azure, sur hello **Rightscale** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-151">In hello Azure portal, on hello **Rightscale** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="b9d4b-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_samlbase.png)

3. <span data-ttu-id="b9d4b-155">Sur hello **Rightscale domaine et les URL** section, si vous le souhaitez application hello tooconfigure **mode initialisée par IDP** vous n’avez pas tooperform toutes les étapes que l’application hello est déjà pré-intégration à Azure.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-155">On hello **Rightscale Domain and URLs** section, if you wish tooconfigure hello application in **IDP initiated mode** you do not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url.png)

4. <span data-ttu-id="b9d4b-157">Sur hello **Rightscale domaine et les URL** section, si vous le souhaitez application hello tooconfigure **mode initiée par SP**, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="b9d4b-157">On hello **Rightscale Domain and URLs** section, if you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url1.png)

    <span data-ttu-id="b9d4b-159">a.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-159">a.</span></span> <span data-ttu-id="b9d4b-160">Cliquez sur hello **afficher les paramètres d’URL avancés**.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-160">Click on hello **Show advanced URL settings**.</span></span>

    <span data-ttu-id="b9d4b-161">b.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-161">b.</span></span> <span data-ttu-id="b9d4b-162">Bonjour **URL de connexion** zone de texte, tapez l’URL hello :`https://login.rightscale.com/`</span><span class="sxs-lookup"><span data-stu-id="b9d4b-162">In hello **Sign On URL** textbox, type hello URL: `https://login.rightscale.com/`</span></span>

5. <span data-ttu-id="b9d4b-163">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-163">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_certificate.png) 

6. <span data-ttu-id="b9d4b-165">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="b9d4b-165">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-rightscale-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="b9d4b-167">Sur hello **Rightscale Configuration** , cliquez sur **Rightscale de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-167">On hello **Rightscale Configuration** section, click **Configure Rightscale** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b9d4b-168">Hello de copie **ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="b9d4b-168">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    <span data-ttu-id="b9d4b-169">![Configurer l’authentification unique](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="b9d4b-169">![Configure Single Sign-On](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_configure.png) 
<CS></span></span>
8. <span data-ttu-id="b9d4b-170">tooget SSO configuré pour votre application, vous devez locataire de RightScale toosign sur tooyour en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-170">tooget SSO configured for your application, you need toosign-on tooyour RightScale tenant as an administrator.</span></span>

    <span data-ttu-id="b9d4b-171">a.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-171">a.</span></span> <span data-ttu-id="b9d4b-172">Dans le menu hello haut de hello, cliquez sur hello **paramètres** onglet et sélectionnez **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-172">In hello menu on hello top, click hello **Settings** tab and select **Single Sign-On**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_001.png) 

    <span data-ttu-id="b9d4b-174">b.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-174">b.</span></span> <span data-ttu-id="b9d4b-175">Cliquez sur hello »**nouveau**» bouton tooadd **vos fournisseurs d’identité SAML**.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-175">Click hello "**new**" button tooadd **Your SAML Identity Providers**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_002.png) 
 
    <span data-ttu-id="b9d4b-177">c.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-177">c.</span></span> <span data-ttu-id="b9d4b-178">Dans la zone de texte hello de **nom d’affichage**, entrez le nom de votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-178">In hello textbox of **Display Name**, input your company name.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_003.png)
 
    <span data-ttu-id="b9d4b-180">d.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-180">d.</span></span> <span data-ttu-id="b9d4b-181">Sélectionnez **initiées RightScale de permettre à l’aide d’un indicateur de détection** et d’entrée votre **nom de domaine** Bonjour sous la zone de texte.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-181">Select **Allow RightScale-initiated SSO using a discovery hint** and input your **domain name** in hello below textbox.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_004.png)

    <span data-ttu-id="b9d4b-183">e.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-183">e.</span></span> <span data-ttu-id="b9d4b-184">Collez la valeur hello **SAML Sign-On URL du Service unique** dont vous avez copié à partir du portail Azure en **le point de terminaison SAML SSO** dans RightScale.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-184">Paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal into **SAML SSO Endpoint** in RightScale.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_006.png)

    <span data-ttu-id="b9d4b-186">f.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-186">f.</span></span> <span data-ttu-id="b9d4b-187">Collez la valeur hello **ID d’entité SAML** dont vous avez copié à partir du portail Azure en **SAML EntityID** dans RightScale.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-187">Paste hello value of **SAML Entity ID** which you have copied from Azure portal into **SAML EntityID** in RightScale.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_008.png)

    <span data-ttu-id="b9d4b-189">g.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-189">g.</span></span> <span data-ttu-id="b9d4b-190">Cliquez sur **navigateur** bouton tooupload hello certificat que vous avez téléchargé à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-190">Click **Browser** button tooupload hello certificate which you downloaded from Azure portal.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_009.png)

    <span data-ttu-id="b9d4b-192">h.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-192">h.</span></span> <span data-ttu-id="b9d4b-193">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-193">Click **Save**.</span></span>
<CE>
> [!TIP]
> <span data-ttu-id="b9d4b-194">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="b9d4b-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b9d4b-195">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b9d4b-196">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b9d4b-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b9d4b-197">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9d4b-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="b9d4b-198">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="b9d4b-200">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b9d4b-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9d4b-201">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b9d4b-203">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b9d4b-205">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b9d4b-207">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="b9d4b-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b9d4b-209">a.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-209">a.</span></span> <span data-ttu-id="b9d4b-210">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b9d4b-211">b.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-211">b.</span></span> <span data-ttu-id="b9d4b-212">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b9d4b-213">c.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-213">c.</span></span> <span data-ttu-id="b9d4b-214">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b9d4b-215">d.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-215">d.</span></span> <span data-ttu-id="b9d4b-216">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-216">Click **Create**.</span></span>
 
### <a name="creating-a-rightscale-test-user"></a><span data-ttu-id="b9d4b-217">Création d’un utilisateur de test RightScale</span><span class="sxs-lookup"><span data-stu-id="b9d4b-217">Creating a Rightscale test user</span></span>

<span data-ttu-id="b9d4b-218">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans RightScale.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-218">In this section, you create a user called Britta Simon in RightScale.</span></span> <span data-ttu-id="b9d4b-219">Travailler avec [équipe de support Client de Rightscale](mailto:support@rightscale.com) tooadd les utilisateurs de hello dans la plateforme de RightScale hello.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-219">Work with [Rightscale Client support team](mailto:support@rightscale.com) tooadd hello users in hello RightScale platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b9d4b-220">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9d4b-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b9d4b-221">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooRightscale.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRightscale.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="b9d4b-223">**tooassign Britta Simon tooRightscale, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b9d4b-223">**tooassign Britta Simon tooRightscale, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9d4b-224">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="b9d4b-226">Dans la liste des applications hello, sélectionnez **Rightscale**.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-226">In hello applications list, select **Rightscale**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_app.png) 

3. <span data-ttu-id="b9d4b-228">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="b9d4b-230">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-230">Click **Add** button.</span></span> <span data-ttu-id="b9d4b-231">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="b9d4b-233">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b9d4b-234">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b9d4b-235">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b9d4b-236">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="b9d4b-236">Testing single sign-on</span></span>

<span data-ttu-id="b9d4b-237">objectif Hello de cette section est tootest votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-237">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="b9d4b-238">Lorsque vous cliquez sur mosaïque RightScale hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour RightScale application.</span><span class="sxs-lookup"><span data-stu-id="b9d4b-238">When you click hello RightScale tile in hello Access Panel, you should get automatically signed-on tooyour RightScale application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b9d4b-239">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="b9d4b-239">Additional resources</span></span>

* [<span data-ttu-id="b9d4b-240">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b9d4b-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b9d4b-241">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="b9d4b-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_203.png

