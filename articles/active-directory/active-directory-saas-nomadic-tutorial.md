---
title: "Didacticiel : Intégration d’Azure Active Directory à Nomadic | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Nomadic."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 13d02b1c-d98a-40b1-824f-afa45a2deb6a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 8c1d3e350ce03c373cf475b2786ec299a7ce5f80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-nomadic"></a><span data-ttu-id="6b894-103">Didacticiel : Intégration d’Azure Active Directory à Nomadic</span><span class="sxs-lookup"><span data-stu-id="6b894-103">Tutorial: Azure Active Directory integration with Nomadic</span></span>

<span data-ttu-id="6b894-104">Dans ce didacticiel, vous apprendrez comment toointegrate Nomadic avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6b894-104">In this tutorial, you learn how toointegrate Nomadic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6b894-105">Intégration Nomadic à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="6b894-105">Integrating Nomadic with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6b894-106">Vous pouvez contrôler dans Azure AD qui a accès tooNomadic.</span><span class="sxs-lookup"><span data-stu-id="6b894-106">You can control in Azure AD who has access tooNomadic.</span></span>
- <span data-ttu-id="6b894-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooNomadic (Single Sign-On) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6b894-107">You can enable your users tooautomatically get signed-on tooNomadic (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="6b894-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="6b894-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="6b894-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6b894-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6b894-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="6b894-110">Prerequisites</span></span>

<span data-ttu-id="6b894-111">tooconfigure intégration d’Azure AD avec Nomadic, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="6b894-111">tooconfigure Azure AD integration with Nomadic, you need hello following items:</span></span>

- <span data-ttu-id="6b894-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="6b894-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6b894-113">Un abonnement Nomadic pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="6b894-113">A Nomadic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6b894-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="6b894-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6b894-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="6b894-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6b894-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="6b894-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6b894-117">Si vous ne disposez pas d’un environnement d’essai Azure AD, vous pouvez [vous inscrire pour un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6b894-117">If you don't have an Azure AD trial environment, you can [get a one-month trial here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6b894-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="6b894-118">Scenario description</span></span>
<span data-ttu-id="6b894-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="6b894-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6b894-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="6b894-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6b894-121">Ajouter des Nomadic à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="6b894-121">Add Nomadic from hello gallery</span></span>
2. <span data-ttu-id="6b894-122">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="6b894-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-nomadic-from-hello-gallery"></a><span data-ttu-id="6b894-123">Ajouter des Nomadic à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="6b894-123">Add Nomadic from hello gallery</span></span>
<span data-ttu-id="6b894-124">intégration de hello tooconfigure de Nomadic dans Azure AD, vous devez tooadd Nomadic à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="6b894-124">tooconfigure hello integration of Nomadic into Azure AD, you need tooadd Nomadic from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6b894-125">**tooadd Nomadic à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6b894-125">**tooadd Nomadic from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6b894-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="6b894-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="6b894-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="6b894-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6b894-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="6b894-129">Then go too**All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="6b894-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="6b894-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="6b894-133">Dans la zone de recherche de hello, tapez **Nomadic**, sélectionnez **Nomadic** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="6b894-133">In hello search box, type **Nomadic**, select **Nomadic** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Nomades dans la liste des résultats hello](./media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="6b894-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="6b894-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="6b894-136">Dans cette section, vous configurez et vous testez l’authentification unique Azure AD avec Nomadic, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="6b894-136">In this section, you configure and test Azure AD single sign-on with Nomadic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6b894-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Nomadic est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6b894-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Nomadic is tooa user in Azure AD.</span></span> <span data-ttu-id="6b894-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Nomadic doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="6b894-138">In other words, a link relationship between an Azure AD user and hello related user in Nomadic needs toobe established.</span></span>

<span data-ttu-id="6b894-139">Dans Nomadic, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="6b894-139">In Nomadic, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6b894-140">tooconfigure et test Azure AD l’authentification unique avec Nomadic, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="6b894-140">tooconfigure and test Azure AD single sign-on with Nomadic, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6b894-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="6b894-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6b894-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6b894-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6b894-143">**[Créer un utilisateur test nomades](#create-a-nomadic-test-user)**  -toohave un équivalent de Britta Simon dans Nomadic est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6b894-143">**[Create a Nomadic test user](#create-a-nomadic-test-user)** - toohave a counterpart of Britta Simon in Nomadic that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6b894-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="6b894-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6b894-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="6b894-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="6b894-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="6b894-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="6b894-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application nomades.</span><span class="sxs-lookup"><span data-stu-id="6b894-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Nomadic application.</span></span>

<span data-ttu-id="6b894-148">**tooconfigure Azure AD single sign-on avec Nomadic, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6b894-148">**tooconfigure Azure AD single sign-on with Nomadic, perform hello following steps:**</span></span>

1. <span data-ttu-id="6b894-149">Bonjour portail Azure, sur hello **Nomadic** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="6b894-149">In hello Azure portal, on hello **Nomadic** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="6b894-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="6b894-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_samlbase.png)

3. <span data-ttu-id="6b894-153">Sur hello **domaine nomades et URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="6b894-153">On hello **Nomadic Domain and URLs** section, perform hello following steps:</span></span>

    ![Informations d’authentification unique dans Nomadic Domain and URLs (Domaine et URL Nomadic)](./media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_url.png)

    <span data-ttu-id="6b894-155">a.</span><span class="sxs-lookup"><span data-stu-id="6b894-155">a.</span></span> <span data-ttu-id="6b894-156">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company name>.nomadic.fm/signin`</span><span class="sxs-lookup"><span data-stu-id="6b894-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.nomadic.fm/signin`</span></span>

    <span data-ttu-id="6b894-157">b.</span><span class="sxs-lookup"><span data-stu-id="6b894-157">b.</span></span> <span data-ttu-id="6b894-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle : `https://<company name>.nomadic.fm/auth/saml2/sp`,`https://<company name>.staging.nomadic.fm/auth/saml2/sp`</span><span class="sxs-lookup"><span data-stu-id="6b894-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.nomadic.fm/auth/saml2/sp`, `https://<company name>.staging.nomadic.fm/auth/saml2/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6b894-159">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="6b894-159">These values are not real.</span></span> <span data-ttu-id="6b894-160">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="6b894-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="6b894-161">Contact [équipe de support Client nomades](mailto:help@nomadic.fm) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="6b894-161">Contact [Nomadic Client support team](mailto:help@nomadic.fm) tooget these values.</span></span> 
 


4. <span data-ttu-id="6b894-162">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="6b894-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_certificate.png) 

5. <span data-ttu-id="6b894-164">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="6b894-164">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-nomadic-tutorial/tutorial_general_400.png)

