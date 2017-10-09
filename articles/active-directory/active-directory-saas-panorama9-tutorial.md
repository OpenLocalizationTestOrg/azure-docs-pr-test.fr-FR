---
title: "Didacticiel : Intégration d’Azure Active Directory avec Panorama9 | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Panorama9."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5e28d7fa-03be-49f3-96c8-b567f1257d44
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 548fb6434d920e076db98a0193f8dfdf8a958a91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-panorama9"></a><span data-ttu-id="259c7-103">Didacticiel : Intégration d’Azure Active Directory avec Panorama9</span><span class="sxs-lookup"><span data-stu-id="259c7-103">Tutorial: Azure Active Directory integration with Panorama9</span></span>

<span data-ttu-id="259c7-104">Dans ce didacticiel, vous apprendrez comment toointegrate Panorama9 avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="259c7-104">In this tutorial, you learn how toointegrate Panorama9 with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="259c7-105">Intégration de Panorama9 à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="259c7-105">Integrating Panorama9 with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="259c7-106">Vous pouvez contrôler dans Azure AD qui a accès tooPanorama9</span><span class="sxs-lookup"><span data-stu-id="259c7-106">You can control in Azure AD who has access tooPanorama9</span></span>
- <span data-ttu-id="259c7-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooPanorama9 (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="259c7-107">You can enable your users tooautomatically get signed-on tooPanorama9 (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="259c7-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="259c7-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="259c7-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="259c7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="259c7-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="259c7-110">Prerequisites</span></span>

<span data-ttu-id="259c7-111">tooconfigure intégration d’Azure AD avec Panorama9, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="259c7-111">tooconfigure Azure AD integration with Panorama9, you need hello following items:</span></span>

- <span data-ttu-id="259c7-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="259c7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="259c7-113">Un abonnement Panorama9 pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="259c7-113">A Panorama9 single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="259c7-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="259c7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="259c7-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="259c7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="259c7-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="259c7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="259c7-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="259c7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="259c7-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="259c7-118">Scenario description</span></span>
<span data-ttu-id="259c7-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="259c7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="259c7-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="259c7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="259c7-121">Ajout de Panorama9 à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="259c7-121">Adding Panorama9 from hello gallery</span></span>
2. <span data-ttu-id="259c7-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="259c7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-panorama9-from-hello-gallery"></a><span data-ttu-id="259c7-123">Ajout de Panorama9 à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="259c7-123">Adding Panorama9 from hello gallery</span></span>
<span data-ttu-id="259c7-124">intégration de hello tooconfigure de Panorama9 dans Azure AD, vous devez tooadd Panorama9 à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="259c7-124">tooconfigure hello integration of Panorama9 into Azure AD, you need tooadd Panorama9 from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="259c7-125">**tooadd Panorama9 à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="259c7-125">**tooadd Panorama9 from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="259c7-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="259c7-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="259c7-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="259c7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="259c7-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="259c7-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="259c7-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="259c7-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="259c7-133">Dans la zone de recherche de hello, tapez **Panorama9**.</span><span class="sxs-lookup"><span data-stu-id="259c7-133">In hello search box, type **Panorama9**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_search.png)

5. <span data-ttu-id="259c7-135">Dans le volet de résultats hello, sélectionnez **Panorama9**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="259c7-135">In hello results panel, select **Panorama9**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="259c7-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="259c7-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="259c7-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Panorama9 sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="259c7-138">In this section, you configure and test Azure AD single sign-on with Panorama9 based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="259c7-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Panorama9 est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="259c7-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Panorama9 is tooa user in Azure AD.</span></span> <span data-ttu-id="259c7-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Panorama9 doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="259c7-140">In other words, a link relationship between an Azure AD user and hello related user in Panorama9 needs toobe established.</span></span>

<span data-ttu-id="259c7-141">Dans Panorama9, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="259c7-141">In Panorama9, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="259c7-142">tooconfigure et test Azure AD l’authentification unique avec Panorama9, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="259c7-142">tooconfigure and test Azure AD single sign-on with Panorama9, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="259c7-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="259c7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="259c7-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="259c7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="259c7-145">**[Création d’un utilisateur de test de Panorama9](#creating-a-panorama9-test-user)**  -toohave un équivalent de Britta Simon dans Panorama9 est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="259c7-145">**[Creating a Panorama9 test user](#creating-a-panorama9-test-user)** - toohave a counterpart of Britta Simon in Panorama9 that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="259c7-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="259c7-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="259c7-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="259c7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="259c7-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="259c7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="259c7-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Panorama9.</span><span class="sxs-lookup"><span data-stu-id="259c7-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Panorama9 application.</span></span>

<span data-ttu-id="259c7-150">**tooconfigure Azure AD single sign-on avec Panorama9, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="259c7-150">**tooconfigure Azure AD single sign-on with Panorama9, perform hello following steps:**</span></span>

1. <span data-ttu-id="259c7-151">Bonjour portail Azure, sur hello **Panorama9** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="259c7-151">In hello Azure portal, on hello **Panorama9** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="259c7-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="259c7-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_samlbase.png)

