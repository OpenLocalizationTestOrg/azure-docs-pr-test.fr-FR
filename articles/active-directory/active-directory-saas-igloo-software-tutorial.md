---
title: "Didacticiel : Intégration d’Azure Active Directory avec Igloo Software | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Igloo Software."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2eb625c1-d3fc-4ae1-a304-6a6733a10e6e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 406405d4faa6e56f1005a61e69a29ef2ef2eb34b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-igloo-software"></a><span data-ttu-id="016d2-103">Didacticiel : Intégration d’Azure Active Directory avec Igloo Software</span><span class="sxs-lookup"><span data-stu-id="016d2-103">Tutorial: Azure Active Directory integration with Igloo Software</span></span>

<span data-ttu-id="016d2-104">Dans ce didacticiel, vous apprendrez comment toointegrate Igloo Software avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="016d2-104">In this tutorial, you learn how toointegrate Igloo Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="016d2-105">Intégration de Igloo Software à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="016d2-105">Integrating Igloo Software with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="016d2-106">Vous pouvez contrôler dans Azure AD qui a accès tooIgloo logiciel</span><span class="sxs-lookup"><span data-stu-id="016d2-106">You can control in Azure AD who has access tooIgloo Software</span></span>
- <span data-ttu-id="016d2-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooIgloo logiciels (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="016d2-107">You can enable your users tooautomatically get signed-on tooIgloo Software (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="016d2-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="016d2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="016d2-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="016d2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="016d2-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="016d2-110">Prerequisites</span></span>

<span data-ttu-id="016d2-111">tooconfigure intégration d’Azure AD à Igloo Software, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="016d2-111">tooconfigure Azure AD integration with Igloo Software, you need hello following items:</span></span>

- <span data-ttu-id="016d2-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="016d2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="016d2-113">Un abonnement Igloo Software pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="016d2-113">An Igloo Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="016d2-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="016d2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="016d2-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="016d2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="016d2-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="016d2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="016d2-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="016d2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="016d2-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="016d2-118">Scenario description</span></span>
<span data-ttu-id="016d2-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="016d2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="016d2-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="016d2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="016d2-121">Ajout de Igloo Software à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="016d2-121">Adding Igloo Software from hello gallery</span></span>
2. <span data-ttu-id="016d2-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="016d2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-igloo-software-from-hello-gallery"></a><span data-ttu-id="016d2-123">Ajout de Igloo Software à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="016d2-123">Adding Igloo Software from hello gallery</span></span>
<span data-ttu-id="016d2-124">intégration de hello tooconfigure de Igloo Software dans Azure AD, vous devez tooadd Igloo Software à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="016d2-124">tooconfigure hello integration of Igloo Software into Azure AD, you need tooadd Igloo Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="016d2-125">**tooadd Igloo Software à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="016d2-125">**tooadd Igloo Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="016d2-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="016d2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="016d2-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="016d2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="016d2-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="016d2-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="016d2-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="016d2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="016d2-133">Dans la zone de recherche de hello, tapez **Igloo Software**.</span><span class="sxs-lookup"><span data-stu-id="016d2-133">In hello search box, type **Igloo Software**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_search.png)

5. <span data-ttu-id="016d2-135">Dans le volet de résultats hello, sélectionnez **Igloo Software**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="016d2-135">In hello results panel, select **Igloo Software**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="016d2-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="016d2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="016d2-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Igloo Software à l’aide d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="016d2-138">In this section, you configure and test Azure AD single sign-on with Igloo Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="016d2-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello Igloo Software est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="016d2-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Igloo Software is tooa user in Azure AD.</span></span> <span data-ttu-id="016d2-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Igloo Software doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="016d2-140">In other words, a link relationship between an Azure AD user and hello related user in Igloo Software needs toobe established.</span></span>

