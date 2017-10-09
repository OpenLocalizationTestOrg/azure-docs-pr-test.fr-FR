---
title: "Didacticiel : Intégration d’Azure Active Directory à Tableau Online | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et en ligne de Tableau."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d4b1149-ba3b-4f4e-8bce-9791316b730d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: 590b2674270c340b4750c7b6feeaf4f0df4bf853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-online"></a><span data-ttu-id="cf90b-103">Didacticiel : Intégration d’Azure Active Directory à Tableau Online</span><span class="sxs-lookup"><span data-stu-id="cf90b-103">Tutorial: Azure Active Directory integration with Tableau Online</span></span>

<span data-ttu-id="cf90b-104">Dans ce didacticiel, vous apprendrez comment toointegrate Tableau Online avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cf90b-104">In this tutorial, you learn how toointegrate Tableau Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cf90b-105">Intégration de Tableau en ligne auprès d’Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="cf90b-105">Integrating Tableau Online with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cf90b-106">Vous pouvez contrôler dans Azure AD qui a accès tooTableau en ligne</span><span class="sxs-lookup"><span data-stu-id="cf90b-106">You can control in Azure AD who has access tooTableau Online</span></span>
- <span data-ttu-id="cf90b-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooTableau en ligne (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="cf90b-107">You can enable your users tooautomatically get signed-on tooTableau Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cf90b-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="cf90b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="cf90b-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cf90b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cf90b-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="cf90b-110">Prerequisites</span></span>

<span data-ttu-id="cf90b-111">tooconfigure intégration d’Azure AD avec un Tableau en ligne, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="cf90b-111">tooconfigure Azure AD integration with Tableau Online, you need hello following items:</span></span>

- <span data-ttu-id="cf90b-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="cf90b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cf90b-113">Un abonnement Tableau Online pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="cf90b-113">A Tableau Online single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cf90b-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="cf90b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cf90b-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="cf90b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cf90b-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="cf90b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cf90b-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cf90b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cf90b-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="cf90b-118">Scenario description</span></span>
<span data-ttu-id="cf90b-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="cf90b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cf90b-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="cf90b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cf90b-121">Ajout en ligne de Tableau à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="cf90b-121">Adding Tableau Online from hello gallery</span></span>
2. <span data-ttu-id="cf90b-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="cf90b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tableau-online-from-hello-gallery"></a><span data-ttu-id="cf90b-123">Ajout en ligne de Tableau à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="cf90b-123">Adding Tableau Online from hello gallery</span></span>
<span data-ttu-id="cf90b-124">intégration de hello tooconfigure en ligne de Tableau dans Azure AD, vous devez tooadd en ligne de Tableau à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="cf90b-124">tooconfigure hello integration of Tableau Online into Azure AD, you need tooadd Tableau Online from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cf90b-125">**tooadd Tableau Online à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="cf90b-125">**tooadd Tableau Online from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cf90b-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="cf90b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cf90b-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="cf90b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cf90b-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="cf90b-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="cf90b-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="cf90b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="cf90b-133">Dans la zone de recherche de hello, tapez **en ligne de Tableau**.</span><span class="sxs-lookup"><span data-stu-id="cf90b-133">In hello search box, type **Tableau Online**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_search.png)

5. <span data-ttu-id="cf90b-135">Dans le volet de résultats hello, sélectionnez **en ligne de Tableau**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="cf90b-135">In hello results panel, select **Tableau Online**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cf90b-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="cf90b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cf90b-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Tableau Online à l’aide d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="cf90b-138">In this section, you configure and test Azure AD single sign-on with Tableau Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="cf90b-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans le Tableau en ligne est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cf90b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Tableau Online is tooa user in Azure AD.</span></span> <span data-ttu-id="cf90b-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans le Tableau en ligne hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="cf90b-140">In other words, a link relationship between an Azure AD user and hello related user in Tableau Online needs toobe established.</span></span>

