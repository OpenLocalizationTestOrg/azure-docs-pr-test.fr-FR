---
title: "Didacticiel : Intégration d’Azure Active Directory à Bime | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Bime."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bdcf0729-c880-4c95-b739-0f6345b17dd8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 1213725028dd8ce90f22fa6e9c50ffabebc8f3fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bime"></a><span data-ttu-id="de7fe-103">Didacticiel : Intégration d’Azure Active Directory à Bime</span><span class="sxs-lookup"><span data-stu-id="de7fe-103">Tutorial: Azure Active Directory integration with Bime</span></span>

<span data-ttu-id="de7fe-104">Dans ce didacticiel, vous apprendrez comment toointegrate Bime avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="de7fe-104">In this tutorial, you learn how toointegrate Bime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="de7fe-105">Intégration de Bime à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="de7fe-105">Integrating Bime with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="de7fe-106">Vous pouvez contrôler dans Azure AD qui a accès tooBime</span><span class="sxs-lookup"><span data-stu-id="de7fe-106">You can control in Azure AD who has access tooBime</span></span>
- <span data-ttu-id="de7fe-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooBime (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="de7fe-107">You can enable your users tooautomatically get signed-on tooBime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="de7fe-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="de7fe-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="de7fe-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="de7fe-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="de7fe-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="de7fe-110">Prerequisites</span></span>

<span data-ttu-id="de7fe-111">tooconfigure intégration d’Azure AD à Bime, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="de7fe-111">tooconfigure Azure AD integration with Bime, you need hello following items:</span></span>

- <span data-ttu-id="de7fe-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="de7fe-112">An Azure AD subscription</span></span>
- <span data-ttu-id="de7fe-113">Un abonnement Bime pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="de7fe-113">A Bime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="de7fe-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="de7fe-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="de7fe-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="de7fe-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="de7fe-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="de7fe-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="de7fe-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois ici : [offre d’essai](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="de7fe-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="de7fe-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="de7fe-118">Scenario description</span></span>
<span data-ttu-id="de7fe-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="de7fe-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="de7fe-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="de7fe-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="de7fe-121">Ajout de Bime à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="de7fe-121">Adding Bime from hello gallery</span></span>
2. <span data-ttu-id="de7fe-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="de7fe-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bime-from-hello-gallery"></a><span data-ttu-id="de7fe-123">Ajout de Bime à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="de7fe-123">Adding Bime from hello gallery</span></span>
<span data-ttu-id="de7fe-124">intégration de hello tooconfigure de Bime dans Azure AD, vous devez tooadd Bime à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="de7fe-124">tooconfigure hello integration of Bime into Azure AD, you need tooadd Bime from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="de7fe-125">**tooadd Bime à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="de7fe-125">**tooadd Bime from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="de7fe-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="de7fe-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="de7fe-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="de7fe-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="de7fe-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="de7fe-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="de7fe-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="de7fe-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="de7fe-133">Dans la zone de recherche de hello, tapez **Bime**.</span><span class="sxs-lookup"><span data-stu-id="de7fe-133">In hello search box, type **Bime**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bime-tutorial/tutorial_bime_search.png)

5. <span data-ttu-id="de7fe-135">Dans le volet de résultats hello, sélectionnez **Bime**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="de7fe-135">In hello results panel, select **Bime**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bime-tutorial/tutorial_bime_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="de7fe-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="de7fe-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="de7fe-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Bime, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="de7fe-138">In this section, you configure and test Azure AD single sign-on with Bime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="de7fe-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Bime est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="de7fe-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Bime is tooa user in Azure AD.</span></span> <span data-ttu-id="de7fe-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Bime doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="de7fe-140">In other words, a link relationship between an Azure AD user and hello related user in Bime needs toobe established.</span></span>