<span data-ttu-id="016d2-141">Dans Igloo Software, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="016d2-141">In Igloo Software, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="016d2-142">tooconfigure et test Azure AD l’authentification unique à Igloo Software, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="016d2-142">tooconfigure and test Azure AD single sign-on with Igloo Software, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="016d2-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="016d2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="016d2-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="016d2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="016d2-145">**[Création d’un utilisateur de test de Igloo Software](#creating-an-igloo-software-test-user)**  -toohave un équivalent de Britta Simon dans Igloo Software qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="016d2-145">**[Creating an Igloo Software test user](#creating-an-igloo-software-test-user)** - toohave a counterpart of Britta Simon in Igloo Software that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="016d2-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="016d2-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="016d2-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="016d2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="016d2-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="016d2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="016d2-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Igloo Software.</span><span class="sxs-lookup"><span data-stu-id="016d2-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Igloo Software application.</span></span>

<span data-ttu-id="016d2-150">**tooconfigure Azure AD single sign-on avec Igloo Software, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="016d2-150">**tooconfigure Azure AD single sign-on with Igloo Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="016d2-151">Bonjour portail Azure, sur hello **Igloo Software** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="016d2-151">In hello Azure portal, on hello **Igloo Software** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="016d2-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="016d2-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_samlbase.png)

3. <span data-ttu-id="016d2-155">Sur hello **Igloo Software domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="016d2-155">On hello **Igloo Software Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_url.png)
    
    <span data-ttu-id="016d2-157">a.</span><span class="sxs-lookup"><span data-stu-id="016d2-157">a.</span></span> <span data-ttu-id="016d2-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company name>.igloocommmunities.com`</span><span class="sxs-lookup"><span data-stu-id="016d2-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.igloocommmunities.com`</span></span>

    <span data-ttu-id="016d2-159">b.</span><span class="sxs-lookup"><span data-stu-id="016d2-159">b.</span></span> <span data-ttu-id="016d2-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company name>.igloocommmunities.com/saml.digest`</span><span class="sxs-lookup"><span data-stu-id="016d2-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.igloocommmunities.com/saml.digest`</span></span>

    <span data-ttu-id="016d2-161">c.</span><span class="sxs-lookup"><span data-stu-id="016d2-161">c.</span></span> <span data-ttu-id="016d2-162">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company name>.igloocommmunities.com/saml.digest`</span><span class="sxs-lookup"><span data-stu-id="016d2-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.igloocommmunities.com/saml.digest`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="016d2-163">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="016d2-163">These values are not real.</span></span> <span data-ttu-id="016d2-164">Mettre à jour ces valeurs avec hello réel identificateur, URL de réponse et URL de connexion.</span><span class="sxs-lookup"><span data-stu-id="016d2-164">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="016d2-165">Contact [équipe de support Client de Igloo Software](https://www.igloosoftware.com/services/support) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="016d2-165">Contact [Igloo Software Client support team](https://www.igloosoftware.com/services/support) tooget these values.</span></span> 

4. <span data-ttu-id="016d2-166">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="016d2-166">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_certificate.png) 

5. <span data-ttu-id="016d2-168">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="016d2-168">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-igloo-software-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="016d2-170">Sur hello **Igloo Software Configuration** , cliquez sur **configurer Igloo Software** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="016d2-170">On hello **Igloo Software Configuration** section, click **Configure Igloo Software** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="016d2-171">Hello de copie **URL de déconnexion et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="016d2-171">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_configure.png) 

7. <span data-ttu-id="016d2-173">Dans une fenêtre de navigateur web, ouvrez une session dans le site d’entreprise Igloo Software tooyour en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="016d2-173">In a different web browser window, log in tooyour Igloo Software company site as an administrator.</span></span>

8. <span data-ttu-id="016d2-174">Accédez toohello **le panneau de configuration**.</span><span class="sxs-lookup"><span data-stu-id="016d2-174">Go toohello **Control Panel**.</span></span>
   
     <span data-ttu-id="016d2-175">![Control Panel (Panneau de configuration)](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "Control Panel (Panneau de configuration)")</span><span class="sxs-lookup"><span data-stu-id="016d2-175">![Control Panel](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "Control Panel")</span></span>