<span data-ttu-id="cf90b-141">Dans la ligne de Tableau, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="cf90b-141">In Tableau Online, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="cf90b-142">tooconfigure et test Azure AD l’authentification unique avec un Tableau en ligne, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="cf90b-142">tooconfigure and test Azure AD single sign-on with Tableau Online, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cf90b-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="cf90b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cf90b-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cf90b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cf90b-145">**[Création d’un utilisateur de test en ligne de Tableau](#creating-a-tableau-online-test-user)**  -toohave un équivalent de Britta Simon dans le Tableau en ligne qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="cf90b-145">**[Creating a Tableau Online test user](#creating-a-tableau-online-test-user)** - toohave a counterpart of Britta Simon in Tableau Online that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cf90b-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="cf90b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cf90b-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="cf90b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cf90b-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="cf90b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cf90b-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application en ligne de Tableau.</span><span class="sxs-lookup"><span data-stu-id="cf90b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Tableau Online application.</span></span>

<span data-ttu-id="cf90b-150">**tooconfigure Azure AD authentification unique avec Tableau Online, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="cf90b-150">**tooconfigure Azure AD single sign-on with Tableau Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="cf90b-151">Bonjour portail Azure, sur hello **en ligne de Tableau** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="cf90b-151">In hello Azure portal, on hello **Tableau Online** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="cf90b-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="cf90b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_samlbase.png)

3. <span data-ttu-id="cf90b-155">Sur hello **domaine en ligne du Tableau et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="cf90b-155">On hello **Tableau Online Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_url.png)
    
    <span data-ttu-id="cf90b-157">a.</span><span class="sxs-lookup"><span data-stu-id="cf90b-157">a.</span></span> <span data-ttu-id="cf90b-158">Bonjour **URL de connexion** zone de texte, tapez l’URL hello :`https://sso.online.tableau.com`</span><span class="sxs-lookup"><span data-stu-id="cf90b-158">In hello **Sign-on URL** textbox, type hello URL: `https://sso.online.tableau.com`</span></span>

    <span data-ttu-id="cf90b-159">b.</span><span class="sxs-lookup"><span data-stu-id="cf90b-159">b.</span></span> <span data-ttu-id="cf90b-160">Bonjour **identificateur** zone de texte, tapez l’URL hello :`https://sso.online.tableau.com/public/sp/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="cf90b-160">In hello **Identifier** textbox, type hello URL: `https://sso.online.tableau.com/public/sp/<instancename>`</span></span>

4. <span data-ttu-id="cf90b-161">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="cf90b-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_certificate.png) 

5. <span data-ttu-id="cf90b-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="cf90b-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-tableauonline-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cf90b-165">Dans une autre fenêtre de navigateur, l’authentification tooyour application en ligne de Tableau.</span><span class="sxs-lookup"><span data-stu-id="cf90b-165">In a different browser window, sign-on tooyour Tableau Online application.</span></span> <span data-ttu-id="cf90b-166">Accédez trop**paramètres** , puis **authentification**.</span><span class="sxs-lookup"><span data-stu-id="cf90b-166">Go too**Settings** and then **Authentication**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_09.png)
    
7. <span data-ttu-id="cf90b-168">tooenable SAML, sous **Types d’authentification** section.</span><span class="sxs-lookup"><span data-stu-id="cf90b-168">tooenable SAML, Under **Authentication Types** section.</span></span> <span data-ttu-id="cf90b-169">Vérifiez hello **Single sign-on avec SAML** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="cf90b-169">Check hello **Single sign-on with SAML** checkbox.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_12.png)

8. <span data-ttu-id="cf90b-171">Faites défiler la page jusqu’à la section **Import metadata file into Tableau Online (Importer le fichier de métadonnées dans Tableau Online)** .</span><span class="sxs-lookup"><span data-stu-id="cf90b-171">Scroll down until **Import metadata file into Tableau Online** section.</span></span>  <span data-ttu-id="cf90b-172">Cliquez sur Parcourir et importer le fichier de métadonnées hello que vous avez téléchargé à partir d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cf90b-172">Click Browse and import hello metadata file you have downloaded from Azure AD.</span></span> <span data-ttu-id="cf90b-173">Cliquez alors sur **Apply (Appliquer)**.</span><span class="sxs-lookup"><span data-stu-id="cf90b-173">Then, click **Apply**.</span></span>
   
   ![Configurer l’authentification unique](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_13.png)

