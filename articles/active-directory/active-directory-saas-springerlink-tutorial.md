---
title: "Didacticiel : Intégration d’Azure Active Directory avec Springer Link | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Springer lien."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 58cdf029-bdc0-43c4-a469-b921c2a669bd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: jeedes
ms.openlocfilehash: dabd2f72b3a195fc359826a4863a197e5019f5c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-springer-link"></a><span data-ttu-id="93558-103">Didacticiel : Intégration d’Azure Active Directory avec Springer Link</span><span class="sxs-lookup"><span data-stu-id="93558-103">Tutorial: Azure Active Directory integration with Springer Link</span></span>

<span data-ttu-id="93558-104">Dans ce didacticiel, vous apprendrez comment créer un lien toointegrate Springer avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="93558-104">In this tutorial, you learn how toointegrate Springer Link with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="93558-105">Intégration Springer lien à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="93558-105">Integrating Springer Link with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="93558-106">Vous pouvez contrôler dans Azure AD qui a accès tooSpringer lien.</span><span class="sxs-lookup"><span data-stu-id="93558-106">You can control in Azure AD who has access tooSpringer Link.</span></span>
- <span data-ttu-id="93558-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSpringer lien (Single Sign-On) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="93558-107">You can enable your users tooautomatically get signed-on tooSpringer Link (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="93558-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="93558-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="93558-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="93558-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="93558-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="93558-110">Prerequisites</span></span>

<span data-ttu-id="93558-111">tooconfigure intégration d’Azure AD avec Springer lien, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="93558-111">tooconfigure Azure AD integration with Springer Link, you need hello following items:</span></span>

- <span data-ttu-id="93558-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="93558-112">An Azure AD subscription</span></span>
- <span data-ttu-id="93558-113">Un abonnement Springer Link pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="93558-113">A Springer Link single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="93558-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="93558-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="93558-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="93558-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="93558-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="93558-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="93558-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="93558-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="93558-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="93558-118">Scenario description</span></span>
<span data-ttu-id="93558-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="93558-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="93558-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="93558-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="93558-121">Ajout de Springer lien à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="93558-121">Adding Springer Link from hello gallery</span></span>
2. <span data-ttu-id="93558-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="93558-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-springer-link-from-hello-gallery"></a><span data-ttu-id="93558-123">Ajout de Springer lien à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="93558-123">Adding Springer Link from hello gallery</span></span>
<span data-ttu-id="93558-124">intégration de hello tooconfigure de lien de Springer dans Azure AD, vous devez tooadd Springer lien à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="93558-124">tooconfigure hello integration of Springer Link into Azure AD, you need tooadd Springer Link from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="93558-125">**tooadd lien Springer à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="93558-125">**tooadd Springer Link from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="93558-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="93558-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="93558-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="93558-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="93558-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="93558-129">Then go too**All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="93558-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="93558-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="93558-133">Dans la zone de recherche de hello, tapez **Springer lien**, sélectionnez **Springer lien** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="93558-133">In hello search box, type **Springer Link**, select **Springer Link** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Liste des résultats de lien Springer Bonjour](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="93558-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="93558-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="93558-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Springer Link, sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="93558-136">In this section, you configure and test Azure AD single sign-on with Springer Link based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="93558-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Springer lien est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="93558-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Springer Link is tooa user in Azure AD.</span></span> <span data-ttu-id="93558-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Springer lien doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="93558-138">In other words, a link relationship between an Azure AD user and hello related user in Springer Link needs toobe established.</span></span>

<span data-ttu-id="93558-139">Dans le lien de Springer, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="93558-139">In Springer Link, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="93558-140">tooconfigure et test Azure AD l’authentification unique avec Springer lien, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="93558-140">tooconfigure and test Azure AD single sign-on with Springer Link, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="93558-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="93558-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="93558-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="93558-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="93558-143">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="93558-143">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
4. <span data-ttu-id="93558-144">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="93558-144">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="93558-145">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="93558-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="93558-146">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Springer lien.</span><span class="sxs-lookup"><span data-stu-id="93558-146">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Springer Link application.</span></span>

