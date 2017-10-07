---
title: "Didacticiel : Intégration d’Azure Active Directory avec Samanage | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Samanage."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f0db4fb0-7eec-48c2-9c7a-beab1ab49bc2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: c8edc29f113b8088438618a731e97c0f4f155b9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-samanage"></a><span data-ttu-id="d84c4-103">Didacticiel : Intégration d’Azure Active Directory à Samanage</span><span class="sxs-lookup"><span data-stu-id="d84c4-103">Tutorial: Azure Active Directory integration with Samanage</span></span>

<span data-ttu-id="d84c4-104">Dans ce didacticiel, vous apprendrez comment toointegrate Samanage avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d84c4-104">In this tutorial, you learn how toointegrate Samanage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d84c4-105">Intégration de Samanage à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="d84c4-105">Integrating Samanage with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d84c4-106">Vous pouvez contrôler dans Azure AD qui a accès tooSamanage</span><span class="sxs-lookup"><span data-stu-id="d84c4-106">You can control in Azure AD who has access tooSamanage</span></span>
- <span data-ttu-id="d84c4-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSamanage (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="d84c4-107">You can enable your users tooautomatically get signed-on tooSamanage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d84c4-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="d84c4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d84c4-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d84c4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d84c4-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d84c4-110">Prerequisites</span></span>

<span data-ttu-id="d84c4-111">tooconfigure intégration d’Azure AD à Samanage, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="d84c4-111">tooconfigure Azure AD integration with Samanage, you need hello following items:</span></span>

- <span data-ttu-id="d84c4-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="d84c4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d84c4-113">Un abonnement Samanage pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="d84c4-113">A Samanage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d84c4-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="d84c4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d84c4-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="d84c4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d84c4-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="d84c4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d84c4-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d84c4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d84c4-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="d84c4-118">Scenario description</span></span>
<span data-ttu-id="d84c4-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="d84c4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d84c4-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="d84c4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d84c4-121">Ajout de Samanage à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="d84c4-121">Adding Samanage from hello gallery</span></span>
2. <span data-ttu-id="d84c4-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d84c4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-samanage-from-hello-gallery"></a><span data-ttu-id="d84c4-123">Ajout de Samanage à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="d84c4-123">Adding Samanage from hello gallery</span></span>
<span data-ttu-id="d84c4-124">intégration de hello tooconfigure de Samanage dans Azure AD, vous devez tooadd Samanage à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="d84c4-124">tooconfigure hello integration of Samanage into Azure AD, you need tooadd Samanage from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d84c4-125">**tooadd Samanage à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d84c4-125">**tooadd Samanage from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d84c4-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="d84c4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d84c4-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="d84c4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d84c4-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="d84c4-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="d84c4-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="d84c4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="d84c4-133">Dans la zone de recherche de hello, tapez **Samanage**.</span><span class="sxs-lookup"><span data-stu-id="d84c4-133">In hello search box, type **Samanage**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_search.png)

5. <span data-ttu-id="d84c4-135">Dans le volet de résultats hello, sélectionnez **Samanage**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="d84c4-135">In hello results panel, select **Samanage**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d84c4-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d84c4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d84c4-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Samanage sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="d84c4-138">In this section, you configure and test Azure AD single sign-on with Samanage based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d84c4-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Samanage est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d84c4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Samanage is tooa user in Azure AD.</span></span> <span data-ttu-id="d84c4-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Samanage doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="d84c4-140">In other words, a link relationship between an Azure AD user and hello related user in Samanage needs toobe established.</span></span>

<span data-ttu-id="d84c4-141">Dans Samanage, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="d84c4-141">In Samanage, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d84c4-142">tooconfigure et test Azure AD l’authentification unique à Samanage, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="d84c4-142">tooconfigure and test Azure AD single sign-on with Samanage, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d84c4-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="d84c4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d84c4-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d84c4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d84c4-145">**[Création d’un utilisateur de test de Samanage](#creating-a-samanage-test-user)**  -toohave un équivalent de Britta Simon dans Samanage est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d84c4-145">**[Creating a Samanage test user](#creating-a-samanage-test-user)** - toohave a counterpart of Britta Simon in Samanage that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d84c4-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="d84c4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d84c4-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="d84c4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d84c4-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d84c4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d84c4-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de Samanage.</span><span class="sxs-lookup"><span data-stu-id="d84c4-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Samanage application.</span></span>

<span data-ttu-id="d84c4-150">**tooconfigure Azure AD single sign-on avec Samanage, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d84c4-150">**tooconfigure Azure AD single sign-on with Samanage, perform hello following steps:**</span></span>

1. <span data-ttu-id="d84c4-151">Bonjour portail Azure, sur hello **Samanage** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="d84c4-151">In hello Azure portal, on hello **Samanage** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="d84c4-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="d84c4-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_samlbase.png)