6.  <span data-ttu-id="6b894-166">tooget l’authentification unique configurée pour votre application, contactez [équipe de support nomades](mailto:help@nomadic.fm) et fournissez-leur hello téléchargé **métadonnées**.</span><span class="sxs-lookup"><span data-stu-id="6b894-166">tooget SSO configured for your application, contact [Nomadic support team](mailto:help@nomadic.fm) and provide them with hello downloaded **metadata**.</span></span>

> [!TIP]
> <span data-ttu-id="6b894-167">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="6b894-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6b894-168">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="6b894-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6b894-169">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6b894-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="6b894-170">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="6b894-170">Create an Azure AD test user</span></span>

<span data-ttu-id="6b894-171">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="6b894-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="6b894-173">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6b894-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6b894-174">Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.</span><span class="sxs-lookup"><span data-stu-id="6b894-174">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-nomadic-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="6b894-176">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="6b894-176">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-nomadic-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="6b894-178">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="6b894-178">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![bouton Ajouter de Hello](./media/active-directory-saas-nomadic-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="6b894-180">Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="6b894-180">In hello **User** dialog box, perform hello following steps:</span></span>

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-nomadic-tutorial/create_aaduser_04.png)

    <span data-ttu-id="6b894-182">a.</span><span class="sxs-lookup"><span data-stu-id="6b894-182">a.</span></span> <span data-ttu-id="6b894-183">Bonjour **nom** , tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6b894-183">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6b894-184">b.</span><span class="sxs-lookup"><span data-stu-id="6b894-184">b.</span></span> <span data-ttu-id="6b894-185">Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6b894-185">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="6b894-186">c.</span><span class="sxs-lookup"><span data-stu-id="6b894-186">c.</span></span> <span data-ttu-id="6b894-187">Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.</span><span class="sxs-lookup"><span data-stu-id="6b894-187">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="6b894-188">d.</span><span class="sxs-lookup"><span data-stu-id="6b894-188">d.</span></span> <span data-ttu-id="6b894-189">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="6b894-189">Click **Create**.</span></span>
 
