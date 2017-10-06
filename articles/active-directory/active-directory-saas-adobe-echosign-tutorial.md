---
title: "Didacticiel : Intégration d’Azure Active Directory à Adobe Sign | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de connexion d’Adobe."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f9385723-8fe7-4340-8afb-1508dac3e92b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: b4b07907f30a0890003554a02a76d968400b43ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-sign"></a><span data-ttu-id="3732c-103">Didacticiel : Intégration d’Azure Active Directory à Adobe Sign</span><span class="sxs-lookup"><span data-stu-id="3732c-103">Tutorial: Azure Active Directory integration with Adobe Sign</span></span>

<span data-ttu-id="3732c-104">Dans ce didacticiel, vous apprendrez comment toointegrate Adobe signer avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3732c-104">In this tutorial, you learn how toointegrate Adobe Sign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3732c-105">Intégration d’Adobe connexion à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="3732c-105">Integrating Adobe Sign with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3732c-106">Vous pouvez contrôler dans Azure AD qui a accès tooAdobe signe</span><span class="sxs-lookup"><span data-stu-id="3732c-106">You can control in Azure AD who has access tooAdobe Sign</span></span>
- <span data-ttu-id="3732c-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooAdobe signe (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="3732c-107">You can enable your users tooautomatically get signed-on tooAdobe Sign (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3732c-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="3732c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3732c-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3732c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3732c-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="3732c-110">Prerequisites</span></span>

<span data-ttu-id="3732c-111">tooconfigure intégration d’Azure AD avec informations d’identification Adobe, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="3732c-111">tooconfigure Azure AD integration with Adobe Sign, you need hello following items:</span></span>

- <span data-ttu-id="3732c-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="3732c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3732c-113">Un abonnement Adobe Sign pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="3732c-113">An Adobe Sign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3732c-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="3732c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3732c-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="3732c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3732c-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="3732c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3732c-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3732c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3732c-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="3732c-118">Scenario description</span></span>
<span data-ttu-id="3732c-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="3732c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3732c-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="3732c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3732c-121">Ajout de l’authentification à partir de la galerie de hello Adobe</span><span class="sxs-lookup"><span data-stu-id="3732c-121">Adding Adobe Sign from hello gallery</span></span>
2. <span data-ttu-id="3732c-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="3732c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adobe-sign-from-hello-gallery"></a><span data-ttu-id="3732c-123">Ajout de l’authentification à partir de la galerie de hello Adobe</span><span class="sxs-lookup"><span data-stu-id="3732c-123">Adding Adobe Sign from hello gallery</span></span>
<span data-ttu-id="3732c-124">tooconfigure hello intégration d’Adobe signe dans Azure AD, vous devez tooadd Adobe signe à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="3732c-124">tooconfigure hello integration of Adobe Sign into Azure AD, you need tooadd Adobe Sign from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3732c-125">**tooadd Adobe de connexion à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="3732c-125">**tooadd Adobe Sign from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3732c-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="3732c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3732c-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="3732c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3732c-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="3732c-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="3732c-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="3732c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="3732c-133">Dans la zone de recherche de hello, tapez **Adobe signe**.</span><span class="sxs-lookup"><span data-stu-id="3732c-133">In hello search box, type **Adobe Sign**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_search.png)

5. <span data-ttu-id="3732c-135">Dans le volet de résultats hello, sélectionnez **Adobe signe**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="3732c-135">In hello results panel, select **Adobe Sign**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3732c-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="3732c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3732c-138">Dans cette section, vous configurez et testez l’authentification unique Azure AD avec Adobe Sign au moyen d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="3732c-138">In this section, you configure and test Azure AD single sign-on with Adobe Sign based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3732c-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Adobe signe est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3732c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Adobe Sign is tooa user in Azure AD.</span></span> <span data-ttu-id="3732c-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Adobe signe doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="3732c-140">In other words, a link relationship between an Azure AD user and hello related user in Adobe Sign needs toobe established.</span></span>

<span data-ttu-id="3732c-141">Dans Adobe signe, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="3732c-141">In Adobe Sign, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3732c-142">tooconfigure et test Azure AD l’authentification unique avec une connexion d’Adobe, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="3732c-142">tooconfigure and test Azure AD single sign-on with Adobe Sign, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3732c-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="3732c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3732c-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3732c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3732c-145">**[Création d’un utilisateur de test de connexion d’Adobe](#creating-an-adobe-sign-test-user)**  -toohave un équivalent de Britta Simon dans Adobe de connexion qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="3732c-145">**[Creating an Adobe Sign test user](#creating-an-adobe-sign-test-user)** - toohave a counterpart of Britta Simon in Adobe Sign that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3732c-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="3732c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3732c-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="3732c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3732c-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="3732c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3732c-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de connexion d’Adobe.</span><span class="sxs-lookup"><span data-stu-id="3732c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Adobe Sign application.</span></span>

