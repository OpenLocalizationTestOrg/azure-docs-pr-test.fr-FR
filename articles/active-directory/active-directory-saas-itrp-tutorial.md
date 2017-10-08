---
title: "Didacticiel : Intégration d’Azure Active Directory avec ITRP | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et ITRP."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e09716a3-4200-4853-9414-2390e6c10d98
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 35463a55fcfc1e55c90700737961c1ff2e58992a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-itrp"></a><span data-ttu-id="9f295-103">Didacticiel : Intégration d’Azure Active Directory avec ITRP</span><span class="sxs-lookup"><span data-stu-id="9f295-103">Tutorial: Azure Active Directory integration with ITRP</span></span>

<span data-ttu-id="9f295-104">Dans ce didacticiel, vous apprendrez comment toointegrate ITRP avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9f295-104">In this tutorial, you learn how toointegrate ITRP with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9f295-105">Intégration d’ITRP à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="9f295-105">Integrating ITRP with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9f295-106">Vous pouvez contrôler dans Azure AD qui a accès tooITRP</span><span class="sxs-lookup"><span data-stu-id="9f295-106">You can control in Azure AD who has access tooITRP</span></span>
- <span data-ttu-id="9f295-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooITRP (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f295-107">You can enable your users tooautomatically get signed-on tooITRP (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9f295-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="9f295-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9f295-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9f295-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9f295-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9f295-110">Prerequisites</span></span>

<span data-ttu-id="9f295-111">tooconfigure intégration d’Azure AD à ITRP, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="9f295-111">tooconfigure Azure AD integration with ITRP, you need hello following items:</span></span>

- <span data-ttu-id="9f295-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f295-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9f295-113">Un abonnement ITRP pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="9f295-113">An ITRP single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9f295-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="9f295-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9f295-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="9f295-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9f295-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="9f295-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9f295-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9f295-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9f295-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="9f295-118">Scenario description</span></span>
<span data-ttu-id="9f295-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="9f295-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9f295-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="9f295-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9f295-121">Ajout d’ITRP à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="9f295-121">Adding ITRP from hello gallery</span></span>
2. <span data-ttu-id="9f295-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f295-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-itrp-from-hello-gallery"></a><span data-ttu-id="9f295-123">Ajout d’ITRP à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="9f295-123">Adding ITRP from hello gallery</span></span>
<span data-ttu-id="9f295-124">intégration de hello tooconfigure de ITRP dans tooAzure AD, vous devez tooadd ITRP à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="9f295-124">tooconfigure hello integration of ITRP in tooAzure AD, you need tooadd ITRP from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9f295-125">**tooadd ITRP à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9f295-125">**tooadd ITRP from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f295-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="9f295-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9f295-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="9f295-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9f295-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="9f295-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="9f295-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="9f295-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="9f295-133">Dans la zone de recherche de hello, tapez **ITRP**.</span><span class="sxs-lookup"><span data-stu-id="9f295-133">In hello search box, type **ITRP**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_search.png)

5. <span data-ttu-id="9f295-135">Dans le volet de résultats hello, sélectionnez **ITRP**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="9f295-135">In hello results panel, select **ITRP**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9f295-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f295-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="9f295-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec ITRP, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="9f295-138">In this section, you configure and test Azure AD single sign-on with ITRP based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9f295-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans ITRP est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9f295-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ITRP is tooa user in Azure AD.</span></span> <span data-ttu-id="9f295-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans ITRP doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="9f295-140">In other words, a link relationship between an Azure AD user and hello related user in ITRP needs toobe established.</span></span>

<span data-ttu-id="9f295-141">Dans ITRP, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="9f295-141">In ITRP, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9f295-142">tooconfigure et test Azure AD l’authentification unique à ITRP, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="9f295-142">tooconfigure and test Azure AD single sign-on with ITRP, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9f295-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="9f295-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9f295-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9f295-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9f295-145">**[Utilisateur de test de création d’un ITRP](#creating-an-itrp-test-user)**  -toohave un équivalent de Britta Simon dans ITRP est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9f295-145">**[Creating an ITRP test user](#creating-an-itrp-test-user)** - toohave a counterpart of Britta Simon in ITRP that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9f295-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="9f295-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9f295-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="9f295-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9f295-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f295-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9f295-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application ITRP.</span><span class="sxs-lookup"><span data-stu-id="9f295-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ITRP application.</span></span>

<span data-ttu-id="9f295-150">**tooconfigure Azure AD single sign-on avec ITRP, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9f295-150">**tooconfigure Azure AD single sign-on with ITRP, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f295-151">Bonjour portail Azure, sur hello **ITRP** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="9f295-151">In hello Azure portal, on hello **ITRP** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="9f295-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="9f295-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_samlbase.png)

3. <span data-ttu-id="9f295-155">Sur hello **ITRP domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="9f295-155">On hello **ITRP Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_url.png)

    <span data-ttu-id="9f295-157">a.</span><span class="sxs-lookup"><span data-stu-id="9f295-157">a.</span></span> <span data-ttu-id="9f295-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<tenant-name>.itrp.com`</span><span class="sxs-lookup"><span data-stu-id="9f295-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.itrp.com`</span></span>

    <span data-ttu-id="9f295-159">b.</span><span class="sxs-lookup"><span data-stu-id="9f295-159">b.</span></span> <span data-ttu-id="9f295-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<tenant-name>.itrp.com`</span><span class="sxs-lookup"><span data-stu-id="9f295-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenant-name>.itrp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9f295-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="9f295-161">These values are not real.</span></span> <span data-ttu-id="9f295-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="9f295-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="9f295-163">Contact [équipe de support Client de ITRP](https://www.itrp.com/support) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="9f295-163">Contact [ITRP Client support team](https://www.itrp.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="9f295-164">Sur hello **le certificat de signature SAML** section, hello de copie **l’empreinte numérique** valeur du certificat.</span><span class="sxs-lookup"><span data-stu-id="9f295-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_certificate.png) 