3. <span data-ttu-id="d84c4-155">Sur hello **Samanage domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d84c4-155">On hello **Samanage Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_url.png)

    <span data-ttu-id="d84c4-157">a.</span><span class="sxs-lookup"><span data-stu-id="d84c4-157">a.</span></span> <span data-ttu-id="d84c4-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<Company Name>.samanage.com/saml_login/<Company Name>`</span><span class="sxs-lookup"><span data-stu-id="d84c4-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<Company Name>.samanage.com/saml_login/<Company Name>`</span></span>

    <span data-ttu-id="d84c4-159">b.</span><span class="sxs-lookup"><span data-stu-id="d84c4-159">b.</span></span> <span data-ttu-id="d84c4-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<Company Name>.samanage.com`</span><span class="sxs-lookup"><span data-stu-id="d84c4-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<Company Name>.samanage.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d84c4-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="d84c4-161">These values are not real.</span></span> <span data-ttu-id="d84c4-162">Mettre à jour ces valeurs avec l’URL de connexion réel hello et identificateur, qui est expliquée plus loin dans le didacticiel de hello.</span><span class="sxs-lookup"><span data-stu-id="d84c4-162">Update these values with hello actual Sign-on URL and Identifier, which is explained later in hello tutorial.</span></span> <span data-ttu-id="d84c4-163">Pour plus de détails, contactez l’[équipe de support technique Samanage](https://www.samanage.com/support).</span><span class="sxs-lookup"><span data-stu-id="d84c4-163">For more details contact [Samanage Client support team](https://www.samanage.com/support).</span></span>    
 
4. <span data-ttu-id="d84c4-164">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d84c4-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_certificate.png) 

5. <span data-ttu-id="d84c4-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="d84c4-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-samanage-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d84c4-168">Sur hello **Samanage Configuration** , cliquez sur **configurer de Samanage** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="d84c4-168">On hello **Samanage Configuration** section, click **Configure Samanage** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d84c4-169">Hello de copie **URL de déconnexion et l’ID d’entité SAML** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="d84c4-169">Copy hello **Sign-Out URL, and SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_configure.png) 

7. <span data-ttu-id="d84c4-171">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Samanage en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="d84c4-171">In a different web browser window, log into your Samanage company site as an administrator.</span></span>

8. <span data-ttu-id="d84c4-172">Cliquez sur **Dashboard** et sélectionnez **Setup** dans le volet de navigation de gauche.</span><span class="sxs-lookup"><span data-stu-id="d84c4-172">Click **Dashboard** and select **Setup** in left navigation pane.</span></span>
   
    <span data-ttu-id="d84c4-173">![Tableau de bord](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Tableau de bord")</span><span class="sxs-lookup"><span data-stu-id="d84c4-173">![Dashboard](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Dashboard")</span></span>

9. <span data-ttu-id="d84c4-174">Cliquez sur **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="d84c4-174">Click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="d84c4-175">![Authentification unique](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_002.png "Authentification unique")</span><span class="sxs-lookup"><span data-stu-id="d84c4-175">![Single Sign-On](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_002.png "Single Sign-On")</span></span>

