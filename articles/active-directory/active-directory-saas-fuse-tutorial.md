---
title: "Didacticiel : Intégration d’Azure AD à Fuse | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et fusible."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 5ef34f58-863a-4b37-875c-e8efa3e18bb3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 720ed8af0b5de1e3bee5a40353ca0ee661766864
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fuse"></a><span data-ttu-id="c90ec-103">Didacticiel : Intégration d’Azure Active Directory avec Fuse</span><span class="sxs-lookup"><span data-stu-id="c90ec-103">Tutorial: Azure Active Directory integration with Fuse</span></span>

<span data-ttu-id="c90ec-104">Dans ce didacticiel, vous apprendrez comment toointegrate fusible avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c90ec-104">In this tutorial, you learn how toointegrate Fuse with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c90ec-105">Intégration fusible à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="c90ec-105">Integrating Fuse with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c90ec-106">Vous pouvez contrôler dans Azure AD qui a accès tooFuse.</span><span class="sxs-lookup"><span data-stu-id="c90ec-106">You can control in Azure AD who has access tooFuse.</span></span>
- <span data-ttu-id="c90ec-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooFuse (Single Sign-On) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c90ec-107">You can enable your users tooautomatically get signed-on tooFuse (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="c90ec-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c90ec-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="c90ec-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c90ec-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c90ec-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c90ec-110">Prerequisites</span></span>

<span data-ttu-id="c90ec-111">intégration de tooconfigure Azure AD à fusible, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="c90ec-111">tooconfigure Azure AD integration with Fuse, you need hello following items:</span></span>

- <span data-ttu-id="c90ec-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="c90ec-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c90ec-113">Un abonnement Fuse pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="c90ec-113">A Fuse single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c90ec-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="c90ec-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c90ec-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="c90ec-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c90ec-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="c90ec-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c90ec-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c90ec-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c90ec-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="c90ec-118">Scenario description</span></span>
<span data-ttu-id="c90ec-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="c90ec-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c90ec-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="c90ec-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c90ec-121">Ajouter un fusible à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="c90ec-121">Add Fuse from hello gallery</span></span>
2. <span data-ttu-id="c90ec-122">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c90ec-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-fuse-from-hello-gallery"></a><span data-ttu-id="c90ec-123">Ajouter un fusible à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="c90ec-123">Add Fuse from hello gallery</span></span>
<span data-ttu-id="c90ec-124">tooconfigure hello intégration de fusible dans Azure AD, vous devez tooadd fusible à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="c90ec-124">tooconfigure hello integration of Fuse into Azure AD, you need tooadd Fuse from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c90ec-125">**tooadd fusible à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c90ec-125">**tooadd Fuse from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c90ec-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="c90ec-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="c90ec-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="c90ec-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c90ec-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="c90ec-129">Then go too**All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="c90ec-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="c90ec-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="c90ec-133">Dans la zone de recherche de hello, tapez **fusible**, sélectionnez **fusible** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="c90ec-133">In hello search box, type **Fuse**, select **Fuse** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Dans la liste des résultats hello de fusible](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c90ec-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c90ec-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="c90ec-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Fuse, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="c90ec-136">In this section, you configure and test Azure AD single sign-on with Fuse based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c90ec-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello fusible est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c90ec-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Fuse is tooa user in Azure AD.</span></span> <span data-ttu-id="c90ec-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans fusible besoins toobe est établie.</span><span class="sxs-lookup"><span data-stu-id="c90ec-138">In other words, a link relationship between an Azure AD user and hello related user in Fuse needs toobe established.</span></span>

<span data-ttu-id="c90ec-139">Dans fusible, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="c90ec-139">In Fuse, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c90ec-140">tooconfigure et test Azure AD l’authentification unique avec fusible, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="c90ec-140">tooconfigure and test Azure AD single sign-on with Fuse, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c90ec-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="c90ec-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c90ec-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c90ec-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c90ec-143">**[Créer un utilisateur de test fusible](#create-a-fuse-test-user)**  -toohave un équivalent de Britta Simon dans fusible est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c90ec-143">**[Create a Fuse test user](#create-a-fuse-test-user)** - toohave a counterpart of Britta Simon in Fuse that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c90ec-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c90ec-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c90ec-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="c90ec-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="c90ec-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c90ec-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="c90ec-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application fusible.</span><span class="sxs-lookup"><span data-stu-id="c90ec-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Fuse application.</span></span>

<span data-ttu-id="c90ec-148">**tooconfigure Azure AD l’authentification unique avec fusible, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c90ec-148">**tooconfigure Azure AD single sign-on with Fuse, perform hello following steps:**</span></span>

1. <span data-ttu-id="c90ec-149">Bonjour portail Azure, sur hello **fusible** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="c90ec-149">In hello Azure portal, on hello **Fuse** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="c90ec-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c90ec-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_samlbase.png)

3. <span data-ttu-id="c90ec-153">Sur hello **fusible de domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c90ec-153">On hello **Fuse Domain and URLs** section, perform hello following steps:</span></span>

    ![Informations d’authentification unique dans Fuse Domain and URLs (Domaine et URL Fuse)](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_url.png)
    
    <span data-ttu-id="c90ec-155">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<tenant name>.fusion-universal.com/`</span><span class="sxs-lookup"><span data-stu-id="c90ec-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant name>.fusion-universal.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c90ec-156">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="c90ec-156">This value is not real.</span></span> <span data-ttu-id="c90ec-157">Mettre à jour de cette valeur avec hello URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="c90ec-157">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="c90ec-158">Contact [équipe de support Client de fusible](mailto:support@fusion-universal.com) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="c90ec-158">Contact [Fuse Client support team](mailto:support@fusion-universal.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="c90ec-159">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Raw)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="c90ec-159">On hello **SAML Signing Certificate** section, click **Certificate (Raw)** and then save hello certificate file on your computer.</span></span>

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_certificate.png) 

5. <span data-ttu-id="c90ec-161">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="c90ec-161">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-fuse-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c90ec-163">Sur hello **fusible de Configuration** , cliquez sur **configurer fusible** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="c90ec-163">On hello **Fuse Configuration** section, click **Configure Fuse** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c90ec-164">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="c90ec-164">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuration de Fuse](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_configure.png) 

7. <span data-ttu-id="c90ec-166">tooget l’authentification unique configurée pour votre application, contactez [équipe de support fusible](mailto:support@fusion-universal.com) et leur fournir des éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="c90ec-166">tooget SSO configured for your application, contact [Fuse support team](mailto:support@fusion-universal.com) and provide them with hello following:</span></span>

    * <span data-ttu-id="c90ec-167">Hello téléchargé **fichier de certificat (Raw)**</span><span class="sxs-lookup"><span data-stu-id="c90ec-167">hello downloaded **Certificate (Raw) file**</span></span>
    * <span data-ttu-id="c90ec-168">Hello **SAML Sign-On URL du Service unique**</span><span class="sxs-lookup"><span data-stu-id="c90ec-168">hello **SAML Single Sign-On Service URL**</span></span>
    * <span data-ttu-id="c90ec-169">Hello **ID d’entité SAML**</span><span class="sxs-lookup"><span data-stu-id="c90ec-169">hello **SAML Entity ID**</span></span>
    * <span data-ttu-id="c90ec-170">Hello **URL de déconnexion**</span><span class="sxs-lookup"><span data-stu-id="c90ec-170">hello **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="c90ec-171">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="c90ec-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c90ec-172">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="c90ec-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c90ec-173">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c90ec-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c90ec-174">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="c90ec-174">Create an Azure AD test user</span></span>

<span data-ttu-id="c90ec-175">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="c90ec-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="c90ec-177">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c90ec-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c90ec-178">Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.</span><span class="sxs-lookup"><span data-stu-id="c90ec-178">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-fuse-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="c90ec-180">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="c90ec-180">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-fuse-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="c90ec-182">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="c90ec-182">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![bouton Ajouter de Hello](./media/active-directory-saas-fuse-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="c90ec-184">Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c90ec-184">In hello **User** dialog box, perform hello following steps:</span></span>

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-fuse-tutorial/create_aaduser_04.png)

    <span data-ttu-id="c90ec-186">a.</span><span class="sxs-lookup"><span data-stu-id="c90ec-186">a.</span></span> <span data-ttu-id="c90ec-187">Bonjour **nom** , tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c90ec-187">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c90ec-188">b.</span><span class="sxs-lookup"><span data-stu-id="c90ec-188">b.</span></span> <span data-ttu-id="c90ec-189">Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c90ec-189">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="c90ec-190">c.</span><span class="sxs-lookup"><span data-stu-id="c90ec-190">c.</span></span> <span data-ttu-id="c90ec-191">Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.</span><span class="sxs-lookup"><span data-stu-id="c90ec-191">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="c90ec-192">d.</span><span class="sxs-lookup"><span data-stu-id="c90ec-192">d.</span></span> <span data-ttu-id="c90ec-193">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="c90ec-193">Click **Create**.</span></span>
 
### <a name="create-a-fuse-test-user"></a><span data-ttu-id="c90ec-194">Créer un utilisateur de test Fuse</span><span class="sxs-lookup"><span data-stu-id="c90ec-194">Create a Fuse test user</span></span>

<span data-ttu-id="c90ec-195">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Fuse.</span><span class="sxs-lookup"><span data-stu-id="c90ec-195">In this section, you create a user called Britta Simon in Fuse.</span></span> <span data-ttu-id="c90ec-196">Collaborez avec [équipe de support fusible](mailto:support@fusion-universal.com) tooadd les utilisateurs de hello dans la plateforme de fusible hello.</span><span class="sxs-lookup"><span data-stu-id="c90ec-196">Please work with [Fuse support team](mailto:support@fusion-universal.com) tooadd hello users in hello Fuse platform.</span></span>


### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="c90ec-197">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c90ec-197">Assign hello Azure AD test user</span></span>

<span data-ttu-id="c90ec-198">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooFuse.</span><span class="sxs-lookup"><span data-stu-id="c90ec-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFuse.</span></span>

![Attribuer le rôle d’utilisateur hello][200] 

<span data-ttu-id="c90ec-200">**tooassign Britta Simon tooFuse, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c90ec-200">**tooassign Britta Simon tooFuse, perform hello following steps:**</span></span>

1. <span data-ttu-id="c90ec-201">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="c90ec-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="c90ec-203">Dans la liste des applications hello, sélectionnez **fusible**.</span><span class="sxs-lookup"><span data-stu-id="c90ec-203">In hello applications list, select **Fuse**.</span></span>

    ![lien de fusible Hello dans la liste des Applications hello](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_app.png)  

3. <span data-ttu-id="c90ec-205">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="c90ec-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202]

4. <span data-ttu-id="c90ec-207">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="c90ec-207">Click **Add** button.</span></span> <span data-ttu-id="c90ec-208">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="c90ec-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="c90ec-210">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="c90ec-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c90ec-211">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="c90ec-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c90ec-212">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="c90ec-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="c90ec-213">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="c90ec-213">Test single sign-on</span></span>

<span data-ttu-id="c90ec-214">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="c90ec-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c90ec-215">Lorsque vous cliquez sur mosaïque fusible hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour fusible application.</span><span class="sxs-lookup"><span data-stu-id="c90ec-215">When you click hello Fuse tile in hello Access Panel, you should get automatically signed-on tooyour Fuse application.</span></span>
<span data-ttu-id="c90ec-216">Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c90ec-216">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c90ec-217">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="c90ec-217">Additional resources</span></span>

* [<span data-ttu-id="c90ec-218">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c90ec-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c90ec-219">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="c90ec-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_203.png

