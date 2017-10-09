---
title: "Didacticiel : Intégration d’Azure Active Directory à UserVoice | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de UserVoice."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 684a405b-8932-46f6-b43a-4d97a42b6b87
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.openlocfilehash: 9eade8435ae6c6a3821bbbec9ab7c27ed7ad91ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-uservoice"></a><span data-ttu-id="44a7f-103">Didacticiel : Intégration d’Azure Active Directory à UserVoice</span><span class="sxs-lookup"><span data-stu-id="44a7f-103">Tutorial: Azure Active Directory integration with UserVoice</span></span>

<span data-ttu-id="44a7f-104">Dans ce didacticiel, vous apprendrez comment toointegrate UserVoice avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="44a7f-104">In this tutorial, you learn how toointegrate UserVoice with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="44a7f-105">Intégration de UserVoice à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="44a7f-105">Integrating UserVoice with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="44a7f-106">Vous pouvez contrôler dans Azure AD qui a accès tooUserVoice.</span><span class="sxs-lookup"><span data-stu-id="44a7f-106">You can control in Azure AD who has access tooUserVoice.</span></span>
- <span data-ttu-id="44a7f-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooUserVoice (Single Sign-On) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="44a7f-107">You can enable your users tooautomatically get signed-on tooUserVoice (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="44a7f-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="44a7f-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="44a7f-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="44a7f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44a7f-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="44a7f-110">Prerequisites</span></span>

<span data-ttu-id="44a7f-111">tooconfigure intégration d’Azure AD à UserVoice, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="44a7f-111">tooconfigure Azure AD integration with UserVoice, you need hello following items:</span></span>

- <span data-ttu-id="44a7f-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="44a7f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="44a7f-113">Un abonnement UserVoice pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="44a7f-113">A UserVoice single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="44a7f-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="44a7f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="44a7f-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="44a7f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="44a7f-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="44a7f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="44a7f-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="44a7f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="44a7f-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="44a7f-118">Scenario description</span></span>
<span data-ttu-id="44a7f-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="44a7f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="44a7f-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="44a7f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="44a7f-121">Ajout de UserVoice à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="44a7f-121">Adding UserVoice from hello gallery</span></span>
2. <span data-ttu-id="44a7f-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="44a7f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-uservoice-from-hello-gallery"></a><span data-ttu-id="44a7f-123">Ajout de UserVoice à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="44a7f-123">Adding UserVoice from hello gallery</span></span>
<span data-ttu-id="44a7f-124">intégration de hello tooconfigure de UserVoice dans Azure AD, vous devez tooadd UserVoice à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="44a7f-124">tooconfigure hello integration of UserVoice into Azure AD, you need tooadd UserVoice from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="44a7f-125">**tooadd UserVoice à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="44a7f-125">**tooadd UserVoice from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="44a7f-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="44a7f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="44a7f-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="44a7f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="44a7f-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="44a7f-129">Then go too**All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="44a7f-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="44a7f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="44a7f-133">Dans la zone de recherche de hello, tapez **UserVoice**, sélectionnez **UserVoice** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="44a7f-133">In hello search box, type **UserVoice**, select **UserVoice** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Liste des résultats de UserVoice Bonjour](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="44a7f-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="44a7f-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="44a7f-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec UserVoice, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="44a7f-136">In this section, you configure and test Azure AD single sign-on with UserVoice based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="44a7f-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans UserVoice est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="44a7f-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in UserVoice is tooa user in Azure AD.</span></span> <span data-ttu-id="44a7f-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans UserVoice doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="44a7f-138">In other words, a link relationship between an Azure AD user and hello related user in UserVoice needs toobe established.</span></span>