### <a name="create-a-nomadic-test-user"></a><span data-ttu-id="6b894-190">Créer un utilisateur de test Nomadic</span><span class="sxs-lookup"><span data-stu-id="6b894-190">Create a Nomadic test user</span></span>

<span data-ttu-id="6b894-191">Dans cette section, vous créez un utilisateur nommé Britta Simon dans Nomadic.</span><span class="sxs-lookup"><span data-stu-id="6b894-191">In this section, you create a user called Britta Simon in Nomadic.</span></span> <span data-ttu-id="6b894-192">Collaborez avec [équipe de support nomades](mailto:help@nomadic.fm) utilisateurs hello tooadd plateforme nomades de hello.</span><span class="sxs-lookup"><span data-stu-id="6b894-192">Please work with [Nomadic support team](mailto:help@nomadic.fm) tooadd hello users in hello Nomadic platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="6b894-193">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="6b894-193">Assign hello Azure AD test user</span></span>

<span data-ttu-id="6b894-194">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooNomadic.</span><span class="sxs-lookup"><span data-stu-id="6b894-194">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNomadic.</span></span>

![Attribuer le rôle d’utilisateur hello][200] 

<span data-ttu-id="6b894-196">**tooassign Britta Simon tooNomadic, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6b894-196">**tooassign Britta Simon tooNomadic, perform hello following steps:**</span></span>

1. <span data-ttu-id="6b894-197">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="6b894-197">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="6b894-199">Dans la liste des applications hello, sélectionnez **Nomadic**.</span><span class="sxs-lookup"><span data-stu-id="6b894-199">In hello applications list, select **Nomadic**.</span></span>

    ![Hello Nomadic lien dans la liste des Applications hello](./media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_app.png)  

3. <span data-ttu-id="6b894-201">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="6b894-201">In hello menu on hello left, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202]

4. <span data-ttu-id="6b894-203">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="6b894-203">Click **Add** button.</span></span> <span data-ttu-id="6b894-204">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="6b894-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="6b894-206">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="6b894-206">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6b894-207">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="6b894-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6b894-208">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="6b894-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="6b894-209">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="6b894-209">Test single sign-on</span></span>

<span data-ttu-id="6b894-210">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="6b894-210">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6b894-211">Lorsque vous cliquez sur la vignette de nomades hello dans hello volet d’accès, vous devez obtenir les applications nomades tooyour automatiquement signé sur.</span><span class="sxs-lookup"><span data-stu-id="6b894-211">When you click hello Nomadic tile in hello Access Panel, you should get automatically signed-on tooyour Nomadic application.</span></span>
<span data-ttu-id="6b894-212">Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6b894-212">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6b894-213">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="6b894-213">Additional resources</span></span>

* [<span data-ttu-id="6b894-214">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6b894-214">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6b894-215">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="6b894-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_203.png