3. <span data-ttu-id="259c7-155">Sur hello **Panorama9 domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="259c7-155">On hello **Panorama9 Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_url.png)

    <span data-ttu-id="259c7-157">a.</span><span class="sxs-lookup"><span data-stu-id="259c7-157">a.</span></span> <span data-ttu-id="259c7-158">Bonjour **URL de connexion** zone de texte, tapez une URL en tant que :`https://dashboard.panorama9.com/saml/access/3262`</span><span class="sxs-lookup"><span data-stu-id="259c7-158">In hello **Sign-on URL** textbox, type a URL as: `https://dashboard.panorama9.com/saml/access/3262`</span></span>

    <span data-ttu-id="259c7-159">b.</span><span class="sxs-lookup"><span data-stu-id="259c7-159">b.</span></span> <span data-ttu-id="259c7-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`http://www.panorama9.com/saml20/<tenant-name>`</span><span class="sxs-lookup"><span data-stu-id="259c7-160">In hello **Identifier** textbox, type a URL using hello following pattern: `http://www.panorama9.com/saml20/<tenant-name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="259c7-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="259c7-161">These values are not real.</span></span> <span data-ttu-id="259c7-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="259c7-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="259c7-163">Contact [équipe de support Client de Panorama9](https://support.panorama9.com) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="259c7-163">Contact [Panorama9 Client support team](https://support.panorama9.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="259c7-164">Sur hello **le certificat de signature SAML** section, hello de copie **l’empreinte numérique** valeur du certificat.</span><span class="sxs-lookup"><span data-stu-id="259c7-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_certificate.png) 

5. <span data-ttu-id="259c7-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="259c7-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-panorama9-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="259c7-168">Sur hello **Panorama9 Configuration** , cliquez sur **configurer de Panorama9** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="259c7-168">On hello **Panorama9 Configuration** section, click **Configure Panorama9** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="259c7-169">Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="259c7-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_configure.png) 

5. <span data-ttu-id="259c7-171">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Panorama9 en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="259c7-171">In a different web browser window, log into your Panorama9 company site as an administrator.</span></span>

6. <span data-ttu-id="259c7-172">Dans la barre d’outils de hello en haut de hello, cliquez sur **gérer**, puis cliquez sur **Extensions**.</span><span class="sxs-lookup"><span data-stu-id="259c7-172">In hello toolbar on hello top, click **Manage**, and then click **Extensions**.</span></span>
   
   <span data-ttu-id="259c7-173">![Extensions](./media/active-directory-saas-panorama9-tutorial/ic790023.png "Extensions")</span><span class="sxs-lookup"><span data-stu-id="259c7-173">![Extensions](./media/active-directory-saas-panorama9-tutorial/ic790023.png "Extensions")</span></span>
7. <span data-ttu-id="259c7-174">Sur hello **Extensions** boîte de dialogue, cliquez sur **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="259c7-174">On hello **Extensions** dialog, click **Single Sign-On**.</span></span>
   
   <span data-ttu-id="259c7-175">![Authentification unique](./media/active-directory-saas-panorama9-tutorial/ic790024.png "Authentification unique")</span><span class="sxs-lookup"><span data-stu-id="259c7-175">![Single Sign-On](./media/active-directory-saas-panorama9-tutorial/ic790024.png "Single Sign-On")</span></span>
8. <span data-ttu-id="259c7-176">Bonjour **paramètres** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="259c7-176">In hello **Settings** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="259c7-177">![Paramètres](./media/active-directory-saas-panorama9-tutorial/ic790025.png "Paramètres")</span><span class="sxs-lookup"><span data-stu-id="259c7-177">![Settings](./media/active-directory-saas-panorama9-tutorial/ic790025.png "Settings")</span></span>
   
    <span data-ttu-id="259c7-178">a.</span><span class="sxs-lookup"><span data-stu-id="259c7-178">a.</span></span> <span data-ttu-id="259c7-179">Dans **URL du fournisseur d’identité** zone de texte, valeur hello coller **-Service URL d’authentification**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="259c7-179">In **Identity provider URL** textbox, paste hello value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="259c7-180">b.</span><span class="sxs-lookup"><span data-stu-id="259c7-180">b.</span></span> <span data-ttu-id="259c7-181">Dans **empreinte numérique du certificat** zone de texte, collez hello **l’empreinte numérique** valeur de certificat, ce qui vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="259c7-181">In **Certificate fingerprint** textbox, paste hello **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>    
         
9. <span data-ttu-id="259c7-182">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="259c7-182">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="259c7-183">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="259c7-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="259c7-184">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="259c7-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="259c7-185">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="259c7-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="259c7-186">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="259c7-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="259c7-187">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="259c7-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="259c7-189">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="259c7-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="259c7-190">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="259c7-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="259c7-192">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="259c7-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="259c7-194">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="259c7-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="259c7-196">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="259c7-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="259c7-198">a.</span><span class="sxs-lookup"><span data-stu-id="259c7-198">a.</span></span> <span data-ttu-id="259c7-199">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="259c7-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="259c7-200">b.</span><span class="sxs-lookup"><span data-stu-id="259c7-200">b.</span></span> <span data-ttu-id="259c7-201">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="259c7-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="259c7-202">c.</span><span class="sxs-lookup"><span data-stu-id="259c7-202">c.</span></span> <span data-ttu-id="259c7-203">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="259c7-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="259c7-204">d.</span><span class="sxs-lookup"><span data-stu-id="259c7-204">d.</span></span> <span data-ttu-id="259c7-205">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="259c7-205">Click **Create**.</span></span>
 
### <a name="creating-a-panorama9-test-user"></a><span data-ttu-id="259c7-206">Création d’un utilisateur de test Panorama9</span><span class="sxs-lookup"><span data-stu-id="259c7-206">Creating a Panorama9 test user</span></span>

<span data-ttu-id="259c7-207">Dans l’ordre tooenable Azure AD les utilisateurs toolog à Panorama9, vous devez les configurer dans Panorama9.</span><span class="sxs-lookup"><span data-stu-id="259c7-207">In order tooenable Azure AD users toolog into Panorama9, they must be provisioned into Panorama9.</span></span>  

<span data-ttu-id="259c7-208">Dans les cas de hello de Panorama9, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="259c7-208">In hello case of Panorama9, provisioning is a manual task.</span></span>

<span data-ttu-id="259c7-209">**configuration, de l’utilisateur tooconfigure effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="259c7-209">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="259c7-210">Connectez-vous à tooyour **Panorama9** site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="259c7-210">Log in tooyour **Panorama9** company site as an administrator.</span></span>

2. <span data-ttu-id="259c7-211">Dans le menu hello haut de hello, cliquez sur **gérer**, puis cliquez sur **utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="259c7-211">In hello menu on hello top, click **Manage**, and then click **Users**.</span></span>
   
  <span data-ttu-id="259c7-212">![Utilisateurs](./media/active-directory-saas-panorama9-tutorial/ic790027.png "Utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="259c7-212">![Users](./media/active-directory-saas-panorama9-tutorial/ic790027.png "Users")</span></span>

3. <span data-ttu-id="259c7-213">Bonjour section utilisateurs, cliquez sur  **+**  tooadd nouvel utilisateur.</span><span class="sxs-lookup"><span data-stu-id="259c7-213">In hello Users section, Click **+** tooadd new user.</span></span>

 <span data-ttu-id="259c7-214">![Utilisateurs](./media/active-directory-saas-panorama9-tutorial/ic790028.png "Utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="259c7-214">![Users](./media/active-directory-saas-panorama9-tutorial/ic790028.png "Users")</span></span>

4. <span data-ttu-id="259c7-215">Accédez toohello section User data, hello de type adresse de messagerie d’un utilisateur Azure Active Directory valide que vous souhaitez tooprovision dans hello **messagerie** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="259c7-215">Go toohello User data section, type hello email address of a valid Azure Active Directory user you want tooprovision into hello **Email** textbox.</span></span>

5. <span data-ttu-id="259c7-216">Provenir toohello section utilisateurs, cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="259c7-216">Come toohello Users section, Click **Save**.</span></span>
   
> [!NOTE]
    > <span data-ttu-id="259c7-217">titulaire du compte Azure Active Directory Hello reçoit un message électronique et suit un tooconfirm de lier leur compte avant son activation.</span><span class="sxs-lookup"><span data-stu-id="259c7-217">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="259c7-218">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="259c7-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="259c7-219">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooPanorama9.</span><span class="sxs-lookup"><span data-stu-id="259c7-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPanorama9.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="259c7-221">**tooassign Britta Simon tooPanorama9, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="259c7-221">**tooassign Britta Simon tooPanorama9, perform hello following steps:**</span></span>

1. <span data-ttu-id="259c7-222">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="259c7-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="259c7-224">Dans la liste des applications hello, sélectionnez **Panorama9**.</span><span class="sxs-lookup"><span data-stu-id="259c7-224">In hello applications list, select **Panorama9**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_app.png) 

3. <span data-ttu-id="259c7-226">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="259c7-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="259c7-228">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="259c7-228">Click **Add** button.</span></span> <span data-ttu-id="259c7-229">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="259c7-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="259c7-231">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="259c7-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="259c7-232">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="259c7-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="259c7-233">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="259c7-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="259c7-234">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="259c7-234">Testing single sign-on</span></span>

<span data-ttu-id="259c7-235">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="259c7-235">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="259c7-236">Lorsque vous cliquez sur mosaïque hello Panorama9 Bonjour volet d’accès, vous devez obtenir tooPanorama9 automatiquement signé sur application.</span><span class="sxs-lookup"><span data-stu-id="259c7-236">When you click hello Panorama9 tile in hello Access Panel, you should get automatically signed-on tooPanorama9 application.</span></span>
<span data-ttu-id="259c7-237">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="259c7-237">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="259c7-238">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="259c7-238">Additional resources</span></span>

* [<span data-ttu-id="259c7-239">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="259c7-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="259c7-240">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="259c7-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_203.png