<span data-ttu-id="44a7f-139">Dans UserVoice, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="44a7f-139">In UserVoice, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="44a7f-140">tooconfigure et test Azure AD l’authentification unique avec UserVoice, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="44a7f-140">tooconfigure and test Azure AD single sign-on with UserVoice, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="44a7f-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="44a7f-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="44a7f-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="44a7f-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="44a7f-143">**[Créer un utilisateur de test UserVoice](#create-a-uservoice-test-user)**  -toohave un équivalent de Britta Simon dans UserVoice est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="44a7f-143">**[Create a UserVoice test user](#create-a-uservoice-test-user)** - toohave a counterpart of Britta Simon in UserVoice that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="44a7f-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="44a7f-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="44a7f-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="44a7f-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="44a7f-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="44a7f-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="44a7f-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de UserVoice.</span><span class="sxs-lookup"><span data-stu-id="44a7f-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your UserVoice application.</span></span>

<span data-ttu-id="44a7f-148">**tooconfigure Azure AD single sign-on avec UserVoice, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="44a7f-148">**tooconfigure Azure AD single sign-on with UserVoice, perform hello following steps:**</span></span>

1. <span data-ttu-id="44a7f-149">Bonjour portail Azure, sur hello **UserVoice** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="44a7f-149">In hello Azure portal, on hello **UserVoice** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="44a7f-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="44a7f-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_samlbase.png)

3. <span data-ttu-id="44a7f-153">Sur hello **UserVoice domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="44a7f-153">On hello **UserVoice Domain and URLs** section, perform hello following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL UserVoice](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_url.png)

    <span data-ttu-id="44a7f-155">a.</span><span class="sxs-lookup"><span data-stu-id="44a7f-155">a.</span></span> <span data-ttu-id="44a7f-156">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<tenantname>.UserVoice.com`</span><span class="sxs-lookup"><span data-stu-id="44a7f-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.UserVoice.com`</span></span>

    <span data-ttu-id="44a7f-157">b.</span><span class="sxs-lookup"><span data-stu-id="44a7f-157">b.</span></span> <span data-ttu-id="44a7f-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<tenantname>.UserVoice.com`</span><span class="sxs-lookup"><span data-stu-id="44a7f-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenantname>.UserVoice.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="44a7f-159">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="44a7f-159">These values are not real.</span></span> <span data-ttu-id="44a7f-160">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="44a7f-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="44a7f-161">Contact [équipe de support Client de UserVoice](https://www.uservoice.com/) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="44a7f-161">Contact [UserVoice Client support team](https://www.uservoice.com/) tooget these values.</span></span>

4. <span data-ttu-id="44a7f-162">Sur hello **le certificat de signature SAML** section, hello de copie **l’empreinte numérique** valeur du certificat.</span><span class="sxs-lookup"><span data-stu-id="44a7f-162">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_certificate.png) 

5. <span data-ttu-id="44a7f-164">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="44a7f-164">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-uservoice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="44a7f-166">Sur hello **UserVoice Configuration** , cliquez sur **UserVoice de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="44a7f-166">On hello **UserVoice Configuration** section, click **Configure UserVoice** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="44a7f-167">Hello de copie **URL de déconnexion et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="44a7f-167">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuration de UserVoice](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_configure.png) 

7. <span data-ttu-id="44a7f-169">Dans une fenêtre de navigateur web, ouvrez une session dans le site d’entreprise UserVoice tooyour en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="44a7f-169">In a different web browser window, log in tooyour UserVoice company site as an administrator.</span></span>

8. <span data-ttu-id="44a7f-170">Dans la barre d’outils de hello en haut de hello, cliquez sur **paramètres**, puis sélectionnez **portail Web** à partir du menu de hello.</span><span class="sxs-lookup"><span data-stu-id="44a7f-170">In hello toolbar on hello top, click **Settings**, and then select **Web portal** from hello menu.</span></span>
   
    <span data-ttu-id="44a7f-171">![Section Paramètres côté application](./media/active-directory-saas-uservoice-tutorial/ic777519.png "Paramètres")</span><span class="sxs-lookup"><span data-stu-id="44a7f-171">![Settings Section On App Side](./media/active-directory-saas-uservoice-tutorial/ic777519.png "Settings")</span></span>

