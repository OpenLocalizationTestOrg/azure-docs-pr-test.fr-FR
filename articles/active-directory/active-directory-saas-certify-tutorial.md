---
title: "Didacticiel : Intégration d’Azure Active Directory à Certify | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et certifier."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0b36e020-175a-4534-b341-85260739f889
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 000bef7b679a6f291b1f3cb42e10cb3ed424b25d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-certify"></a><span data-ttu-id="4714d-103">Didacticiel : Intégration d’Azure Active Directory à Certify</span><span class="sxs-lookup"><span data-stu-id="4714d-103">Tutorial: Azure Active Directory integration with Certify</span></span>

<span data-ttu-id="4714d-104">Dans ce didacticiel, vous apprendrez comment toointegrate certifier avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4714d-104">In this tutorial, you learn how toointegrate Certify with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4714d-105">Intégration de certifier à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="4714d-105">Integrating Certify with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4714d-106">Vous pouvez contrôler dans Azure AD qui a accès tooCertify</span><span class="sxs-lookup"><span data-stu-id="4714d-106">You can control in Azure AD who has access tooCertify</span></span>
- <span data-ttu-id="4714d-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooCertify (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="4714d-107">You can enable your users tooautomatically get signed-on tooCertify (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4714d-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="4714d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4714d-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4714d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4714d-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="4714d-110">Prerequisites</span></span>

<span data-ttu-id="4714d-111">intégration d’Azure AD de tooconfigure avec Certify, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="4714d-111">tooconfigure Azure AD integration with Certify, you need hello following items:</span></span>

- <span data-ttu-id="4714d-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="4714d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4714d-113">Un abonnement Certify pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="4714d-113">A Certify single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4714d-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="4714d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4714d-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="4714d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4714d-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="4714d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4714d-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4714d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4714d-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="4714d-118">Scenario description</span></span>
<span data-ttu-id="4714d-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="4714d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4714d-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="4714d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4714d-121">Ajout de certifier à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="4714d-121">Adding Certify from hello gallery</span></span>
2. <span data-ttu-id="4714d-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4714d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-certify-from-hello-gallery"></a><span data-ttu-id="4714d-123">Ajout de certifier à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="4714d-123">Adding Certify from hello gallery</span></span>
<span data-ttu-id="4714d-124">tooconfigure hello intégration de certifier dans Azure AD, vous devez tooadd certifier à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="4714d-124">tooconfigure hello integration of Certify into Azure AD, you need tooadd Certify from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4714d-125">**tooadd certifier à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4714d-125">**tooadd Certify from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4714d-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="4714d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4714d-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="4714d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4714d-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="4714d-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="4714d-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="4714d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="4714d-133">Dans la zone de recherche de hello, tapez **Certify**.</span><span class="sxs-lookup"><span data-stu-id="4714d-133">In hello search box, type **Certify**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-certify-tutorial/tutorial_certify_search.png)

5. <span data-ttu-id="4714d-135">Dans le volet de résultats hello, sélectionnez **Certify**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="4714d-135">In hello results panel, select **Certify**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-certify-tutorial/tutorial_certify_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4714d-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4714d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4714d-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Certify avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="4714d-138">In this section, you configure and test Azure AD single sign-on with Certify based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4714d-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello certifier est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4714d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Certify is tooa user in Azure AD.</span></span> <span data-ttu-id="4714d-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur de certifier hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="4714d-140">In other words, a link relationship between an Azure AD user and hello related user in Certify needs toobe established.</span></span>

<span data-ttu-id="4714d-141">Dans les certifier, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="4714d-141">In Certify, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4714d-142">tooconfigure et test Azure AD sur l’authentification unique avec certifier, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="4714d-142">tooconfigure and test Azure AD single sign-on with Certify, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4714d-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="4714d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4714d-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4714d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4714d-145">**[Création d’un utilisateur de test de certifier](#creating-a-certify-test-user)**  -toohave un équivalent de Britta Simon dans certifier est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4714d-145">**[Creating a Certify test user](#creating-a-certify-test-user)** - toohave a counterpart of Britta Simon in Certify that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4714d-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="4714d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4714d-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="4714d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4714d-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4714d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4714d-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de certifier.</span><span class="sxs-lookup"><span data-stu-id="4714d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Certify application.</span></span>

<span data-ttu-id="4714d-150">**tooconfigure Azure AD single sign-on avec certifier, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4714d-150">**tooconfigure Azure AD single sign-on with Certify, perform hello following steps:**</span></span>

1. <span data-ttu-id="4714d-151">Bonjour portail Azure, sur hello **Certify** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="4714d-151">In hello Azure portal, on hello **Certify** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="4714d-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="4714d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-certify-tutorial/tutorial_certify_samlbase.png)

3. <span data-ttu-id="4714d-155">Sur hello **certifier le domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="4714d-155">On hello **Certify Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-certify-tutorial/tutorial_certify_url.png)

    <span data-ttu-id="4714d-157">Bonjour **identificateur** zone de texte, tapez l’URL hello :`https://www.certify.com`</span><span class="sxs-lookup"><span data-stu-id="4714d-157">In hello **Identifier** textbox, type hello URL: `https://www.certify.com`</span></span>

