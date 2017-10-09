---
title: "Didacticiel : Intégration d’Azure Active Directory à TigerText Secure Messenger | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Messenger de sécuriser TigerText."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 03f1e128-5bcb-4e49-b6a3-fe22eedc6d5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.openlocfilehash: a3d7bb9598658c75c567c15751740d885fe4fc27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tigertext-secure-messenger"></a><span data-ttu-id="36026-103">Didacticiel : Intégration d’Azure Active Directory à TigerText Secure Messenger</span><span class="sxs-lookup"><span data-stu-id="36026-103">Tutorial: Azure Active Directory integration with TigerText Secure Messenger</span></span>

<span data-ttu-id="36026-104">Dans ce didacticiel, vous apprendrez comment toointegrate TigerText Secure Messenger avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="36026-104">In this tutorial, you learn how toointegrate TigerText Secure Messenger with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="36026-105">Intégration Messenger de sécuriser TigerText à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="36026-105">Integrating TigerText Secure Messenger with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="36026-106">Vous pouvez contrôler dans Azure AD qui a accès tooTigerText Messenger sécurisé</span><span class="sxs-lookup"><span data-stu-id="36026-106">You can control in Azure AD who has access tooTigerText Secure Messenger</span></span>
- <span data-ttu-id="36026-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooTigerText Messenger de sécuriser (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="36026-107">You can enable your users tooautomatically get signed-on tooTigerText Secure Messenger (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="36026-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="36026-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="36026-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="36026-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="36026-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="36026-110">Prerequisites</span></span>

<span data-ttu-id="36026-111">tooconfigure intégration d’Azure AD avec Messenger de sécuriser TigerText, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="36026-111">tooconfigure Azure AD integration with TigerText Secure Messenger, you need hello following items:</span></span>

