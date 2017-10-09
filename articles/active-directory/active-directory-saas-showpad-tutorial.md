---
title: "Didacticiel : Intégration d’Azure Active Directory à Showpad | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Showpad."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 48b6bee0-dbc5-4863-964d-75b25e517741
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 2c8c306b4b94c368a93f92123d3abe9fe35167db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-showpad"></a><span data-ttu-id="4b4d9-103">Didacticiel : intégration d’Azure Active Directory à Showpad</span><span class="sxs-lookup"><span data-stu-id="4b4d9-103">Tutorial: Azure Active Directory integration with Showpad</span></span>

<span data-ttu-id="4b4d9-104">Dans ce didacticiel, vous apprendrez comment toointegrate Showpad avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4b4d9-104">In this tutorial, you learn how toointegrate Showpad with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4b4d9-105">Intégration Showpad à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="4b4d9-105">Integrating Showpad with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4b4d9-106">Vous pouvez contrôler dans Azure AD qui a accès tooShowpad</span><span class="sxs-lookup"><span data-stu-id="4b4d9-106">You can control in Azure AD who has access tooShowpad</span></span>
- <span data-ttu-id="4b4d9-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooShowpad (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b4d9-107">You can enable your users tooautomatically get signed-on tooShowpad (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4b4d9-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="4b4d9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4b4d9-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4b4d9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4b4d9-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="4b4d9-110">Prerequisites</span></span>

<span data-ttu-id="4b4d9-111">tooconfigure intégration d’Azure AD avec Showpad, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="4b4d9-111">tooconfigure Azure AD integration with Showpad, you need hello following items:</span></span>

- <span data-ttu-id="4b4d9-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b4d9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4b4d9-113">Abonnement Showpad pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="4b4d9-113">A Showpad single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4b4d9-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4b4d9-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="4b4d9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4b4d9-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4b4d9-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4b4d9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4b4d9-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="4b4d9-118">Scenario description</span></span>
<span data-ttu-id="4b4d9-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4b4d9-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="4b4d9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4b4d9-121">Ajout de Showpad à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="4b4d9-121">Adding Showpad from hello gallery</span></span>
2. <span data-ttu-id="4b4d9-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b4d9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-showpad-from-hello-gallery"></a><span data-ttu-id="4b4d9-123">Ajout de Showpad à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="4b4d9-123">Adding Showpad from hello gallery</span></span>

<span data-ttu-id="4b4d9-124">intégration de hello tooconfigure de Showpad dans Azure AD, vous devez tooadd Showpad à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-124">tooconfigure hello integration of Showpad into Azure AD, you need tooadd Showpad from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4b4d9-125">**tooadd Showpad à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4b4d9-125">**tooadd Showpad from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4b4d9-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4b4d9-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4b4d9-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="4b4d9-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="4b4d9-133">Dans la zone de recherche de hello, tapez **Showpad**.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-133">In hello search box, type **Showpad**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_search.png)

5. <span data-ttu-id="4b4d9-135">Dans le volet de résultats hello, sélectionnez **Showpad**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-135">In hello results panel, select **Showpad**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4b4d9-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b4d9-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="4b4d9-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Showpad sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="4b4d9-138">In this section, you configure and test Azure AD single sign-on with Showpad based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4b4d9-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Showpad est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Showpad is tooa user in Azure AD.</span></span> <span data-ttu-id="4b4d9-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Showpad doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-140">In other words, a link relationship between an Azure AD user and hello related user in Showpad needs toobe established.</span></span>

<span data-ttu-id="4b4d9-141">Dans Showpad, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-141">In Showpad, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4b4d9-142">tooconfigure et test Azure AD l’authentification unique avec Showpad, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="4b4d9-142">tooconfigure and test Azure AD single sign-on with Showpad, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4b4d9-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4b4d9-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4b4d9-145">**[Création d’un utilisateur de test Showpad](#creating-a-showpad-test-user)**  -toohave un équivalent de Britta Simon dans Showpad est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-145">**[Creating a Showpad test user](#creating-a-showpad-test-user)** - toohave a counterpart of Britta Simon in Showpad that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4b4d9-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4b4d9-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4b4d9-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b4d9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4b4d9-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Showpad.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Showpad application.</span></span>

<span data-ttu-id="4b4d9-150">**tooconfigure Azure AD single sign-on avec Showpad, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4b4d9-150">**tooconfigure Azure AD single sign-on with Showpad, perform hello following steps:**</span></span>

1. <span data-ttu-id="4b4d9-151">Bonjour portail Azure, sur hello **Showpad** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-151">In hello Azure portal, on hello **Showpad** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="4b4d9-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_samlbase.png)

3. <span data-ttu-id="4b4d9-155">Sur hello **Showpad domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="4b4d9-155">On hello **Showpad Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_url.png)

    <span data-ttu-id="4b4d9-157">a.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-157">a.</span></span> <span data-ttu-id="4b4d9-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<comapany-name>.showpad.biz/login`</span><span class="sxs-lookup"><span data-stu-id="4b4d9-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<comapany-name>.showpad.biz/login`</span></span>

    <span data-ttu-id="4b4d9-159">b.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-159">b.</span></span> <span data-ttu-id="4b4d9-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company-name>.showpad.biz`</span><span class="sxs-lookup"><span data-stu-id="4b4d9-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company-name>.showpad.biz`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4b4d9-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-161">These values are not real.</span></span> <span data-ttu-id="4b4d9-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4b4d9-163">Contact [équipe de support Showpad](https://help.showpad.com) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-163">Contact [Showpad support team](https://help.showpad.com) tooget these values.</span></span> 
 


4. <span data-ttu-id="4b4d9-164">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_certificate.png) 