9. <span data-ttu-id="44a7f-172">Sur hello **portail Web** onglet hello **l’authentification utilisateur** , cliquez sur **modifier** tooopen hello **modifier l’authentification utilisateur** boîte de dialogue page.</span><span class="sxs-lookup"><span data-stu-id="44a7f-172">On hello **Web portal** tab, in hello **User authentication** section, click **Edit** tooopen hello **Edit User Authentication** dialog page.</span></span>
   
    <span data-ttu-id="44a7f-173">![Onglet Portail Web](./media/active-directory-saas-uservoice-tutorial/ic777520.png "Portail Web")</span><span class="sxs-lookup"><span data-stu-id="44a7f-173">![Web portal Tab](./media/active-directory-saas-uservoice-tutorial/ic777520.png "Web portal")</span></span>

10. <span data-ttu-id="44a7f-174">Sur hello **modifier l’authentification utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="44a7f-174">On hello **Edit User Authentication** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="44a7f-175">![Modifier l’authentification utilisateur](./media/active-directory-saas-uservoice-tutorial/ic777521.png "modifier l’authentification utilisateur")</span><span class="sxs-lookup"><span data-stu-id="44a7f-175">![Edit user authentication](./media/active-directory-saas-uservoice-tutorial/ic777521.png "Edit user authentication")</span></span>
   
    <span data-ttu-id="44a7f-176">a.</span><span class="sxs-lookup"><span data-stu-id="44a7f-176">a.</span></span> <span data-ttu-id="44a7f-177">Cliquez sur **Single Sign-On (SSO)**.</span><span class="sxs-lookup"><span data-stu-id="44a7f-177">Click **Single Sign-On (SSO)**.</span></span>
 
    <span data-ttu-id="44a7f-178">b.</span><span class="sxs-lookup"><span data-stu-id="44a7f-178">b.</span></span> <span data-ttu-id="44a7f-179">Hello de coller **SAML Sign-On URL du Service unique** valeur, ce qui vous avez copié à partir de hello portail Azure en hello **SSO distant connectez-vous** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="44a7f-179">Paste hello **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **SSO Remote Sign-In** textbox.</span></span>

    <span data-ttu-id="44a7f-180">c.</span><span class="sxs-lookup"><span data-stu-id="44a7f-180">c.</span></span> <span data-ttu-id="44a7f-181">Hello de coller **URL de déconnexion** valeur, ce qui vous avez copié à partir de hello portail Azure en hello **déconnexion à distance de l’authentification unique de zone de texte**.</span><span class="sxs-lookup"><span data-stu-id="44a7f-181">Paste hello **Sign-Out URL** value, which you have copied from hello Azure portal into hello **SSO Remote Sign-Out textbox**.</span></span>
 
    <span data-ttu-id="44a7f-182">d.</span><span class="sxs-lookup"><span data-stu-id="44a7f-182">d.</span></span> <span data-ttu-id="44a7f-183">Hello de coller **l’empreinte numérique** valeur, qui vous avez copié à partir du portail Azure dans le **empreinte de certificat SHA1 actuelle** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="44a7f-183">Paste hello **Thumbprint** value , which you have copied from Azure portal  into the **Current certificate SHA1 fingerprint** textbox.</span></span>
    
    <span data-ttu-id="44a7f-184">e.</span><span class="sxs-lookup"><span data-stu-id="44a7f-184">e.</span></span> <span data-ttu-id="44a7f-185">Cliquez sur **Save authentication settings**.</span><span class="sxs-lookup"><span data-stu-id="44a7f-185">Click **Save authentication settings**.</span></span>

> [!TIP]
> <span data-ttu-id="44a7f-186">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="44a7f-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="44a7f-187">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="44a7f-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="44a7f-188">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="44a7f-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="44a7f-189">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="44a7f-189">Create an Azure AD test user</span></span>