4. <span data-ttu-id="4714d-158">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Raw)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="4714d-158">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-certify-tutorial/tutorial_certify_certificate.png) 

5. <span data-ttu-id="4714d-160">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="4714d-160">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-certify-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4714d-162">Sur hello **certifier une Configuration** , cliquez sur **configurer certifier** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="4714d-162">On hello **Certify Configuration** section, click **Configure Certify** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4714d-163">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="4714d-163">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-certify-tutorial/tutorial_certify_configure.png) 

7. <span data-ttu-id="4714d-165">tooconfigure l’authentification unique sur **Certify** côté, vous devez hello toosend téléchargé **Certificate(Raw)** et **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique**trop[équipe de support technique de certifier](mailto:support@certify.com).</span><span class="sxs-lookup"><span data-stu-id="4714d-165">tooconfigure single sign-on on **Certify** side, you need toosend hello downloaded **Certificate(Raw)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Certify support team](mailto:support@certify.com).</span></span> <span data-ttu-id="4714d-166">Ils définir ce hello toohave de paramètre connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="4714d-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="4714d-167">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="4714d-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4714d-168">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="4714d-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4714d-169">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4714d-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4714d-170">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="4714d-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="4714d-171">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="4714d-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="4714d-173">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4714d-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4714d-174">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="4714d-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-certify-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4714d-176">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="4714d-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-certify-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4714d-178">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="4714d-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-certify-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4714d-180">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="4714d-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-certify-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4714d-182">a.</span><span class="sxs-lookup"><span data-stu-id="4714d-182">a.</span></span> <span data-ttu-id="4714d-183">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4714d-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4714d-184">b.</span><span class="sxs-lookup"><span data-stu-id="4714d-184">b.</span></span> <span data-ttu-id="4714d-185">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4714d-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4714d-186">c.</span><span class="sxs-lookup"><span data-stu-id="4714d-186">c.</span></span> <span data-ttu-id="4714d-187">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="4714d-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4714d-188">d.</span><span class="sxs-lookup"><span data-stu-id="4714d-188">d.</span></span> <span data-ttu-id="4714d-189">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="4714d-189">Click **Create**.</span></span>
 
### <a name="creating-a-certify-test-user"></a><span data-ttu-id="4714d-190">Création d’un utilisateur de test Certify</span><span class="sxs-lookup"><span data-stu-id="4714d-190">Creating a Certify test user</span></span>

<span data-ttu-id="4714d-191">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans certifier.</span><span class="sxs-lookup"><span data-stu-id="4714d-191">hello objective of this section is toocreate a user called Britta Simon in Certify.</span></span> <span data-ttu-id="4714d-192">Certify prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="4714d-192">Certify supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="4714d-193">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="4714d-193">There is no action item for you in this section.</span></span> <span data-ttu-id="4714d-194">Un nouvel utilisateur s’affichera pendant une tentative de tooaccess certifier s’il n’existe pas encore.</span><span class="sxs-lookup"><span data-stu-id="4714d-194">A new user will be created during an attempt tooaccess Certify if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="4714d-195">Si vous devez manuellement toocreate un utilisateur, vous devez toocontact hello [équipe de support technique de certifier](mailto:support@certify.com).</span><span class="sxs-lookup"><span data-stu-id="4714d-195">If you need toocreate an user manually, you need toocontact hello [Certify support team](mailto:support@certify.com).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4714d-196">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4714d-196">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4714d-197">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooCertify.</span><span class="sxs-lookup"><span data-stu-id="4714d-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCertify.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="4714d-199">**tooassign Britta Simon tooCertify, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4714d-199">**tooassign Britta Simon tooCertify, perform hello following steps:**</span></span>

1. <span data-ttu-id="4714d-200">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="4714d-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="4714d-202">Dans la liste des applications hello, sélectionnez **Certify**.</span><span class="sxs-lookup"><span data-stu-id="4714d-202">In hello applications list, select **Certify**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-certify-tutorial/tutorial_certify_app.png) 

3. <span data-ttu-id="4714d-204">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="4714d-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="4714d-206">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="4714d-206">Click **Add** button.</span></span> <span data-ttu-id="4714d-207">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="4714d-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="4714d-209">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="4714d-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4714d-210">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="4714d-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4714d-211">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="4714d-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4714d-212">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="4714d-212">Testing single sign-on</span></span>

<span data-ttu-id="4714d-213">objectif Hello de cette section est tootest votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="4714d-213">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="4714d-214">Lorsque vous cliquez sur mosaïque de certifier hello Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour Certify application.</span><span class="sxs-lookup"><span data-stu-id="4714d-214">When you click hello Certify tile in hello Access Panel, you should get automatically signed-on tooyour Certify application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4714d-215">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="4714d-215">Additional resources</span></span>

* [<span data-ttu-id="4714d-216">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4714d-216">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4714d-217">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="4714d-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-certify-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-certify-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-certify-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-certify-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-certify-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-certify-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-certify-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-certify-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-certify-tutorial/tutorial_general_203.png

