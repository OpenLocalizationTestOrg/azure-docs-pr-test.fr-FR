---
title: "Didacticiel : Intégration d’Azure Active Directory avec LockPath Keylight | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et LockPath Keylight."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 234a32f1-9f56-4650-9e31-7b38ad734b1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 5485aeb068ba6fbdb4ea9bfc89d401e00c5b1d29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lockpath-keylight"></a><span data-ttu-id="70261-103">Didacticiel : Intégration d’Azure Active Directory avec LockPath Keylight</span><span class="sxs-lookup"><span data-stu-id="70261-103">Tutorial: Azure Active Directory integration with LockPath Keylight</span></span>

<span data-ttu-id="70261-104">Dans ce didacticiel, vous apprendrez comment toointegrate LockPath Keylight avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="70261-104">In this tutorial, you learn how toointegrate LockPath Keylight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="70261-105">Intégration LockPath Keylight à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="70261-105">Integrating LockPath Keylight with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="70261-106">Vous pouvez contrôler dans Azure AD qui a accès tooLockPath Keylight</span><span class="sxs-lookup"><span data-stu-id="70261-106">You can control in Azure AD who has access tooLockPath Keylight</span></span>
- <span data-ttu-id="70261-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooLockPath Keylight (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="70261-107">You can enable your users tooautomatically get signed-on tooLockPath Keylight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="70261-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="70261-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="70261-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="70261-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="70261-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="70261-110">Prerequisites</span></span>

<span data-ttu-id="70261-111">tooconfigure intégration d’Azure AD avec LockPath Keylight, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="70261-111">tooconfigure Azure AD integration with LockPath Keylight, you need hello following items:</span></span>

- <span data-ttu-id="70261-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="70261-112">An Azure AD subscription</span></span>
- <span data-ttu-id="70261-113">Un abonnement LockPath Keylight pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="70261-113">A LockPath Keylight single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="70261-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="70261-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="70261-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="70261-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="70261-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="70261-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="70261-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="70261-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="70261-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="70261-118">Scenario description</span></span>
<span data-ttu-id="70261-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="70261-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="70261-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="70261-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="70261-121">Ajout de LockPath Keylight à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="70261-121">Adding LockPath Keylight from hello gallery</span></span>
2. <span data-ttu-id="70261-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="70261-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lockpath-keylight-from-hello-gallery"></a><span data-ttu-id="70261-123">Ajout de LockPath Keylight à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="70261-123">Adding LockPath Keylight from hello gallery</span></span>
<span data-ttu-id="70261-124">intégration de hello tooconfigure de LockPath Keylight dans Azure AD, vous devez tooadd LockPath Keylight à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="70261-124">tooconfigure hello integration of LockPath Keylight into Azure AD, you need tooadd LockPath Keylight from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="70261-125">**tooadd LockPath Keylight à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="70261-125">**tooadd LockPath Keylight from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="70261-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="70261-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="70261-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="70261-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="70261-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="70261-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="70261-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="70261-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="70261-133">Dans la zone de recherche de hello, tapez **LockPath Keylight**.</span><span class="sxs-lookup"><span data-stu-id="70261-133">In hello search box, type **LockPath Keylight**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_search.png)

5. <span data-ttu-id="70261-135">Dans le volet de résultats hello, sélectionnez **LockPath Keylight**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="70261-135">In hello results panel, select **LockPath Keylight**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="70261-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="70261-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="70261-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec LockPath Keylight sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="70261-138">In this section, you configure and test Azure AD single sign-on with LockPath Keylight based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="70261-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello LockPath Keylight est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70261-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LockPath Keylight is tooa user in Azure AD.</span></span> <span data-ttu-id="70261-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans LockPath Keylight doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="70261-140">In other words, a link relationship between an Azure AD user and hello related user in LockPath Keylight needs toobe established.</span></span>

<span data-ttu-id="70261-141">Dans LockPath Keylight, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="70261-141">In LockPath Keylight, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="70261-142">tooconfigure et test Azure AD l’authentification unique avec LockPath Keylight, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="70261-142">tooconfigure and test Azure AD single sign-on with LockPath Keylight, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="70261-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="70261-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="70261-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="70261-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="70261-145">**[Création d’un utilisateur de test LockPath Keylight](#creating-a-lockpath-keylight-test-user)**  -toohave un équivalent de Britta Simon dans LockPath Keylight qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="70261-145">**[Creating a LockPath Keylight test user](#creating-a-lockpath-keylight-test-user)** - toohave a counterpart of Britta Simon in LockPath Keylight that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="70261-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="70261-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="70261-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="70261-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="70261-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="70261-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="70261-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application LockPath Keylight.</span><span class="sxs-lookup"><span data-stu-id="70261-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LockPath Keylight application.</span></span>

<span data-ttu-id="70261-150">**tooconfigure Azure AD single sign-on avec LockPath Keylight, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="70261-150">**tooconfigure Azure AD single sign-on with LockPath Keylight, perform hello following steps:**</span></span>

1. <span data-ttu-id="70261-151">Bonjour portail Azure, sur hello **LockPath Keylight** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="70261-151">In hello Azure portal, on hello **LockPath Keylight** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="70261-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="70261-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_samlbase.png)