<span data-ttu-id="de7fe-141">Dans Bime, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="de7fe-141">In Bime, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="de7fe-142">tooconfigure et test Azure AD l’authentification unique à Bime, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="de7fe-142">tooconfigure and test Azure AD single sign-on with Bime, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="de7fe-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="de7fe-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="de7fe-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="de7fe-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="de7fe-145">**[Création d’un utilisateur de test de Bime](#creating-a-bime-test-user)**  -toohave un équivalent de Britta Simon dans Bime est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="de7fe-145">**[Creating a Bime test user](#creating-a-bime-test-user)** - toohave a counterpart of Britta Simon in Bime that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="de7fe-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="de7fe-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="de7fe-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="de7fe-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="de7fe-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="de7fe-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="de7fe-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de Bime.</span><span class="sxs-lookup"><span data-stu-id="de7fe-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Bime application.</span></span>

<span data-ttu-id="de7fe-150">**tooconfigure Azure AD single sign-on avec Bime, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="de7fe-150">**tooconfigure Azure AD single sign-on with Bime, perform hello following steps:**</span></span>

1. <span data-ttu-id="de7fe-151">Bonjour portail Azure, sur hello **Bime** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="de7fe-151">In hello Azure portal, on hello **Bime** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="de7fe-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="de7fe-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-bime-tutorial/tutorial_bime_samlbase.png)