<span data-ttu-id="44a7f-190">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="44a7f-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="44a7f-192">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="44a7f-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="44a7f-193">Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.</span><span class="sxs-lookup"><span data-stu-id="44a7f-193">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-uservoice-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="44a7f-195">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="44a7f-195">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-uservoice-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="44a7f-197">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="44a7f-197">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![bouton Ajouter de Hello](./media/active-directory-saas-uservoice-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="44a7f-199">Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="44a7f-199">In hello **User** dialog box, perform hello following steps:</span></span>

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-uservoice-tutorial/create_aaduser_04.png)

    <span data-ttu-id="44a7f-201">a.</span><span class="sxs-lookup"><span data-stu-id="44a7f-201">a.</span></span> <span data-ttu-id="44a7f-202">Bonjour **nom** , tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="44a7f-202">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="44a7f-203">b.</span><span class="sxs-lookup"><span data-stu-id="44a7f-203">b.</span></span> <span data-ttu-id="44a7f-204">Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="44a7f-204">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="44a7f-205">c.</span><span class="sxs-lookup"><span data-stu-id="44a7f-205">c.</span></span> <span data-ttu-id="44a7f-206">Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.</span><span class="sxs-lookup"><span data-stu-id="44a7f-206">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="44a7f-207">d.</span><span class="sxs-lookup"><span data-stu-id="44a7f-207">d.</span></span> <span data-ttu-id="44a7f-208">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="44a7f-208">Click **Create**.</span></span>
 
### <a name="create-a-uservoice-test-user"></a><span data-ttu-id="44a7f-209">Créer un utilisateur de test UserVoice</span><span class="sxs-lookup"><span data-stu-id="44a7f-209">Create a UserVoice test user</span></span>

<span data-ttu-id="44a7f-210">tooenable Azure AD les utilisateurs toolog dans tooUserVoice, vous devez les configurer dans UserVoice.</span><span class="sxs-lookup"><span data-stu-id="44a7f-210">tooenable Azure AD users toolog in tooUserVoice, they must be provisioned into UserVoice.</span></span> <span data-ttu-id="44a7f-211">Dans les cas de hello de UserVoice, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="44a7f-211">In hello case of UserVoice, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="44a7f-212">tooprovision un compte d’utilisateur, effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="44a7f-212">tooprovision a user account, perform hello following steps:</span></span>
1. <span data-ttu-id="44a7f-213">Connectez-vous à tooyour **UserVoice** client.</span><span class="sxs-lookup"><span data-stu-id="44a7f-213">Log in tooyour **UserVoice** tenant.</span></span>

2. <span data-ttu-id="44a7f-214">Accédez trop**paramètres**.</span><span class="sxs-lookup"><span data-stu-id="44a7f-214">Go too**Settings**.</span></span>
   
    <span data-ttu-id="44a7f-215">![Paramètres](./media/active-directory-saas-uservoice-tutorial/ic777811.png "Paramètres")</span><span class="sxs-lookup"><span data-stu-id="44a7f-215">![Settings](./media/active-directory-saas-uservoice-tutorial/ic777811.png "Settings")</span></span>

3. <span data-ttu-id="44a7f-216">Cliquez sur **General**.</span><span class="sxs-lookup"><span data-stu-id="44a7f-216">Click **General**.</span></span>

4. <span data-ttu-id="44a7f-217">Cliquez sur **Agents and permissions**.</span><span class="sxs-lookup"><span data-stu-id="44a7f-217">Click **Agents and permissions**.</span></span>
   
    <span data-ttu-id="44a7f-218">![Agents et autorisations](./media/active-directory-saas-uservoice-tutorial/ic777812.png "Agents et autorisations")</span><span class="sxs-lookup"><span data-stu-id="44a7f-218">![Agents and permissions](./media/active-directory-saas-uservoice-tutorial/ic777812.png "Agents and permissions")</span></span>