10. <span data-ttu-id="d84c4-176">Accédez trop**connexion à l’aide de SAML** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d84c4-176">Navigate too**Login using SAML** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="d84c4-177">![Connexion avec SAML](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_003.png "Connexion avec SAML")</span><span class="sxs-lookup"><span data-stu-id="d84c4-177">![Login using SAML](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_003.png "Login using SAML")</span></span>
 
    <span data-ttu-id="d84c4-178">a.</span><span class="sxs-lookup"><span data-stu-id="d84c4-178">a.</span></span> <span data-ttu-id="d84c4-179">Cliquez sur **Enable Single Sign-On with SAML**(Activer l’authentification unique avec SAML).</span><span class="sxs-lookup"><span data-stu-id="d84c4-179">Click **Enable Single Sign-On with SAML**.</span></span>  
 
    <span data-ttu-id="d84c4-180">b.</span><span class="sxs-lookup"><span data-stu-id="d84c4-180">b.</span></span> <span data-ttu-id="d84c4-181">Bonjour **URL du fournisseur d’identité** zone de texte, valeur hello coller **ID d’entité SAML** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d84c4-181">In hello **Identity Provider URL** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>    
 
    <span data-ttu-id="d84c4-182">c.</span><span class="sxs-lookup"><span data-stu-id="d84c4-182">c.</span></span> <span data-ttu-id="d84c4-183">Confirmer hello **URL de connexion** correspondances hello **URL de connexion** de **Samanage domaine et les URL** section dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d84c4-183">Confirm hello **Login URL** matches hello **Sign On URL** of **Samanage Domain and URLs** section in Azure portal.</span></span>
 
    <span data-ttu-id="d84c4-184">d.</span><span class="sxs-lookup"><span data-stu-id="d84c4-184">d.</span></span> <span data-ttu-id="d84c4-185">Bonjour **URL de déconnexion** zone de texte, entrez la valeur hello **URL de déconnexion** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d84c4-185">In hello **Logout URL** textbox, enter hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="d84c4-186">e.</span><span class="sxs-lookup"><span data-stu-id="d84c4-186">e.</span></span> <span data-ttu-id="d84c4-187">Bonjour **SAML émetteur** zone de texte, URI de l’id de l’application hello de type défini dans votre fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="d84c4-187">In hello **SAML Issuer** textbox, type hello app id URI set in your identity provider.</span></span>
 
    <span data-ttu-id="d84c4-188">f.</span><span class="sxs-lookup"><span data-stu-id="d84c4-188">f.</span></span> <span data-ttu-id="d84c4-189">Ouvrez votre certificat codé en base 64 téléchargé à partir du portail Azure dans le bloc-notes, hello copie contenu de celui-ci dans le Presse-papiers et le coller ensuite toohello **collez votre x.509 de fournisseur d’identité certificat ci-dessous** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="d84c4-189">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **Paste your Identity Provider x.509 Certificate below** textbox.</span></span>
 
    <span data-ttu-id="d84c4-190">g.</span><span class="sxs-lookup"><span data-stu-id="d84c4-190">g.</span></span> <span data-ttu-id="d84c4-191">Cliquez sur **Create users if they do not exist in Samanage**(Créer des utilisateurs s’ils n’existent pas dans Samanage).</span><span class="sxs-lookup"><span data-stu-id="d84c4-191">Click **Create users if they do not exist in Samanage**.</span></span>
 
    <span data-ttu-id="d84c4-192">h.</span><span class="sxs-lookup"><span data-stu-id="d84c4-192">h.</span></span> <span data-ttu-id="d84c4-193">Cliquez sur **Update**.</span><span class="sxs-lookup"><span data-stu-id="d84c4-193">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="d84c4-194">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="d84c4-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d84c4-195">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="d84c4-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d84c4-196">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d84c4-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d84c4-197">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="d84c4-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="d84c4-198">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="d84c4-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="d84c4-200">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d84c4-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d84c4-201">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="d84c4-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-samanage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d84c4-203">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="d84c4-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-samanage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d84c4-205">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="d84c4-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-samanage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d84c4-207">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d84c4-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-samanage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d84c4-209">a.</span><span class="sxs-lookup"><span data-stu-id="d84c4-209">a.</span></span> <span data-ttu-id="d84c4-210">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d84c4-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d84c4-211">b.</span><span class="sxs-lookup"><span data-stu-id="d84c4-211">b.</span></span> <span data-ttu-id="d84c4-212">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d84c4-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d84c4-213">c.</span><span class="sxs-lookup"><span data-stu-id="d84c4-213">c.</span></span> <span data-ttu-id="d84c4-214">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="d84c4-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d84c4-215">d.</span><span class="sxs-lookup"><span data-stu-id="d84c4-215">d.</span></span> <span data-ttu-id="d84c4-216">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="d84c4-216">Click **Create**.</span></span>
 
### <a name="creating-a-samanage-test-user"></a><span data-ttu-id="d84c4-217">Création d’un utilisateur de test Samanage</span><span class="sxs-lookup"><span data-stu-id="d84c4-217">Creating a Samanage test user</span></span>

<span data-ttu-id="d84c4-218">tooenable Azure AD les utilisateurs toolog dans tooSamanage, vous devez les configurer sur Samanage.</span><span class="sxs-lookup"><span data-stu-id="d84c4-218">tooenable Azure AD users toolog in tooSamanage, they must be provisioned into Samanage.</span></span>  
<span data-ttu-id="d84c4-219">Dans les cas de hello de Samanage, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="d84c4-219">In hello case of Samanage, provisioning is a manual task.</span></span>