<span data-ttu-id="3732c-150">**tooconfigure Azure AD l’authentification unique sur Adobe signe, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="3732c-150">**tooconfigure Azure AD single sign-on with Adobe Sign, perform hello following steps:**</span></span>

1. <span data-ttu-id="3732c-151">Bonjour portail Azure, sur hello **Adobe signe** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="3732c-151">In hello Azure portal, on hello **Adobe Sign** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="3732c-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="3732c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_samlbase.png)

3. <span data-ttu-id="3732c-155">Sur hello **URL et le domaine d’authentification Adobe** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="3732c-155">On hello **Adobe Sign Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_url.png)

    <span data-ttu-id="3732c-157">a.</span><span class="sxs-lookup"><span data-stu-id="3732c-157">a.</span></span> <span data-ttu-id="3732c-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.echosign.com/`</span><span class="sxs-lookup"><span data-stu-id="3732c-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.echosign.com/`</span></span>

    <span data-ttu-id="3732c-159">b.</span><span class="sxs-lookup"><span data-stu-id="3732c-159">b.</span></span> <span data-ttu-id="3732c-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.echosign.com`</span><span class="sxs-lookup"><span data-stu-id="3732c-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.echosign.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3732c-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="3732c-161">These values are not real.</span></span> <span data-ttu-id="3732c-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="3732c-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="3732c-163">Contact [équipe de support Client de connexion d’Adobe](https://helpx.adobe.com/in/contact/support.html) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="3732c-163">Contact [Adobe Sign Client support team](https://helpx.adobe.com/in/contact/support.html) tooget these values.</span></span> 
 
4. <span data-ttu-id="3732c-164">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="3732c-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_certificate.png) 

5. <span data-ttu-id="3732c-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="3732c-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3732c-168">Sur hello **Adobe signe Configuration** , cliquez sur **configurer l’authentification Adobe** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="3732c-168">On hello **Adobe Sign Configuration** section, click **Configure Adobe Sign** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="3732c-169">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="3732c-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_configure.png) 


7. <span data-ttu-id="3732c-171">Dans une fenêtre de navigateur web, ouvrez une session dans le site d’entreprise Adobe signe tooyour en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="3732c-171">In a different web browser window, log in tooyour Adobe Sign company site as an administrator.</span></span>

8. <span data-ttu-id="3732c-172">Dans le menu hello haut de hello, cliquez sur **compte**, puis, dans le volet de navigation hello sur le côté gauche de hello, cliquez sur **paramètres SAML** sous **les paramètres de compte**.</span><span class="sxs-lookup"><span data-stu-id="3732c-172">In hello menu on hello top, click **Account**, and then, in hello navigation pane on hello left side, click **SAML Settings** under **Account Settings**.</span></span>
   
   <span data-ttu-id="3732c-173">![Compte](./media/active-directory-saas-adobe-echosign-tutorial/ic789520.png "Compte")</span><span class="sxs-lookup"><span data-stu-id="3732c-173">![Account](./media/active-directory-saas-adobe-echosign-tutorial/ic789520.png "Account")</span></span>

9. <span data-ttu-id="3732c-174">Dans la section Paramètres SAML de hello, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="3732c-174">In hello SAML Settings section, perform hello following steps:</span></span>
   
   <span data-ttu-id="3732c-175">![Paramètres SAML](./media/active-directory-saas-adobe-echosign-tutorial/ic789521.png "Paramètres SAML")</span><span class="sxs-lookup"><span data-stu-id="3732c-175">![SAML Settings](./media/active-directory-saas-adobe-echosign-tutorial/ic789521.png "SAML Settings")</span></span>
   
   <span data-ttu-id="3732c-176">a.</span><span class="sxs-lookup"><span data-stu-id="3732c-176">a.</span></span> <span data-ttu-id="3732c-177">Pour **SAML Mode** (Mode SAML), sélectionnez **SAML Mandatory** (SAML obligatoire).</span><span class="sxs-lookup"><span data-stu-id="3732c-177">As **SAML Mode**, select **SAML Mandatory**.</span></span>
   
   <span data-ttu-id="3732c-178">b.</span><span class="sxs-lookup"><span data-stu-id="3732c-178">b.</span></span> <span data-ttu-id="3732c-179">Sélectionnez **toolog autoriser les administrateurs de comptes EchoSign à l’aide de leurs informations d’identification EchoSign**.</span><span class="sxs-lookup"><span data-stu-id="3732c-179">Select **Allow EchoSign Account Administrators toolog in using their EchoSign Credentials**.</span></span>
   
   <span data-ttu-id="3732c-180">c.</span><span class="sxs-lookup"><span data-stu-id="3732c-180">c.</span></span> <span data-ttu-id="3732c-181">Pour **User Creation** (Création d’utilisateurs), sélectionnez **Automatically add users authenticated through SAML** (Ajouter automatiquement les utilisateurs authentifiés avec SAML).</span><span class="sxs-lookup"><span data-stu-id="3732c-181">As **User Creation**, select **Automatically add users authenticated through SAML**.</span></span>

