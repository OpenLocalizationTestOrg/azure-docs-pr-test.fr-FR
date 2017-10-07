---
title: "Didacticiel : Intégration d’Azure Active Directory à Help Scout | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Scout d’aide."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0aad9910-0bc1-4394-9f73-267cf39973ab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: jeedes
ms.openlocfilehash: 58edd140eb1eb5980796ca743b5f7acd891729a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-help-scout"></a><span data-ttu-id="1509b-103">Didacticiel : Intégration d’Azure Active Directory à Help Scout</span><span class="sxs-lookup"><span data-stu-id="1509b-103">Tutorial: Azure Active Directory integration with Help Scout</span></span>

<span data-ttu-id="1509b-104">Dans ce didacticiel, vous découvrez comment toointegrate aider conseiller avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1509b-104">In this tutorial, you learn how toointegrate Help Scout with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1509b-105">Vous obtenez hello avantages suivants à partir de l’intégration Scout d’aider à Azure AD :</span><span class="sxs-lookup"><span data-stu-id="1509b-105">You get hello following benefits from integrating Help Scout with Azure AD:</span></span>

- <span data-ttu-id="1509b-106">Dans Azure AD, vous pouvez contrôler qui a accès tooHelp Scout.</span><span class="sxs-lookup"><span data-stu-id="1509b-106">In Azure AD, you can control who has access tooHelp Scout.</span></span>
- <span data-ttu-id="1509b-107">Vous pouvez signer automatiquement dans votre tooHelp utilisateurs Scout à l’aide de l’authentification unique et un compte d’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1509b-107">You can automatically sign in your users tooHelp Scout by using single sign-on and a user's Azure AD account.</span></span>
- <span data-ttu-id="1509b-108">Vous pouvez gérer vos comptes dans un emplacement central, hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1509b-108">You can manage your accounts in one, central location, hello Azure portal.</span></span>

<span data-ttu-id="1509b-109">toolearn savoir plus sur le logiciel en tant qu’une intégration d’application de service (SaaS) avec Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1509b-109">toolearn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1509b-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1509b-110">Prerequisites</span></span>

<span data-ttu-id="1509b-111">tooset d’intégration d’Azure AD avec Scout d’aide, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="1509b-111">tooset up Azure AD integration with Help Scout, you need hello following items:</span></span>

- <span data-ttu-id="1509b-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="1509b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1509b-113">Un abonnement Help Scout, avec authentification unique activée</span><span class="sxs-lookup"><span data-stu-id="1509b-113">A Help Scout subscription, with single sign-on turned on</span></span> 

> [!NOTE]
> <span data-ttu-id="1509b-114">Si vous testez les étapes hello dans ce didacticiel, nous vous recommandons de ne pas les tester dans un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="1509b-114">If you test hello steps in this tutorial, we recommend that you don't test them in a production environment.</span></span>

<span data-ttu-id="1509b-115">Recommandations pour le test des étapes de hello dans ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="1509b-115">Recommendations for testing hello steps in this tutorial:</span></span>

