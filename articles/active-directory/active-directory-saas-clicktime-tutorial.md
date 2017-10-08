---
title: "Didacticiel : Intégration d’Azure Active Directory à ClickTime | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et ClickTime."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d437b5ab-4d71-4c13-96d0-79018cebbbd4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: jeedes
ms.openlocfilehash: a0259e31164cad6c6c77ed8aac1c50cd9a3e46ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clicktime"></a><span data-ttu-id="fcb86-103">Didacticiel : Intégration d’Azure Active Directory à ClickTime</span><span class="sxs-lookup"><span data-stu-id="fcb86-103">Tutorial: Azure Active Directory integration with ClickTime</span></span>

<span data-ttu-id="fcb86-104">Dans ce didacticiel, vous apprendrez comment toointegrate ClickTime avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fcb86-104">In this tutorial, you learn how toointegrate ClickTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fcb86-105">Intégration de ClickTime à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="fcb86-105">Integrating ClickTime with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="fcb86-106">Vous pouvez contrôler dans Azure AD qui a accès tooClickTime</span><span class="sxs-lookup"><span data-stu-id="fcb86-106">You can control in Azure AD who has access tooClickTime</span></span>
- <span data-ttu-id="fcb86-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooClickTime (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="fcb86-107">You can enable your users tooautomatically get signed-on tooClickTime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fcb86-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="fcb86-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="fcb86-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fcb86-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fcb86-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="fcb86-110">Prerequisites</span></span>

<span data-ttu-id="fcb86-111">tooconfigure intégration d’Azure AD à ClickTime, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="fcb86-111">tooconfigure Azure AD integration with ClickTime, you need hello following items:</span></span>

- <span data-ttu-id="fcb86-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="fcb86-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fcb86-113">Un abonnement ClickTime pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="fcb86-113">A ClickTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fcb86-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="fcb86-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fcb86-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="fcb86-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fcb86-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="fcb86-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fcb86-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fcb86-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fcb86-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="fcb86-118">Scenario description</span></span>
<span data-ttu-id="fcb86-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="fcb86-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fcb86-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="fcb86-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fcb86-121">Ajout de ClickTime à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="fcb86-121">Adding ClickTime from hello gallery</span></span>
2. <span data-ttu-id="fcb86-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="fcb86-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-clicktime-from-hello-gallery"></a><span data-ttu-id="fcb86-123">Ajout de ClickTime à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="fcb86-123">Adding ClickTime from hello gallery</span></span>
<span data-ttu-id="fcb86-124">tooconfigure hello intégration de ClickTime dans Azure AD, vous devez tooadd ClickTime à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="fcb86-124">tooconfigure hello integration of ClickTime into Azure AD, you need tooadd ClickTime from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="fcb86-125">**tooadd ClickTime à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="fcb86-125">**tooadd ClickTime from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="fcb86-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="fcb86-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="fcb86-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="fcb86-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="fcb86-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="fcb86-129">Then go too**All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="fcb86-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="fcb86-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="fcb86-133">Dans la zone de recherche de hello, tapez **ClickTime**, sélectionnez **ClickTime** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="fcb86-133">In hello search box, type **ClickTime**, select **ClickTime** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Liste des résultats de ClickTime Bonjour](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="fcb86-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="fcb86-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="fcb86-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec ClickTime, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="fcb86-136">In this section, you configure and test Azure AD single sign-on with ClickTime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fcb86-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans ClickTime est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fcb86-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ClickTime is tooa user in Azure AD.</span></span> <span data-ttu-id="fcb86-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans ClickTime doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="fcb86-138">In other words, a link relationship between an Azure AD user and hello related user in ClickTime needs toobe established.</span></span>

