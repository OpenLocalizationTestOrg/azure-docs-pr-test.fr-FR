---
title: "Didacticiel : Intégration d’Azure Active Directory à Syncplicity | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Syncplicity."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 896a3211-f368-46d7-95b8-e4768c23be08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 6148112a959232ed24d76d1c7b8773f06568fee7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-syncplicity"></a><span data-ttu-id="f4cf5-103">Didacticiel : Intégration d’Azure Active Directory à Syncplicity</span><span class="sxs-lookup"><span data-stu-id="f4cf5-103">Tutorial: Azure Active Directory integration with Syncplicity</span></span>

<span data-ttu-id="f4cf5-104">Dans ce didacticiel, vous apprendrez comment toointegrate Syncplicity avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f4cf5-104">In this tutorial, you learn how toointegrate Syncplicity with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f4cf5-105">Intégration de Syncplicity avec Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="f4cf5-105">Integrating Syncplicity with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f4cf5-106">Vous pouvez contrôler dans Azure AD qui a accès tooSyncplicity</span><span class="sxs-lookup"><span data-stu-id="f4cf5-106">You can control in Azure AD who has access tooSyncplicity</span></span>
- <span data-ttu-id="f4cf5-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSyncplicity (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4cf5-107">You can enable your users tooautomatically get signed-on tooSyncplicity (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f4cf5-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="f4cf5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f4cf5-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f4cf5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f4cf5-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f4cf5-110">Prerequisites</span></span>

<span data-ttu-id="f4cf5-111">tooconfigure intégration d’Azure AD à Syncplicity, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f4cf5-111">tooconfigure Azure AD integration with Syncplicity, you need hello following items:</span></span>

- <span data-ttu-id="f4cf5-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4cf5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f4cf5-113">Un abonnement Syncplicity pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="f4cf5-113">A Syncplicity single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f4cf5-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f4cf5-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="f4cf5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f4cf5-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f4cf5-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f4cf5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f4cf5-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="f4cf5-118">Scenario description</span></span>
<span data-ttu-id="f4cf5-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f4cf5-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="f4cf5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f4cf5-121">Ajout de Syncplicity à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="f4cf5-121">Adding Syncplicity from hello gallery</span></span>
2. <span data-ttu-id="f4cf5-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4cf5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-syncplicity-from-hello-gallery"></a><span data-ttu-id="f4cf5-123">Ajout de Syncplicity à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="f4cf5-123">Adding Syncplicity from hello gallery</span></span>
<span data-ttu-id="f4cf5-124">intégration de hello tooconfigure de Syncplicity dans Azure AD, vous devez tooadd Syncplicity à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-124">tooconfigure hello integration of Syncplicity into Azure AD, you need tooadd Syncplicity from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f4cf5-125">**tooadd Syncplicity à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f4cf5-125">**tooadd Syncplicity from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f4cf5-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f4cf5-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f4cf5-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="f4cf5-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="f4cf5-133">Dans la zone de recherche de hello, tapez **Syncplicity**.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-133">In hello search box, type **Syncplicity**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_search.png)

5. <span data-ttu-id="f4cf5-135">Dans le volet de résultats hello, sélectionnez **Syncplicity**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-135">In hello results panel, select **Syncplicity**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f4cf5-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4cf5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f4cf5-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Syncplicity à l’aide d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="f4cf5-138">In this section, you configure and test Azure AD single sign-on with Syncplicity based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f4cf5-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Syncplicity est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Syncplicity is tooa user in Azure AD.</span></span> <span data-ttu-id="f4cf5-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans Syncplicity hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-140">In other words, a link relationship between an Azure AD user and hello related user in Syncplicity needs toobe established.</span></span>

<span data-ttu-id="f4cf5-141">Dans Syncplicity, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-141">In Syncplicity, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f4cf5-142">tooconfigure et test Azure AD l’authentification unique à Syncplicity, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="f4cf5-142">tooconfigure and test Azure AD single sign-on with Syncplicity, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f4cf5-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f4cf5-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f4cf5-145">**[Création d’un utilisateur de test de Syncplicity](#creating-a-syncplicity-test-user)**  -toohave un équivalent de Britta Simon dans Syncplicity est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-145">**[Creating a Syncplicity test user](#creating-a-syncplicity-test-user)** - toohave a counterpart of Britta Simon in Syncplicity that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f4cf5-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f4cf5-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f4cf5-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4cf5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f4cf5-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Syncplicity application.</span></span>

<span data-ttu-id="f4cf5-150">**tooconfigure Azure AD single sign-on avec Syncplicity, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f4cf5-150">**tooconfigure Azure AD single sign-on with Syncplicity, perform hello following steps:**</span></span>

1. <span data-ttu-id="f4cf5-151">Bonjour portail Azure, sur hello **Syncplicity** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-151">In hello Azure portal, on hello **Syncplicity** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="f4cf5-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_samlbase.png)

3. <span data-ttu-id="f4cf5-155">Sur hello **Syncplicity domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f4cf5-155">On hello **Syncplicity Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_url.png)

    <span data-ttu-id="f4cf5-157">a.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-157">a.</span></span> <span data-ttu-id="f4cf5-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.syncplicity.com`</span><span class="sxs-lookup"><span data-stu-id="f4cf5-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.syncplicity.com`</span></span>

    <span data-ttu-id="f4cf5-159">b.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-159">b.</span></span> <span data-ttu-id="f4cf5-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.syncplicity.com/sp`</span><span class="sxs-lookup"><span data-stu-id="f4cf5-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.syncplicity.com/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f4cf5-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-161">These values are not real.</span></span> <span data-ttu-id="f4cf5-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f4cf5-163">Contact [équipe de support Client de Syncplicity](https://www.syncplicity.com/contact-us) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-163">Contact [Syncplicity Client support team](https://www.syncplicity.com/contact-us) tooget these values.</span></span> 
 

4. <span data-ttu-id="f4cf5-164">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_certificate.png) 

  
5. <span data-ttu-id="f4cf5-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="f4cf5-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-syncplicity-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f4cf5-168">Sur hello **Syncplicity Configuration** , cliquez sur **configurer de Syncplicity** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-168">On hello **Syncplicity Configuration** section, click **Configure Syncplicity** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f4cf5-169">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="f4cf5-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_configure.png) 

7. <span data-ttu-id="f4cf5-171">Connectez-vous à tooyour **Syncplicity** client.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-171">Sign in tooyour **Syncplicity** tenant.</span></span>

8. <span data-ttu-id="f4cf5-172">Dans le menu hello haut de hello, cliquez sur **admin**, sélectionnez **paramètres**, puis cliquez sur **un domaine personnalisé et l’authentification unique sur**.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-172">In hello menu on hello top, click **admin**, select **settings**, and then click **Custom domain and single sign-on**.</span></span>
   
    <span data-ttu-id="f4cf5-173">![Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769545.png "Syncplicity")</span><span class="sxs-lookup"><span data-stu-id="f4cf5-173">![Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769545.png "Syncplicity")</span></span>

9. <span data-ttu-id="f4cf5-174">Sur hello **Single Sign-On (SSO)** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f4cf5-174">On hello **Single Sign-On (SSO)** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="f4cf5-175">![Authentification unique \(SSO\)](./media/active-directory-saas-syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")</span><span class="sxs-lookup"><span data-stu-id="f4cf5-175">![Single Sign-On \(SSO\)](./media/active-directory-saas-syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")</span></span>   

    <span data-ttu-id="f4cf5-176">a.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-176">a.</span></span> <span data-ttu-id="f4cf5-177">Bonjour **un domaine personnalisé** zone de texte, nom du type hello de votre domaine.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-177">In hello **Custom Domain** textbox, type hello name of your domain.</span></span>
  
    <span data-ttu-id="f4cf5-178">b.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-178">b.</span></span> <span data-ttu-id="f4cf5-179">Sélectionnez **Enabled** dans **Single Sign-On Status**.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-179">Select **Enabled** as **Single Sign-On Status**.</span></span>

    <span data-ttu-id="f4cf5-180">c.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-180">c.</span></span> <span data-ttu-id="f4cf5-181">Bonjour **Id d’entité** zone de texte, valeur hello coller **ID d’entité SAML** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-181">In hello **Entity Id** textbox, Paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="f4cf5-182">d.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-182">d.</span></span> <span data-ttu-id="f4cf5-183">Bonjour **URL de la page connexion** zone de texte, hello de coller **SAML Sign-On URL du Service unique** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-183">In hello **Sign-in page URL** textbox, Paste hello **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="f4cf5-184">e.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-184">e.</span></span> <span data-ttu-id="f4cf5-185">Bonjour **Logout page URL** zone de texte, hello de coller **URL de déconnexion** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-185">In hello **Logout page URL** textbox, Paste hello **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="f4cf5-186">f.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-186">f.</span></span> <span data-ttu-id="f4cf5-187">Dans **certificat de fournisseur d’identité**, cliquez sur **choisir un fichier**, puis téléchargez le certificat hello dont vous avez téléchargé à partir de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-187">In **Identity Provider Certificate**, click **Choose file**, and then upload hello certificate which you have downloaded from hello Azure portal.</span></span> 

    <span data-ttu-id="f4cf5-188">g.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-188">g.</span></span> <span data-ttu-id="f4cf5-189">Cliquez sur **ENREGISTRER LES MODIFICATIONS**.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-189">Click **SAVE CHANGES**.</span></span>

> [!TIP]
> <span data-ttu-id="f4cf5-190">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="f4cf5-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f4cf5-191">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f4cf5-192">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f4cf5-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f4cf5-193">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4cf5-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="f4cf5-194">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="f4cf5-196">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f4cf5-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f4cf5-197">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f4cf5-199">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f4cf5-201">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f4cf5-203">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f4cf5-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f4cf5-205">a.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-205">a.</span></span> <span data-ttu-id="f4cf5-206">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f4cf5-207">b.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-207">b.</span></span> <span data-ttu-id="f4cf5-208">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f4cf5-209">c.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-209">c.</span></span> <span data-ttu-id="f4cf5-210">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f4cf5-211">d.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-211">d.</span></span> <span data-ttu-id="f4cf5-212">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-212">Click **Create**.</span></span>
 
### <a name="creating-a-syncplicity-test-user"></a><span data-ttu-id="f4cf5-213">Création d’un utilisateur de test Syncplicity</span><span class="sxs-lookup"><span data-stu-id="f4cf5-213">Creating a Syncplicity test user</span></span>
<span data-ttu-id="f4cf5-214">Pour AAD utilisateurs toobe en mesure de toosign dans, ils doivent être mis en service tooSyncplicity application.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-214">For AAD users toobe able toosign in, they must be provisioned tooSyncplicity application.</span></span> <span data-ttu-id="f4cf5-215">Cette section décrit comment les comptes utilisateur de toocreate AAD dans Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-215">This section describes how toocreate AAD user accounts in Syncplicity.</span></span>

<span data-ttu-id="f4cf5-216">**tooprovision un tooSyncplicity de compte d’utilisateur, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f4cf5-216">**tooprovision a user account tooSyncplicity, perform hello following steps:**</span></span>

1. <span data-ttu-id="f4cf5-217">Connectez-vous à tooyour **Syncplicity** locataire (par exemple : `https://company.Syncplicity.com`).</span><span class="sxs-lookup"><span data-stu-id="f4cf5-217">Log in tooyour **Syncplicity** tenant (for example: `https://company.Syncplicity.com`).</span></span>

2. <span data-ttu-id="f4cf5-218">Cliquez sur **admin** et sélectionnez **Comptes d’utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-218">Click **admin** and select **user accounts**.</span></span>

3. <span data-ttu-id="f4cf5-219">Cliquez sur **AJOUTER UN UTILISATEUR**.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-219">Click **ADD A USER**.</span></span>
   
    <span data-ttu-id="f4cf5-220">![Gestion des utilisateurs](./media/active-directory-saas-syncplicity-tutorial/ic769764.png "Gestion des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="f4cf5-220">![Manage Users](./media/active-directory-saas-syncplicity-tutorial/ic769764.png "Manage Users")</span></span>

4. <span data-ttu-id="f4cf5-221">Hello de type **adresses comprises de messagerie** d’un compte AAD que vous souhaitez tooprovision, sélectionnez **utilisateur** en tant que **rôle**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-221">Type hello **Email addressess** of an AAD account you want tooprovision, select **User** as **Role**, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="f4cf5-222">![Informations du compte](./media/active-directory-saas-syncplicity-tutorial/ic769765.png "Informations du compte")</span><span class="sxs-lookup"><span data-stu-id="f4cf5-222">![Account Information](./media/active-directory-saas-syncplicity-tutorial/ic769765.png "Account Information")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="f4cf5-223">titulaire du compte AAD Hello Obtient un message électronique contenant un lien de tooconfirm et activer le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-223">hello AAD account holder  gets an email including a link tooconfirm and activate hello account.</span></span> 
    > 

5. <span data-ttu-id="f4cf5-224">Sélectionnez un groupe dans votre société dont votre nouvel utilisateur doit devenir membre, puis cliquez sur **SUIVANT**.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-224">Select a group in your company that your new user should become a member of, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="f4cf5-225">![Appartenance de groupe](./media/active-directory-saas-syncplicity-tutorial/ic769772.png "Appartenance de groupe")</span><span class="sxs-lookup"><span data-stu-id="f4cf5-225">![Group Membership](./media/active-directory-saas-syncplicity-tutorial/ic769772.png "Group Membership")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="f4cf5-226">Si aucun groupe n’est répertorié, cliquez sur **SUIVANT**.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-226">If there are no groups listed, click **NEXT**.</span></span> 
    > 

6. <span data-ttu-id="f4cf5-227">Sélectionnez les dossiers hello vous comme tooplace sous contrôle de Syncplicity sur l’ordinateur de l’utilisateur hello et puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-227">Select hello folders you would like tooplace under Syncplicity’s control on hello user’s computer, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="f4cf5-228">![Dossiers Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769773.png "Dossiers Syncplicity")</span><span class="sxs-lookup"><span data-stu-id="f4cf5-228">![Syncplicity Folders](./media/active-directory-saas-syncplicity-tutorial/ic769773.png "Syncplicity Folders")</span></span>

>[!NOTE]
><span data-ttu-id="f4cf5-229">Vous pouvez utiliser n’importe quel autre Syncplicity utilisateur compte outil de création ou API fournie par Syncplicity tooprovision des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-229">You can use any other Syncplicity user account creation tools or APIs provided by Syncplicity tooprovision AAD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f4cf5-230">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4cf5-230">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f4cf5-231">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooSyncplicity.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-231">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSyncplicity.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="f4cf5-233">**tooassign Britta Simon tooSyncplicity, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f4cf5-233">**tooassign Britta Simon tooSyncplicity, perform hello following steps:**</span></span>

1. <span data-ttu-id="f4cf5-234">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="f4cf5-236">Dans la liste des applications hello, sélectionnez **Syncplicity**.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-236">In hello applications list, select **Syncplicity**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_app.png) 

3. <span data-ttu-id="f4cf5-238">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="f4cf5-240">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-240">Click **Add** button.</span></span> <span data-ttu-id="f4cf5-241">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="f4cf5-243">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f4cf5-244">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f4cf5-245">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f4cf5-246">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="f4cf5-246">Testing single sign-on</span></span>

<span data-ttu-id="f4cf5-247">objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-247">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f4cf5-248">Lorsque vous cliquez sur mosaïque Syncplicity hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Syncplicity application.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-248">When you click hello Syncplicity tile in hello Access Panel, you should get automatically signed-on tooyour Syncplicity application.</span></span>
## <a name="additional-resources"></a><span data-ttu-id="f4cf5-249">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="f4cf5-249">Additional resources</span></span>

* [<span data-ttu-id="f4cf5-250">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f4cf5-250">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f4cf5-251">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="f4cf5-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_203.png