- <span data-ttu-id="36026-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="36026-112">An Azure AD subscription</span></span>
- <span data-ttu-id="36026-113">Un abonnement TigerText Secure Messenger pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="36026-113">A TigerText Secure Messenger single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="36026-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="36026-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="36026-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="36026-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="36026-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="36026-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="36026-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="36026-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="36026-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="36026-118">Scenario description</span></span>
<span data-ttu-id="36026-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="36026-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="36026-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="36026-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="36026-121">Ajouter Messenger de sécuriser TigerText à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="36026-121">Add TigerText Secure Messenger from hello gallery</span></span>
2. <span data-ttu-id="36026-122">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="36026-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tigertext-secure-messenger-from-hello-gallery"></a><span data-ttu-id="36026-123">Ajouter Messenger de sécuriser TigerText à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="36026-123">Add TigerText Secure Messenger from hello gallery</span></span>
<span data-ttu-id="36026-124">intégration de hello tooconfigure de Messenger de sécuriser TigerText dans Azure AD, vous devez tooadd Messenger de sécuriser TigerText à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="36026-124">tooconfigure hello integration of TigerText Secure Messenger into Azure AD, you need tooadd TigerText Secure Messenger from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="36026-125">**tooadd TigerText Secure Messenger à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="36026-125">**tooadd TigerText Secure Messenger from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="36026-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="36026-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="36026-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="36026-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="36026-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="36026-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="36026-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="36026-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="36026-133">Dans la zone de recherche de hello, tapez **Messenger de sécuriser TigerText**, sélectionnez **Messenger de sécuriser TigerText** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="36026-133">In hello search box, type **TigerText Secure Messenger**, select **TigerText Secure Messenger** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Ajouter à partir de la galerie](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="36026-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="36026-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="36026-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec TigerText Secure Messenger pour un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="36026-136">In this section, you configure and test Azure AD single sign-on with TigerText Secure Messenger based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="36026-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Messenger de sécuriser TigerText est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="36026-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TigerText Secure Messenger is tooa user in Azure AD.</span></span> <span data-ttu-id="36026-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Messenger de sécuriser TigerText doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="36026-138">In other words, a link relationship between an Azure AD user and hello related user in TigerText Secure Messenger needs toobe established.</span></span>

<span data-ttu-id="36026-139">Dans TigerText Secure Messenger, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="36026-139">In TigerText Secure Messenger, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="36026-140">tooconfigure et test Azure AD l’authentification unique avec Messenger de sécuriser TigerText, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="36026-140">tooconfigure and test Azure AD single sign-on with TigerText Secure Messenger, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="36026-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="36026-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="36026-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="36026-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="36026-143">**[Créer un utilisateur de test Messenger de sécuriser TigerText](#create-a-tigertext-secure-messenger-test-user)**  -toohave un équivalent de Britta Simon dans Messenger TigerText sécurisé qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="36026-143">**[Create a TigerText Secure Messenger test user](#create-a-tigertext-secure-messenger-test-user)** - toohave a counterpart of Britta Simon in TigerText Secure Messenger that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="36026-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="36026-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="36026-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="36026-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="36026-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="36026-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="36026-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Messenger de sécuriser TigerText.</span><span class="sxs-lookup"><span data-stu-id="36026-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TigerText Secure Messenger application.</span></span>

<span data-ttu-id="36026-148">**tooconfigure Azure AD l’authentification unique avec TigerText Secure Messenger, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="36026-148">**tooconfigure Azure AD single sign-on with TigerText Secure Messenger, perform hello following steps:**</span></span>

1. <span data-ttu-id="36026-149">Bonjour portail Azure, sur hello **Messenger de sécuriser TigerText** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="36026-149">In hello Azure portal, on hello **TigerText Secure Messenger** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="36026-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="36026-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Authentification basée sur SAML](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_samlbase.png)

3. <span data-ttu-id="36026-153">Sur hello **TigerText Secure Messenger domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="36026-153">On hello **TigerText Secure Messenger Domain and URLs** section, perform hello following steps:</span></span>

    ![Section Domaine et URL TigerText Secure Messenger](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_url.png)

    <span data-ttu-id="36026-155">a.</span><span class="sxs-lookup"><span data-stu-id="36026-155">a.</span></span> <span data-ttu-id="36026-156">Bonjour **URL de connexion** zone de texte, tapez l’URL en tant que :`https://home.tigertext.com`</span><span class="sxs-lookup"><span data-stu-id="36026-156">In hello **Sign-on URL** textbox, type URL as: `https://home.tigertext.com`</span></span>

    <span data-ttu-id="36026-157">b.</span><span class="sxs-lookup"><span data-stu-id="36026-157">b.</span></span> <span data-ttu-id="36026-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://saml-lb.tigertext.me/v1/organization/<instance Id>`</span><span class="sxs-lookup"><span data-stu-id="36026-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://saml-lb.tigertext.me/v1/organization/<instance Id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="36026-159">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="36026-159">This value is not real.</span></span> <span data-ttu-id="36026-160">Mettre à jour de cette valeur avec hello identificateur réel.</span><span class="sxs-lookup"><span data-stu-id="36026-160">Update this value with hello actual Identifier.</span></span> <span data-ttu-id="36026-161">Contact [équipe de support Client de messagerie sécurisé TigerText](mailTo:prosupport@tigertext.com) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="36026-161">Contact [TigerText Secure Messenger Client support team](mailTo:prosupport@tigertext.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="36026-162">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="36026-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Section Certificat de signature SAML](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_certificate.png) 

5. <span data-ttu-id="36026-164">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="36026-164">Click **Save** button.</span></span>

    ![Bouton Enregistrer](./media/active-directory-saas-tigertext-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="36026-166">tooget l’authentification unique configurée pour votre application, contactez [équipe de support Messenger de sécuriser TigerText](mailTo:prosupport@tigertext.com) et nommez-les hello **téléchargés métadonnées**.</span><span class="sxs-lookup"><span data-stu-id="36026-166">tooget single sign-on configured for your application, contact [TigerText Secure Messenger support team](mailTo:prosupport@tigertext.com) and provide them hello **Downloaded metadata**.</span></span>

> [!TIP]
> <span data-ttu-id="36026-167">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="36026-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="36026-168">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="36026-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="36026-169">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="36026-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="36026-170">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="36026-170">Create an Azure AD test user</span></span>
<span data-ttu-id="36026-171">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="36026-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="36026-173">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="36026-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="36026-174">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="36026-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tigertext-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="36026-176">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="36026-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Utilisateurs et groupes->Tous les utilisateurs](./media/active-directory-saas-tigertext-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="36026-178">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="36026-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bouton Ajouter](./media/active-directory-saas-tigertext-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="36026-180">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="36026-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Boîte de dialogue utilisateur](./media/active-directory-saas-tigertext-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="36026-182">a.</span><span class="sxs-lookup"><span data-stu-id="36026-182">a.</span></span> <span data-ttu-id="36026-183">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="36026-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="36026-184">b.</span><span class="sxs-lookup"><span data-stu-id="36026-184">b.</span></span> <span data-ttu-id="36026-185">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="36026-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="36026-186">c.</span><span class="sxs-lookup"><span data-stu-id="36026-186">c.</span></span> <span data-ttu-id="36026-187">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="36026-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="36026-188">d.</span><span class="sxs-lookup"><span data-stu-id="36026-188">d.</span></span> <span data-ttu-id="36026-189">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="36026-189">Click **Create**.</span></span>
 
### <a name="create-a-tigertext-secure-messenger-test-user"></a><span data-ttu-id="36026-190">Créer un utilisateur de test TigerText Secure Messenger</span><span class="sxs-lookup"><span data-stu-id="36026-190">Create a TigerText Secure Messenger test user</span></span>

<span data-ttu-id="36026-191">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans TigerText.</span><span class="sxs-lookup"><span data-stu-id="36026-191">In this section, you create a user called Britta Simon in TigerText.</span></span> <span data-ttu-id="36026-192">Veuillez contacter trop[équipe de support Client de messagerie sécurisé TigerText](mailTo:prosupport@tigertext.com) tooadd les utilisateurs de hello dans la plateforme de TigerText hello.</span><span class="sxs-lookup"><span data-stu-id="36026-192">Please reach out too[TigerText Secure Messenger Client support team](mailTo:prosupport@tigertext.com) tooadd hello users in hello TigerText platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="36026-193">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="36026-193">Assign hello Azure AD test user</span></span>

<span data-ttu-id="36026-194">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooTigerText Messenger de sécuriser.</span><span class="sxs-lookup"><span data-stu-id="36026-194">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTigerText Secure Messenger.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="36026-196">**tooassign Britta Simon tooTigerText Messenger sécuriser, effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="36026-196">**tooassign Britta Simon tooTigerText Secure Messenger, perform hello following steps:**</span></span>

1. <span data-ttu-id="36026-197">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="36026-197">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="36026-199">Dans la liste des applications hello, sélectionnez **Messenger de Secure TigerText**.</span><span class="sxs-lookup"><span data-stu-id="36026-199">In hello applications list, select **TigerText Secure Messenger**.</span></span>

    ![TigerText Secure Messenger dans la liste des applications](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_app.png) 

3. <span data-ttu-id="36026-201">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="36026-201">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="36026-203">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="36026-203">Click **Add** button.</span></span> <span data-ttu-id="36026-204">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="36026-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="36026-206">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="36026-206">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="36026-207">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="36026-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="36026-208">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="36026-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="36026-209">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="36026-209">Test single sign-on</span></span>

<span data-ttu-id="36026-210">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="36026-210">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="36026-211">Lorsque vous cliquez sur mosaïque TigerText hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour TigerText application.</span><span class="sxs-lookup"><span data-stu-id="36026-211">When you click hello TigerText tile in hello Access Panel, you should get automatically signed-on tooyour TigerText application.</span></span> <span data-ttu-id="36026-212">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="36026-212">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="36026-213">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="36026-213">Additional resources</span></span>

* [<span data-ttu-id="36026-214">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="36026-214">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="36026-215">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="36026-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_203.png