<span data-ttu-id="d84c4-220">**tooprovision un compte d’utilisateur, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d84c4-220">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="d84c4-221">Connectez-vous à votre site d’entreprise Samanage en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="d84c4-221">Log into your Samanage company site as an administrator.</span></span>

2. <span data-ttu-id="d84c4-222">Cliquez sur **Dashboard** et sélectionnez **Setup** dans le volet de navigation gauche.</span><span class="sxs-lookup"><span data-stu-id="d84c4-222">Click **Dashboard** and select **Setup** in left navigation pan.</span></span>
   
    <span data-ttu-id="d84c4-223">![Configuration](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Configuration")</span><span class="sxs-lookup"><span data-stu-id="d84c4-223">![Setup](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Setup")</span></span>

3. <span data-ttu-id="d84c4-224">Cliquez sur hello **utilisateurs** onglet</span><span class="sxs-lookup"><span data-stu-id="d84c4-224">Click hello **Users** tab</span></span>
   
    <span data-ttu-id="d84c4-225">![Utilisateurs](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_006.png "Utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="d84c4-225">![Users](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_006.png "Users")</span></span>

4. <span data-ttu-id="d84c4-226">Cliquez sur **New User**.</span><span class="sxs-lookup"><span data-stu-id="d84c4-226">Click **New User**.</span></span>
   
    <span data-ttu-id="d84c4-227">![Nouvel utilisateur](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_007.png "Nouvel utilisateur")</span><span class="sxs-lookup"><span data-stu-id="d84c4-227">![New User](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_007.png "New User")</span></span>

5. <span data-ttu-id="d84c4-228">Hello de type **nom** et hello **adresse de messagerie** d’un compte Azure Active Directory tooprovision et cliquez sur **créer un utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="d84c4-228">Type hello **Name** and hello **Email Address** of an Azure Active Directory account you want tooprovision and click **Create user**.</span></span>
   
    <span data-ttu-id="d84c4-229">![Create User](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_008.png "Create User")</span><span class="sxs-lookup"><span data-stu-id="d84c4-229">![Create User](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_008.png "Create User")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="d84c4-230">titulaire du compte Azure Active Directory Hello sera reçoivent un e-mail et suivez les leur compte d’un tooconfirm lien avant son activation.</span><span class="sxs-lookup"><span data-stu-id="d84c4-230">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span> <span data-ttu-id="d84c4-231">Vous pouvez utiliser n’importe quel autre Samanage utilisateur compte outil de création ou API fournie par Samanage tooprovision Azure Active Directory des comptes d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d84c4-231">You can use any other Samanage user account creation tools or APIs provided by Samanage tooprovision Azure Active Directory user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d84c4-232">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d84c4-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d84c4-233">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooSamanage.</span><span class="sxs-lookup"><span data-stu-id="d84c4-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSamanage.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="d84c4-235">**tooassign Britta Simon tooSamanage, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d84c4-235">**tooassign Britta Simon tooSamanage, perform hello following steps:**</span></span>

1. <span data-ttu-id="d84c4-236">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="d84c4-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="d84c4-238">Dans la liste des applications hello, sélectionnez **Samanage**.</span><span class="sxs-lookup"><span data-stu-id="d84c4-238">In hello applications list, select **Samanage**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_app.png) 

3. <span data-ttu-id="d84c4-240">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="d84c4-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="d84c4-242">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="d84c4-242">Click **Add** button.</span></span> <span data-ttu-id="d84c4-243">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="d84c4-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="d84c4-245">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="d84c4-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d84c4-246">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="d84c4-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d84c4-247">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="d84c4-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d84c4-248">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="d84c4-248">Testing single sign-on</span></span>

<span data-ttu-id="d84c4-249">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="d84c4-249">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d84c4-250">Lorsque vous cliquez sur mosaïque Samanage hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Samanage application.</span><span class="sxs-lookup"><span data-stu-id="d84c4-250">When you click hello Samanage tile in hello Access Panel, you should get automatically signed-on tooyour Samanage application.</span></span>
<span data-ttu-id="d84c4-251">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d84c4-251">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d84c4-252">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="d84c4-252">Additional resources</span></span>

* [<span data-ttu-id="d84c4-253">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d84c4-253">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d84c4-254">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="d84c4-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_203.png