9. <span data-ttu-id="016d2-176">Bonjour **appartenance** , cliquez sur **paramètres de connexion**.</span><span class="sxs-lookup"><span data-stu-id="016d2-176">In hello **Membership** tab, click **Sign In Settings**.</span></span>
   
    <span data-ttu-id="016d2-177">![Sign in Settings (Paramètres de connexion)](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "Sign in Settings (Paramètres de connexion)")</span><span class="sxs-lookup"><span data-stu-id="016d2-177">![Sign in Settings](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "Sign in Settings")</span></span>

10. <span data-ttu-id="016d2-178">Dans la section de Configuration de SAML de hello, cliquez sur **configurer l’authentification SAML**.</span><span class="sxs-lookup"><span data-stu-id="016d2-178">In hello SAML Configuration section, click **Configure SAML Authentication**.</span></span>
   
    <span data-ttu-id="016d2-179">![Configuration SAML](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "Configuration SAML")</span><span class="sxs-lookup"><span data-stu-id="016d2-179">![SAML Configuration](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "SAML Configuration")</span></span>
   
11. <span data-ttu-id="016d2-180">Bonjour **Configuration générale** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="016d2-180">In hello **General Configuration** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="016d2-181">![General Configuration (Configuration générale)](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "General Configuration (Configuration générale)")</span><span class="sxs-lookup"><span data-stu-id="016d2-181">![General Configuration](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "General Configuration")</span></span>

    <span data-ttu-id="016d2-182">a.</span><span class="sxs-lookup"><span data-stu-id="016d2-182">a.</span></span> <span data-ttu-id="016d2-183">Bonjour **nom de la connexion** zone de texte, tapez un nom personnalisé pour votre configuration.</span><span class="sxs-lookup"><span data-stu-id="016d2-183">In hello **Connection Name** textbox, type a custom name for your configuration.</span></span>
   
    <span data-ttu-id="016d2-184">b.</span><span class="sxs-lookup"><span data-stu-id="016d2-184">b.</span></span> <span data-ttu-id="016d2-185">Bonjour **URL de connexion IdP** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="016d2-185">In hello **IdP Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="016d2-186">c.</span><span class="sxs-lookup"><span data-stu-id="016d2-186">c.</span></span> <span data-ttu-id="016d2-187">Bonjour **URL de déconnexion IdP** zone de texte, valeur hello coller **URL de déconnexion** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="016d2-187">In hello **IdP Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="016d2-188">d.</span><span class="sxs-lookup"><span data-stu-id="016d2-188">d.</span></span> <span data-ttu-id="016d2-189">Pour **Logout Response and Request HTTP Type** (Type de réponse de déconnexion et de requête HTTP), sélectionnez **POST**.</span><span class="sxs-lookup"><span data-stu-id="016d2-189">Select **Logout Response and Request HTTP Type** as **POST**.</span></span>
   
    <span data-ttu-id="016d2-190">e.</span><span class="sxs-lookup"><span data-stu-id="016d2-190">e.</span></span> <span data-ttu-id="016d2-191">Ouvrez votre **base-64** certificat dans le bloc-notes téléchargé à partir du portail Azure, hello copie contenu de celui-ci dans le Presse-papiers et le coller ensuite toohello **certificat Public** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="016d2-191">Open your **base-64** encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **Public Certificate** textbox.</span></span>
    