3. <span data-ttu-id="70261-155">Sur hello **LockPath Keylight domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="70261-155">On hello **LockPath Keylight Domain and URLs** section, perform hello following steps::</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_url.png)

    <span data-ttu-id="70261-157">a.</span><span class="sxs-lookup"><span data-stu-id="70261-157">a.</span></span> <span data-ttu-id="70261-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company name>.keylightgrc.com/`</span><span class="sxs-lookup"><span data-stu-id="70261-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.keylightgrc.com/`</span></span>

    <span data-ttu-id="70261-159">b.</span><span class="sxs-lookup"><span data-stu-id="70261-159">b.</span></span> <span data-ttu-id="70261-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company name>.keylightgrc.com`</span><span class="sxs-lookup"><span data-stu-id="70261-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.keylightgrc.com`</span></span>

    <span data-ttu-id="70261-161">c.</span><span class="sxs-lookup"><span data-stu-id="70261-161">c.</span></span> <span data-ttu-id="70261-162">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company name>.keylightgrc.com/Login.aspx`</span><span class="sxs-lookup"><span data-stu-id="70261-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.keylightgrc.com/Login.aspx`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="70261-163">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="70261-163">These values are not real.</span></span> <span data-ttu-id="70261-164">Mettre à jour ces valeurs avec hello réel identificateur, URL de réponse et URL de connexion.</span><span class="sxs-lookup"><span data-stu-id="70261-164">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="70261-165">Contact [équipe de support Client de Keylight LockPath](https://www.lockpath.com/contact/) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="70261-165">Contact [LockPath Keylight Client support team](https://www.lockpath.com/contact/) tooget these values.</span></span> 

4. <span data-ttu-id="70261-166">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Raw)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="70261-166">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_certificate.png) 

5. <span data-ttu-id="70261-168">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="70261-168">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-keylight-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="70261-170">Sur hello **LockPath Keylight Configuration** , cliquez sur **configurer le LockPath Keylight** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="70261-170">On hello **LockPath Keylight Configuration** section, click **Configure LockPath Keylight** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="70261-171">Hello de copie **URL de déconnexion et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="70261-171">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_configure.png) 

7. <span data-ttu-id="70261-173">tooenable SSO dans LockPath Keylight, effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="70261-173">tooenable SSO in LockPath Keylight, perform hello following steps:</span></span>
   
    <span data-ttu-id="70261-174">a.</span><span class="sxs-lookup"><span data-stu-id="70261-174">a.</span></span> <span data-ttu-id="70261-175">Authentification tooyour compte LockPath Keylight en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="70261-175">Sign-on tooyour LockPath Keylight account as administrator.</span></span>
    
    <span data-ttu-id="70261-176">b.</span><span class="sxs-lookup"><span data-stu-id="70261-176">b.</span></span> <span data-ttu-id="70261-177">Dans le menu hello haut de hello, cliquez sur **personne**, puis sélectionnez **Keylight le programme d’installation**.</span><span class="sxs-lookup"><span data-stu-id="70261-177">In hello menu on hello top, click **Person**, and select **Keylight Setup**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-keylight-tutorial/401.png) 

    <span data-ttu-id="70261-179">c.</span><span class="sxs-lookup"><span data-stu-id="70261-179">c.</span></span> <span data-ttu-id="70261-180">Dans le treeview hello sur hello gauche, cliquez sur **SAML**.</span><span class="sxs-lookup"><span data-stu-id="70261-180">In hello treeview on hello left, click **SAML**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-keylight-tutorial/402.png) 

    <span data-ttu-id="70261-182">d.</span><span class="sxs-lookup"><span data-stu-id="70261-182">d.</span></span> <span data-ttu-id="70261-183">Sur hello **paramètres SAML** boîte de dialogue, cliquez sur **modifier**.</span><span class="sxs-lookup"><span data-stu-id="70261-183">On hello **SAML Settings** dialog, click **Edit**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-keylight-tutorial/404.png) 