5. <span data-ttu-id="4b4d9-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="4b4d9-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-showpad-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4b4d9-168">Client de Showpad tooyour ouverture de session en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-168">Sign-on tooyour Showpad tenant as an administrator.</span></span>

7. <span data-ttu-id="4b4d9-169">Dans le menu hello haut de hello, cliquez sur hello **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-169">In hello menu on hello top, click hello **Settings**.</span></span>
   
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_001.png) 

8. <span data-ttu-id="4b4d9-171">Accédez trop »**Single Sign-On**« et cliquez sur »**activer**. »</span><span class="sxs-lookup"><span data-stu-id="4b4d9-171">Navigate too"**Single Sign-On**" and click "**Enable**."</span></span>
   
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_002.png)

9. <span data-ttu-id="4b4d9-173">Sur hello **ajouter un Service de SAML 2.0** boîte de dialogue, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="4b4d9-173">On hello **Add a SAML 2.0 Service** dialog, perform hello following steps:</span></span>
   
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_003.png) 
   
    <span data-ttu-id="4b4d9-175">a.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-175">a.</span></span> <span data-ttu-id="4b4d9-176">Bonjour **nom** zone de texte, nom de fournisseur de l’identificateur hello de type (par exemple : nom de votre société).</span><span class="sxs-lookup"><span data-stu-id="4b4d9-176">In hello **Name** textbox, type hello name of Identifier Provider (for example: your company name).</span></span>
   
    <span data-ttu-id="4b4d9-177">b.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-177">b.</span></span> <span data-ttu-id="4b4d9-178">Dans **Source des métadonnées**, sélectionnez **XML**.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-178">As **Metadata Source**, select **XML**.</span></span>
   
    <span data-ttu-id="4b4d9-179">c.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-179">c.</span></span> <span data-ttu-id="4b4d9-180">Copier le contenu du fichier XML de métadonnées, ce qui vous avez téléchargé à partir de hello portail Azure, hello et collez-le à hello **Metadata XML** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-180">Copy hello content of metadata XML file, which you have downloaded from hello Azure portal, and then paste it into hello **Metadata XML** textbox.</span></span>
   
    <span data-ttu-id="4b4d9-181">d.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-181">d.</span></span> <span data-ttu-id="4b4d9-182">Sélectionnez **Auto-provision accounts for new users when they log in**(Configurer automatiquement les comptes des nouveaux utilisateurs au moment de la connexion).</span><span class="sxs-lookup"><span data-stu-id="4b4d9-182">Select **Auto-provision accounts for new users when they log in**.</span></span>
   
    <span data-ttu-id="4b4d9-183">e.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-183">e.</span></span> <span data-ttu-id="4b4d9-184">Cliquez sur **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-184">Click **Submit**.</span></span>