<span data-ttu-id="fcb86-139">Dans ClickTime, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="fcb86-139">In ClickTime, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="fcb86-140">tooconfigure et test Azure AD l’authentification unique à ClickTime, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="fcb86-140">tooconfigure and test Azure AD single sign-on with ClickTime, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="fcb86-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="fcb86-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="fcb86-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fcb86-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fcb86-143">**[Créer un utilisateur de test de ClickTime](#create-a-clicktime-test-user)**  -toohave un équivalent de Britta Simon dans ClickTime est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="fcb86-143">**[Create a ClickTime test user](#create-a-clicktime-test-user)** - toohave a counterpart of Britta Simon in ClickTime that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="fcb86-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="fcb86-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fcb86-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="fcb86-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="fcb86-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="fcb86-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="fcb86-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de ClickTime.</span><span class="sxs-lookup"><span data-stu-id="fcb86-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ClickTime application.</span></span>

<span data-ttu-id="fcb86-148">**tooconfigure Azure AD single sign-on avec ClickTime, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="fcb86-148">**tooconfigure Azure AD single sign-on with ClickTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="fcb86-149">Bonjour portail Azure, sur hello **ClickTime** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="fcb86-149">In hello Azure portal, on hello **ClickTime** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="fcb86-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="fcb86-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_samlbase.png)

3. <span data-ttu-id="fcb86-153">Sur hello **ClickTime domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="fcb86-153">On hello **ClickTime Domain and URLs** section, perform hello following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL ClickTime](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_url.png)

    <span data-ttu-id="fcb86-155">a.</span><span class="sxs-lookup"><span data-stu-id="fcb86-155">a.</span></span> <span data-ttu-id="fcb86-156">Bonjour **identificateur** zone de texte, tapez une URL en tant que :`https://app.clicktime.com/sp/`</span><span class="sxs-lookup"><span data-stu-id="fcb86-156">In hello **Identifier** textbox, type a URL as: `https://app.clicktime.com/sp/`</span></span>
    
    <span data-ttu-id="fcb86-157">b.</span><span class="sxs-lookup"><span data-stu-id="fcb86-157">b.</span></span> <span data-ttu-id="fcb86-158">Bonjour **URL de réponse** modèles de zone de texte, tapez une URL à l’aide de hello suivant :</span><span class="sxs-lookup"><span data-stu-id="fcb86-158">In hello **Reply URL** textbox, type a URL using hello following patterns:</span></span> 

    | |
    |--|
    | `https://app.clicktime.com/Login/` |
    | `https://app.clicktime.com/App/Login/Consume.aspx` |

4. <span data-ttu-id="fcb86-159">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="fcb86-159">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_certificate.png) 

5. <span data-ttu-id="fcb86-161">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="fcb86-161">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-clicktime-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fcb86-163">Sur hello **ClickTime Configuration** , cliquez sur **configurer de ClickTime** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="fcb86-163">On hello **ClickTime Configuration** section, click **Configure ClickTime** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="fcb86-164">Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="fcb86-164">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuration de ClickTime](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_configure.png) 

7. <span data-ttu-id="fcb86-166">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise ClickTime en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="fcb86-166">In a different web browser window, log into your ClickTime company site as an administrator.</span></span>

8. <span data-ttu-id="fcb86-167">Dans la barre d’outils de hello en haut de hello, cliquez sur **préférences**, puis cliquez sur **paramètres de sécurité**.</span><span class="sxs-lookup"><span data-stu-id="fcb86-167">In hello toolbar on hello top, click **Preferences**, and then click **Security Settings**.</span></span>

9. <span data-ttu-id="fcb86-168">Bonjour **préférences de l’authentification unique** configuration section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="fcb86-168">In hello **Single Sign-On Preferences** configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="fcb86-169">![Security Settings](./media/active-directory-saas-clicktime-tutorial/tic777280.png "Security Settings")</span><span class="sxs-lookup"><span data-stu-id="fcb86-169">![Security Settings](./media/active-directory-saas-clicktime-tutorial/tic777280.png "Security Settings")</span></span>
   
    <span data-ttu-id="fcb86-170">a.</span><span class="sxs-lookup"><span data-stu-id="fcb86-170">a.</span></span>  <span data-ttu-id="fcb86-171">Sélectionnez **Autoriser** la connexion à l’aide de l’authentification unique (SSO) avec **Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="fcb86-171">Select **Allow** sign-in using Single Sign-On (SSO) with **Azure AD**.</span></span>
   
    <span data-ttu-id="fcb86-172">b.</span><span class="sxs-lookup"><span data-stu-id="fcb86-172">b.</span></span> <span data-ttu-id="fcb86-173">Bonjour **point de terminaison de fournisseur d’identité** zone de texte, collez **SAML Sign-On URL du Service unique** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="fcb86-173">In hello **Identity Provider Endpoint** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="fcb86-174">c.</span><span class="sxs-lookup"><span data-stu-id="fcb86-174">c.</span></span>  <span data-ttu-id="fcb86-175">Ouvrez hello **certificat codé en base 64** téléchargé à partir du portail Azure dans **bloc-notes**, copier le contenu de hello, puis collez-le dans hello **certificat X.509** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="fcb86-175">Open hello **base-64 encoded certificate** downloaded from Azure portal in **Notepad**, copy hello content, and then paste it into hello **X.509 Certificate** textbox.</span></span>
   
    <span data-ttu-id="fcb86-176">d.</span><span class="sxs-lookup"><span data-stu-id="fcb86-176">d.</span></span>  <span data-ttu-id="fcb86-177">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="fcb86-177">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="fcb86-178">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="fcb86-178">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="fcb86-179">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="fcb86-179">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="fcb86-180">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fcb86-180">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="fcb86-181">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="fcb86-181">Create an Azure AD test user</span></span>
