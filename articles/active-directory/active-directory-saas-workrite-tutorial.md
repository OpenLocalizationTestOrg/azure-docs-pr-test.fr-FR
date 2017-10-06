---
title: "Didacticiel : intégration d’Azure Active Directory à Workrite | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Workrite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 2a5c2956-a011-4d5c-877b-80679b6587b5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: a663374ae3c8b102b53d8cf05a9cb083b80dbb83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workrite"></a><span data-ttu-id="35794-103">Didacticiel : intégration d’Azure Active Directory à Workrite</span><span class="sxs-lookup"><span data-stu-id="35794-103">Tutorial: Azure Active Directory integration with Workrite</span></span>

<span data-ttu-id="35794-104">Dans ce didacticiel, vous apprendrez comment toointegrate Workrite avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="35794-104">In this tutorial, you learn how toointegrate Workrite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="35794-105">Intégration Workrite à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="35794-105">Integrating Workrite with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="35794-106">Vous pouvez contrôler dans Azure AD qui a accès tooWorkrite.</span><span class="sxs-lookup"><span data-stu-id="35794-106">You can control in Azure AD who has access tooWorkrite.</span></span>
- <span data-ttu-id="35794-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooWorkrite (Single Sign-On) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="35794-107">You can enable your users tooautomatically get signed-on tooWorkrite (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="35794-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="35794-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="35794-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="35794-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="35794-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="35794-110">Prerequisites</span></span>

<span data-ttu-id="35794-111">tooconfigure intégration d’Azure AD avec Workrite, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="35794-111">tooconfigure Azure AD integration with Workrite, you need hello following items:</span></span>

- <span data-ttu-id="35794-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="35794-112">An Azure AD subscription</span></span>
- <span data-ttu-id="35794-113">Un abonnement Workrite pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="35794-113">A Workrite single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="35794-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="35794-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="35794-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="35794-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="35794-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="35794-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="35794-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="35794-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="35794-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="35794-118">Scenario description</span></span>
<span data-ttu-id="35794-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="35794-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="35794-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="35794-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="35794-121">Ajout de Workrite à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="35794-121">Adding Workrite from hello gallery</span></span>
2. <span data-ttu-id="35794-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="35794-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workrite-from-hello-gallery"></a><span data-ttu-id="35794-123">Ajout de Workrite à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="35794-123">Adding Workrite from hello gallery</span></span>
<span data-ttu-id="35794-124">intégration de hello tooconfigure de Workrite dans Azure AD, vous devez tooadd Workrite à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="35794-124">tooconfigure hello integration of Workrite into Azure AD, you need tooadd Workrite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="35794-125">**tooadd Workrite à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="35794-125">**tooadd Workrite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="35794-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="35794-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="35794-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="35794-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="35794-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="35794-129">Then go too**All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="35794-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="35794-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="35794-133">Dans la zone de recherche de hello, tapez **Workrite**, sélectionnez **Workrite** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="35794-133">In hello search box, type **Workrite**, select **Workrite** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Workrite dans la liste des résultats hello](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="35794-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="35794-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="35794-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Workrite, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="35794-136">In this section, you configure and test Azure AD single sign-on with Workrite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="35794-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Workrite est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="35794-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workrite is tooa user in Azure AD.</span></span> <span data-ttu-id="35794-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Workrite doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="35794-138">In other words, a link relationship between an Azure AD user and hello related user in Workrite needs toobe established.</span></span>

<span data-ttu-id="35794-139">Dans Workrite, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="35794-139">In Workrite, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="35794-140">tooconfigure et test Azure AD l’authentification unique avec Workrite, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="35794-140">tooconfigure and test Azure AD single sign-on with Workrite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="35794-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="35794-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="35794-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="35794-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="35794-143">**[Créer un utilisateur de test Workrite](#create-a-workrite-test-user)**  -toohave un équivalent de Britta Simon dans Workrite est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="35794-143">**[Create a Workrite test user](#create-a-workrite-test-user)** - toohave a counterpart of Britta Simon in Workrite that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="35794-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="35794-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="35794-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="35794-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="35794-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="35794-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="35794-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Workrite.</span><span class="sxs-lookup"><span data-stu-id="35794-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workrite application.</span></span>

<span data-ttu-id="35794-148">**tooconfigure Azure AD single sign-on avec Workrite, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="35794-148">**tooconfigure Azure AD single sign-on with Workrite, perform hello following steps:**</span></span>

1. <span data-ttu-id="35794-149">Bonjour portail Azure, sur hello **Workrite** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="35794-149">In hello Azure portal, on hello **Workrite** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="35794-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="35794-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_samlbase.png)