8. <span data-ttu-id="70261-185">Sur hello **modifier les paramètres SAML** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="70261-185">On hello **Edit SAML Settings** dialog page, perform hello following steps:</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-keylight-tutorial/405.png) 
   
    <span data-ttu-id="70261-187">a.</span><span class="sxs-lookup"><span data-stu-id="70261-187">a.</span></span> <span data-ttu-id="70261-188">Définissez **l’authentification SAML** trop**Active**.</span><span class="sxs-lookup"><span data-stu-id="70261-188">Set **SAML authentication** too**Active**.</span></span>

    <span data-ttu-id="70261-189">b.</span><span class="sxs-lookup"><span data-stu-id="70261-189">b.</span></span> <span data-ttu-id="70261-190">Hello de coller **SAML Sign-On URL du Service unique** valeur sur laquelle vous avez copié à partir de hello portail Azure en hello **Identity Provider Login URL** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="70261-190">Paste hello **SAML Single Sign-On Service URL** value which you have copied from hello Azure portal into hello **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="70261-191">c.</span><span class="sxs-lookup"><span data-stu-id="70261-191">c.</span></span> <span data-ttu-id="70261-192">Hello de coller **URL de Service de déconnexion unique** valeur sur laquelle vous avez copié à partir de hello portail Azure en hello **Identity Provider Logout URL** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="70261-192">Paste hello **Single Sign-Out Service URL** value which you have copied from hello Azure portal into hello **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="70261-193">d.</span><span class="sxs-lookup"><span data-stu-id="70261-193">d.</span></span> <span data-ttu-id="70261-194">Cliquez sur **choisir un fichier** tooselect votre LockPath Keylight téléchargé de certificat, puis cliquez sur **ouvrir** certificat de hello tooupload.</span><span class="sxs-lookup"><span data-stu-id="70261-194">Click **Choose File** tooselect your downloaded LockPath Keylight certificate, and then click **Open** tooupload hello certificate.</span></span>

    <span data-ttu-id="70261-195">e.</span><span class="sxs-lookup"><span data-stu-id="70261-195">e.</span></span> <span data-ttu-id="70261-196">Définissez **emplacement de l’Id d’utilisateur SAML** trop**élément NameIdentifier de l’instruction de sujet hello**.</span><span class="sxs-lookup"><span data-stu-id="70261-196">Set **SAML User Id location** too**NameIdentifier element of hello subject statement**.</span></span>
    
    <span data-ttu-id="70261-197">f.</span><span class="sxs-lookup"><span data-stu-id="70261-197">f.</span></span> <span data-ttu-id="70261-198">Fournir hello **fournisseur de services Keylight** à l’aide de hello modèle : **https://&lt;CompanyName&gt;. keylightgrc.com**.</span><span class="sxs-lookup"><span data-stu-id="70261-198">Provide hello **Keylight Service Provider** using hello following pattern: **https://&lt;CompanyName&gt;.keylightgrc.com**.</span></span>
    
    <span data-ttu-id="70261-199">g.</span><span class="sxs-lookup"><span data-stu-id="70261-199">g.</span></span> <span data-ttu-id="70261-200">Définissez **les utilisateurs de la configuration automatique** trop**Active**.</span><span class="sxs-lookup"><span data-stu-id="70261-200">Set **Auto-provision users** too**Active**.</span></span>

    <span data-ttu-id="70261-201">h.</span><span class="sxs-lookup"><span data-stu-id="70261-201">h.</span></span> <span data-ttu-id="70261-202">Définissez **type de compte de la configuration automatique** trop**utilisateur complet**.</span><span class="sxs-lookup"><span data-stu-id="70261-202">Set **Auto-provision account type** too**Full User**.</span></span>

    <span data-ttu-id="70261-203">i.</span><span class="sxs-lookup"><span data-stu-id="70261-203">i.</span></span> <span data-ttu-id="70261-204">Définissez **Auto-provision security role** (Configuration automatique du rôle de sécurité), sélectionnez **Standard User with SAML** (Utilisateur standard avec SAML).</span><span class="sxs-lookup"><span data-stu-id="70261-204">Set **Auto-provision security role**, select **Standard User with SAML**.</span></span>
    
    <span data-ttu-id="70261-205">j.</span><span class="sxs-lookup"><span data-stu-id="70261-205">j.</span></span> <span data-ttu-id="70261-206">Définissez **Auto-provision security config** (Configuration automatique des paramètres de sécurité), sélectionnez **Standard User Configuration** (Configuration utilisateur standard).</span><span class="sxs-lookup"><span data-stu-id="70261-206">Set **Auto-provision security config**, select **Standard User Configuration**.</span></span>
     
    <span data-ttu-id="70261-207">k.</span><span class="sxs-lookup"><span data-stu-id="70261-207">k.</span></span> <span data-ttu-id="70261-208">Bonjour **attribut Email** zone de texte, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="70261-208">In hello **Email attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
    
    <span data-ttu-id="70261-209">l.</span><span class="sxs-lookup"><span data-stu-id="70261-209">l.</span></span> <span data-ttu-id="70261-210">Bonjour **prénom attribut** zone de texte, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="70261-210">In hello **First name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
    
    <span data-ttu-id="70261-211">m.</span><span class="sxs-lookup"><span data-stu-id="70261-211">m.</span></span> <span data-ttu-id="70261-212">Bonjour **attribut de nom** zone de texte, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="70261-212">In hello **Last name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>
    
    <span data-ttu-id="70261-213">n.</span><span class="sxs-lookup"><span data-stu-id="70261-213">n.</span></span> <span data-ttu-id="70261-214">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="70261-214">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="70261-215">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="70261-215">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="70261-216">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="70261-216">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="70261-217">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="70261-217">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="70261-218">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="70261-218">Creating an Azure AD test user</span></span>
