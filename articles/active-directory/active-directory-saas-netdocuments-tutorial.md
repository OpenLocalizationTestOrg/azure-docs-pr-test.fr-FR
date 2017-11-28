---
title: "Didacticiel : Intégration d’Azure Active Directory à NetDocuments | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de NetDocuments."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1a47dc42-1a17-48a2-965e-eca4cfb2f197
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: ee9887553595a2492642aed4cb4abcd11d9cf599
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netdocuments"></a><span data-ttu-id="e3b9f-103">Didacticiel : Intégration d’Azure Active Directory à NetDocuments</span><span class="sxs-lookup"><span data-stu-id="e3b9f-103">Tutorial: Azure Active Directory integration with NetDocuments</span></span>

<span data-ttu-id="e3b9f-104">Dans ce didacticiel, vous apprendrez comment toointegrate NetDocuments avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e3b9f-104">In this tutorial, you learn how toointegrate NetDocuments with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e3b9f-105">Intégration de NetDocuments à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="e3b9f-105">Integrating NetDocuments with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e3b9f-106">Vous pouvez contrôler dans Azure AD qui a accès tooNetDocuments</span><span class="sxs-lookup"><span data-stu-id="e3b9f-106">You can control in Azure AD who has access tooNetDocuments</span></span>
- <span data-ttu-id="e3b9f-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooNetDocuments (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3b9f-107">You can enable your users tooautomatically get signed-on tooNetDocuments (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e3b9f-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="e3b9f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e3b9f-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e3b9f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e3b9f-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e3b9f-110">Prerequisites</span></span>

<span data-ttu-id="e3b9f-111">tooconfigure intégration d’Azure AD à NetDocuments, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="e3b9f-111">tooconfigure Azure AD integration with NetDocuments, you need hello following items:</span></span>

- <span data-ttu-id="e3b9f-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3b9f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e3b9f-113">Un abonnement NetDocuments pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="e3b9f-113">A NetDocuments single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e3b9f-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e3b9f-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="e3b9f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e3b9f-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e3b9f-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e3b9f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e3b9f-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="e3b9f-118">Scenario description</span></span>
<span data-ttu-id="e3b9f-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e3b9f-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="e3b9f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e3b9f-121">Ajout de NetDocuments à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="e3b9f-121">Adding NetDocuments from hello gallery</span></span>
2. <span data-ttu-id="e3b9f-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3b9f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-netdocuments-from-hello-gallery"></a><span data-ttu-id="e3b9f-123">Ajout de NetDocuments à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="e3b9f-123">Adding NetDocuments from hello gallery</span></span>
<span data-ttu-id="e3b9f-124">intégration de hello tooconfigure de NetDocuments dans Azure AD, vous devez tooadd NetDocuments à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-124">tooconfigure hello integration of NetDocuments into Azure AD, you need tooadd NetDocuments from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e3b9f-125">**tooadd NetDocuments à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e3b9f-125">**tooadd NetDocuments from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e3b9f-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e3b9f-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e3b9f-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="e3b9f-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="e3b9f-133">Dans la zone de recherche de hello, tapez **NetDocuments**.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-133">In hello search box, type **NetDocuments**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_search.png)

5. <span data-ttu-id="e3b9f-135">Dans le volet de résultats hello, sélectionnez **NetDocuments**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-135">In hello results panel, select **NetDocuments**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e3b9f-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3b9f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e3b9f-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec NetDocuments avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="e3b9f-138">In this section, you configure and test Azure AD single sign-on with NetDocuments based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e3b9f-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans NetDocuments est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in NetDocuments is tooa user in Azure AD.</span></span> <span data-ttu-id="e3b9f-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans NetDocuments doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-140">In other words, a link relationship between an Azure AD user and hello related user in NetDocuments needs toobe established.</span></span>

<span data-ttu-id="e3b9f-141">Dans NetDocuments, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-141">In NetDocuments, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e3b9f-142">tooconfigure et test Azure AD l’authentification unique à NetDocuments, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="e3b9f-142">tooconfigure and test Azure AD single sign-on with NetDocuments, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e3b9f-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e3b9f-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e3b9f-145">**[Création d’un utilisateur de test de NetDocuments](#creating-a-netdocuments-test-user)**  -toohave un équivalent de Britta Simon dans NetDocuments est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-145">**[Creating a NetDocuments test user](#creating-a-netdocuments-test-user)** - toohave a counterpart of Britta Simon in NetDocuments that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e3b9f-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e3b9f-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e3b9f-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3b9f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e3b9f-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your NetDocuments application.</span></span>

<span data-ttu-id="e3b9f-150">**tooconfigure Azure AD single sign-on avec NetDocuments, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e3b9f-150">**tooconfigure Azure AD single sign-on with NetDocuments, perform hello following steps:**</span></span>

1. <span data-ttu-id="e3b9f-151">Bonjour portail Azure, sur hello **NetDocuments** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-151">In hello Azure portal, on hello **NetDocuments** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="e3b9f-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_samlbase.png)

3. <span data-ttu-id="e3b9f-155">Sur hello **NetDocuments domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e3b9f-155">On hello **NetDocuments Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_url.png)

    <span data-ttu-id="e3b9f-157">a.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-157">a.</span></span> <span data-ttu-id="e3b9f-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span><span class="sxs-lookup"><span data-stu-id="e3b9f-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span></span>

    <span data-ttu-id="e3b9f-159">b.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-159">b.</span></span> <span data-ttu-id="e3b9f-160">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span><span class="sxs-lookup"><span data-stu-id="e3b9f-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e3b9f-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-161">These values are not real.</span></span> <span data-ttu-id="e3b9f-162">Mettre à jour ces valeurs avec l’URL de connexion réel hello et URL de réponse.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-162">Update these values with hello actual Sign-on URL and Reply URL.</span></span> <span data-ttu-id="e3b9f-163">Contact [NetDocuments l’équipe de support](https://support.netdocuments.com/hc/) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-163">Contact [NetDocuments support team](https://support.netdocuments.com/hc/) tooget these values.</span></span>
 
4. <span data-ttu-id="e3b9f-164">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_certificate.png) 

5. <span data-ttu-id="e3b9f-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="e3b9f-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-netdocuments-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e3b9f-168">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise NetDocuments en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-168">In a different web browser window, log into your NetDocuments company site as an administrator.</span></span>

7. <span data-ttu-id="e3b9f-169">Accédez trop**Admin**.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-169">Go too**Admin**.</span></span>

8. <span data-ttu-id="e3b9f-170">Cliquez sur **Add and remove users and groups**.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-170">Click **Add and remove users and groups**.</span></span>
   
    <span data-ttu-id="e3b9f-171">![Référentiel](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Référentiel")</span><span class="sxs-lookup"><span data-stu-id="e3b9f-171">![Repository](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repository")</span></span>

9. <span data-ttu-id="e3b9f-172">Cliquez sur **Configure advanced authentication options**.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-172">Click **Configure advanced authentication options**.</span></span>
    
    <span data-ttu-id="e3b9f-173">![Configurer les options d’authentification avancées](./media/active-directory-saas-netdocuments-tutorial/ic795048.png "Configurer les options d’authentification avancées")</span><span class="sxs-lookup"><span data-stu-id="e3b9f-173">![Configure advanced authentication options](./media/active-directory-saas-netdocuments-tutorial/ic795048.png "Configure advanced authentication options")</span></span>

10. <span data-ttu-id="e3b9f-174">Sur hello **identité fédérée** boîte de dialogue, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e3b9f-174">On hello **Federated Identity** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="e3b9f-175">![Identité fédérée](./media/active-directory-saas-netdocuments-tutorial/ic795049.png "Identité fédérée")</span><span class="sxs-lookup"><span data-stu-id="e3b9f-175">![Federated Identitty](./media/active-directory-saas-netdocuments-tutorial/ic795049.png "Federated Identitty")</span></span>
   
    <span data-ttu-id="e3b9f-176">a.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-176">a.</span></span> <span data-ttu-id="e3b9f-177">Pour **Federated identity server type**, sélectionnez **Active Directory Federation Services**.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-177">As **Federated identity server type**, select **Active Directory Federation Services**.</span></span>
   
    <span data-ttu-id="e3b9f-178">b.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-178">b.</span></span> <span data-ttu-id="e3b9f-179">Cliquez sur **choisir un fichier**, hello de tooupload téléchargé le fichier de métadonnées qui vous avez téléchargé à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-179">Click **Choose file**, tooupload hello downloaded metadata file which you have downloaded from Azure portal.</span></span>
   
    <span data-ttu-id="e3b9f-180">c.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-180">c.</span></span> <span data-ttu-id="e3b9f-181">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-181">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="e3b9f-182">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="e3b9f-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e3b9f-183">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e3b9f-184">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e3b9f-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e3b9f-185">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3b9f-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="e3b9f-186">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="e3b9f-188">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e3b9f-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e3b9f-189">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-189">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e3b9f-191">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-191">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e3b9f-193">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-193">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e3b9f-195">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e3b9f-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e3b9f-197">a.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-197">a.</span></span> <span data-ttu-id="e3b9f-198">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e3b9f-199">b.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-199">b.</span></span> <span data-ttu-id="e3b9f-200">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-200">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e3b9f-201">c.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-201">c.</span></span> <span data-ttu-id="e3b9f-202">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e3b9f-203">d.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-203">d.</span></span> <span data-ttu-id="e3b9f-204">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-204">Click **Create**.</span></span>
 
### <a name="creating-a-netdocuments-test-user"></a><span data-ttu-id="e3b9f-205">Création d’un utilisateur de test NetDocuments</span><span class="sxs-lookup"><span data-stu-id="e3b9f-205">Creating a NetDocuments test user</span></span>

<span data-ttu-id="e3b9f-206">tooenable Azure AD les utilisateurs toolog dans tooNetDocuments, vous devez les configurer dans NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-206">tooenable Azure AD users toolog in tooNetDocuments, they must be provisioned into NetDocuments.</span></span>  
<span data-ttu-id="e3b9f-207">Dans les cas de hello de NetDocuments, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-207">In hello case of NetDocuments, provisioning is a manual task.</span></span>

<span data-ttu-id="e3b9f-208">**tooprovision un compte d’utilisateur, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e3b9f-208">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="e3b9f-209">Ouverture de session sur tooyour **NetDocuments** site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-209">Sing on tooyour **NetDocuments** company site as administrator.</span></span>

2. <span data-ttu-id="e3b9f-210">Dans le menu hello haut de hello, cliquez sur **Admin**.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-210">In hello menu on hello top, click **Admin**.</span></span>
   
    <span data-ttu-id="e3b9f-211">![Administrateur](./media/active-directory-saas-netdocuments-tutorial/ic795051.png "Administrateur")</span><span class="sxs-lookup"><span data-stu-id="e3b9f-211">![Admin](./media/active-directory-saas-netdocuments-tutorial/ic795051.png "Admin")</span></span>

3. <span data-ttu-id="e3b9f-212">Cliquez sur **Add and remove users and groups**.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-212">Click **Add and remove users and groups**.</span></span>
   
    <span data-ttu-id="e3b9f-213">![Référentiel](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Référentiel")</span><span class="sxs-lookup"><span data-stu-id="e3b9f-213">![Repository](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repository")</span></span>

4. <span data-ttu-id="e3b9f-214">Bonjour **adresse de messagerie** zone de texte, tapez Bonjour adresse de messagerie d’un compte Azure Active Directory valide que vous souhaitez tooprovision, puis cliquez **ajouter un utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-214">In hello **Email Address** textbox, type hello email address of a valid Azure Active Directory account you want tooprovision, and then click **Add User**.</span></span>
   
    <span data-ttu-id="e3b9f-215">![Adresse de messagerie](./media/active-directory-saas-netdocuments-tutorial/ic795053.png "adresse de messagerie")</span><span class="sxs-lookup"><span data-stu-id="e3b9f-215">![Email Address](./media/active-directory-saas-netdocuments-tutorial/ic795053.png "Email Address")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="e3b9f-216">détenteur du compte de Hello Azure Active Directory reçoit un message électronique qui inclut un compte de hello tooconfirm lien avant son activation.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-216">hello Azure Active Directory account holder will get an email that includes a link tooconfirm hello account before it becomes active.</span></span> <span data-ttu-id="e3b9f-217">Vous pouvez utiliser n’importe quel autre NetDocuments utilisateur compte outil de création ou API fournie par NetDocuments tooprovision Azure Active Directory des comptes d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-217">You can use any other NetDocuments user account creation tools or APIs provided by NetDocuments tooprovision Azure Active Directory user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e3b9f-218">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3b9f-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e3b9f-219">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooNetDocuments.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNetDocuments.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="e3b9f-221">**tooassign Britta Simon tooNetDocuments, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e3b9f-221">**tooassign Britta Simon tooNetDocuments, perform hello following steps:**</span></span>

1. <span data-ttu-id="e3b9f-222">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="e3b9f-224">Dans la liste des applications hello, sélectionnez **NetDocuments**.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-224">In hello applications list, select **NetDocuments**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_app.png) 

3. <span data-ttu-id="e3b9f-226">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="e3b9f-228">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-228">Click **Add** button.</span></span> <span data-ttu-id="e3b9f-229">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="e3b9f-231">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e3b9f-232">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e3b9f-233">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e3b9f-234">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="e3b9f-234">Testing single sign-on</span></span>

<span data-ttu-id="e3b9f-235">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-235">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e3b9f-236">Lorsque vous cliquez sur hello NetDocuments vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour application NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="e3b9f-236">When you click hello NetDocuments tile in hello Access Panel, you should get automatically signed-on tooyour NetDocuments application.</span></span>
<span data-ttu-id="e3b9f-237">Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e3b9f-237">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e3b9f-238">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="e3b9f-238">Additional resources</span></span>

* [<span data-ttu-id="e3b9f-239">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e3b9f-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e3b9f-240">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="e3b9f-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_203.png