9. <span data-ttu-id="cf90b-175">Bonjour **correspondent des assertions** section, insérer hello fournisseur d’identité assertion nom correspondant **adresse de messagerie**, **prénom**, et **nom** .</span><span class="sxs-lookup"><span data-stu-id="cf90b-175">In hello **Match assertions** section, insert hello corresponding Identity Provider assertion name for **email address**, **first name**, and **last name**.</span></span> <span data-ttu-id="cf90b-176">tooget ces informations à partir d’Azure AD :</span><span class="sxs-lookup"><span data-stu-id="cf90b-176">tooget this information from Azure AD:</span></span> 
  
    <span data-ttu-id="cf90b-177">a.</span><span class="sxs-lookup"><span data-stu-id="cf90b-177">a.</span></span> <span data-ttu-id="cf90b-178">Dans hello portail Azure, passez hello **en ligne de Tableau** page d’intégration d’application.</span><span class="sxs-lookup"><span data-stu-id="cf90b-178">In hello Azure portal, go on hello **Tableau Online** application integration page.</span></span>
    
    <span data-ttu-id="cf90b-179">b.</span><span class="sxs-lookup"><span data-stu-id="cf90b-179">b.</span></span> <span data-ttu-id="cf90b-180">Dans la section d’attributs hello, sélectionnez hello **« afficher et modifier tous les autres attributs de l’utilisateur »** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="cf90b-180">In hello attributes section, Select hello **"view and edit all other user attributes"** checkbox.</span></span> 
    
   ![Configurer l’authentification unique](./media/active-directory-saas-tableauonline-tutorial/attributesection.png)
      
    <span data-ttu-id="cf90b-182">c.</span><span class="sxs-lookup"><span data-stu-id="cf90b-182">c.</span></span> <span data-ttu-id="cf90b-183">Copiez la valeur d’espace de noms hello pour ces attributs : givenname, adresse électronique et le nom à l’aide de hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="cf90b-183">Copy hello namespace value for these attributes: givenname, email and surname by using hello following steps:</span></span>

   ![Authentification unique Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_10.png)
    
    <span data-ttu-id="cf90b-185">d.</span><span class="sxs-lookup"><span data-stu-id="cf90b-185">d.</span></span> <span data-ttu-id="cf90b-186">Cliquez sur la valeur **user.givenname**.</span><span class="sxs-lookup"><span data-stu-id="cf90b-186">Click **user.givenname** value</span></span> 
    
    <span data-ttu-id="cf90b-187">e.</span><span class="sxs-lookup"><span data-stu-id="cf90b-187">e.</span></span> <span data-ttu-id="cf90b-188">Copier la valeur de hello de hello **espace de noms** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="cf90b-188">Copy hello value from hello **namespace** textbox.</span></span>

   ![Configurer l’authentification unique](./media/active-directory-saas-tableauonline-tutorial/attributesection2.png)

    <span data-ttu-id="cf90b-190">f.</span><span class="sxs-lookup"><span data-stu-id="cf90b-190">f.</span></span> <span data-ttu-id="cf90b-191">les valeurs d’espace de noms toocopy hello pour les e-mails hello et surname suivent hello étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="cf90b-191">toocopy hello namesapce values for hello email and surname follow hello preceding steps.</span></span>

    <span data-ttu-id="cf90b-192">g.</span><span class="sxs-lookup"><span data-stu-id="cf90b-192">g.</span></span> <span data-ttu-id="cf90b-193">Basculer vers l’application en ligne de Tableau de toohello, puis définissez hello **attributs en ligne du Tableau** section comme suit :</span><span class="sxs-lookup"><span data-stu-id="cf90b-193">Switch toohello Tableau Online application, then set hello **Tableau Online Attributes** section as follows:</span></span>
     * <span data-ttu-id="cf90b-194">Email (Adresse de messagerie) : **mail** ou **userPrincipalName**</span><span class="sxs-lookup"><span data-stu-id="cf90b-194">Email: **mail** or **userprincipalname**</span></span>
     * <span data-ttu-id="cf90b-195">First name (Prénom) : **givenName**</span><span class="sxs-lookup"><span data-stu-id="cf90b-195">First name: **givenname**</span></span>
     * <span data-ttu-id="cf90b-196">Last name (Nom) : **surname**</span><span class="sxs-lookup"><span data-stu-id="cf90b-196">Last name: **surname**</span></span>
   
   ![Configurer l’authentification unique](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_14.png)