<span data-ttu-id="70261-219">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="70261-219">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="70261-221">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="70261-221">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="70261-222">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="70261-222">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="70261-224">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="70261-224">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="70261-226">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="70261-226">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="70261-228">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="70261-228">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="70261-230">a.</span><span class="sxs-lookup"><span data-stu-id="70261-230">a.</span></span> <span data-ttu-id="70261-231">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="70261-231">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="70261-232">b.</span><span class="sxs-lookup"><span data-stu-id="70261-232">b.</span></span> <span data-ttu-id="70261-233">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="70261-233">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="70261-234">c.</span><span class="sxs-lookup"><span data-stu-id="70261-234">c.</span></span> <span data-ttu-id="70261-235">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="70261-235">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="70261-236">d.</span><span class="sxs-lookup"><span data-stu-id="70261-236">d.</span></span> <span data-ttu-id="70261-237">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="70261-237">Click **Create**.</span></span>
 
### <a name="creating-a-lockpath-keylight-test-user"></a><span data-ttu-id="70261-238">Création d’un utilisateur de test LockPath Keylight</span><span class="sxs-lookup"><span data-stu-id="70261-238">Creating a LockPath Keylight test user</span></span>

<span data-ttu-id="70261-239">Dans cette section, vous allez créer un utilisateur nommé Britta Simon dans LockPath Keylight.</span><span class="sxs-lookup"><span data-stu-id="70261-239">In this section, you create a user called Britta Simon in LockPath Keylight.</span></span> <span data-ttu-id="70261-240">LockPath Keylight prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="70261-240">LockPath Keylight supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="70261-241">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="70261-241">There is no action item for you in this section.</span></span> <span data-ttu-id="70261-242">Un nouvel utilisateur est créé lors de l’accès LockPath Keylight si l’utilisateur de hello n’existe pas encore.</span><span class="sxs-lookup"><span data-stu-id="70261-242">A new user is created when accessing LockPath Keylight if hello user doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="70261-243">Si vous devez manuellement toocreate un utilisateur, vous devez toocontact hello [équipe de support LockPath Keylight Client](https://www.lockpath.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="70261-243">If you need toocreate a user manually, you need toocontact hello [LockPath Keylight Client support team](https://www.lockpath.com/contact/).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="70261-244">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="70261-244">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="70261-245">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooLockPath Keylight.</span><span class="sxs-lookup"><span data-stu-id="70261-245">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLockPath Keylight.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="70261-247">**tooassign Britta Simon tooLockPath Keylight, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="70261-247">**tooassign Britta Simon tooLockPath Keylight, perform hello following steps:**</span></span>

1. <span data-ttu-id="70261-248">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="70261-248">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="70261-250">Dans la liste des applications hello, sélectionnez **LockPath Keylight**.</span><span class="sxs-lookup"><span data-stu-id="70261-250">In hello applications list, select **LockPath Keylight**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_app.png) 

3. <span data-ttu-id="70261-252">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="70261-252">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="70261-254">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="70261-254">Click **Add** button.</span></span> <span data-ttu-id="70261-255">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="70261-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="70261-257">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="70261-257">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="70261-258">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="70261-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="70261-259">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="70261-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="70261-260">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="70261-260">Testing single sign-on</span></span>

<span data-ttu-id="70261-261">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="70261-261">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="70261-262">Lorsque vous cliquez sur hello LockPath Keylight vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour LockPath Keylight application.</span><span class="sxs-lookup"><span data-stu-id="70261-262">When you click hello LockPath Keylight tile in hello Access Panel, you should get automatically signed-on tooyour LockPath Keylight application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="70261-263">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="70261-263">Additional resources</span></span>

* [<span data-ttu-id="70261-264">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="70261-264">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="70261-265">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="70261-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_203.png