10. <span data-ttu-id="3732c-182">Poursuivez en effectuant hello suivant les étapes :</span><span class="sxs-lookup"><span data-stu-id="3732c-182">Move on, performing hello following steps:</span></span>

       <span data-ttu-id="3732c-183">![Paramètres SAML](./media/active-directory-saas-adobe-echosign-tutorial/ic789522.png "Paramètres SAML")</span><span class="sxs-lookup"><span data-stu-id="3732c-183">![SAML Settings](./media/active-directory-saas-adobe-echosign-tutorial/ic789522.png "SAML Settings")</span></span>

    <span data-ttu-id="3732c-184">a.</span><span class="sxs-lookup"><span data-stu-id="3732c-184">a.</span></span> <span data-ttu-id="3732c-185">Coller **ID d’entité SAML**, lequel vous avez copié à partir du portail Azure en hello **IdP Entity ID** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="3732c-185">Paste **SAML Entity ID**, which you have copied from Azure portal into hello **IdP Entity ID** textbox.</span></span>
    
    <span data-ttu-id="3732c-186">b.</span><span class="sxs-lookup"><span data-stu-id="3732c-186">b.</span></span> <span data-ttu-id="3732c-187">Coller **SAML Sign-On URL du Service unique**, lequel vous avez copié à partir du portail Azure en hello **URL de connexion IdP** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="3732c-187">Paste **SAML Single Sign-On Service URL**, which you have copied from Azure portal into hello **IdP Login URL** textbox.</span></span>
   
    <span data-ttu-id="3732c-188">c.</span><span class="sxs-lookup"><span data-stu-id="3732c-188">c.</span></span> <span data-ttu-id="3732c-189">Coller **URL de déconnexion**, lequel vous avez copié à partir du portail Azure en hello **URL de déconnexion IdP** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="3732c-189">Paste **Sign-Out URL**, which you have copied from Azure portal into hello **IdP Logout URL** textbox.</span></span>

    <span data-ttu-id="3732c-190">d.</span><span class="sxs-lookup"><span data-stu-id="3732c-190">d.</span></span> <span data-ttu-id="3732c-191">Ouvrez votre téléchargé **Certificate(Base64)** dans le bloc-notes, hello copie contenu de celui-ci dans le Presse-papiers et collez-la toohello **certificat IdP** zone de texte</span><span class="sxs-lookup"><span data-stu-id="3732c-191">Open your downloaded **Certificate(Base64)** file in notepad, copy hello content of it into your clipboard, and then paste it toohello **IdP Certificate** textbox</span></span>

    <span data-ttu-id="3732c-192">e.</span><span class="sxs-lookup"><span data-stu-id="3732c-192">e.</span></span> <span data-ttu-id="3732c-193">Cliquez sur **Enregistrer les modifications**.</span><span class="sxs-lookup"><span data-stu-id="3732c-193">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="3732c-194">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="3732c-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3732c-195">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="3732c-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3732c-196">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3732c-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3732c-197">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="3732c-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="3732c-198">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="3732c-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="3732c-200">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="3732c-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3732c-201">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="3732c-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3732c-203">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="3732c-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3732c-205">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="3732c-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3732c-207">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="3732c-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3732c-209">a.</span><span class="sxs-lookup"><span data-stu-id="3732c-209">a.</span></span> <span data-ttu-id="3732c-210">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3732c-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3732c-211">b.</span><span class="sxs-lookup"><span data-stu-id="3732c-211">b.</span></span> <span data-ttu-id="3732c-212">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3732c-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3732c-213">c.</span><span class="sxs-lookup"><span data-stu-id="3732c-213">c.</span></span> <span data-ttu-id="3732c-214">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="3732c-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3732c-215">d.</span><span class="sxs-lookup"><span data-stu-id="3732c-215">d.</span></span> <span data-ttu-id="3732c-216">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="3732c-216">Click **Create**.</span></span>
 
### <a name="creating-an-adobe-sign-test-user"></a><span data-ttu-id="3732c-217">Création d’un utilisateur de test Adobe Sign</span><span class="sxs-lookup"><span data-stu-id="3732c-217">Creating an Adobe Sign test user</span></span>

