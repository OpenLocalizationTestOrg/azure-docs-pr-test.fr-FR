---
title: "Didacticiel : Intégration d’Azure Active Directory avec Envoy | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et d’envoi."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 71f7afcc-1033-4098-9b7e-4f9f2b26f734
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: 93add7c1f3cf1fc163acc505f11e34bd696c571c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-envoy"></a><span data-ttu-id="b59b7-103">Didacticiel : Intégration d’Azure Active Directory avec Envoy</span><span class="sxs-lookup"><span data-stu-id="b59b7-103">Tutorial: Azure Active Directory integration with Envoy</span></span>

<span data-ttu-id="b59b7-104">Dans ce didacticiel, vous apprendrez comment toointegrate Envoy avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b59b7-104">In this tutorial, you learn how toointegrate Envoy with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b59b7-105">Intégration Envoy à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="b59b7-105">Integrating Envoy with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b59b7-106">Vous pouvez contrôler dans Azure AD qui a accès tooEnvoy.</span><span class="sxs-lookup"><span data-stu-id="b59b7-106">You can control in Azure AD who has access tooEnvoy.</span></span>
- <span data-ttu-id="b59b7-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooEnvoy (Single Sign-On) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b59b7-107">You can enable your users tooautomatically get signed-on tooEnvoy (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="b59b7-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="b59b7-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="b59b7-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b59b7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b59b7-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b59b7-110">Prerequisites</span></span>

<span data-ttu-id="b59b7-111">tooconfigure intégration d’Azure AD à Envoy, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="b59b7-111">tooconfigure Azure AD integration with Envoy, you need hello following items:</span></span>

- <span data-ttu-id="b59b7-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="b59b7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b59b7-113">Un abonnement Envoy pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="b59b7-113">An Envoy single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b59b7-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="b59b7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b59b7-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="b59b7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b59b7-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="b59b7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b59b7-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b59b7-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b59b7-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="b59b7-118">Scenario description</span></span>
<span data-ttu-id="b59b7-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="b59b7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b59b7-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="b59b7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b59b7-121">Ajout d’envoi à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="b59b7-121">Adding Envoy from hello gallery</span></span>
2. <span data-ttu-id="b59b7-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b59b7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-envoy-from-hello-gallery"></a><span data-ttu-id="b59b7-123">Ajout d’envoi à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="b59b7-123">Adding Envoy from hello gallery</span></span>
<span data-ttu-id="b59b7-124">tooconfigure hello intégration de Envoy dans Azure AD, vous devez tooadd Envoy à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="b59b7-124">tooconfigure hello integration of Envoy into Azure AD, you need tooadd Envoy from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b59b7-125">**tooadd Envoy à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b59b7-125">**tooadd Envoy from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b59b7-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="b59b7-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="b59b7-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="b59b7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b59b7-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="b59b7-129">Then go too**All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="b59b7-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="b59b7-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="b59b7-133">Dans la zone de recherche de hello, tapez **Envoy**, sélectionnez **Envoy** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="b59b7-133">In hello search box, type **Envoy**, select **Envoy** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Liste des résultats de envoy Bonjour](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b59b7-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b59b7-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="b59b7-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Envoy, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="b59b7-136">In this section, you configure and test Azure AD single sign-on with Envoy based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b59b7-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello Envoy est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b59b7-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Envoy is tooa user in Azure AD.</span></span> <span data-ttu-id="b59b7-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Envoy doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="b59b7-138">In other words, a link relationship between an Azure AD user and hello related user in Envoy needs toobe established.</span></span>

<span data-ttu-id="b59b7-139">Dans Envoy, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="b59b7-139">In Envoy, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b59b7-140">tooconfigure et test Azure AD l’authentification unique à Envoy, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="b59b7-140">tooconfigure and test Azure AD single sign-on with Envoy, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b59b7-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="b59b7-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b59b7-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b59b7-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b59b7-143">**[Créer un utilisateur de test Envoy](#create-an-envoy-test-user)**  -toohave un équivalent de Britta Simon dans Envoy est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b59b7-143">**[Create an Envoy test user](#create-an-envoy-test-user)** - toohave a counterpart of Britta Simon in Envoy that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b59b7-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="b59b7-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b59b7-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="b59b7-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b59b7-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b59b7-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b59b7-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application d’envoi.</span><span class="sxs-lookup"><span data-stu-id="b59b7-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Envoy application.</span></span>

<span data-ttu-id="b59b7-148">**tooconfigure Azure AD single sign-on avec Envoy, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b59b7-148">**tooconfigure Azure AD single sign-on with Envoy, perform hello following steps:**</span></span>

1. <span data-ttu-id="b59b7-149">Bonjour portail Azure, sur hello **Envoy** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="b59b7-149">In hello Azure portal, on hello **Envoy** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="b59b7-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="b59b7-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_samlbase.png)

3. <span data-ttu-id="b59b7-153">Sur hello **Envoy domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="b59b7-153">On hello **Envoy Domain and URLs** section, perform hello following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL Envoy](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_url.png)

    <span data-ttu-id="b59b7-155">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<tenant-name>.Envoy.com`</span><span class="sxs-lookup"><span data-stu-id="b59b7-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.Envoy.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="b59b7-156">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="b59b7-156">This value is not real.</span></span> <span data-ttu-id="b59b7-157">Mettre à jour de cette valeur avec hello URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="b59b7-157">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="b59b7-158">Contact [équipe de support Client de Envoy](https://envoy.com/contact/) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="b59b7-158">Contact [Envoy Client support team](https://envoy.com/contact/) tooget this value.</span></span>

4. <span data-ttu-id="b59b7-159">Sur hello **le certificat de signature SAML** section, hello de copie **l’empreinte numérique** valeur du certificat...</span><span class="sxs-lookup"><span data-stu-id="b59b7-159">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate..</span></span>

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_certificate.png) 

5. <span data-ttu-id="b59b7-161">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="b59b7-161">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-envoy-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b59b7-163">Sur hello **Envoy Configuration** , cliquez sur **Envoy de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="b59b7-163">On hello **Envoy Configuration** section, click **Configure Envoy** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b59b7-164">Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="b59b7-164">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuration d’Envoy](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_configure.png)

7. <span data-ttu-id="b59b7-166">Dans une autre fenêtre de navigateur web, connectez-vous au site de votre entreprise Envoy en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="b59b7-166">In a different web browser window, log into your Envoy company site as an administrator.</span></span>

8. <span data-ttu-id="b59b7-167">Dans la barre d’outils de hello en haut de hello, cliquez sur **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="b59b7-167">In hello toolbar on hello top, click **Settings**.</span></span>

    <span data-ttu-id="b59b7-168">![Envoy](./media/active-directory-saas-envoy-tutorial/ic776782.png "Envoy")</span><span class="sxs-lookup"><span data-stu-id="b59b7-168">![Envoy](./media/active-directory-saas-envoy-tutorial/ic776782.png "Envoy")</span></span>

9. <span data-ttu-id="b59b7-169">Cliquez sur **Company**.</span><span class="sxs-lookup"><span data-stu-id="b59b7-169">Click **Company**.</span></span>

    <span data-ttu-id="b59b7-170">![Company](./media/active-directory-saas-envoy-tutorial/ic776783.png "Company")</span><span class="sxs-lookup"><span data-stu-id="b59b7-170">![Company](./media/active-directory-saas-envoy-tutorial/ic776783.png "Company")</span></span>

10. <span data-ttu-id="b59b7-171">Cliquez sur **SAML**.</span><span class="sxs-lookup"><span data-stu-id="b59b7-171">Click **SAML**.</span></span>

    <span data-ttu-id="b59b7-172">![SAML](./media/active-directory-saas-envoy-tutorial/ic776784.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="b59b7-172">![SAML](./media/active-directory-saas-envoy-tutorial/ic776784.png "SAML")</span></span>

11. <span data-ttu-id="b59b7-173">Bonjour **l’authentification SAML** configuration section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="b59b7-173">In hello **SAML Authentication** configuration section, perform hello following steps:</span></span>

    <span data-ttu-id="b59b7-174">![SAML authentication](./media/active-directory-saas-envoy-tutorial/ic776785.png "SAML authentication")</span><span class="sxs-lookup"><span data-stu-id="b59b7-174">![SAML authentication](./media/active-directory-saas-envoy-tutorial/ic776785.png "SAML authentication")</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="b59b7-175">valeur de Hello pour l’ID d’emplacement du siège hello est générée automatiquement par l’application hello.</span><span class="sxs-lookup"><span data-stu-id="b59b7-175">hello value for hello HQ location ID is auto generated by hello application.</span></span>
    
    <span data-ttu-id="b59b7-176">a.</span><span class="sxs-lookup"><span data-stu-id="b59b7-176">a.</span></span> <span data-ttu-id="b59b7-177">Dans **par empreinte digitale** zone de texte, collez hello **l’empreinte numérique** valeur de certificat, ce qui vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="b59b7-177">In **Fingerprint** textbox, paste hello **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="b59b7-178">b.</span><span class="sxs-lookup"><span data-stu-id="b59b7-178">b.</span></span> <span data-ttu-id="b59b7-179">Coller **SAML Sign-On URL du Service unique** valeur, qui vous avez copié écran hello Azure portail dans hello **URL SAML HTTP du fournisseur d’identité** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="b59b7-179">Paste **SAML Single Sign-On Service URL** value, which you have copied form hello Azure portal into hello **IDENTITY PROVIDER HTTP SAML URL** textbox.</span></span>
    
    <span data-ttu-id="b59b7-180">c.</span><span class="sxs-lookup"><span data-stu-id="b59b7-180">c.</span></span> <span data-ttu-id="b59b7-181">Cliquez sur **Save changes**.</span><span class="sxs-lookup"><span data-stu-id="b59b7-181">Click **Save changes**.</span></span>

> [!TIP]
> <span data-ttu-id="b59b7-182">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="b59b7-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b59b7-183">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="b59b7-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b59b7-184">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b59b7-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b59b7-185">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="b59b7-185">Create an Azure AD test user</span></span>

<span data-ttu-id="b59b7-186">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="b59b7-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="b59b7-188">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b59b7-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b59b7-189">Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.</span><span class="sxs-lookup"><span data-stu-id="b59b7-189">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-envoy-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="b59b7-191">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="b59b7-191">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-envoy-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="b59b7-193">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="b59b7-193">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![bouton Ajouter de Hello](./media/active-directory-saas-envoy-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="b59b7-195">Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="b59b7-195">In hello **User** dialog box, perform hello following steps:</span></span>

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-envoy-tutorial/create_aaduser_04.png)

    <span data-ttu-id="b59b7-197">a.</span><span class="sxs-lookup"><span data-stu-id="b59b7-197">a.</span></span> <span data-ttu-id="b59b7-198">Bonjour **nom** , tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b59b7-198">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b59b7-199">b.</span><span class="sxs-lookup"><span data-stu-id="b59b7-199">b.</span></span> <span data-ttu-id="b59b7-200">Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b59b7-200">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="b59b7-201">c.</span><span class="sxs-lookup"><span data-stu-id="b59b7-201">c.</span></span> <span data-ttu-id="b59b7-202">Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.</span><span class="sxs-lookup"><span data-stu-id="b59b7-202">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="b59b7-203">d.</span><span class="sxs-lookup"><span data-stu-id="b59b7-203">d.</span></span> <span data-ttu-id="b59b7-204">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="b59b7-204">Click **Create**.</span></span>
 
### <a name="create-an-envoy-test-user"></a><span data-ttu-id="b59b7-205">Créer un utilisateur de test Envoy</span><span class="sxs-lookup"><span data-stu-id="b59b7-205">Create an Envoy test user</span></span>

<span data-ttu-id="b59b7-206">Il n’existe aucun élément d’action pour vous tooconfigure configuration de l’utilisateur tooEnvoy.</span><span class="sxs-lookup"><span data-stu-id="b59b7-206">There is no action item for you tooconfigure user provisioning tooEnvoy.</span></span> <span data-ttu-id="b59b7-207">Quand un utilisateur affecté tente de toolog à Envoy à l’aide du volet d’accès hello, Envoy vérifie l’existence d’un utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="b59b7-207">When an assigned user tries toolog into Envoy using hello access panel, Envoy checks whether hello user exists.</span></span> <span data-ttu-id="b59b7-208">Si aucun compte d'utilisateur n’est disponible, Envoy le crée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="b59b7-208">If there is no user account available yet, it is automatically created by Envoy.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="b59b7-209">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b59b7-209">Assign hello Azure AD test user</span></span>

<span data-ttu-id="b59b7-210">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooEnvoy.</span><span class="sxs-lookup"><span data-stu-id="b59b7-210">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEnvoy.</span></span>

![Attribuer le rôle d’utilisateur hello][200] 

<span data-ttu-id="b59b7-212">**tooassign Britta Simon tooEnvoy, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b59b7-212">**tooassign Britta Simon tooEnvoy, perform hello following steps:**</span></span>

1. <span data-ttu-id="b59b7-213">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="b59b7-213">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="b59b7-215">Dans la liste des applications hello, sélectionnez **Envoy**.</span><span class="sxs-lookup"><span data-stu-id="b59b7-215">In hello applications list, select **Envoy**.</span></span>

    ![lien d’Envoy Hello dans la liste des Applications hello](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_app.png)  

3. <span data-ttu-id="b59b7-217">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="b59b7-217">In hello menu on hello left, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202]

4. <span data-ttu-id="b59b7-219">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="b59b7-219">Click **Add** button.</span></span> <span data-ttu-id="b59b7-220">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="b59b7-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="b59b7-222">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="b59b7-222">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b59b7-223">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="b59b7-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b59b7-224">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="b59b7-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b59b7-225">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="b59b7-225">Test single sign-on</span></span>

<span data-ttu-id="b59b7-226">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="b59b7-226">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b59b7-227">Lorsque vous cliquez sur mosaïque Envoy hello hello volet d’accès, vous devez obtenir l’application d’Envoy automatiquement signé sur tooyour.</span><span class="sxs-lookup"><span data-stu-id="b59b7-227">When you click hello Envoy tile in hello Access Panel, you should get automatically signed-on tooyour Envoy application.</span></span>
<span data-ttu-id="b59b7-228">Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b59b7-228">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b59b7-229">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="b59b7-229">Additional resources</span></span>

* [<span data-ttu-id="b59b7-230">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b59b7-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b59b7-231">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="b59b7-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_203.png