3. <span data-ttu-id="35794-153">Sur hello **Workrite domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="35794-153">On hello **Workrite Domain and URLs** section, perform hello following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL Workrite](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_url.png)

    <span data-ttu-id="35794-155">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://app.workrite.co.uk/securelogin/samlgateway.aspx?id=<uniqueid>`</span><span class="sxs-lookup"><span data-stu-id="35794-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://app.workrite.co.uk/securelogin/samlgateway.aspx?id=<uniqueid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="35794-156">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="35794-156">This value is not real.</span></span> <span data-ttu-id="35794-157">Mettre à jour de cette valeur avec hello URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="35794-157">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="35794-158">Contact [équipe de support Client de Workrite](mailto:support@workrite.co.uk) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="35794-158">Contact [Workrite Client support team](mailto:support@workrite.co.uk) tooget this value.</span></span>

4. <span data-ttu-id="35794-159">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="35794-159">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_certificate.png) 

5. <span data-ttu-id="35794-161">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="35794-161">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-workrite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="35794-163">Sur hello **Workrite Configuration** , cliquez sur **Workrite de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="35794-163">On hello **Workrite Configuration** section, click **Configure Workrite** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="35794-164">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="35794-164">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuration de Workrite](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_configure.png) 

7. <span data-ttu-id="35794-166">tooconfigure l’authentification unique sur **Workrite** côté, vous devez hello toosend téléchargé **Certificate(Base64), l’URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** trop[Workrite l’équipe de support](mailto:support@workrite.co.uk).</span><span class="sxs-lookup"><span data-stu-id="35794-166">tooconfigure single sign-on on **Workrite** side, you need toosend hello downloaded **Certificate(Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Workrite support team](mailto:support@workrite.co.uk).</span></span>

> [!TIP]
> <span data-ttu-id="35794-167">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="35794-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="35794-168">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="35794-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="35794-169">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="35794-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="35794-170">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="35794-170">Create an Azure AD test user</span></span>

<span data-ttu-id="35794-171">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="35794-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="35794-173">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="35794-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="35794-174">Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.</span><span class="sxs-lookup"><span data-stu-id="35794-174">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-workrite-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="35794-176">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="35794-176">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-workrite-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="35794-178">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="35794-178">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![bouton Ajouter de Hello](./media/active-directory-saas-workrite-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="35794-180">Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="35794-180">In hello **User** dialog box, perform hello following steps:</span></span>

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-workrite-tutorial/create_aaduser_04.png)

    <span data-ttu-id="35794-182">a.</span><span class="sxs-lookup"><span data-stu-id="35794-182">a.</span></span> <span data-ttu-id="35794-183">Bonjour **nom** , tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="35794-183">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="35794-184">b.</span><span class="sxs-lookup"><span data-stu-id="35794-184">b.</span></span> <span data-ttu-id="35794-185">Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="35794-185">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="35794-186">c.</span><span class="sxs-lookup"><span data-stu-id="35794-186">c.</span></span> <span data-ttu-id="35794-187">Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.</span><span class="sxs-lookup"><span data-stu-id="35794-187">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="35794-188">d.</span><span class="sxs-lookup"><span data-stu-id="35794-188">d.</span></span> <span data-ttu-id="35794-189">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="35794-189">Click **Create**.</span></span>
 
### <a name="create-a-workrite-test-user"></a><span data-ttu-id="35794-190">Créer un utilisateur de test Workrite</span><span class="sxs-lookup"><span data-stu-id="35794-190">Create a Workrite test user</span></span>

<span data-ttu-id="35794-191">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans Workrite.</span><span class="sxs-lookup"><span data-stu-id="35794-191">hello objective of this section is toocreate a user called Britta Simon in Workrite.</span></span>

<span data-ttu-id="35794-192">**toocreate un utilisateur appelé Britta Simon dans Workrite, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="35794-192">**toocreate a user called Britta Simon in Workrite, perform hello following steps:**</span></span>

1. <span data-ttu-id="35794-193">Connectez-vous sur le site d’entreprise tooyour workrite tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="35794-193">Sign on tooyour workrite company site as administrator.</span></span>