- <span data-ttu-id="1509b-116">N’utilisez pas votre environnement de production, à moins que cela ne soit nécessaire.</span><span class="sxs-lookup"><span data-stu-id="1509b-116">Do not use your production environment, unless it's necessary.</span></span>
- <span data-ttu-id="1509b-117">Si vous ne disposez pas d’un environnement d’essai Azure AD, vous pouvez [obtenir un essai gratuit d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1509b-117">If you don't have an Azure AD trial environment, you can [get a one-month free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1509b-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="1509b-118">Scenario description</span></span>
<span data-ttu-id="1509b-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="1509b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="1509b-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="1509b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1509b-121">Ajouter Scout d’aide à partir de la galerie de hello.</span><span class="sxs-lookup"><span data-stu-id="1509b-121">Add Help Scout from hello gallery.</span></span>
2. <span data-ttu-id="1509b-122">Configurez et testez l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1509b-122">Set up and test Azure AD single sign-on.</span></span>

## <a name="add-help-scout-from-hello-gallery"></a><span data-ttu-id="1509b-123">Ajouter Scout d’aide à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="1509b-123">Add Help Scout from hello gallery</span></span>
<span data-ttu-id="1509b-124">tooset intégration hello d’aider les Scout avec Azure AD, dans la galerie hello, ajoutez la liste de tooyour de Scout d’aide des applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="1509b-124">tooset up hello integration of Help Scout with Azure AD, in hello gallery, add Help Scout tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1509b-125">tooadd Scout d’aide à partir de la galerie de hello :</span><span class="sxs-lookup"><span data-stu-id="1509b-125">tooadd Help Scout from hello gallery:</span></span>

1. <span data-ttu-id="1509b-126">Bonjour [portail Azure](https://portal.azure.com)hello du menu de gauche, dans Sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1509b-126">In hello [Azure portal](https://portal.azure.com), in hello left menu, select **Azure Active Directory**.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="1509b-128">Sélectionnez **Applications d’entreprise**, puis **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1509b-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![page des applications Enterprise Hello][2]
    
3. <span data-ttu-id="1509b-130">tooadd une nouvelle application, sélectionnez **nouvelle application**.</span><span class="sxs-lookup"><span data-stu-id="1509b-130">tooadd a new application, select **New application**.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="1509b-132">Dans la zone de recherche de hello, entrez **Scout d’aide**.</span><span class="sxs-lookup"><span data-stu-id="1509b-132">In hello search box, enter **Help Scout**.</span></span> <span data-ttu-id="1509b-133">Dans les résultats de recherche de hello, sélectionnez **Scout d’aide**, puis sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="1509b-133">In hello search results, select **Help Scout**, and then select **Add**.</span></span>

    ![Aide Scout dans la liste des résultats hello](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_addfromgallery.png)

## <a name="set-up-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="1509b-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1509b-135">Set up and test Azure AD single sign-on</span></span>

<span data-ttu-id="1509b-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Help Scout pour un utilisateur de test nommé *Britta Simon*.</span><span class="sxs-lookup"><span data-stu-id="1509b-136">In this section, you set up and test Azure AD single sign-on with Help Scout based on a test user named *Britta Simon*.</span></span>

<span data-ttu-id="1509b-137">Pour toowork de l’authentification unique, Azure AD doit utilisateur tooknow hello Azure AD équivalent Scout d’aide.</span><span class="sxs-lookup"><span data-stu-id="1509b-137">For single sign-on toowork, Azure AD needs tooknow hello Azure AD counterpart user in Help Scout.</span></span> <span data-ttu-id="1509b-138">Une relation de lien entre un utilisateur Azure AD et un utilisateur dans l’aide de Scout hello doit être établie.</span><span class="sxs-lookup"><span data-stu-id="1509b-138">A link relationship between an Azure AD user and hello related user in Help Scout must be established.</span></span>

<span data-ttu-id="1509b-139">relation, dans l’aide Scout, de liens tooestablish hello pour **nom d’utilisateur**, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1509b-139">tooestablish hello link relationship, in Help Scout, for **Username**, assign hello value of hello **user name** in Azure AD.</span></span>

<span data-ttu-id="1509b-140">tooconfigure et test Azure AD l’authentification unique avec aide Scout, hello complète tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="1509b-140">tooconfigure and test Azure AD single sign-on with Help Scout, complete hello following tasks:</span></span>

1. <span data-ttu-id="1509b-141">[Configurer l’authentification unique Azure AD](#set-up-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="1509b-141">[Set up Azure AD single sign-on](#set-up-azure-ad-single-sign-on).</span></span> <span data-ttu-id="1509b-142">Définit un toouse utilisateur cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="1509b-142">Sets up a user toouse this feature.</span></span>
2. <span data-ttu-id="1509b-143">[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="1509b-143">[Create an Azure AD test user](#create-an-azure-ad-test-user).</span></span> <span data-ttu-id="1509b-144">Tests AD Azure authentification unique avec l’utilisateur hello Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1509b-144">Tests Azure AD single sign-on with hello user Britta Simon.</span></span>
3. <span data-ttu-id="1509b-145">[Créer un utilisateur de test Help Scout](#create-a-help-scout-test-user).</span><span class="sxs-lookup"><span data-stu-id="1509b-145">[Create a Help Scout test user](#create-a-help-scout-test-user).</span></span> <span data-ttu-id="1509b-146">Crée un équivalent de Britta Simon Scout aide qui est lié toohello la représentation sous forme de Azure AD de l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="1509b-146">Creates a counterpart of Britta Simon in Help Scout that is linked toohello Azure AD representation of hello user.</span></span>
4. <span data-ttu-id="1509b-147">[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="1509b-147">[Assign hello Azure AD test user](#assign-the-azure-ad-test-user).</span></span> <span data-ttu-id="1509b-148">Définit les toouse Britta Simon Azure AD l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="1509b-148">Sets up Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1509b-149">[Tester l’authentification unique](#test-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="1509b-149">[Test single sign-on](#test-single-sign-on).</span></span> <span data-ttu-id="1509b-150">Vérifie que la configuration hello fonctionne.</span><span class="sxs-lookup"><span data-stu-id="1509b-150">Verifies that hello configuration works.</span></span>

### <a name="set-up-azure-ad-single-sign-on"></a><span data-ttu-id="1509b-151">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1509b-151">Set up Azure AD single sign-on</span></span>

<span data-ttu-id="1509b-152">Dans cette section, vous configurer Azure AD l’authentification unique sur Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1509b-152">In this section, you set up Azure AD single sign-on in hello Azure portal.</span></span> <span data-ttu-id="1509b-153">Ensuite, vous configurerez l’authentification unique dans votre application Help Scout.</span><span class="sxs-lookup"><span data-stu-id="1509b-153">Then, you set up single sign-on in your Help Scout application.</span></span>

<span data-ttu-id="1509b-154">tooset d’Azure AD single sign-on avec Scout d’aide :</span><span class="sxs-lookup"><span data-stu-id="1509b-154">tooset up Azure AD single sign-on with Help Scout:</span></span>

1. <span data-ttu-id="1509b-155">Bonjour portail Azure, sur hello **Scout d’aide** page d’intégration d’application, sélectionnez **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="1509b-155">In hello Azure portal, on hello **Help Scout** application integration page, select **Single sign-on**.</span></span>
 
    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="1509b-157">Sur hello **l’authentification unique** page, pour **Mode**, sélectionnez **SAML-authentification**.</span><span class="sxs-lookup"><span data-stu-id="1509b-157">On hello **Single sign-on** page, for **Mode**, select **SAML-based Sign-on**.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_samlbase.png)

3. <span data-ttu-id="1509b-159">Sous **URL et aider à un domaine Scout**, si vous souhaitez tooset des application hello en mode initié par IDP, hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="1509b-159">Under **Help Scout Domain and URLs**, if you want tooset up hello application in IDP-initiated mode, complete hello following steps:</span></span>

    1. <span data-ttu-id="1509b-160">Bonjour **identificateur** , entrez une URL qui pointe hello modèle :`urn:auth0:helpscout:<instancename>`</span><span class="sxs-lookup"><span data-stu-id="1509b-160">In hello **Identifier** box, enter a URL that has hello following pattern: `urn:auth0:helpscout:<instancename>`</span></span>

    2. <span data-ttu-id="1509b-161">Bonjour **URL de réponse** , entrez une URL qui pointe hello modèle :`https://helpscout.auth0.com/login/callback?connection=<instancename>`</span><span class="sxs-lookup"><span data-stu-id="1509b-161">In hello **Reply URL** box, enter a URL that has hello following pattern: `https://helpscout.auth0.com/login/callback?connection=<instancename>`</span></span>

    ![Informations d’authentification unique dans Domaine et URL Help Scout](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url.png)

4. <span data-ttu-id="1509b-163">Si vous souhaitez tooset des application hello en mode initié par le Service Pack, sélectionnez hello **afficher les paramètres d’URL avancés** case à cocher, puis hello suivant :</span><span class="sxs-lookup"><span data-stu-id="1509b-163">If you want tooset up hello application in SP-initiated mode, select hello **Show advanced URL settings** check box, and then do hello following:</span></span>

    * <span data-ttu-id="1509b-164">Bonjour **URL de connexion** , entrez une URL qui pointe hello suivant le format :`https://secure.helpscout.net/members/login/`</span><span class="sxs-lookup"><span data-stu-id="1509b-164">In hello **Sign on URL** box, enter a URL that has hello following format: `https://secure.helpscout.net/members/login/`</span></span>

    ![Informations d’authentification unique dans Domaine et URL Help Scout](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url1.png)
 
    > [!NOTE] 
    > <span data-ttu-id="1509b-166">les valeurs Hello dans ces URL sont fins de démonstration uniquement.</span><span class="sxs-lookup"><span data-stu-id="1509b-166">hello values in these URLs are for demonstration only.</span></span> <span data-ttu-id="1509b-167">Mettre à jour les valeurs hello avec hello identificateur réel URL et l’URL de réponse.</span><span class="sxs-lookup"><span data-stu-id="1509b-167">Update hello values with hello actual identifier URL and reply URL.</span></span> <span data-ttu-id="1509b-168">Ces valeurs, contactez le tooget [équipe de support Scout d’aide](mailto:help@helpscout.com).</span><span class="sxs-lookup"><span data-stu-id="1509b-168">tooget these values, contact [Help Scout support team](mailto:help@helpscout.com).</span></span> 

5. <span data-ttu-id="1509b-169">Sous **le certificat de signature SAML**, sélectionnez **Metadata XML**, puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="1509b-169">Under **SAML Signing Certificate**, select **Metadata XML**, and then save hello metadata file on your computer.</span></span>

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_certificate.png) 

6. <span data-ttu-id="1509b-171">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="1509b-171">Select **Save**.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-helpscout-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="1509b-173">tooset des unique authentification côté de hello Scout d’aide, envoyez hello téléchargé métadonnées XML fichier toohello [équipe de support Scout d’aide](mailto:help@helpscout.com).</span><span class="sxs-lookup"><span data-stu-id="1509b-173">tooset up single sign-on on hello Help Scout side, send hello downloaded metadata XML file toohello [Help Scout support team](mailto:help@helpscout.com).</span></span> <span data-ttu-id="1509b-174">équipe de support Hello Scout d’aide applique ce paramètre afin que hello SAML session connexion unique est correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="1509b-174">hello Help Scout support team applies this setting so that hello SAML single sign-on connection is set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="1509b-175">Vous pouvez lire une version concise de ces instructions Bonjour [portail Azure](https://portal.azure.com), alors que vous configurez votre application !</span><span class="sxs-lookup"><span data-stu-id="1509b-175">You can read a concise version of these instructions in hello [Azure portal](https://portal.azure.com), while you are setting up your app!</span></span> <span data-ttu-id="1509b-176">Après avoir ajouté l’application hello en sélectionnant **Active Directory** > **des Applications d’entreprise**, sélectionnez hello **Single Sign-On** onglet. Vous pouvez accéder à documentation hello incorporé Bonjour **Configuration** section, au bas de hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="1509b-176">After you add hello app by selecting **Active Directory** > **Enterprise Applications**, select hello **Single Sign-On** tab. You can access hello embedded documentation in hello **Configuration** section, at hello bottom of hello page.</span></span> <span data-ttu-id="1509b-177">Pour plus d’informations, consultez la page [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="1509b-177">For more information, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="1509b-178">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="1509b-178">Create an Azure AD test user</span></span>

<span data-ttu-id="1509b-179">Dans cette section, Bonjour portail Azure, vous créez un utilisateur de test nommé Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1509b-179">In this section, in hello Azure portal, you create a test user named Britta Simon.</span></span>

![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="1509b-181">toocreate un utilisateur test dans Azure AD :</span><span class="sxs-lookup"><span data-stu-id="1509b-181">toocreate a test user in Azure AD:</span></span>

1. <span data-ttu-id="1509b-182">Bonjour portail Azure, dans le menu de gauche hello, sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1509b-182">In hello Azure portal, in hello left menu, select **Azure Active Directory**.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-helpscout-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="1509b-184">liste de hello toodisplay d’utilisateurs, sélectionnez **utilisateurs et groupes**, puis sélectionnez **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="1509b-184">toodisplay hello list of users, select **Users and groups**, and then select **All users**.</span></span>

    ![Sélectionnez Utilisateurs et groupes, puis Tous les utilisateurs.](./media/active-directory-saas-helpscout-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="1509b-186">tooopen hello **utilisateur** boîte de dialogue, en haut de hello Hello **tous les utilisateurs** page, sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="1509b-186">tooopen hello **User** dialog box, at hello top of hello **All Users** page, select **Add**.</span></span>

    ![bouton Ajouter de Hello](./media/active-directory-saas-helpscout-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="1509b-188">Bonjour **utilisateur** boîte de dialogue, hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="1509b-188">In hello **User** dialog box, complete hello following steps:</span></span>

    1. <span data-ttu-id="1509b-189">Bonjour **nom** , entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1509b-189">In hello **Name** box, enter **BrittaSimon**.</span></span>

    2. <span data-ttu-id="1509b-190">Bonjour **nom d’utilisateur** , entrez l’adresse de messagerie hello d’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1509b-190">In hello **User name** box, enter hello email address of user Britta Simon.</span></span>

    3. <span data-ttu-id="1509b-191">Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.</span><span class="sxs-lookup"><span data-stu-id="1509b-191">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    4. <span data-ttu-id="1509b-192">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="1509b-192">Select **Create**.</span></span>

        ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-helpscout-tutorial/create_aaduser_04.png)

 
### <a name="create-a-help-scout-test-user"></a><span data-ttu-id="1509b-194">Créer un utilisateur de test Help Scout</span><span class="sxs-lookup"><span data-stu-id="1509b-194">Create a Help Scout test user</span></span>

<span data-ttu-id="1509b-195">objet Hello de cette section est toocreate un utilisateur nommé Britta Simon dans Scout d’aide.</span><span class="sxs-lookup"><span data-stu-id="1509b-195">hello object of this section is toocreate a user named Britta Simon in Help Scout.</span></span> <span data-ttu-id="1509b-196">Help Scout prend en charge l’approvisionnement juste-à-temps (JIT), activé par défaut.</span><span class="sxs-lookup"><span data-stu-id="1509b-196">Help Scout supports just-in-time (JIT) provisioning, which is turned on by default.</span></span>

<span data-ttu-id="1509b-197">Dans cette section, il n’existe aucun toocomplete action ou une tâche.</span><span class="sxs-lookup"><span data-stu-id="1509b-197">In this section, there's no action or task toocomplete.</span></span> <span data-ttu-id="1509b-198">Si un utilisateur n’existe pas déjà dans l’aide de Scout, un nouveau est créé lorsque vous essayez de tooaccess Scout d’aide.</span><span class="sxs-lookup"><span data-stu-id="1509b-198">If a user doesn't already exist in Help Scout, a new one is created when you attempt tooaccess Help Scout.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="1509b-199">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="1509b-199">Assign hello Azure AD test user</span></span>

<span data-ttu-id="1509b-200">Dans cette section, vous permettre à l’utilisateur hello Britta Simon toouse Azure AD l’authentification unique en accordant hello utilisateur compte accès tooHelp Scout.</span><span class="sxs-lookup"><span data-stu-id="1509b-200">In this section, you allow hello user Britta Simon toouse Azure AD single sign-on by granting hello user account access tooHelp Scout.</span></span>

![Attribuer le rôle d’utilisateur hello][200] 

<span data-ttu-id="1509b-202">tooassign Britta Simon tooHelp Scout :</span><span class="sxs-lookup"><span data-stu-id="1509b-202">tooassign Britta Simon tooHelp Scout:</span></span>

1. <span data-ttu-id="1509b-203">Bonjour portail Azure, ouvrez la vue des applications hello et passez toohello vue d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="1509b-203">In hello Azure portal, open hello applications view, and then go toohello directory view.</span></span> <span data-ttu-id="1509b-204">Sélectionnez **Applications d’entreprise**, puis **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1509b-204">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="1509b-206">Dans la liste des applications hello, sélectionnez **Scout d’aide**.</span><span class="sxs-lookup"><span data-stu-id="1509b-206">In hello applications list, select **Help Scout**.</span></span>

    ![lien d’aide les Scout Hello dans la liste des Applications hello](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_app.png)  

3. <span data-ttu-id="1509b-208">Dans le menu de gauche hello, sélectionnez **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1509b-208">In hello left menu, select **Users and groups**.</span></span>

    ![Hello les utilisateurs et groupes lien][202]

4. <span data-ttu-id="1509b-210">Sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="1509b-210">Select **Add**.</span></span> <span data-ttu-id="1509b-211">Ensuite, sous hello **ajouter l’affectation** page, sélectionnez **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1509b-211">Then, on hello **Add Assignment** page, select **Users and groups**.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="1509b-213">Sur hello **utilisateurs et groupes** page, dans la liste de hello des utilisateurs, sélectionnez **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="1509b-213">On hello **Users and groups** page, in hello list of users, select **Britta Simon**.</span></span>

6. <span data-ttu-id="1509b-214">Sur hello **utilisateurs et groupes** page, sélectionnez **sélectionnez**.</span><span class="sxs-lookup"><span data-stu-id="1509b-214">On hello **Users and groups** page, select **Select**.</span></span>

7. <span data-ttu-id="1509b-215">Sur hello **ajouter l’affectation** page, sélectionnez **affecter**.</span><span class="sxs-lookup"><span data-stu-id="1509b-215">On hello **Add Assignment** page, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="1509b-216">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="1509b-216">Test single sign-on</span></span>

<span data-ttu-id="1509b-217">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide du volet d’accès hello.</span><span class="sxs-lookup"><span data-stu-id="1509b-217">In this section, you test your Azure AD single sign-on configuration by using hello access panel.</span></span>

<span data-ttu-id="1509b-218">Lorsque vous sélectionnez la vignette d’aider les Scout hello hello panneau d’accès, vous devez être connecté automatiquement dans tooyour application de Scout d’aide.</span><span class="sxs-lookup"><span data-stu-id="1509b-218">When you select hello Help Scout tile in hello access panel, you should be automatically signed in tooyour Help Scout application.</span></span>

<span data-ttu-id="1509b-219">Pour plus d’informations sur le volet d’accès, consultez [volet d’accès toohello Introduction](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1509b-219">For more information about the access panel, see [Introduction toohello access panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1509b-220">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="1509b-220">Additional resources</span></span>

* [<span data-ttu-id="1509b-221">Liste des didacticiels sur la façon de toointegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1509b-221">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1509b-222">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="1509b-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_203.png