12. <span data-ttu-id="016d2-192">Bonjour **réponse et la Configuration de l’authentification**, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="016d2-192">In hello **Response and Authentication Configuration**, perform hello following steps:</span></span>
    
    <span data-ttu-id="016d2-193">![Response and Authentication Configuration (Configuration de la réponse et de l’authentification)](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "Response and Authentication Configuration (Configuration de la réponse et de l’authentification)")</span><span class="sxs-lookup"><span data-stu-id="016d2-193">![Response and Authentication Configuration](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "Response and Authentication Configuration")</span></span>
  
      <span data-ttu-id="016d2-194">a.</span><span class="sxs-lookup"><span data-stu-id="016d2-194">a.</span></span> <span data-ttu-id="016d2-195">Pour **Fournisseur d’identité**, sélectionnez **Microsoft ADFS**.</span><span class="sxs-lookup"><span data-stu-id="016d2-195">As **Identity Provider**, select **Microsoft ADFS**.</span></span>
      
      <span data-ttu-id="016d2-196">b.</span><span class="sxs-lookup"><span data-stu-id="016d2-196">b.</span></span> <span data-ttu-id="016d2-197">Pour **Type d’identificateur**, sélectionnez **Adresse de messagerie**.</span><span class="sxs-lookup"><span data-stu-id="016d2-197">As **Identifier Type**, select **Email Address**.</span></span> 

      <span data-ttu-id="016d2-198">c.</span><span class="sxs-lookup"><span data-stu-id="016d2-198">c.</span></span> <span data-ttu-id="016d2-199">Bonjour **attribut Email** zone de texte, type **emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="016d2-199">In hello **Email Attribute** textbox, type **emailaddress**.</span></span>

      <span data-ttu-id="016d2-200">d.</span><span class="sxs-lookup"><span data-stu-id="016d2-200">d.</span></span> <span data-ttu-id="016d2-201">Bonjour **prénom attribut** zone de texte, type **givenname**.</span><span class="sxs-lookup"><span data-stu-id="016d2-201">In hello **First Name Attribute** textbox, type **givenname**.</span></span>

      <span data-ttu-id="016d2-202">e.</span><span class="sxs-lookup"><span data-stu-id="016d2-202">e.</span></span> <span data-ttu-id="016d2-203">Bonjour **attribut de nom** zone de texte, type **surname**.</span><span class="sxs-lookup"><span data-stu-id="016d2-203">In hello **Last Name Attribute** textbox, type **surname**.</span></span>

13. <span data-ttu-id="016d2-204">Effectuez hello étapes toocomplete hello configuration suivante :</span><span class="sxs-lookup"><span data-stu-id="016d2-204">Perform hello following steps toocomplete hello configuration:</span></span>
    
    <span data-ttu-id="016d2-205">![Création d’utilisateurs à l’authentification](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "Création d’utilisateurs à l’authentification")</span><span class="sxs-lookup"><span data-stu-id="016d2-205">![User creation on Sign in](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "User creation on Sign in")</span></span> 

     <span data-ttu-id="016d2-206">a.</span><span class="sxs-lookup"><span data-stu-id="016d2-206">a.</span></span> <span data-ttu-id="016d2-207">Pour **Création d’utilisateurs à l’authentification**, sélectionnez **Create a new user in your site when they sign in** (Créer un nouvel utilisateur sur votre site au moment de la connexion).</span><span class="sxs-lookup"><span data-stu-id="016d2-207">As **User creation on Sign in**, select **Create a new user in your site when they sign in**.</span></span>

     <span data-ttu-id="016d2-208">b.</span><span class="sxs-lookup"><span data-stu-id="016d2-208">b.</span></span> <span data-ttu-id="016d2-209">Pour **Paramètres de connexion**, sélectionnez **Use SAML button on “Sign in” screen** (Utiliser le bouton SAML sur l’écran de connexion).</span><span class="sxs-lookup"><span data-stu-id="016d2-209">As **Sign in Settings**, select **Use SAML button on “Sign in” screen**.</span></span>

     <span data-ttu-id="016d2-210">c.</span><span class="sxs-lookup"><span data-stu-id="016d2-210">c.</span></span> <span data-ttu-id="016d2-211">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="016d2-211">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="016d2-212">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="016d2-212">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="016d2-213">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="016d2-213">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="016d2-214">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="016d2-214">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="016d2-215">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="016d2-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="016d2-216">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="016d2-216">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="016d2-218">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="016d2-218">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="016d2-219">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="016d2-219">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="016d2-221">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="016d2-221">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="016d2-223">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="016d2-223">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="016d2-225">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="016d2-225">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="016d2-227">a.</span><span class="sxs-lookup"><span data-stu-id="016d2-227">a.</span></span> <span data-ttu-id="016d2-228">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="016d2-228">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="016d2-229">b.</span><span class="sxs-lookup"><span data-stu-id="016d2-229">b.</span></span> <span data-ttu-id="016d2-230">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="016d2-230">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="016d2-231">c.</span><span class="sxs-lookup"><span data-stu-id="016d2-231">c.</span></span> <span data-ttu-id="016d2-232">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="016d2-232">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="016d2-233">d.</span><span class="sxs-lookup"><span data-stu-id="016d2-233">d.</span></span> <span data-ttu-id="016d2-234">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="016d2-234">Click **Create**.</span></span>
 