<span data-ttu-id="3732c-218">tooenable Azure AD les utilisateurs toolog dans tooAdobe de connexion, vous devez les configurer dans Adobe signe.</span><span class="sxs-lookup"><span data-stu-id="3732c-218">tooenable Azure AD users toolog in tooAdobe Sign, they must be provisioned into Adobe Sign.</span></span> <span data-ttu-id="3732c-219">Dans les cas de hello du signe d’Adobe, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="3732c-219">In hello case of Adobe Sign, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="3732c-220">Vous pouvez utiliser n’importe quel autre Adobe connexion utilisateur compte outil de création ou API fournie par Adobe signe tooprovision des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="3732c-220">You can use any other Adobe Sign user account creation tools or APIs provided by Adobe Sign tooprovision AAD user accounts.</span></span> 

<span data-ttu-id="3732c-221">**tooprovision un compte d’utilisateur, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="3732c-221">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="3732c-222">Connectez-vous à tooyour **Adobe signe** site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="3732c-222">Log in tooyour **Adobe Sign** company site as administrator.</span></span>

2. <span data-ttu-id="3732c-223">Dans le menu hello haut de hello, cliquez sur **compte**, puis, dans le volet de navigation hello sur le côté gauche de hello, cliquez sur **utilisateurs et groupes**, puis cliquez sur **créer un nouvel utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="3732c-223">In hello menu on hello top, click **Account**, and then, in hello navigation pane on hello left side, click **Users & Groups**, and then, click **Create a new user**.</span></span>
   
   <span data-ttu-id="3732c-224">![Compte](./media/active-directory-saas-adobe-echosign-tutorial/ic789524.png "Compte")</span><span class="sxs-lookup"><span data-stu-id="3732c-224">![Account](./media/active-directory-saas-adobe-echosign-tutorial/ic789524.png "Account")</span></span>
   
3. <span data-ttu-id="3732c-225">Bonjour **créer un nouvel utilisateur** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="3732c-225">In hello **Create New User** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="3732c-226">![Create User](./media/active-directory-saas-adobe-echosign-tutorial/ic789525.png "Create User")</span><span class="sxs-lookup"><span data-stu-id="3732c-226">![Create User](./media/active-directory-saas-adobe-echosign-tutorial/ic789525.png "Create User")</span></span>
   
   <span data-ttu-id="3732c-227">a.</span><span class="sxs-lookup"><span data-stu-id="3732c-227">a.</span></span> <span data-ttu-id="3732c-228">Hello de type **adresse de messagerie**, **prénom**, et **nom** d’un compte AAD valide que vous voulez tooprovision dans hello relatives des zones de texte.</span><span class="sxs-lookup"><span data-stu-id="3732c-228">Type hello **Email Address**, **First Name**, and **Last Name** of a valid AAD account you want tooprovision into hello related textboxes.</span></span>
   
   <span data-ttu-id="3732c-229">b.</span><span class="sxs-lookup"><span data-stu-id="3732c-229">b.</span></span> <span data-ttu-id="3732c-230">Cliquez sur **Create User**.</span><span class="sxs-lookup"><span data-stu-id="3732c-230">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="3732c-231">titulaire du compte Azure Active Directory Hello reçoit un message électronique qui inclut un compte de hello tooconfirm lien avant son activation.</span><span class="sxs-lookup"><span data-stu-id="3732c-231">hello Azure Active Directory account holder receives an email that includes a link tooconfirm hello account before it becomes active.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3732c-232">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="3732c-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3732c-233">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooAdobe signe.</span><span class="sxs-lookup"><span data-stu-id="3732c-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAdobe Sign.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="3732c-235">**tooassign Britta Simon tooAdobe de connexion, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="3732c-235">**tooassign Britta Simon tooAdobe Sign, perform hello following steps:**</span></span>

1. <span data-ttu-id="3732c-236">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="3732c-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="3732c-238">Dans la liste des applications hello, sélectionnez **Adobe signe**.</span><span class="sxs-lookup"><span data-stu-id="3732c-238">In hello applications list, select **Adobe Sign**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_app.png) 

3. <span data-ttu-id="3732c-240">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="3732c-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="3732c-242">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="3732c-242">Click **Add** button.</span></span> <span data-ttu-id="3732c-243">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="3732c-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="3732c-245">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="3732c-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3732c-246">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="3732c-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3732c-247">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="3732c-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3732c-248">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="3732c-248">Testing single sign-on</span></span>

<span data-ttu-id="3732c-249">Lorsque vous cliquez sur hello Adobe signe vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour signer d’Adobe application.</span><span class="sxs-lookup"><span data-stu-id="3732c-249">When you click hello Adobe Sign tile in hello Access Panel, you should get automatically signed-on tooyour Adobe Sign application.</span></span>
<span data-ttu-id="3732c-250">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3732c-250">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3732c-251">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="3732c-251">Additional resources</span></span>

* [<span data-ttu-id="3732c-252">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3732c-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3732c-253">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="3732c-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_203.png

