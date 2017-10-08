---
title: "Didacticiel : Intégration d’Azure Active Directory à Clarizen | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Clarizen."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: f24ccda3b90e5df9a203a444dfda905043b30276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clarizen"></a><span data-ttu-id="89ab4-103">Didacticiel : Intégration d’Azure Active Directory à Clarizen</span><span class="sxs-lookup"><span data-stu-id="89ab4-103">Tutorial: Azure Active Directory integration with Clarizen</span></span>

<span data-ttu-id="89ab4-104">Dans ce didacticiel, vous apprendrez comment toointegrate Azure Active Directory (Azure AD) à Clarizen.</span><span class="sxs-lookup"><span data-stu-id="89ab4-104">In this tutorial, you learn how toointegrate Azure Active Directory (Azure AD) with Clarizen.</span></span> <span data-ttu-id="89ab4-105">Ceci permet d’intégration vous hello suivants avantages :</span><span class="sxs-lookup"><span data-stu-id="89ab4-105">This integration gives you hello following benefits:</span></span>

- <span data-ttu-id="89ab4-106">Vous pouvez contrôler, dans Azure AD, qui a accès tooClarizen.</span><span class="sxs-lookup"><span data-stu-id="89ab4-106">You can control, in Azure AD, who has access tooClarizen.</span></span>
- <span data-ttu-id="89ab4-107">Vous pouvez activer votre toobe utilisateurs automatiquement connecté tooClarizen (SSO) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89ab4-107">You can enable your users toobe automatically signed in tooClarizen (single sign-on) with their Azure AD accounts.</span></span>
- <span data-ttu-id="89ab4-108">Vous pouvez gérer vos comptes dans un emplacement central, hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="89ab4-108">You can manage your accounts in one central location, hello Azure portal.</span></span>

<span data-ttu-id="89ab4-109">scénario Hello dans ce didacticiel se compose de deux tâches principales :</span><span class="sxs-lookup"><span data-stu-id="89ab4-109">hello scenario in this tutorial consists of two main tasks:</span></span>

1. <span data-ttu-id="89ab4-110">Ajouter Clarizen à partir de la galerie de hello.</span><span class="sxs-lookup"><span data-stu-id="89ab4-110">Add Clarizen from hello gallery.</span></span>
2. <span data-ttu-id="89ab4-111">Configurez et testez l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89ab4-111">Configure and test Azure AD single sign-on.</span></span>