### <a name="creating-an-igloo-software-test-user"></a><span data-ttu-id="016d2-235">Création d’un utilisateur de test Igloo Software</span><span class="sxs-lookup"><span data-stu-id="016d2-235">Creating an Igloo Software test user</span></span>

<span data-ttu-id="016d2-236">Il n’existe aucun élément d’action pour l’utilisateur tooconfigure vous tooIgloo logiciel de configuration.</span><span class="sxs-lookup"><span data-stu-id="016d2-236">There is no action item for you tooconfigure user provisioning tooIgloo Software.</span></span>  

<span data-ttu-id="016d2-237">Quand un utilisateur affecté tente toolog dans tooIgloo logiciels à l’aide du volet d’accès hello, Igloo Software vérifie l’existence d’un utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="016d2-237">When an assigned user tries toolog in tooIgloo Software using hello access panel, Igloo Software checks whether hello user exists.</span></span>  <span data-ttu-id="016d2-238">Si aucun compte d’utilisateur n’est disponible, Igloo Software le crée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="016d2-238">If there is no user account available yet, it is automatically created by Igloo Software.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="016d2-239">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="016d2-239">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="016d2-240">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooIgloo logiciel.</span><span class="sxs-lookup"><span data-stu-id="016d2-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIgloo Software.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="016d2-242">**tooassign Britta Simon tooIgloo logiciel, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="016d2-242">**tooassign Britta Simon tooIgloo Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="016d2-243">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="016d2-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="016d2-245">Dans la liste des applications hello, sélectionnez **Igloo Software**.</span><span class="sxs-lookup"><span data-stu-id="016d2-245">In hello applications list, select **Igloo Software**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_app.png) 

3. <span data-ttu-id="016d2-247">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="016d2-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="016d2-249">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="016d2-249">Click **Add** button.</span></span> <span data-ttu-id="016d2-250">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="016d2-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="016d2-252">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="016d2-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="016d2-253">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="016d2-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="016d2-254">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="016d2-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="016d2-255">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="016d2-255">Testing single sign-on</span></span>

<span data-ttu-id="016d2-256">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="016d2-256">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="016d2-257">Lorsque vous cliquez sur mosaïque de Igloo Software hello Bonjour volet d’accès, vous devez obtenir l’application de Igloo Software tooyour automatiquement signé sur.</span><span class="sxs-lookup"><span data-stu-id="016d2-257">When you click hello Igloo Software tile in hello Access Panel, you should get automatically signed-on tooyour Igloo Software application.</span></span>
<span data-ttu-id="016d2-258">Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="016d2-258">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="016d2-259">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="016d2-259">Additional resources</span></span>

* [<span data-ttu-id="016d2-260">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="016d2-260">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="016d2-261">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="016d2-261">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_203.png