5. <span data-ttu-id="9f295-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="9f295-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-itrp-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9f295-168">Sur hello **ITRP Configuration** , cliquez sur **ITRP de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="9f295-168">On hello **ITRP Configuration** section, click **Configure ITRP** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="9f295-169">Hello de copie **SAML Sign-On URL du Service unique et l’URL de déconnexion** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="9f295-169">Copy hello **SAML Single Sign-On Service URL and Sign-Out URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_configure.png) 

7. <span data-ttu-id="9f295-171">Dans une fenêtre de navigateur web, ouvrez une session dans le site d’entreprise tooyour ITRP en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="9f295-171">In a different web browser window, log in tooyour ITRP company site as an administrator.</span></span>

8. <span data-ttu-id="9f295-172">Dans la barre d’outils de hello en haut de hello, cliquez sur **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="9f295-172">In hello toolbar on hello top, click **Settings**.</span></span>
   
    <span data-ttu-id="9f295-173">![ITRP](./media/active-directory-saas-itrp-tutorial/ic775570.png "ITRP")</span><span class="sxs-lookup"><span data-stu-id="9f295-173">![ITRP](./media/active-directory-saas-itrp-tutorial/ic775570.png "ITRP")</span></span>

8. <span data-ttu-id="9f295-174">Dans le volet de navigation gauche hello, sélectionnez **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="9f295-174">In hello left navigation pane, select **Single Sign-On**.</span></span>
   
    <span data-ttu-id="9f295-175">![Authentification unique](./media/active-directory-saas-itrp-tutorial/ic775571.png "Authentification unique")</span><span class="sxs-lookup"><span data-stu-id="9f295-175">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775571.png "Single Sign-On")</span></span>