> [!TIP]
> <span data-ttu-id="cf90b-198">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="cf90b-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cf90b-199">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="cf90b-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cf90b-200">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cf90b-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cf90b-201">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="cf90b-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="cf90b-202">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="cf90b-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="cf90b-204">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="cf90b-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cf90b-205">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="cf90b-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cf90b-207">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="cf90b-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cf90b-209">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="cf90b-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cf90b-211">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="cf90b-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cf90b-213">a.</span><span class="sxs-lookup"><span data-stu-id="cf90b-213">a.</span></span> <span data-ttu-id="cf90b-214">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cf90b-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cf90b-215">b.</span><span class="sxs-lookup"><span data-stu-id="cf90b-215">b.</span></span> <span data-ttu-id="cf90b-216">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cf90b-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cf90b-217">c.</span><span class="sxs-lookup"><span data-stu-id="cf90b-217">c.</span></span> <span data-ttu-id="cf90b-218">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="cf90b-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cf90b-219">d.</span><span class="sxs-lookup"><span data-stu-id="cf90b-219">d.</span></span> <span data-ttu-id="cf90b-220">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="cf90b-220">Click **Create**.</span></span>
 
### <a name="creating-a-tableau-online-test-user"></a><span data-ttu-id="cf90b-221">Création d’un utilisateur de test Tableau Online</span><span class="sxs-lookup"><span data-stu-id="cf90b-221">Creating a Tableau Online test user</span></span>

<span data-ttu-id="cf90b-222">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="cf90b-222">In this section, you create a user called Britta Simon in Tableau Online.</span></span>

1. <span data-ttu-id="cf90b-223">Dans **Tableau Online**, cliquez sur **Paramètres**, puis sur la section **Authentification**.</span><span class="sxs-lookup"><span data-stu-id="cf90b-223">On **Tableau Online**, click **Settings** and then **Authentication** section.</span></span> <span data-ttu-id="cf90b-224">Faites défiler la liste trop**sélectionner des utilisateurs** section.</span><span class="sxs-lookup"><span data-stu-id="cf90b-224">Scroll down too**Select Users** section.</span></span> <span data-ttu-id="cf90b-225">Cliquez sur **Ajouter des utilisateurs**, puis sur **Entrer les adresses de messagerie**.</span><span class="sxs-lookup"><span data-stu-id="cf90b-225">Click **Add Users** and then **Enter Email Addresses**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_15.png)
2. <span data-ttu-id="cf90b-227">Sélectionnez **Add users for single sign-on (SSO) authentication (Ajouter des utilisateurs pour l’authentification unique (SSO))**.</span><span class="sxs-lookup"><span data-stu-id="cf90b-227">Select **Add users for single sign-on (SSO) authentication**.</span></span> <span data-ttu-id="cf90b-228">Bonjour **Entrez les adresses de messagerie** ajouter de la zone de textebritta.simon@contoso.com</span><span class="sxs-lookup"><span data-stu-id="cf90b-228">In hello **Enter Email Addresses** textbox add britta.simon@contoso.com</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_11.png)
3. <span data-ttu-id="cf90b-230">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="cf90b-230">Click **Create**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cf90b-231">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="cf90b-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cf90b-232">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant tooTableau accès en ligne.</span><span class="sxs-lookup"><span data-stu-id="cf90b-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTableau Online.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="cf90b-234">**tooassign tooTableau Britta Simon en ligne, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="cf90b-234">**tooassign Britta Simon tooTableau Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="cf90b-235">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="cf90b-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="cf90b-237">Dans la liste des applications hello, sélectionnez **en ligne de Tableau**.</span><span class="sxs-lookup"><span data-stu-id="cf90b-237">In hello applications list, select **Tableau Online**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_app.png) 

3. <span data-ttu-id="cf90b-239">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="cf90b-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="cf90b-241">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="cf90b-241">Click **Add** button.</span></span> <span data-ttu-id="cf90b-242">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="cf90b-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="cf90b-244">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="cf90b-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cf90b-245">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="cf90b-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cf90b-246">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="cf90b-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cf90b-247">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="cf90b-247">Testing single sign-on</span></span>

<span data-ttu-id="cf90b-248">objectif Hello de cette section est tootest votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="cf90b-248">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="cf90b-249">Lorsque vous cliquez sur vignette de Tableau en ligne hello Bonjour volet d’accès, vous devez obtenir tooyour automatiquement signé sur les applications en ligne de Tableau.</span><span class="sxs-lookup"><span data-stu-id="cf90b-249">When you click hello Tableau Online tile in hello Access Panel, you should get automatically signed-on tooyour Tableau Online application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cf90b-250">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="cf90b-250">Additional resources</span></span>

* [<span data-ttu-id="cf90b-251">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cf90b-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cf90b-252">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="cf90b-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_203.png

