---
title: "Didacticiel : Intégration d’Azure Active Directory à Sprinklr | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Sprinklr."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b33938a1-25a5-484c-8e75-7dc6de2d534d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 14b467c72d4a453ed7ad248eadcdade710f105af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sprinklr"></a><span data-ttu-id="40ec3-103">Didacticiel : Intégration d’Azure Active Directory à Sprinklr</span><span class="sxs-lookup"><span data-stu-id="40ec3-103">Tutorial: Azure Active Directory integration with Sprinklr</span></span>

<span data-ttu-id="40ec3-104">Dans ce didacticiel, vous apprendrez comment toointegrate Sprinklr avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="40ec3-104">In this tutorial, you learn how toointegrate Sprinklr with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="40ec3-105">Intégration de Sprinklr à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="40ec3-105">Integrating Sprinklr with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="40ec3-106">Vous pouvez contrôler dans Azure AD qui a accès tooSprinklr</span><span class="sxs-lookup"><span data-stu-id="40ec3-106">You can control in Azure AD who has access tooSprinklr</span></span>
- <span data-ttu-id="40ec3-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSprinklr (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="40ec3-107">You can enable your users tooautomatically get signed-on tooSprinklr (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="40ec3-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="40ec3-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="40ec3-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="40ec3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="40ec3-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="40ec3-110">Prerequisites</span></span>

<span data-ttu-id="40ec3-111">tooconfigure intégration d’Azure AD à Sprinklr, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="40ec3-111">tooconfigure Azure AD integration with Sprinklr, you need hello following items:</span></span>

- <span data-ttu-id="40ec3-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="40ec3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="40ec3-113">Un abonnement Sprinklr pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="40ec3-113">A Sprinklr single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="40ec3-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="40ec3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="40ec3-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="40ec3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="40ec3-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="40ec3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="40ec3-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="40ec3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="40ec3-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="40ec3-118">Scenario description</span></span>
<span data-ttu-id="40ec3-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="40ec3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="40ec3-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="40ec3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="40ec3-121">Ajout de Sprinklr à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="40ec3-121">Adding Sprinklr from hello gallery</span></span>
2. <span data-ttu-id="40ec3-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="40ec3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sprinklr-from-hello-gallery"></a><span data-ttu-id="40ec3-123">Ajout de Sprinklr à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="40ec3-123">Adding Sprinklr from hello gallery</span></span>
<span data-ttu-id="40ec3-124">intégration de hello tooconfigure de Sprinklr à Azure AD, vous devez tooadd Sprinklr à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="40ec3-124">tooconfigure hello integration of Sprinklr into Azure AD, you need tooadd Sprinklr from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="40ec3-125">**tooadd Sprinklr à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="40ec3-125">**tooadd Sprinklr from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="40ec3-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="40ec3-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="40ec3-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="40ec3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="40ec3-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="40ec3-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="40ec3-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="40ec3-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="40ec3-133">Dans la zone de recherche de hello, tapez **Sprinklr**.</span><span class="sxs-lookup"><span data-stu-id="40ec3-133">In hello search box, type **Sprinklr**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_search.png)

5. <span data-ttu-id="40ec3-135">Dans le volet de résultats hello, sélectionnez **Sprinklr**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="40ec3-135">In hello results panel, select **Sprinklr**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="40ec3-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="40ec3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="40ec3-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Sprinklr, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="40ec3-138">In this section, you configure and test Azure AD single sign-on with Sprinklr based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="40ec3-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Sprinklr est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="40ec3-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Sprinklr is tooa user in Azure AD.</span></span> <span data-ttu-id="40ec3-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans Sprinklr hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="40ec3-140">In other words, a link relationship between an Azure AD user and hello related user in Sprinklr needs toobe established.</span></span>

<span data-ttu-id="40ec3-141">Dans Sprinklr, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="40ec3-141">In Sprinklr, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="40ec3-142">tooconfigure et test Azure AD l’authentification unique à Sprinklr, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="40ec3-142">tooconfigure and test Azure AD single sign-on with Sprinklr, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="40ec3-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="40ec3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="40ec3-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="40ec3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="40ec3-145">**[Création d’un utilisateur de test Sprinklr](#creating-a-sprinklr-test-user)**  -toohave un équivalent de Britta Simon dans Sprinklr est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="40ec3-145">**[Creating a Sprinklr test user](#creating-a-sprinklr-test-user)** - toohave a counterpart of Britta Simon in Sprinklr that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="40ec3-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="40ec3-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="40ec3-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="40ec3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="40ec3-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="40ec3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="40ec3-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Sprinklr.</span><span class="sxs-lookup"><span data-stu-id="40ec3-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Sprinklr application.</span></span>

<span data-ttu-id="40ec3-150">**tooconfigure Azure AD single sign-on avec Sprinklr, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="40ec3-150">**tooconfigure Azure AD single sign-on with Sprinklr, perform hello following steps:**</span></span>

1. <span data-ttu-id="40ec3-151">Bonjour portail Azure, sur hello **Sprinklr** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="40ec3-151">In hello Azure portal, on hello **Sprinklr** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="40ec3-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="40ec3-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_samlbase.png)