<span data-ttu-id="89ab4-112">Pour plus d’informations sur l’intégration d’applications SaaS (software as a service) à Azure AD, consultez l’article [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="89ab4-112">If you want more details about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89ab4-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="89ab4-113">Prerequisites</span></span>
<span data-ttu-id="89ab4-114">tooconfigure intégration d’Azure AD à Clarizen, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="89ab4-114">tooconfigure Azure AD integration with Clarizen, you need hello following items:</span></span>

- <span data-ttu-id="89ab4-115">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="89ab4-115">An Azure AD subscription</span></span>
- <span data-ttu-id="89ab4-116">Un abonnement Clarizen activé pour l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="89ab4-116">A Clarizen subscription that's enabled for single sign-on</span></span>

<span data-ttu-id="89ab4-117">étapes de hello tootest dans ce didacticiel, suivez ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="89ab4-117">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="89ab4-118">Testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="89ab4-118">Test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="89ab4-119">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="89ab4-119">Don't use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="89ab4-120">Si vous ne disposez pas d’un environnement de test Azure AD, vous pouvez [vous inscrire pour un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="89ab4-120">If you don't have an Azure AD test environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="add-clarizen-from-hello-gallery"></a><span data-ttu-id="89ab4-121">Ajouter des Clarizen à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="89ab4-121">Add Clarizen from hello gallery</span></span>
<span data-ttu-id="89ab4-122">intégration de hello tooconfigure de Clarizen dans Azure AD, ajoutez Clarizen à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="89ab4-122">tooconfigure hello integration of Clarizen into Azure AD, add Clarizen from hello gallery tooyour list of managed SaaS apps.</span></span>

1. <span data-ttu-id="89ab4-123">Bonjour [portail Azure](https://portal.azure.com)hello du volet gauche, cliquez sur dans hello **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="89ab4-123">In hello [Azure portal](https://portal.azure.com), in hello left pane, click hello **Azure Active Directory** icon.</span></span>

    ![Icône Azure Active Directory][1]

2. <span data-ttu-id="89ab4-125">Cliquez sur **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="89ab4-125">Click **Enterprise applications**.</span></span> <span data-ttu-id="89ab4-126">Puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="89ab4-126">Then click **All applications**.</span></span>

    ![Sélection des options « Applications d’entreprise » et « Toutes les applications »][2]

3. <span data-ttu-id="89ab4-128">Cliquez sur hello **ajouter** bouton en haut de hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="89ab4-128">Click hello **Add** button at hello top of hello dialog box.</span></span>

    ![bouton « Ajouter » de Hello][3]

4. <span data-ttu-id="89ab4-130">Dans la zone de recherche de hello, tapez **Clarizen**.</span><span class="sxs-lookup"><span data-stu-id="89ab4-130">In hello search box, type **Clarizen**.</span></span>

    ![Taper « Clarizen » dans la zone de recherche hello](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_000.png)

5. <span data-ttu-id="89ab4-132">Dans le volet de résultats hello, sélectionnez **Clarizen**, puis cliquez sur **ajouter** application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="89ab4-132">In hello results pane, select **Clarizen**, and then click **Add** tooadd hello application.</span></span>

    ![Sélection de Clarizen dans le volet de résultats hello](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_0001.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="89ab4-134">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="89ab4-134">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="89ab4-135">Bonjour les sections suivantes, vous configurez et testez Azure AD l’authentification unique sur Clarizen en fonction de l’utilisateur de test hello Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="89ab4-135">In hello following sections, you configure and test Azure AD single sign-on with Clarizen based on hello test user Britta Simon.</span></span>

<span data-ttu-id="89ab4-136">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Clarizen est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89ab4-136">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Clarizen is tooa user in Azure AD.</span></span> <span data-ttu-id="89ab4-137">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Clarizen doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="89ab4-137">In other words, a link relationship between an Azure AD user and hello related user in Clarizen needs toobe established.</span></span> <span data-ttu-id="89ab4-138">Vous établissez cette relation de lien en assignant la valeur hello **nom d’utilisateur** dans Azure AD en tant que valeur hello **nom d’utilisateur** dans Clarizen.</span><span class="sxs-lookup"><span data-stu-id="89ab4-138">You establish this link relationship by assigning hello value of **user name** in Azure AD as hello value of **Username** in Clarizen.</span></span>

<span data-ttu-id="89ab4-139">tooconfigure et test Azure AD l’authentification unique avec l’occurrence, hello terminée après les blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="89ab4-139">tooconfigure and test Azure AD single sign-on with Clarizen, complete hello following building blocks:</span></span>

1. <span data-ttu-id="89ab4-140">**[Configurer Azure AD l’authentification unique sur](#configure-azure-ad-single-sign-on)**  tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="89ab4-140">**[Configure Azure AD single sign-on](#configure-azure-ad-single-sign-on)** tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="89ab4-141">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  tootest AD Azure l’authentification unique avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="89ab4-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="89ab4-142">**[Créer un utilisateur de test de Clarizen](#create-a-clarizen-test-user)**  toohave de Britta Simon dans Clarizen qui est la représentation sous forme de toohello lié Azure AD de sa contrepartie.</span><span class="sxs-lookup"><span data-stu-id="89ab4-142">**[Create a Clarizen test user](#create-a-clarizen-test-user)** toohave a counterpart of Britta Simon in Clarizen that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="89ab4-143">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="89ab4-143">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="89ab4-144">**[Tester l’authentification unique sur](#test-single-sign-on)**  tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="89ab4-144">**[Test single sign-on](#test-single-sign-on)** tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="89ab4-145">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="89ab4-145">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="89ab4-146">Activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de Clarizen.</span><span class="sxs-lookup"><span data-stu-id="89ab4-146">Enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Clarizen application.</span></span>

1. <span data-ttu-id="89ab4-147">Bonjour portail Azure, sur hello **Clarizen** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="89ab4-147">In hello Azure portal, on hello **Clarizen** application integration page, click **Single sign-on**.</span></span>

    ![Sélection de l’option « Authentification unique »][4]

2. <span data-ttu-id="89ab4-149">Bonjour **l’authentification unique** boîte de dialogue, pour **Mode**, sélectionnez **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="89ab4-149">In hello **Single sign-on** dialog box, for **Mode**, select **SAML-based Sign-on** tooenable single sign-on.</span></span>

    ![Sélection de l’option « Authentification basée sur SAML »](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_01.png)

3. <span data-ttu-id="89ab4-151">Bonjour **Clarizen domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="89ab4-151">In hello **Clarizen Domain and URLs** section, perform hello following steps:</span></span>

    ![Zones d’identificateur et d’URL de réponse](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_02.png)

    <span data-ttu-id="89ab4-153">a.</span><span class="sxs-lookup"><span data-stu-id="89ab4-153">a.</span></span> <span data-ttu-id="89ab4-154">Bonjour **identificateur** zone, type valeur hello : **Clarizen**</span><span class="sxs-lookup"><span data-stu-id="89ab4-154">In hello **Identifier** box, type hello value as: **Clarizen**</span></span>

    <span data-ttu-id="89ab4-155">b.</span><span class="sxs-lookup"><span data-stu-id="89ab4-155">b.</span></span> <span data-ttu-id="89ab4-156">Bonjour **URL de réponse** , tapez une URL à l’aide de hello modèle : **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**</span><span class="sxs-lookup"><span data-stu-id="89ab4-156">In hello **Reply URL** box, type a URL by using hello following pattern: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**</span></span>

    > [!NOTE]
    > <span data-ttu-id="89ab4-157">Ils ne sont pas des valeurs réelles hello.</span><span class="sxs-lookup"><span data-stu-id="89ab4-157">These are not hello real values.</span></span> <span data-ttu-id="89ab4-158">Avoir identificateur réel de toouse hello et URL de réponse.</span><span class="sxs-lookup"><span data-stu-id="89ab4-158">You have toouse hello actual identifier and reply URL.</span></span> <span data-ttu-id="89ab4-159">Ici, nous vous suggérons d’utiliser hello de valeur unique d’une chaîne comme identificateur de hello.</span><span class="sxs-lookup"><span data-stu-id="89ab4-159">Here we suggest that you use hello unique value of a string as hello identifier.</span></span> <span data-ttu-id="89ab4-160">tooget hello valeurs réelles, contact hello [équipe de support technique de Clarizen](https://success.clarizen.com/hc/en-us/requests/new).</span><span class="sxs-lookup"><span data-stu-id="89ab4-160">tooget hello actual values, contact hello [Clarizen support team](https://success.clarizen.com/hc/en-us/requests/new).</span></span>

4. <span data-ttu-id="89ab4-161">Sur hello **le certificat de signature SAML** , cliquez sur **créer un nouveau certificat**.</span><span class="sxs-lookup"><span data-stu-id="89ab4-161">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Sélection de l’option « Créer un certificat »](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_03.png)  

5. <span data-ttu-id="89ab4-163">Bonjour **créer un nouveau certificat** boîte de dialogue zone, cliquez sur icône du calendrier hello et sélectionnez une date d’expiration.</span><span class="sxs-lookup"><span data-stu-id="89ab4-163">In hello **Create New Certificate** dialog box, click hello calendar icon and select an expiry date.</span></span> <span data-ttu-id="89ab4-164">Cliquez ensuite sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="89ab4-164">Then click **Save**.</span></span>

    ![Sélection et enregistrement d’une date d’expiration](./media/active-directory-saas-clarizen-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="89ab4-166">Bonjour **le certificat de signature SAML** section, sélectionnez **activer le nouveau certificat**, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="89ab4-166">In hello **SAML Signing Certificate** section, select **Make new certificate active**, and then click **Save**.</span></span>

    ![En sélectionnant la case à cocher pour l’activation d’un nouveau certificat hello hello](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_04.png)

7. <span data-ttu-id="89ab4-168">Bonjour **le certificat de substitution** boîte de dialogue, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="89ab4-168">In hello **Rollover certificate** dialog box, click **OK**.</span></span>

    ![En cliquant sur « OK » les tooconfirm que vous souhaitez toomake hello certificat active](./media/active-directory-saas-clarizen-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="89ab4-170">Bonjour **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="89ab4-170">In hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![En cliquant sur le téléchargement de hello toostart « Certificat (Base64) »](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_05.png)

9. <span data-ttu-id="89ab4-172">Bonjour **Clarizen Configuration** , cliquez sur **configurer de Clarizen** tooopen hello **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="89ab4-172">In hello **Clarizen Configuration** section, click **Configure Clarizen** tooopen hello **Configure sign-on** window.</span></span>

    ![Sélection de l’option « Configurer Clarizen »](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_06.png)

    ![Fenêtre « Configurer l’authentification », incluant les URL et les fichiers](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_07.png)

10. <span data-ttu-id="89ab4-175">Dans une fenêtre de navigateur web, connectez-vous dans un site d’entreprise Clarizen tooyour en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="89ab4-175">In a different web browser window, sign in tooyour Clarizen company site as an administrator.</span></span>

11. <span data-ttu-id="89ab4-176">Cliquez sur votre nom d’utilisateur, puis sur **Settings** (Paramètres).</span><span class="sxs-lookup"><span data-stu-id="89ab4-176">Click your username, and then click **Settings**.</span></span>

    <span data-ttu-id="89ab4-177">![Sélection de l’option « Settings » (Paramètres) sous votre nom d’utilisateur](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "Settings") (Paramètres)</span><span class="sxs-lookup"><span data-stu-id="89ab4-177">![Clicking "Settings" under your username](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "Settings")</span></span>

12. <span data-ttu-id="89ab4-178">Cliquez sur hello **paramètres globaux** onglet. Ensuite, suivant trop**authentification fédérée**, cliquez sur **modifier**.</span><span class="sxs-lookup"><span data-stu-id="89ab4-178">Click hello **Global Settings** tab. Then, next too**Federated Authentication**, click **edit**.</span></span>

    <span data-ttu-id="89ab4-179">![Onglet « Global Settings » (Paramètres globaux)](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "Global Settings") (Paramètres globaux)</span><span class="sxs-lookup"><span data-stu-id="89ab4-179">!["Global Settings" tab](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "Global Settings")</span></span>

13. <span data-ttu-id="89ab4-180">Bonjour **authentification fédérée** boîte de dialogue, exécutez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="89ab4-180">In hello **Federated Authentication** dialog box, perform hello following steps:</span></span>

    <span data-ttu-id="89ab4-181">![Boîte de dialogue « Federated Authentication » (Authentification fédérée)](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "Federated Authentication") (Authentification fédérée)</span><span class="sxs-lookup"><span data-stu-id="89ab4-181">!["Federated Authentication" dialog box](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "Federated Authentication")</span></span>

    <span data-ttu-id="89ab4-182">a.</span><span class="sxs-lookup"><span data-stu-id="89ab4-182">a.</span></span> <span data-ttu-id="89ab4-183">Sélectionnez **Activer l'authentification fédérée**.</span><span class="sxs-lookup"><span data-stu-id="89ab4-183">Select **Enable Federated Authentication**.</span></span>

    <span data-ttu-id="89ab4-184">b.</span><span class="sxs-lookup"><span data-stu-id="89ab4-184">b.</span></span> <span data-ttu-id="89ab4-185">Cliquez sur **télécharger** tooupload votre certificat téléchargé.</span><span class="sxs-lookup"><span data-stu-id="89ab4-185">Click **Upload** tooupload your downloaded certificate.</span></span>

    <span data-ttu-id="89ab4-186">c.</span><span class="sxs-lookup"><span data-stu-id="89ab4-186">c.</span></span> <span data-ttu-id="89ab4-187">Bonjour **URL de connexion** , entrez la valeur hello **SAML Sign-On URL du Service unique** à partir de la fenêtre de configuration d’application hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89ab4-187">In hello **Sign-in URL** box, enter hello value of **SAML Single Sign-On Service URL** from hello Azure AD application configuration window.</span></span>

    <span data-ttu-id="89ab4-188">d.</span><span class="sxs-lookup"><span data-stu-id="89ab4-188">d.</span></span> <span data-ttu-id="89ab4-189">Bonjour **URL de déconnexion** , entrez la valeur hello **URL de déconnexion** à partir de la fenêtre de configuration d’application hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89ab4-189">In hello **Sign-out URL** box, enter hello value of **Sign-Out URL** from hello Azure AD application configuration window.</span></span>

    <span data-ttu-id="89ab4-190">e.</span><span class="sxs-lookup"><span data-stu-id="89ab4-190">e.</span></span> <span data-ttu-id="89ab4-191">Sélectionnez **Use POST**.</span><span class="sxs-lookup"><span data-stu-id="89ab4-191">Select **Use POST**.</span></span>

    <span data-ttu-id="89ab4-192">f.</span><span class="sxs-lookup"><span data-stu-id="89ab4-192">f.</span></span> <span data-ttu-id="89ab4-193">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="89ab4-193">Click **Save**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="89ab4-194">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="89ab4-194">Create an Azure AD test user</span></span>
<span data-ttu-id="89ab4-195">Bonjour portail Azure, créez un utilisateur de test appelé Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="89ab4-195">In hello Azure portal, create a test user called Britta Simon.</span></span>

![Nom et adresse de messagerie de l’utilisateur de test hello Azure AD][100]

1. <span data-ttu-id="89ab4-197">Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="89ab4-197">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** icon.</span></span>

    ![Icône Azure Active Directory](./media/active-directory-saas-clarizen-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="89ab4-199">Cliquez sur **utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs** liste de hello toodisplay des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="89ab4-199">Click **Users and groups**, and then click **All users** toodisplay hello list of users.</span></span>

    ![Sélection des options « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/active-directory-saas-clarizen-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="89ab4-201">En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="89ab4-201">At hello top of hello dialog box, click **Add** tooopen hello **User** dialog box.</span></span>

    ![bouton « Ajouter » de Hello](./media/active-directory-saas-clarizen-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="89ab4-203">Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="89ab4-203">In hello **User** dialog box, perform hello following steps:</span></span>

    ![Boîte de dialogue « Utilisateur » renseignée avec le nom, l’adresse e-mail et le mot de passe](./media/active-directory-saas-clarizen-tutorial/create_aaduser_04.png)

    <span data-ttu-id="89ab4-205">a.</span><span class="sxs-lookup"><span data-stu-id="89ab4-205">a.</span></span> <span data-ttu-id="89ab4-206">Bonjour **nom** , tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="89ab4-206">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="89ab4-207">b.</span><span class="sxs-lookup"><span data-stu-id="89ab4-207">b.</span></span> <span data-ttu-id="89ab4-208">Bonjour **nom d’utilisateur** zone, l’adresse de messagerie de type hello Hello compte de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="89ab4-208">In hello **User name** box, type hello email address of hello Britta Simon account.</span></span>

    <span data-ttu-id="89ab4-209">c.</span><span class="sxs-lookup"><span data-stu-id="89ab4-209">c.</span></span> <span data-ttu-id="89ab4-210">Sélectionnez **afficher le mot de passe** et notez la valeur hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="89ab4-210">Select **Show Password** and write down hello value of **Password**.</span></span>

    <span data-ttu-id="89ab4-211">d.</span><span class="sxs-lookup"><span data-stu-id="89ab4-211">d.</span></span> <span data-ttu-id="89ab4-212">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="89ab4-212">Click **Create**.</span></span>

### <a name="create-a-clarizen-test-user"></a><span data-ttu-id="89ab4-213">Créer un utilisateur de test Clarizen</span><span class="sxs-lookup"><span data-stu-id="89ab4-213">Create a Clarizen test user</span></span>
<span data-ttu-id="89ab4-214">tooenable le toosign les utilisateurs Azure AD dans tooClarizen, vous devez configurer des comptes d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="89ab4-214">tooenable Azure AD users toosign in tooClarizen, you must provision user accounts.</span></span> <span data-ttu-id="89ab4-215">Dans les cas de hello d’occurrence, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="89ab4-215">In hello case of Clarizen, provisioning is a manual task.</span></span>

1. <span data-ttu-id="89ab4-216">Se connecter tooyour site d’entreprise Clarizen en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="89ab4-216">Sign in tooyour Clarizen company site as an administrator.</span></span>

2. <span data-ttu-id="89ab4-217">Cliquez sur **People**.</span><span class="sxs-lookup"><span data-stu-id="89ab4-217">Click **People**.</span></span>

    <span data-ttu-id="89ab4-218">![Sélection de l’option « People » (Contacts)](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "People") (Contacts)</span><span class="sxs-lookup"><span data-stu-id="89ab4-218">![Clicking "People"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "People")</span></span>

3. <span data-ttu-id="89ab4-219">Cliquez sur **Invite User**.</span><span class="sxs-lookup"><span data-stu-id="89ab4-219">Click **Invite User**.</span></span>

    <span data-ttu-id="89ab4-220">![Bouton « Invite User » (Inviter un utilisateur)](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "Invite Users") (Inviter un utilisateur)</span><span class="sxs-lookup"><span data-stu-id="89ab4-220">!["Invite User" button](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "Invite Users")</span></span>

4. <span data-ttu-id="89ab4-221">Bonjour **inviter des personnes** boîte de dialogue, exécutez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="89ab4-221">In hello **Invite People** dialog box, perform hello following steps:</span></span>

    <span data-ttu-id="89ab4-222">![Boîte de dialogue « Invite People » (Inviter un contact)](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "Invite People") (Inviter un contact)</span><span class="sxs-lookup"><span data-stu-id="89ab4-222">!["Invite People" dialog box](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "Invite People")</span></span>

    <span data-ttu-id="89ab4-223">a.</span><span class="sxs-lookup"><span data-stu-id="89ab4-223">a.</span></span> <span data-ttu-id="89ab4-224">Bonjour **messagerie** zone, l’adresse de messagerie de type hello Hello compte de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="89ab4-224">In hello **Email** box, type hello email address of hello Britta Simon account.</span></span>

    <span data-ttu-id="89ab4-225">b.</span><span class="sxs-lookup"><span data-stu-id="89ab4-225">b.</span></span> <span data-ttu-id="89ab4-226">Cliquez sur **Invite**.</span><span class="sxs-lookup"><span data-stu-id="89ab4-226">Click **Invite**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="89ab4-227">titulaire du compte Azure Active Directory Hello sera reçoivent un e-mail et suivez les leur compte d’un tooconfirm lien avant son activation.</span><span class="sxs-lookup"><span data-stu-id="89ab4-227">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="89ab4-228">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="89ab4-228">Assign hello Azure AD test user</span></span>
<span data-ttu-id="89ab4-229">Activer toouse Britta Simon Azure l’authentification unique en accordant tooClarizen de son accès.</span><span class="sxs-lookup"><span data-stu-id="89ab4-229">Enable Britta Simon toouse Azure single sign-on by granting her access tooClarizen.</span></span>

![Utilisateur de test affecté][200]

1. <span data-ttu-id="89ab4-231">Dans hello portail Azure, ouvrez la vue des applications hello, vue de répertoire toohello, cliquez sur **des applications d’entreprise**, puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="89ab4-231">In hello Azure portal, open hello applications view, browse toohello directory view, click **Enterprise applications**, and then click **All applications**.</span></span>

    ![Sélection des options « Applications d’entreprise » et « Toutes les applications »][201]

2. <span data-ttu-id="89ab4-233">Dans la liste des applications hello, sélectionnez **Clarizen**.</span><span class="sxs-lookup"><span data-stu-id="89ab4-233">In hello applications list, select **Clarizen**.</span></span>

    ![Sélection de Clarizen dans la liste de hello](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_50.png)

3. <span data-ttu-id="89ab4-235">Dans le volet gauche de hello, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="89ab4-235">In hello left pane, click **Users and groups**.</span></span>

    ![Sélection de l’option « Utilisateurs et groupes »][202]

4. <span data-ttu-id="89ab4-237">Cliquez sur hello **ajouter** bouton.</span><span class="sxs-lookup"><span data-stu-id="89ab4-237">Click hello **Add** button.</span></span> <span data-ttu-id="89ab4-238">Ensuite, dans hello **ajouter l’affectation** boîte de dialogue, sélectionnez **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="89ab4-238">Then, in hello **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![bouton « Ajouter » de Hello et de la boîte de dialogue « Ajouter l’affectation » hello][203]

5. <span data-ttu-id="89ab4-240">Bonjour **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans liste hello des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="89ab4-240">In hello **Users and groups** dialog box, select **Britta Simon** in hello list of users.</span></span>

6. <span data-ttu-id="89ab4-241">Bonjour **utilisateurs et groupes** boîte de dialogue, cliquez sur hello **sélectionnez** bouton.</span><span class="sxs-lookup"><span data-stu-id="89ab4-241">In hello **Users and groups** dialog box, click hello **Select** button.</span></span>

7. <span data-ttu-id="89ab4-242">Bonjour **ajouter l’affectation** boîte de dialogue, cliquez sur hello **affecter** bouton.</span><span class="sxs-lookup"><span data-stu-id="89ab4-242">In hello **Add Assignment** dialog box, click hello **Assign** button.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="89ab4-243">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="89ab4-243">Test single sign-on</span></span>
<span data-ttu-id="89ab4-244">Tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="89ab4-244">Test your Azure AD single sign-on configuration by using hello Access Panel.</span></span>

<span data-ttu-id="89ab4-245">Lorsque vous cliquez sur mosaïque Clarizen hello hello volet d’accès, vous devez être connecté automatiquement dans tooyour Clarizen application.</span><span class="sxs-lookup"><span data-stu-id="89ab4-245">When you click hello Clarizen tile in hello Access Panel, you should be automatically signed in tooyour Clarizen application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="89ab4-246">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="89ab4-246">Additional resources</span></span>

* [<span data-ttu-id="89ab4-247">Liste des didacticiels sur la façon de toointegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="89ab4-247">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="89ab4-248">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="89ab4-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_203.png