<span data-ttu-id="93558-147">**tooconfigure Azure AD single sign-on avec Springer lien, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="93558-147">**tooconfigure Azure AD single sign-on with Springer Link, perform hello following steps:**</span></span>

1. <span data-ttu-id="93558-148">Bonjour portail Azure, sur hello **Springer lien** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="93558-148">In hello Azure portal, on hello **Springer Link** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="93558-150">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="93558-150">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_samlbase.png)

3. <span data-ttu-id="93558-152">Sur hello **URL et le domaine du lien Springer** section, si vous le souhaitez application hello tooconfigure **IDP** en mode initié par :</span><span class="sxs-lookup"><span data-stu-id="93558-152">On hello **Springer Link Domain and URLs** section,  If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Informations d’authentification unique dans Domaine et URL Springer Link](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_url1.png)

    <span data-ttu-id="93558-154">a.</span><span class="sxs-lookup"><span data-stu-id="93558-154">a.</span></span> <span data-ttu-id="93558-155">Bonjour **identificateur** zone de texte, tapez l’URL hello :`https://fsso.springer.com`</span><span class="sxs-lookup"><span data-stu-id="93558-155">In hello **Identifier** textbox, type hello URL: `https://fsso.springer.com`</span></span>

    <span data-ttu-id="93558-156">b.</span><span class="sxs-lookup"><span data-stu-id="93558-156">b.</span></span> <span data-ttu-id="93558-157">Bonjour **URL de réponse** zone de texte, tapez l’URL hello :`https://fsso-qa1.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span><span class="sxs-lookup"><span data-stu-id="93558-157">In hello **Reply URL** textbox, type hello URL: `https://fsso-qa1.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span></span>    

4. <span data-ttu-id="93558-158">Cliquez sur **Afficher les paramètres d’URL avancés**.</span><span class="sxs-lookup"><span data-stu-id="93558-158">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="93558-159">Si vous le souhaitez application hello tooconfigure **SP** en mode initié par :</span><span class="sxs-lookup"><span data-stu-id="93558-159">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Informations d’authentification unique dans Domaine et URL Springer Link](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_url.png)

    <span data-ttu-id="93558-161">Bonjour **URL de connexion** zone de texte, tapez l’URL hello :`https://fsso.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span><span class="sxs-lookup"><span data-stu-id="93558-161">In hello **Sign-on URL** textbox, type hello URL : `https://fsso.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span></span>    