2. <span data-ttu-id="35794-194">Dans le volet de navigation hello, cliquez sur **Admin**.</span><span class="sxs-lookup"><span data-stu-id="35794-194">In hello navigation pane, click **Admin**.</span></span>
   
    ![Contrôle d’administration][400]

3. <span data-ttu-id="35794-196">Consultez les liens tooQuick, puis cliquez sur **créer un utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="35794-196">Go tooQuick Links, and then click **Create a User**.</span></span>
   
    ![Section Create User][401]

4. <span data-ttu-id="35794-198">Sur hello **Create User** boîte de dialogue, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="35794-198">On hello **Create User** dialog, perform hello following steps:</span></span>
   
    ![Boîte de dialogue Create User][402]
    
    <span data-ttu-id="35794-200">a.</span><span class="sxs-lookup"><span data-stu-id="35794-200">a.</span></span> <span data-ttu-id="35794-201">Bonjour **messagerie** adresse de messagerie de type hello d’utilisateur de zone de texte, comme Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="35794-201">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="35794-202">b.</span><span class="sxs-lookup"><span data-stu-id="35794-202">b.</span></span> <span data-ttu-id="35794-203">Bonjour **prénom** firstname hello de type d’utilisateur comme Brian zone de texte.</span><span class="sxs-lookup"><span data-stu-id="35794-203">In hello **First Name** textbox, type hello firstname of user like Britta.</span></span>

    <span data-ttu-id="35794-204">c.</span><span class="sxs-lookup"><span data-stu-id="35794-204">c.</span></span> <span data-ttu-id="35794-205">Bonjour **Surname** zone de texte, nom de famille type hello d’utilisateur comme Simon.</span><span class="sxs-lookup"><span data-stu-id="35794-205">In hello **Surname** textbox, type hello surname of user like Simon.</span></span>
    
    <span data-ttu-id="35794-206">d.</span><span class="sxs-lookup"><span data-stu-id="35794-206">d.</span></span> <span data-ttu-id="35794-207">Sélectionnez **Client Administrator** pour **Choose Role**.</span><span class="sxs-lookup"><span data-stu-id="35794-207">Select **Client Administrator** as **Choose Role**.</span></span>
    
    <span data-ttu-id="35794-208">e.</span><span class="sxs-lookup"><span data-stu-id="35794-208">e.</span></span> <span data-ttu-id="35794-209">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="35794-209">Click **Save**.</span></span>   

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="35794-210">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="35794-210">Assign hello Azure AD test user</span></span>

<span data-ttu-id="35794-211">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooWorkrite.</span><span class="sxs-lookup"><span data-stu-id="35794-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkrite.</span></span>

![Attribuer le rôle d’utilisateur hello][200] 

<span data-ttu-id="35794-213">**tooassign Britta Simon tooWorkrite, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="35794-213">**tooassign Britta Simon tooWorkrite, perform hello following steps:**</span></span>

1. <span data-ttu-id="35794-214">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="35794-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="35794-216">Dans la liste des applications hello, sélectionnez **Workrite**.</span><span class="sxs-lookup"><span data-stu-id="35794-216">In hello applications list, select **Workrite**.</span></span>

    ![lien de Workrite Hello dans la liste des Applications hello](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_app.png)  

3. <span data-ttu-id="35794-218">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="35794-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202]

4. <span data-ttu-id="35794-220">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="35794-220">Click **Add** button.</span></span> <span data-ttu-id="35794-221">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="35794-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="35794-223">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="35794-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="35794-224">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="35794-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="35794-225">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="35794-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="35794-226">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="35794-226">Test single sign-on</span></span>

<span data-ttu-id="35794-227">objectif Hello de cette section est tootest votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="35794-227">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="35794-228">Lorsque vous cliquez sur mosaïque Workrite hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Workrite application.</span><span class="sxs-lookup"><span data-stu-id="35794-228">When you click hello Workrite tile in hello Access Panel, you should get automatically signed-on tooyour Workrite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="35794-229">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="35794-229">Additional resources</span></span>

* [<span data-ttu-id="35794-230">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="35794-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="35794-231">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="35794-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_203.png
[400]: ./media/active-directory-saas-workrite-tutorial/tutorial_workrite_400.png
[401]: ./media/active-directory-saas-workrite-tutorial/tutorial_workrite_401.png
[402]: ./media/active-directory-saas-workrite-tutorial/tutorial_workrite_402.png