9. <span data-ttu-id="9f295-176">Dans la section de configuration de l’authentification unique de hello, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="9f295-176">In hello Single Sign-On configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="9f295-177">![Authentification unique](./media/active-directory-saas-itrp-tutorial/ic775572.png "Authentification unique")</span><span class="sxs-lookup"><span data-stu-id="9f295-177">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775572.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="9f295-178">![Authentification unique](./media/active-directory-saas-itrp-tutorial/ic775573.png "Authentification unique")</span><span class="sxs-lookup"><span data-stu-id="9f295-178">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775573.png "Single Sign-On")</span></span>   

    <span data-ttu-id="9f295-179">a.</span><span class="sxs-lookup"><span data-stu-id="9f295-179">a.</span></span> <span data-ttu-id="9f295-180">Cliquez sur **Enable**.</span><span class="sxs-lookup"><span data-stu-id="9f295-180">Click **Enable**.</span></span>

    <span data-ttu-id="9f295-181">b.</span><span class="sxs-lookup"><span data-stu-id="9f295-181">b.</span></span> <span data-ttu-id="9f295-182">Dans **distant URL de déconnexion** zone de texte, valeur hello coller **URL de déconnexion**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="9f295-182">In **Remote Log Out URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="9f295-183">c.</span><span class="sxs-lookup"><span data-stu-id="9f295-183">c.</span></span> <span data-ttu-id="9f295-184">Dans **URL SSO SAML** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="9f295-184">In **SAML SSO URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="9f295-185">d.In **empreinte numérique du certificat** zone de texte, collez hello **l’empreinte numérique** valeur de certificat, ce qui vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="9f295-185">d.In **Certificate Fingerprint** textbox, paste hello **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span> 
      
10. <span data-ttu-id="9f295-186">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="9f295-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="9f295-187">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="9f295-187">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9f295-188">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="9f295-188">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9f295-189">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9f295-189">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9f295-190">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f295-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="9f295-191">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="9f295-191">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="9f295-193">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9f295-193">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f295-194">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="9f295-194">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-itrp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9f295-196">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="9f295-196">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-itrp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9f295-198">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="9f295-198">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-itrp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9f295-200">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="9f295-200">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-itrp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9f295-202">a.</span><span class="sxs-lookup"><span data-stu-id="9f295-202">a.</span></span> <span data-ttu-id="9f295-203">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9f295-203">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9f295-204">b.</span><span class="sxs-lookup"><span data-stu-id="9f295-204">b.</span></span> <span data-ttu-id="9f295-205">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9f295-205">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9f295-206">c.</span><span class="sxs-lookup"><span data-stu-id="9f295-206">c.</span></span> <span data-ttu-id="9f295-207">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="9f295-207">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9f295-208">d.</span><span class="sxs-lookup"><span data-stu-id="9f295-208">d.</span></span> <span data-ttu-id="9f295-209">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="9f295-209">Click **Create**.</span></span>
 
### <a name="creating-an-itrp-test-user"></a><span data-ttu-id="9f295-210">Création d’un utilisateur de test ITRP</span><span class="sxs-lookup"><span data-stu-id="9f295-210">Creating an ITRP test user</span></span>

<span data-ttu-id="9f295-211">tooenable Azure AD les utilisateurs toolog dans tooITRP, ils doivent être configurés dans tooITRP.</span><span class="sxs-lookup"><span data-stu-id="9f295-211">tooenable Azure AD users toolog in tooITRP, they must be provisioned in tooITRP.</span></span>  

<span data-ttu-id="9f295-212">Dans le cas de hello d’ITRP, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="9f295-212">In hello case of ITRP, provisioning is a manual task.</span></span>

<span data-ttu-id="9f295-213">**tooprovision un compte d’utilisateur, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9f295-213">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f295-214">Connectez-vous à tooyour **ITRP** client.</span><span class="sxs-lookup"><span data-stu-id="9f295-214">Log in tooyour **ITRP** tenant.</span></span>

2. <span data-ttu-id="9f295-215">Dans la barre d’outils de hello en haut de hello, cliquez sur **enregistrements**.</span><span class="sxs-lookup"><span data-stu-id="9f295-215">In hello toolbar on hello top, click **Records**.</span></span>
   
    <span data-ttu-id="9f295-216">![Administrateur](./media/active-directory-saas-itrp-tutorial/ic775575.png "Administrateur")</span><span class="sxs-lookup"><span data-stu-id="9f295-216">![Admin](./media/active-directory-saas-itrp-tutorial/ic775575.png "Admin")</span></span>