5. <span data-ttu-id="93558-162">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="93558-162">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-springerlink-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="93558-164">toogenerate hello **métadonnées** url, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="93558-164">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="93558-165">a.</span><span class="sxs-lookup"><span data-stu-id="93558-165">a.</span></span> <span data-ttu-id="93558-166">Cliquez sur **Inscriptions des applications**.</span><span class="sxs-lookup"><span data-stu-id="93558-166">Click **App registrations**.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_appregistrations.png)
   
    <span data-ttu-id="93558-168">b.</span><span class="sxs-lookup"><span data-stu-id="93558-168">b.</span></span> <span data-ttu-id="93558-169">Cliquez sur **points de terminaison** tooopen **points de terminaison** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="93558-169">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Configurer l’authentification unique](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_endpointicon.png)

    <span data-ttu-id="93558-171">c.</span><span class="sxs-lookup"><span data-stu-id="93558-171">c.</span></span> <span data-ttu-id="93558-172">Cliquez sur hello copie bouton toocopy **DOCUMENT de métadonnées de fédération** url et collez-le dans le bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="93558-172">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_endpoint.png)
     
    <span data-ttu-id="93558-174">d.</span><span class="sxs-lookup"><span data-stu-id="93558-174">d.</span></span> <span data-ttu-id="93558-175">Maintenant accédez toohello page de propriétés de **Springer lien** et copie Bonjour **Id d’Application** à l’aide de **copie** bouton et collez-le dans le bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="93558-175">Now go toohello property page of **Springer Link** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_appid.png)

    <span data-ttu-id="93558-177">e.</span><span class="sxs-lookup"><span data-stu-id="93558-177">e.</span></span> <span data-ttu-id="93558-178">Générer hello **URL de métadonnées** hello suivant le modèle à l’aide de :`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="93558-178">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

7. <span data-ttu-id="93558-179">tooconfigure l’authentification unique sur **Springer lien** côté, vous devez hello toosend généré **URL de métadonnées** trop[équipe de support Springer lien](mailto:identity@springernature.com).</span><span class="sxs-lookup"><span data-stu-id="93558-179">tooconfigure single sign-on on **Springer Link** side, you need toosend hello generated **Metadata URL** too[Springer Link support team](mailto:identity@springernature.com).</span></span>

> [!TIP]
> <span data-ttu-id="93558-180">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="93558-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="93558-181">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="93558-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="93558-182">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="93558-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="93558-183">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="93558-183">Create an Azure AD test user</span></span>

<span data-ttu-id="93558-184">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="93558-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="93558-186">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="93558-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="93558-187">Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.</span><span class="sxs-lookup"><span data-stu-id="93558-187">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-springerlink-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="93558-189">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="93558-189">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-springerlink-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="93558-191">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="93558-191">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![bouton Ajouter de Hello](./media/active-directory-saas-springerlink-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="93558-193">Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="93558-193">In hello **User** dialog box, perform hello following steps:</span></span>

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-springerlink-tutorial/create_aaduser_04.png)

    <span data-ttu-id="93558-195">a.</span><span class="sxs-lookup"><span data-stu-id="93558-195">a.</span></span> <span data-ttu-id="93558-196">Bonjour **nom** , tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="93558-196">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="93558-197">b.</span><span class="sxs-lookup"><span data-stu-id="93558-197">b.</span></span> <span data-ttu-id="93558-198">Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="93558-198">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="93558-199">c.</span><span class="sxs-lookup"><span data-stu-id="93558-199">c.</span></span> <span data-ttu-id="93558-200">Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.</span><span class="sxs-lookup"><span data-stu-id="93558-200">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="93558-201">d.</span><span class="sxs-lookup"><span data-stu-id="93558-201">d.</span></span> <span data-ttu-id="93558-202">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="93558-202">Click **Create**.</span></span>
 
### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="93558-203">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="93558-203">Assign hello Azure AD test user</span></span>

<span data-ttu-id="93558-204">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooSpringer lien.</span><span class="sxs-lookup"><span data-stu-id="93558-204">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSpringer Link.</span></span>

![Attribuer le rôle d’utilisateur hello][200] 

<span data-ttu-id="93558-206">**tooassign Britta Simon tooSpringer lien, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="93558-206">**tooassign Britta Simon tooSpringer Link, perform hello following steps:**</span></span>

1. <span data-ttu-id="93558-207">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="93558-207">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="93558-209">Dans la liste des applications hello, sélectionnez **Springer lien**.</span><span class="sxs-lookup"><span data-stu-id="93558-209">In hello applications list, select **Springer Link**.</span></span>

    ![Hello Springer liaison liaison dans la liste des Applications hello](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_app.png)  

3. <span data-ttu-id="93558-211">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="93558-211">In hello menu on hello left, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202]

4. <span data-ttu-id="93558-213">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="93558-213">Click **Add** button.</span></span> <span data-ttu-id="93558-214">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="93558-214">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="93558-216">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="93558-216">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="93558-217">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="93558-217">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="93558-218">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="93558-218">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="93558-219">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="93558-219">Test single sign-on</span></span>

<span data-ttu-id="93558-220">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="93558-220">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="93558-221">Lorsque vous cliquez sur mosaïque Springer lien hello hello volet d’accès, vous devez obtenir l’application de Springer lien automatiquement signé sur tooyour.</span><span class="sxs-lookup"><span data-stu-id="93558-221">When you click hello Springer Link tile in hello Access Panel, you should get automatically signed-on tooyour Springer Link application.</span></span>
<span data-ttu-id="93558-222">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="93558-222">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="93558-223">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="93558-223">Additional resources</span></span>

* [<span data-ttu-id="93558-224">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="93558-224">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="93558-225">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="93558-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_203.png