5. <span data-ttu-id="44a7f-219">Cliquez sur **Add admins**.</span><span class="sxs-lookup"><span data-stu-id="44a7f-219">Click **Add admins**.</span></span>
   
    <span data-ttu-id="44a7f-220">![Ajouter des administrateurs](./media/active-directory-saas-uservoice-tutorial/ic777813.png "ajouter des administrateurs")</span><span class="sxs-lookup"><span data-stu-id="44a7f-220">![Add admins](./media/active-directory-saas-uservoice-tutorial/ic777813.png "Add admins")</span></span>

6. <span data-ttu-id="44a7f-221">Sur hello **inviter des administrateurs** boîte de dialogue, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="44a7f-221">On hello **Invite admins** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="44a7f-222">![Inviter des administrateurs](./media/active-directory-saas-uservoice-tutorial/ic777814.png "inviter des administrateurs")</span><span class="sxs-lookup"><span data-stu-id="44a7f-222">![Invite admins](./media/active-directory-saas-uservoice-tutorial/ic777814.png "Invite admins")</span></span>
   
    <span data-ttu-id="44a7f-223">a.</span><span class="sxs-lookup"><span data-stu-id="44a7f-223">a.</span></span> <span data-ttu-id="44a7f-224">Dans la zone de texte hello des messages électroniques, tapez adresse de messagerie hello de hello compte tooprovision, puis cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="44a7f-224">In hello Emails textbox, type hello email address of hello account you want tooprovision, and then click **Add**.</span></span>
   
    <span data-ttu-id="44a7f-225">b.</span><span class="sxs-lookup"><span data-stu-id="44a7f-225">b.</span></span> <span data-ttu-id="44a7f-226">Cliquez sur **Invite**.</span><span class="sxs-lookup"><span data-stu-id="44a7f-226">Click **Invite**.</span></span>

> [!NOTE]
> <span data-ttu-id="44a7f-227">Vous pouvez utiliser n’importe quel autre UserVoice utilisateur compte outil de création ou API fournie par UserVoice tooprovision des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="44a7f-227">You can use any other UserVoice user account creation tools or APIs provided by UserVoice tooprovision AAD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="44a7f-228">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="44a7f-228">Assign hello Azure AD test user</span></span>

<span data-ttu-id="44a7f-229">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooUserVoice.</span><span class="sxs-lookup"><span data-stu-id="44a7f-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooUserVoice.</span></span>

![Attribuer le rôle d’utilisateur hello][200] 

<span data-ttu-id="44a7f-231">**tooassign Britta Simon tooUserVoice, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="44a7f-231">**tooassign Britta Simon tooUserVoice, perform hello following steps:**</span></span>

1. <span data-ttu-id="44a7f-232">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="44a7f-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="44a7f-234">Dans la liste des applications hello, sélectionnez **UserVoice**.</span><span class="sxs-lookup"><span data-stu-id="44a7f-234">In hello applications list, select **UserVoice**.</span></span>

    ![lien de UserVoice Hello dans la liste des Applications hello](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_app.png)  

3. <span data-ttu-id="44a7f-236">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="44a7f-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202]

4. <span data-ttu-id="44a7f-238">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="44a7f-238">Click **Add** button.</span></span> <span data-ttu-id="44a7f-239">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="44a7f-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="44a7f-241">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="44a7f-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="44a7f-242">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="44a7f-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="44a7f-243">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="44a7f-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="44a7f-244">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="44a7f-244">Test single sign-on</span></span>

<span data-ttu-id="44a7f-245">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="44a7f-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="44a7f-246">Lorsque vous cliquez sur mosaïque UserVoice hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour UserVoice application.</span><span class="sxs-lookup"><span data-stu-id="44a7f-246">When you click hello UserVoice tile in hello Access Panel, you should get automatically signed-on tooyour UserVoice application.</span></span>
<span data-ttu-id="44a7f-247">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="44a7f-247">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="44a7f-248">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="44a7f-248">Additional resources</span></span>

* [<span data-ttu-id="44a7f-249">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="44a7f-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="44a7f-250">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="44a7f-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_203.png