3. <span data-ttu-id="9f295-217">Dans le menu contextuel de hello, sélectionnez **personnes**.</span><span class="sxs-lookup"><span data-stu-id="9f295-217">From hello popup menu, select **People**.</span></span>
   
    <span data-ttu-id="9f295-218">![Personnes](./media/active-directory-saas-itrp-tutorial/ic775587.png "Personnes")</span><span class="sxs-lookup"><span data-stu-id="9f295-218">![People](./media/active-directory-saas-itrp-tutorial/ic775587.png "People")</span></span>

4. <span data-ttu-id="9f295-219">Cliquez sur **Add New Person** (« + »).</span><span class="sxs-lookup"><span data-stu-id="9f295-219">Click **Add New Person** (“+”).</span></span>
   
    <span data-ttu-id="9f295-220">![Administrateur](./media/active-directory-saas-itrp-tutorial/ic775576.png "Administrateur")</span><span class="sxs-lookup"><span data-stu-id="9f295-220">![Admin](./media/active-directory-saas-itrp-tutorial/ic775576.png "Admin")</span></span>

5. <span data-ttu-id="9f295-221">Dans la boîte de dialogue Ajouter une nouvelle personne hello, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="9f295-221">On hello Add New Person dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="9f295-222">![Utilisateur](./media/active-directory-saas-itrp-tutorial/ic775577.png "Utilisateur")</span><span class="sxs-lookup"><span data-stu-id="9f295-222">![User](./media/active-directory-saas-itrp-tutorial/ic775577.png "User")</span></span> 
      
    <span data-ttu-id="9f295-223">a.</span><span class="sxs-lookup"><span data-stu-id="9f295-223">a.</span></span> <span data-ttu-id="9f295-224">Hello de type **nom**, **messagerie** d’un compte AAD valide que vous souhaitez tooprovision.</span><span class="sxs-lookup"><span data-stu-id="9f295-224">Type hello **Name**, **Email** of a valid AAD account you want tooprovision.</span></span>

    <span data-ttu-id="9f295-225">b.</span><span class="sxs-lookup"><span data-stu-id="9f295-225">b.</span></span> <span data-ttu-id="9f295-226">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="9f295-226">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="9f295-227">Vous pouvez utiliser n’importe quel autre ITRP utilisateur compte outil de création ou API fournie par ITRP tooprovision des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="9f295-227">You can use any other ITRP user account creation tools or APIs provided by ITRP tooprovision AAD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9f295-228">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f295-228">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9f295-229">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooITRP.</span><span class="sxs-lookup"><span data-stu-id="9f295-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooITRP.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="9f295-231">**tooassign Britta Simon tooITRP, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9f295-231">**tooassign Britta Simon tooITRP, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f295-232">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="9f295-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="9f295-234">Dans la liste des applications hello, sélectionnez **ITRP**.</span><span class="sxs-lookup"><span data-stu-id="9f295-234">In hello applications list, select **ITRP**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_app.png) 

3. <span data-ttu-id="9f295-236">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="9f295-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="9f295-238">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="9f295-238">Click **Add** button.</span></span> <span data-ttu-id="9f295-239">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="9f295-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="9f295-241">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="9f295-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9f295-242">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="9f295-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9f295-243">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="9f295-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9f295-244">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="9f295-244">Testing single sign-on</span></span>

<span data-ttu-id="9f295-245">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="9f295-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9f295-246">Lorsque vous cliquez sur hello ITRP vignette Bonjour volet d’accès, vous devez obtenir l’application d’ITRP tooyour automatiquement signé sur.</span><span class="sxs-lookup"><span data-stu-id="9f295-246">When you click hello ITRP tile in hello Access Panel, you should get automatically signed-on tooyour ITRP application.</span></span>
<span data-ttu-id="9f295-247">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9f295-247">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9f295-248">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="9f295-248">Additional resources</span></span>

* [<span data-ttu-id="9f295-249">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9f295-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9f295-250">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="9f295-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_203.png