<span data-ttu-id="fcb86-182">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="fcb86-182">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="fcb86-184">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="fcb86-184">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="fcb86-185">Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.</span><span class="sxs-lookup"><span data-stu-id="fcb86-185">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-clicktime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fcb86-187">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="fcb86-187">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>
    
    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-clicktime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fcb86-189">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="fcb86-189">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>
 
    ![bouton Ajouter de Hello](./media/active-directory-saas-clicktime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fcb86-191">Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="fcb86-191">In hello **User** dialog box, perform hello following steps:</span></span>
 
    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-clicktime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fcb86-193">a.</span><span class="sxs-lookup"><span data-stu-id="fcb86-193">a.</span></span> <span data-ttu-id="fcb86-194">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fcb86-194">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fcb86-195">b.</span><span class="sxs-lookup"><span data-stu-id="fcb86-195">b.</span></span> <span data-ttu-id="fcb86-196">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="fcb86-196">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fcb86-197">c.</span><span class="sxs-lookup"><span data-stu-id="fcb86-197">c.</span></span> <span data-ttu-id="fcb86-198">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="fcb86-198">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="fcb86-199">d.</span><span class="sxs-lookup"><span data-stu-id="fcb86-199">d.</span></span> <span data-ttu-id="fcb86-200">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="fcb86-200">Click **Create**.</span></span>
 
### <a name="create-a-clicktime-test-user"></a><span data-ttu-id="fcb86-201">Créer un utilisateur de test ClickTime</span><span class="sxs-lookup"><span data-stu-id="fcb86-201">Create a ClickTime test user</span></span>

<span data-ttu-id="fcb86-202">Dans l’ordre tooenable le toolog d’utilisateurs Azure AD à ClickTime, vous devez les configurer dans ClickTime.</span><span class="sxs-lookup"><span data-stu-id="fcb86-202">In order tooenable Azure AD users toolog into ClickTime, they must be provisioned into ClickTime.</span></span>  
<span data-ttu-id="fcb86-203">Dans les cas de hello de ClickTime, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="fcb86-203">In hello case of ClickTime, provisioning is a manual task.</span></span>

> [!NOTE]
> <span data-ttu-id="fcb86-204">Vous pouvez utiliser n’importe quel autre ClickTime utilisateur compte outil de création ou API fournie par ClickTime tooprovision comptes d’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fcb86-204">You can use any other ClickTime user account creation tools or APIs provided by ClickTime tooprovision Azure AD user accounts.</span></span>

<span data-ttu-id="fcb86-205">**tooprovision un compte d’utilisateur, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="fcb86-205">**tooprovision a user account, perform hello following steps:**</span></span>
1. <span data-ttu-id="fcb86-206">Connectez-vous à tooyour **ClickTime** client.</span><span class="sxs-lookup"><span data-stu-id="fcb86-206">Log in tooyour **ClickTime** tenant.</span></span>
2. <span data-ttu-id="fcb86-207">Dans la barre d’outils de hello en haut de hello, cliquez sur **société**, puis cliquez sur **personnes**.</span><span class="sxs-lookup"><span data-stu-id="fcb86-207">In hello toolbar on hello top, click **Company**, and then click **People**.</span></span>
   
    <span data-ttu-id="fcb86-208">![Personnes](./media/active-directory-saas-clicktime-tutorial/tic777282.png "Personnes")</span><span class="sxs-lookup"><span data-stu-id="fcb86-208">![People](./media/active-directory-saas-clicktime-tutorial/tic777282.png "People")</span></span>
3. <span data-ttu-id="fcb86-209">Cliquez sur **Add Person**.</span><span class="sxs-lookup"><span data-stu-id="fcb86-209">Click **Add Person**.</span></span>
   
    <span data-ttu-id="fcb86-210">![Add Person](./media/active-directory-saas-clicktime-tutorial/tic777283.png "Add Person")</span><span class="sxs-lookup"><span data-stu-id="fcb86-210">![Add Person](./media/active-directory-saas-clicktime-tutorial/tic777283.png "Add Person")</span></span>
4. <span data-ttu-id="fcb86-211">Dans la section nouveau contact de hello, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="fcb86-211">In hello New Person section, perform hello following steps:</span></span>
   
    <span data-ttu-id="fcb86-212">![Personnes](./media/active-directory-saas-clicktime-tutorial/tic777284.png "Personnes")</span><span class="sxs-lookup"><span data-stu-id="fcb86-212">![People](./media/active-directory-saas-clicktime-tutorial/tic777284.png "People")</span></span>
   
    <span data-ttu-id="fcb86-213">a.</span><span class="sxs-lookup"><span data-stu-id="fcb86-213">a.</span></span>  <span data-ttu-id="fcb86-214">Bonjour **nom complet** zone de texte, tapez nom complet d’utilisateur comme **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="fcb86-214">In hello **full name** textbox, type full name of user like **Britta Simon**.</span></span> 
  
    <span data-ttu-id="fcb86-215">b.</span><span class="sxs-lookup"><span data-stu-id="fcb86-215">b.</span></span>  <span data-ttu-id="fcb86-216">Bonjour **adresse de messagerie** par courrier électronique de type hello d’utilisateur de zone de texte, comme  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="fcb86-216">In hello **email address** textbox, type hello email of user like **brittasimon@contoso.com**.</span></span>
       
    > [!NOTE]
    > <span data-ttu-id="fcb86-217">Si vous le souhaitez, vous pouvez définir des propriétés supplémentaires de l’objet person hello.</span><span class="sxs-lookup"><span data-stu-id="fcb86-217">If you want to, you can set additional properties of hello new person object.</span></span>
   
    <span data-ttu-id="fcb86-218">c.</span><span class="sxs-lookup"><span data-stu-id="fcb86-218">c.</span></span>  <span data-ttu-id="fcb86-219">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="fcb86-219">Click **Save**.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="fcb86-220">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="fcb86-220">Assign hello Azure AD test user</span></span>

<span data-ttu-id="fcb86-221">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooClickTime.</span><span class="sxs-lookup"><span data-stu-id="fcb86-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooClickTime.</span></span>

![Attribuer le rôle d’utilisateur hello][200] 

<span data-ttu-id="fcb86-223">**tooassign Britta Simon tooClickTime, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="fcb86-223">**tooassign Britta Simon tooClickTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="fcb86-224">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="fcb86-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="fcb86-226">Dans la liste des applications hello, sélectionnez **ClickTime**.</span><span class="sxs-lookup"><span data-stu-id="fcb86-226">In hello applications list, select **ClickTime**.</span></span>

    ![Lien ClickTimne dans la liste des Applications hello](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_app.png) 

3. <span data-ttu-id="fcb86-228">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="fcb86-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202] 

4. <span data-ttu-id="fcb86-230">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="fcb86-230">Click **Add** button.</span></span> <span data-ttu-id="fcb86-231">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="fcb86-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="fcb86-233">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="fcb86-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="fcb86-234">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="fcb86-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fcb86-235">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="fcb86-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="fcb86-236">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="fcb86-236">Test single sign-on</span></span>

<span data-ttu-id="fcb86-237">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="fcb86-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="fcb86-238">Lorsque vous cliquez sur mosaïque ClickTime hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour ClickTime application.</span><span class="sxs-lookup"><span data-stu-id="fcb86-238">When you click hello ClickTime tile in hello Access Panel, you should get automatically signed-on tooyour ClickTime application.</span></span>
<span data-ttu-id="fcb86-239">Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fcb86-239">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fcb86-240">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="fcb86-240">Additional resources</span></span>

* [<span data-ttu-id="fcb86-241">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fcb86-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fcb86-242">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="fcb86-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_203.png