> [!TIP]
> <span data-ttu-id="4b4d9-185">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="4b4d9-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4b4d9-186">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4b4d9-187">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4b4d9-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4b4d9-188">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b4d9-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="4b4d9-189">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="4b4d9-191">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4b4d9-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4b4d9-192">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-showpad-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4b4d9-194">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-showpad-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4b4d9-196">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-showpad-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4b4d9-198">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="4b4d9-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-showpad-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4b4d9-200">a.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-200">a.</span></span> <span data-ttu-id="4b4d9-201">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4b4d9-202">b.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-202">b.</span></span> <span data-ttu-id="4b4d9-203">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4b4d9-204">c.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-204">c.</span></span> <span data-ttu-id="4b4d9-205">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4b4d9-206">d.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-206">d.</span></span> <span data-ttu-id="4b4d9-207">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-207">Click **Create**.</span></span>
 
### <a name="creating-a-showpad-test-user"></a><span data-ttu-id="4b4d9-208">Création d’un utilisateur de test Showpad</span><span class="sxs-lookup"><span data-stu-id="4b4d9-208">Creating a Showpad test user</span></span>

<span data-ttu-id="4b4d9-209">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans Showpad.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-209">hello objective of this section is toocreate a user called Britta Simon in Showpad.</span></span> 

<span data-ttu-id="4b4d9-210">Showpad prend en charge l’approvisionnement juste-à-temps.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-210">Showpad supports just-in-time provisioning.</span></span> <span data-ttu-id="4b4d9-211">Vous l’avez déjà activé dans **[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)**.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-211">You have enabled provisioning in **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**.</span></span> 

<span data-ttu-id="4b4d9-212">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-212">There is no action item for you in this section.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4b4d9-213">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b4d9-213">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4b4d9-214">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooShowpad.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooShowpad.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="4b4d9-216">**tooassign Britta Simon tooShowpad, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4b4d9-216">**tooassign Britta Simon tooShowpad, perform hello following steps:**</span></span>

1. <span data-ttu-id="4b4d9-217">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="4b4d9-219">Dans la liste des applications hello, sélectionnez **Showpad**.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-219">In hello applications list, select **Showpad**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_app.png) 

3. <span data-ttu-id="4b4d9-221">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="4b4d9-223">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-223">Click **Add** button.</span></span> <span data-ttu-id="4b4d9-224">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="4b4d9-226">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4b4d9-227">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4b4d9-228">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4b4d9-229">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="4b4d9-229">Testing single sign-on</span></span>

<span data-ttu-id="4b4d9-230">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-230">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4b4d9-231">Lorsque vous cliquez sur mosaïque Showpad hello hello volet d’accès, vous devez obtenir tooShowpad automatiquement signé sur application.</span><span class="sxs-lookup"><span data-stu-id="4b4d9-231">When you click hello Showpad tile in hello Access Panel, you should get automatically signed-on tooShowpad application.</span></span>
<span data-ttu-id="4b4d9-232">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4b4d9-232">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4b4d9-233">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="4b4d9-233">Additional resources</span></span>

* [<span data-ttu-id="4b4d9-234">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4b4d9-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4b4d9-235">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="4b4d9-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_203.png