3. <span data-ttu-id="de7fe-155">Sur hello **Bime domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="de7fe-155">On hello **Bime Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bime-tutorial/tutorial_bime_url.png)

    <span data-ttu-id="de7fe-157">a.</span><span class="sxs-lookup"><span data-stu-id="de7fe-157">a.</span></span> <span data-ttu-id="de7fe-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<tenant-name>.Bimeapp.com`</span><span class="sxs-lookup"><span data-stu-id="de7fe-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.Bimeapp.com`</span></span>

    <span data-ttu-id="de7fe-159">b.</span><span class="sxs-lookup"><span data-stu-id="de7fe-159">b.</span></span> <span data-ttu-id="de7fe-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<tenant-name>.Bimeapp.com`</span><span class="sxs-lookup"><span data-stu-id="de7fe-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenant-name>.Bimeapp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="de7fe-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="de7fe-161">These values are not real.</span></span> <span data-ttu-id="de7fe-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="de7fe-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="de7fe-163">Contact [équipe de support Client de Bime](https://bime.zendesk.com/hc/categories/202604307-Support-tech-notes-and-tips-) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="de7fe-163">Contact [Bime Client support team](https://bime.zendesk.com/hc/categories/202604307-Support-tech-notes-and-tips-) tooget these values.</span></span> 
 
4. <span data-ttu-id="de7fe-164">Sur hello **le certificat de signature SAML** section, hello de copie **l’empreinte numérique** valeur à partir du certificat de hello.</span><span class="sxs-lookup"><span data-stu-id="de7fe-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value from hello certificate.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bime-tutorial/tutorial_bime_certificate.png) 

5. <span data-ttu-id="de7fe-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="de7fe-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bime-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="de7fe-168">Sur hello **Bime Configuration** , cliquez sur **configurer de Bime** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="de7fe-168">On hello **Bime Configuration** section, click **Configure Bime** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="de7fe-169">Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="de7fe-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bime-tutorial/tutorial_bime_configure.png) 

7. <span data-ttu-id="de7fe-171">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Bime en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="de7fe-171">In a different web browser window, log into your Bime company site as an administrator.</span></span>

8. <span data-ttu-id="de7fe-172">Dans la barre d’outils de hello, cliquez sur **Admin**, puis **compte**.</span><span class="sxs-lookup"><span data-stu-id="de7fe-172">In hello toolbar, click **Admin**, and then **Account**.</span></span>
   
    <span data-ttu-id="de7fe-173">![Administrateur](./media/active-directory-saas-bime-tutorial/ic775558.png "Administrateur")</span><span class="sxs-lookup"><span data-stu-id="de7fe-173">![Admin](./media/active-directory-saas-bime-tutorial/ic775558.png "Admin")</span></span>

9. <span data-ttu-id="de7fe-174">Sur la page de configuration de compte hello, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="de7fe-174">On hello account configuration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="de7fe-175">![Configurer l’authentification unique](./media/active-directory-saas-bime-tutorial/ic775559.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="de7fe-175">![Configure Single Sign-On](./media/active-directory-saas-bime-tutorial/ic775559.png "Configure Single Sign-On")</span></span>
   
    <span data-ttu-id="de7fe-176">a.</span><span class="sxs-lookup"><span data-stu-id="de7fe-176">a.</span></span> <span data-ttu-id="de7fe-177">Sélectionnez **Activer l’authentification SAML**.</span><span class="sxs-lookup"><span data-stu-id="de7fe-177">Select **Enable SAML authentication**.</span></span>

    <span data-ttu-id="de7fe-178">b.</span><span class="sxs-lookup"><span data-stu-id="de7fe-178">b.</span></span> <span data-ttu-id="de7fe-179">Bonjour **URL de connexion distante** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="de7fe-179">In hello **Remote Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="de7fe-180">c.</span><span class="sxs-lookup"><span data-stu-id="de7fe-180">c.</span></span>  <span data-ttu-id="de7fe-181">Hello de coller **l’empreinte numérique** valeur à partir du portail Azure en hello **empreinte numérique du certificat** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="de7fe-181">Paste hello **Thumbprint** value from Azure portal into hello **Certificate Fingerprint** textbox.</span></span>       
   
    <span data-ttu-id="de7fe-182">d.</span><span class="sxs-lookup"><span data-stu-id="de7fe-182">d.</span></span> <span data-ttu-id="de7fe-183">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="de7fe-183">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="de7fe-184">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="de7fe-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="de7fe-185">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="de7fe-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="de7fe-186">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="de7fe-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="de7fe-187">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="de7fe-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="de7fe-188">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="de7fe-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="de7fe-190">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="de7fe-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="de7fe-191">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="de7fe-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="de7fe-193">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="de7fe-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="de7fe-195">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="de7fe-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="de7fe-197">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="de7fe-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="de7fe-199">a.</span><span class="sxs-lookup"><span data-stu-id="de7fe-199">a.</span></span> <span data-ttu-id="de7fe-200">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="de7fe-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="de7fe-201">b.</span><span class="sxs-lookup"><span data-stu-id="de7fe-201">b.</span></span> <span data-ttu-id="de7fe-202">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="de7fe-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="de7fe-203">c.</span><span class="sxs-lookup"><span data-stu-id="de7fe-203">c.</span></span> <span data-ttu-id="de7fe-204">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="de7fe-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="de7fe-205">d.</span><span class="sxs-lookup"><span data-stu-id="de7fe-205">d.</span></span> <span data-ttu-id="de7fe-206">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="de7fe-206">Click **Create**.</span></span>
 
### <a name="creating-a-bime-test-user"></a><span data-ttu-id="de7fe-207">Création d’un utilisateur de test Bime</span><span class="sxs-lookup"><span data-stu-id="de7fe-207">Creating a Bime test user</span></span>

<span data-ttu-id="de7fe-208">Dans l’ordre tooenable Azure AD les utilisateurs toolog dans tooBime, ils doivent être configurés dans Bime.</span><span class="sxs-lookup"><span data-stu-id="de7fe-208">In order tooenable Azure AD users toolog in tooBime, they must be provisioned into Bime.</span></span> <span data-ttu-id="de7fe-209">Dans les cas de hello de Bime, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="de7fe-209">In hello case of Bime, provisioning is a manual task.</span></span>

<span data-ttu-id="de7fe-210">**configuration, de l’utilisateur tooconfigure effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="de7fe-210">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="de7fe-211">Connectez-vous à tooyour **Bime** client.</span><span class="sxs-lookup"><span data-stu-id="de7fe-211">Log in tooyour **Bime** tenant.</span></span>

2. <span data-ttu-id="de7fe-212">Dans la barre d’outils de hello, cliquez sur **Admin**, puis **utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="de7fe-212">In hello toolbar, click **Admin**, and then **Users**.</span></span>
   
    <span data-ttu-id="de7fe-213">![Administrateur](./media/active-directory-saas-bime-tutorial/ic775561.png "Administrateur")</span><span class="sxs-lookup"><span data-stu-id="de7fe-213">![Admin](./media/active-directory-saas-bime-tutorial/ic775561.png "Admin")</span></span>

3. <span data-ttu-id="de7fe-214">Bonjour **liste des utilisateurs**, cliquez sur **ajouter un nouvel utilisateur** (« + »).</span><span class="sxs-lookup"><span data-stu-id="de7fe-214">In hello **Users List**, click **Add New User** (“+”).</span></span>
   
    <span data-ttu-id="de7fe-215">![Utilisateurs](./media/active-directory-saas-bime-tutorial/ic775562.png "Utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="de7fe-215">![Users](./media/active-directory-saas-bime-tutorial/ic775562.png "Users")</span></span>

4. <span data-ttu-id="de7fe-216">Sur hello **détails de l’utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="de7fe-216">On hello **User Details** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="de7fe-217">![Détails de l’utilisateur](./media/active-directory-saas-bime-tutorial/ic775563.png "Détails de l’utilisateur")</span><span class="sxs-lookup"><span data-stu-id="de7fe-217">![User Details](./media/active-directory-saas-bime-tutorial/ic775563.png "User Details")</span></span>
   
    <span data-ttu-id="de7fe-218">a.</span><span class="sxs-lookup"><span data-stu-id="de7fe-218">a.</span></span> <span data-ttu-id="de7fe-219">Bonjour **prénom** zone de texte, entrez hello premier nom d’utilisateur comme **Brian**.</span><span class="sxs-lookup"><span data-stu-id="de7fe-219">In hello **First name** textbox, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="de7fe-220">b.</span><span class="sxs-lookup"><span data-stu-id="de7fe-220">b.</span></span> <span data-ttu-id="de7fe-221">Bonjour **nom** zone de texte, entrez le nom d’utilisateur comme hello **Simon**.</span><span class="sxs-lookup"><span data-stu-id="de7fe-221">In hello **Last name** textbox, enter hello last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="de7fe-222">c.</span><span class="sxs-lookup"><span data-stu-id="de7fe-222">c.</span></span> <span data-ttu-id="de7fe-223">Bonjour **messagerie** zone de texte, entrez hello adresse de messagerie de l’utilisateur comme  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="de7fe-223">In hello **Email** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="de7fe-224">d.</span><span class="sxs-lookup"><span data-stu-id="de7fe-224">d.</span></span> <span data-ttu-id="de7fe-225">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="de7fe-225">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="de7fe-226">Vous pouvez utiliser n’importe quel autre Bime utilisateur compte outil de création ou API fournie par Bime tooprovision des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="de7fe-226">You can use any other Bime user account creation tools or APIs provided by Bime tooprovision AAD user accounts.</span></span>
>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="de7fe-227">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="de7fe-227">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="de7fe-228">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooBime.</span><span class="sxs-lookup"><span data-stu-id="de7fe-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBime.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="de7fe-230">**tooassign Britta Simon tooBime, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="de7fe-230">**tooassign Britta Simon tooBime, perform hello following steps:**</span></span>

1. <span data-ttu-id="de7fe-231">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="de7fe-231">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="de7fe-233">Dans la liste des applications hello, sélectionnez **Bime**.</span><span class="sxs-lookup"><span data-stu-id="de7fe-233">In hello applications list, select **Bime**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bime-tutorial/tutorial_bime_app.png) 

3. <span data-ttu-id="de7fe-235">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="de7fe-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="de7fe-237">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="de7fe-237">Click **Add** button.</span></span> <span data-ttu-id="de7fe-238">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="de7fe-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="de7fe-240">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="de7fe-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="de7fe-241">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="de7fe-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="de7fe-242">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="de7fe-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="de7fe-243">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="de7fe-243">Testing single sign-on</span></span>

<span data-ttu-id="de7fe-244">objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="de7fe-244">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="de7fe-245">Lorsque vous cliquez sur mosaïque Bime hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Bime application.</span><span class="sxs-lookup"><span data-stu-id="de7fe-245">When you click hello Bime tile in hello Access Panel, you should get automatically signed-on tooyour Bime application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="de7fe-246">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="de7fe-246">Additional resources</span></span>

* [<span data-ttu-id="de7fe-247">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="de7fe-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="de7fe-248">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="de7fe-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bime-tutorial/tutorial_general_203.png