3. <span data-ttu-id="40ec3-155">Sur hello **Sprinklr domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="40ec3-155">On hello **Sprinklr Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_url.png)

    <span data-ttu-id="40ec3-157">a.</span><span class="sxs-lookup"><span data-stu-id="40ec3-157">a.</span></span> <span data-ttu-id="40ec3-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.sprinklr.com`</span><span class="sxs-lookup"><span data-stu-id="40ec3-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.sprinklr.com`</span></span>

    <span data-ttu-id="40ec3-159">b.</span><span class="sxs-lookup"><span data-stu-id="40ec3-159">b.</span></span> <span data-ttu-id="40ec3-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.sprinklr.com`</span><span class="sxs-lookup"><span data-stu-id="40ec3-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.sprinklr.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="40ec3-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="40ec3-161">These values are not real.</span></span> <span data-ttu-id="40ec3-162">Mettre à jour la valeur de hello avec hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="40ec3-162">Update hello value with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="40ec3-163">Contact [équipe de support Client de Sprinklr](https://www.sprinklr.com/contact-us/) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="40ec3-163">Contact [Sprinklr Client support team](https://www.sprinklr.com/contact-us/) tooget these values.</span></span> 
 
4. <span data-ttu-id="40ec3-164">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="40ec3-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_certificate.png) 

5. <span data-ttu-id="40ec3-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="40ec3-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sprinklr-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="40ec3-168">Sur hello **Sprinklr Configuration** , cliquez sur **Sprinklr de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="40ec3-168">On hello **Sprinklr Configuration** section, click **Configure Sprinklr** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="40ec3-169">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="40ec3-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

7. <span data-ttu-id="40ec3-170">Dans une fenêtre de navigateur web, ouvrez une session dans le site d’entreprise Sprinklr tooyour en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="40ec3-170">In a different web browser window, log in tooyour Sprinklr company site as an administrator.</span></span>

8. <span data-ttu-id="40ec3-171">Accédez trop**Administration \> paramètres**.</span><span class="sxs-lookup"><span data-stu-id="40ec3-171">Go too**Administration \> Settings**.</span></span>
   
    <span data-ttu-id="40ec3-172">![Administration](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="40ec3-172">![Administration](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administration")</span></span>

9. <span data-ttu-id="40ec3-173">Accédez trop**gérer un partenaire \> l’authentification unique** sur hello volet de gauche.</span><span class="sxs-lookup"><span data-stu-id="40ec3-173">Go too**Manage Partner \> Single Sign** on from hello left pane.</span></span>
   
    <span data-ttu-id="40ec3-174">![Gérer les partenaires](./media/active-directory-saas-sprinklr-tutorial/ic782908.png "Gérer les partenaires")</span><span class="sxs-lookup"><span data-stu-id="40ec3-174">![Manage Partner](./media/active-directory-saas-sprinklr-tutorial/ic782908.png "Manage Partner")</span></span>

10. <span data-ttu-id="40ec3-175">Cliquez sur **+Add Single Sign Ons**.</span><span class="sxs-lookup"><span data-stu-id="40ec3-175">Click **+Add Single Sign Ons**.</span></span>
   
    <span data-ttu-id="40ec3-176">![Authentification unique](./media/active-directory-saas-sprinklr-tutorial/ic782909.png "Authentification unique")</span><span class="sxs-lookup"><span data-stu-id="40ec3-176">![Single Sign-Ons](./media/active-directory-saas-sprinklr-tutorial/ic782909.png "Single Sign-Ons")</span></span>

11. <span data-ttu-id="40ec3-177">Sur hello **Single Sign on** page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="40ec3-177">On hello **Single Sign on** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="40ec3-178">![Authentification unique](./media/active-directory-saas-sprinklr-tutorial/ic782910.png "Authentification unique")</span><span class="sxs-lookup"><span data-stu-id="40ec3-178">![Single Sign-Ons](./media/active-directory-saas-sprinklr-tutorial/ic782910.png "Single Sign-Ons")</span></span>

    <span data-ttu-id="40ec3-179">a.</span><span class="sxs-lookup"><span data-stu-id="40ec3-179">a.</span></span> <span data-ttu-id="40ec3-180">Bonjour **nom** zone de texte, tapez un nom pour votre configuration (par exemple : *WAADSSOTest*).</span><span class="sxs-lookup"><span data-stu-id="40ec3-180">In hello **Name** textbox, type a name for your configuration (for example: *WAADSSOTest*).</span></span>

    <span data-ttu-id="40ec3-181">b.</span><span class="sxs-lookup"><span data-stu-id="40ec3-181">b.</span></span> <span data-ttu-id="40ec3-182">Sélectionnez **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="40ec3-182">Select **Enabled**.</span></span>

    <span data-ttu-id="40ec3-183">c.</span><span class="sxs-lookup"><span data-stu-id="40ec3-183">c.</span></span> <span data-ttu-id="40ec3-184">Sélectionnez **Use new SSO Certificate**.</span><span class="sxs-lookup"><span data-stu-id="40ec3-184">Select **Use new SSO Certificate**.</span></span>
             
    <span data-ttu-id="40ec3-185">e.</span><span class="sxs-lookup"><span data-stu-id="40ec3-185">e.</span></span> <span data-ttu-id="40ec3-186">Ouvrez votre certificat codé en base 64 dans le bloc-notes, hello copie contenu de celui-ci dans le Presse-papiers et le coller ensuite toohello **certificat de fournisseur d’identité** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="40ec3-186">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Identity Provider Certificate** textbox.</span></span>

    <span data-ttu-id="40ec3-187">f.</span><span class="sxs-lookup"><span data-stu-id="40ec3-187">f.</span></span> <span data-ttu-id="40ec3-188">Hello de coller **ID d’entité SAML** valeur sur laquelle vous avez copié à partir du portail Azure en hello **Id d’entité** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="40ec3-188">Paste hello **SAML Entity ID** value which you have copied from Azure Portal into hello **Entity Id** textbox.</span></span>

    <span data-ttu-id="40ec3-189">g.</span><span class="sxs-lookup"><span data-stu-id="40ec3-189">g.</span></span> <span data-ttu-id="40ec3-190">Hello de coller **SAML Sign-On URL du Service unique** valeur sur laquelle vous avez copié à partir du portail Azure en hello **Identity Provider Login URL** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="40ec3-190">Paste hello **SAML Single Sign-On Service URL** value which you have copied from Azure Portal into hello **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="40ec3-191">h.</span><span class="sxs-lookup"><span data-stu-id="40ec3-191">h.</span></span> <span data-ttu-id="40ec3-192">Hello de coller **URL de déconnexion** valeur sur laquelle vous avez copié à partir du portail Azure en hello **Identity Provider Logout URL** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="40ec3-192">Paste hello **Sign-Out URL** value which you have copied from Azure Portal into hello **Identity Provider Logout URL** textbox.</span></span>
     
    <span data-ttu-id="40ec3-193">i.</span><span class="sxs-lookup"><span data-stu-id="40ec3-193">i.</span></span> <span data-ttu-id="40ec3-194">Dans **SAML User ID Type**, sélectionnez **Assertion contains User’s sprinklr.com username**.</span><span class="sxs-lookup"><span data-stu-id="40ec3-194">As **SAML User ID Type**, select **Assertion contains User”s sprinklr.com username**.</span></span>

    <span data-ttu-id="40ec3-195">j.</span><span class="sxs-lookup"><span data-stu-id="40ec3-195">j.</span></span> <span data-ttu-id="40ec3-196">En tant que **emplacement d’ID utilisateur SAML**, sélectionnez **ID d’utilisateur est dans l’élément identificateur de nom de hello Hello Subject statement**.</span><span class="sxs-lookup"><span data-stu-id="40ec3-196">As **SAML User ID Location**, select **User ID is in hello Name Identifier element of hello Subject statement**.</span></span>

    <span data-ttu-id="40ec3-197">k.</span><span class="sxs-lookup"><span data-stu-id="40ec3-197">k.</span></span> <span data-ttu-id="40ec3-198">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="40ec3-198">Click **Save**.</span></span>
       
    <span data-ttu-id="40ec3-199">![SAML](./media/active-directory-saas-sprinklr-tutorial/ic782911.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="40ec3-199">![SAML](./media/active-directory-saas-sprinklr-tutorial/ic782911.png "SAML")</span></span>

> [!TIP]
> <span data-ttu-id="40ec3-200">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="40ec3-200">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="40ec3-201">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="40ec3-201">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="40ec3-202">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="40ec3-202">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="40ec3-203">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="40ec3-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="40ec3-204">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="40ec3-204">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="40ec3-206">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="40ec3-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="40ec3-207">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="40ec3-207">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="40ec3-209">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="40ec3-209">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="40ec3-211">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="40ec3-211">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="40ec3-213">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="40ec3-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="40ec3-215">a.</span><span class="sxs-lookup"><span data-stu-id="40ec3-215">a.</span></span> <span data-ttu-id="40ec3-216">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="40ec3-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="40ec3-217">b.</span><span class="sxs-lookup"><span data-stu-id="40ec3-217">b.</span></span> <span data-ttu-id="40ec3-218">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="40ec3-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="40ec3-219">c.</span><span class="sxs-lookup"><span data-stu-id="40ec3-219">c.</span></span> <span data-ttu-id="40ec3-220">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="40ec3-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="40ec3-221">d.</span><span class="sxs-lookup"><span data-stu-id="40ec3-221">d.</span></span> <span data-ttu-id="40ec3-222">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="40ec3-222">Click **Create**.</span></span>
 
### <a name="creating-a-sprinklr-test-user"></a><span data-ttu-id="40ec3-223">Création d’un utilisateur de test Sprinklr</span><span class="sxs-lookup"><span data-stu-id="40ec3-223">Creating a Sprinklr test user</span></span>

1. <span data-ttu-id="40ec3-224">Ouvrez une session dans tooyour site d’entreprise Sprinklr en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="40ec3-224">Log in tooyour Sprinklr company site as an administrator.</span></span>

2. <span data-ttu-id="40ec3-225">Accédez trop**Administration \> paramètres**.</span><span class="sxs-lookup"><span data-stu-id="40ec3-225">Go too**Administration \> Settings**.</span></span>
   
    <span data-ttu-id="40ec3-226">![Administration](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="40ec3-226">![Administration](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administration")</span></span>

3. <span data-ttu-id="40ec3-227">Accédez trop**gérer le Client \> utilisateurs** hello volet de gauche.</span><span class="sxs-lookup"><span data-stu-id="40ec3-227">Go too**Manage Client \> Users** from hello left pane.</span></span>
   
    <span data-ttu-id="40ec3-228">![Paramètres](./media/active-directory-saas-sprinklr-tutorial/ic782914.png "Paramètres")</span><span class="sxs-lookup"><span data-stu-id="40ec3-228">![Settings](./media/active-directory-saas-sprinklr-tutorial/ic782914.png "Settings")</span></span>

4. <span data-ttu-id="40ec3-229">Cliquez sur **Add User**.</span><span class="sxs-lookup"><span data-stu-id="40ec3-229">Click **Add User**.</span></span>
   
    <span data-ttu-id="40ec3-230">![Paramètres](./media/active-directory-saas-sprinklr-tutorial/ic782915.png "Paramètres")</span><span class="sxs-lookup"><span data-stu-id="40ec3-230">![Settings](./media/active-directory-saas-sprinklr-tutorial/ic782915.png "Settings")</span></span>

5. <span data-ttu-id="40ec3-231">Sur hello **modifier l’utilisateur** boîte de dialogue, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="40ec3-231">On hello **Edit user** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="40ec3-232">![Modifier l’utilisateur](./media/active-directory-saas-sprinklr-tutorial/ic782916.png "Modifier l’utilisateur")</span><span class="sxs-lookup"><span data-stu-id="40ec3-232">![Edit user](./media/active-directory-saas-sprinklr-tutorial/ic782916.png "Edit user")</span></span> 

    <span data-ttu-id="40ec3-233">a.</span><span class="sxs-lookup"><span data-stu-id="40ec3-233">a.</span></span> <span data-ttu-id="40ec3-234">Bonjour **messagerie**, **prénom** et **nom** zones de texte, de type hello d’informations d’un compte d’utilisateur Azure AD vous souhaitez tooprovision.</span><span class="sxs-lookup"><span data-stu-id="40ec3-234">In hello **Email**, **First Name** and **Last Name** textboxes, type hello information of an Azure AD user account you want tooprovision.</span></span>

    <span data-ttu-id="40ec3-235">b.</span><span class="sxs-lookup"><span data-stu-id="40ec3-235">b.</span></span> <span data-ttu-id="40ec3-236">Sélectionnez **Password Disabled**.</span><span class="sxs-lookup"><span data-stu-id="40ec3-236">Select **Password Disabled**.</span></span>

    <span data-ttu-id="40ec3-237">c.</span><span class="sxs-lookup"><span data-stu-id="40ec3-237">c.</span></span> <span data-ttu-id="40ec3-238">Sélectionner une **Langue**.</span><span class="sxs-lookup"><span data-stu-id="40ec3-238">Select **Language**.</span></span>

    <span data-ttu-id="40ec3-239">d.</span><span class="sxs-lookup"><span data-stu-id="40ec3-239">d.</span></span> <span data-ttu-id="40ec3-240">Sélectionnez un **Type d’utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="40ec3-240">Select **User Type**.</span></span>

    <span data-ttu-id="40ec3-241">e.</span><span class="sxs-lookup"><span data-stu-id="40ec3-241">e.</span></span> <span data-ttu-id="40ec3-242">Cliquez sur **Update**.</span><span class="sxs-lookup"><span data-stu-id="40ec3-242">Click **Update**.</span></span>
   
     >[!IMPORTANT]
     ><span data-ttu-id="40ec3-243">**Mot de passe désactivé** doit être sélectionné tooenable un toolog utilisateur dans via un fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="40ec3-243">**Password Disabled** must be selected tooenable a user toolog in via an Identity provider.</span></span> 
     
6. <span data-ttu-id="40ec3-244">Accédez trop**rôle**, puis exécutez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="40ec3-244">Go too**Role**, and then perform hello following steps:</span></span>
   
    <span data-ttu-id="40ec3-245">![Rôles de partenaires](./media/active-directory-saas-sprinklr-tutorial/ic782917.png "Rôles de partenaires")</span><span class="sxs-lookup"><span data-stu-id="40ec3-245">![Partner Roles](./media/active-directory-saas-sprinklr-tutorial/ic782917.png "Partner Roles")</span></span>

    <span data-ttu-id="40ec3-246">a.</span><span class="sxs-lookup"><span data-stu-id="40ec3-246">a.</span></span> <span data-ttu-id="40ec3-247">À partir de hello **Global** liste, sélectionnez **tous les\_autorisations**.</span><span class="sxs-lookup"><span data-stu-id="40ec3-247">From hello **Global** list, select **ALL\_Permissions**.</span></span>  

    <span data-ttu-id="40ec3-248">b.</span><span class="sxs-lookup"><span data-stu-id="40ec3-248">b.</span></span> <span data-ttu-id="40ec3-249">Cliquez sur **Update**.</span><span class="sxs-lookup"><span data-stu-id="40ec3-249">Click **Update**.</span></span>

>[!NOTE]
><span data-ttu-id="40ec3-250">Vous pouvez utiliser n’importe quel autre Sprinklr utilisateur compte outil de création ou API fournie par Sprinklr tooprovision comptes d’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="40ec3-250">You can use any other Sprinklr user account creation tools or APIs provided by Sprinklr tooprovision Azure AD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="40ec3-251">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="40ec3-251">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="40ec3-252">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooSprinklr.</span><span class="sxs-lookup"><span data-stu-id="40ec3-252">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSprinklr.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="40ec3-254">**tooassign Britta Simon tooSprinklr, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="40ec3-254">**tooassign Britta Simon tooSprinklr, perform hello following steps:**</span></span>

1. <span data-ttu-id="40ec3-255">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="40ec3-255">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="40ec3-257">Dans la liste des applications hello, sélectionnez **Sprinklr**.</span><span class="sxs-lookup"><span data-stu-id="40ec3-257">In hello applications list, select **Sprinklr**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_app.png) 

3. <span data-ttu-id="40ec3-259">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="40ec3-259">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="40ec3-261">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="40ec3-261">Click **Add** button.</span></span> <span data-ttu-id="40ec3-262">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="40ec3-262">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="40ec3-264">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="40ec3-264">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="40ec3-265">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="40ec3-265">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="40ec3-266">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="40ec3-266">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="40ec3-267">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="40ec3-267">Testing single sign-on</span></span>

<span data-ttu-id="40ec3-268">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="40ec3-268">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="40ec3-269">Lorsque vous cliquez sur mosaïque Sprinklr hello hello volet d’accès, vous devez obtenir application Sprinklr d’automatiquement signé sur tooyour pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="40ec3-269">When you click hello Sprinklr tile in hello Access Panel, you should get automatically signed-on tooyour Sprinklr application For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="40ec3-270">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="40ec3-270">Additional resources</span></span>

* [<span data-ttu-id="40ec3-271">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="40ec3-271">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="40ec3-272">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="40ec3-272">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_203.png

