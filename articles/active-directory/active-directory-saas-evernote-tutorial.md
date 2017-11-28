---
title: "Didacticiel : Intégration d’Azure Active Directory avec Evernote | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Evernote."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 4d7017e571ed12a0b155aa188c6b0ecb3c9898a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-evernote"></a><span data-ttu-id="7d7e1-103">Didacticiel : Intégration d’Azure Active Directory avec Evernote</span><span class="sxs-lookup"><span data-stu-id="7d7e1-103">Tutorial: Azure Active Directory integration with Evernote</span></span>

<span data-ttu-id="7d7e1-104">Dans ce didacticiel, vous apprendrez comment toointegrate Evernote avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7d7e1-104">In this tutorial, you learn how toointegrate Evernote with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7d7e1-105">Intégration Evernote à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="7d7e1-105">Integrating Evernote with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7d7e1-106">Vous pouvez contrôler dans Azure AD qui a accès tooEvernote.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-106">You can control in Azure AD who has access tooEvernote.</span></span>
- <span data-ttu-id="7d7e1-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooEvernote (Single Sign-On) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-107">You can enable your users tooautomatically get signed-on tooEvernote (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="7d7e1-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="7d7e1-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7d7e1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7d7e1-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7d7e1-110">Prerequisites</span></span>

<span data-ttu-id="7d7e1-111">tooconfigure intégration d’Azure AD avec Evernote, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="7d7e1-111">tooconfigure Azure AD integration with Evernote, you need hello following items:</span></span>

- <span data-ttu-id="7d7e1-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="7d7e1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7d7e1-113">Un abonnement Evernote pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="7d7e1-113">An Evernote single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7d7e1-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7d7e1-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="7d7e1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7d7e1-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7d7e1-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7d7e1-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7d7e1-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="7d7e1-118">Scenario description</span></span>
<span data-ttu-id="7d7e1-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7d7e1-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="7d7e1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7d7e1-121">Ajout de Evernote à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="7d7e1-121">Adding Evernote from hello gallery</span></span>
2. <span data-ttu-id="7d7e1-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="7d7e1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-evernote-from-hello-gallery"></a><span data-ttu-id="7d7e1-123">Ajout de Evernote à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="7d7e1-123">Adding Evernote from hello gallery</span></span>
<span data-ttu-id="7d7e1-124">intégration de hello tooconfigure de Evernote dans Azure AD, vous devez tooadd Evernote à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-124">tooconfigure hello integration of Evernote into Azure AD, you need tooadd Evernote from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7d7e1-125">**tooadd Evernote à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7d7e1-125">**tooadd Evernote from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7d7e1-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="7d7e1-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7d7e1-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-129">Then go too**All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="7d7e1-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="7d7e1-133">Dans la zone de recherche de hello, tapez **Evernote**, sélectionnez **Evernote** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-133">In hello search box, type **Evernote**, select **Evernote** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Evernote dans la liste des résultats hello](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7d7e1-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="7d7e1-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="7d7e1-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Evernote, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="7d7e1-136">In this section, you configure and test Azure AD single sign-on with Evernote based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7d7e1-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Evernote est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Evernote is tooa user in Azure AD.</span></span> <span data-ttu-id="7d7e1-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Evernote doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-138">In other words, a link relationship between an Azure AD user and hello related user in Evernote needs toobe established.</span></span>

<span data-ttu-id="7d7e1-139">Dans Evernote, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-139">In Evernote, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7d7e1-140">tooconfigure et test Azure AD l’authentification unique avec Evernote, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="7d7e1-140">tooconfigure and test Azure AD single sign-on with Evernote, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7d7e1-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7d7e1-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7d7e1-143">**[Créer un utilisateur de test Evernote](#create-an-evernote-test-user)**  -toohave un équivalent de Britta Simon dans Evernote est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-143">**[Create an Evernote test user](#create-an-evernote-test-user)** - toohave a counterpart of Britta Simon in Evernote that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7d7e1-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7d7e1-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7d7e1-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="7d7e1-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7d7e1-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Evernote.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Evernote application.</span></span>

<span data-ttu-id="7d7e1-148">**tooconfigure Azure AD single sign-on avec Evernote, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7d7e1-148">**tooconfigure Azure AD single sign-on with Evernote, perform hello following steps:**</span></span>

1. <span data-ttu-id="7d7e1-149">Bonjour portail Azure, sur hello **Evernote** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-149">In hello Azure portal, on hello **Evernote** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="7d7e1-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_samlbase.png)

3. <span data-ttu-id="7d7e1-153">Sur hello **Evernote domaine et les URL** section, effectuer hello comme suit si vous le souhaitez en mode initié par l’application hello tooconfigure IDP :</span><span class="sxs-lookup"><span data-stu-id="7d7e1-153">On hello **Evernote Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in IDP initiated mode:</span></span>

    ![Informations d’authentification unique dans Domaine et URL Evernote](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_url.png)

    <span data-ttu-id="7d7e1-155">Bonjour **identificateur** zone de texte, tapez l’URL hello :`https://www.evernote.com/saml2`</span><span class="sxs-lookup"><span data-stu-id="7d7e1-155">In hello **Identifier** textbox, type hello URL: `https://www.evernote.com/saml2`</span></span>

4. <span data-ttu-id="7d7e1-156">Vérifiez **afficher les paramètres d’URL avancés** et effectuer hello suivant l’étape si vous le souhaitez application hello tooconfigure **SP** en mode initié par :</span><span class="sxs-lookup"><span data-stu-id="7d7e1-156">Check **Show advanced URL settings** and perform hello following step if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Informations d’authentification unique dans Domaine et URL Evernote](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_url1.png)

    <span data-ttu-id="7d7e1-158">Bonjour **URL de connexion** zone de texte, tapez l’URL hello :`https://www.evernote.com/Login.action`</span><span class="sxs-lookup"><span data-stu-id="7d7e1-158">In hello **Sign on URL** textbox, type hello URL: `https://www.evernote.com/Login.action`</span></span>   

5. <span data-ttu-id="7d7e1-159">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-159">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_certificate.png) 

6. <span data-ttu-id="7d7e1-161">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="7d7e1-161">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-evernote-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="7d7e1-163">Sur hello **Evernote Configuration** , cliquez sur **Evernote de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-163">On hello **Evernote Configuration** section, click **Configure Evernote** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7d7e1-164">Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="7d7e1-164">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuration d’Evernote](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_configure.png) 

8. <span data-ttu-id="7d7e1-166">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Evernote en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-166">In a different web browser window, log into your Evernote company site as an administrator.</span></span>

9. <span data-ttu-id="7d7e1-167">Accédez trop**« Console d’administration »**</span><span class="sxs-lookup"><span data-stu-id="7d7e1-167">Go too**'Admin Console'**</span></span>

    ![Admin-Console](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

10. <span data-ttu-id="7d7e1-169">À partir de hello **'Console d’administration'**, accédez trop**'Security'** et sélectionnez **' Single Sign-On'**</span><span class="sxs-lookup"><span data-stu-id="7d7e1-169">From hello **'Admin Console'**, go too**‘Security’** and select **‘Single Sign-On’**</span></span>

    ![SSO-Setting](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_sso.png)

11. <span data-ttu-id="7d7e1-171">Configurer hello valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="7d7e1-171">Configure hello following values:</span></span>

    ![Certificate-Setting](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_certx.png)
    
    <span data-ttu-id="7d7e1-173">a.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-173">a.</span></span>  <span data-ttu-id="7d7e1-174">**Activer l’authentification unique :** l’authentification unique est activée par défaut (cliquez sur **désactiver Single Sign-on** exigence d’authentification unique tooremove hello)</span><span class="sxs-lookup"><span data-stu-id="7d7e1-174">**Enable SSO:** SSO is enabled by default (Click **Disable Single Sign-on** tooremove hello SSO requirement)</span></span>

    <span data-ttu-id="7d7e1-175">b.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-175">b.</span></span> <span data-ttu-id="7d7e1-176">Coller **SAML SSO Service URL** valeur, ce qui vous avez copié à partir de hello portail Azure en hello **URL de demande HTTP SAML** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-176">Paste **SAML Single sign-on Service URL** value, which you have copied from hello Azure portal into hello **SAML HTTP Request URL** textbox.</span></span>

    <span data-ttu-id="7d7e1-177">c.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-177">c.</span></span> <span data-ttu-id="7d7e1-178">Ouvrez le certificat téléchargé de hello d’Azure AD dans un contenu hello bloc-notes, puis copiez notamment « BEGIN CERTIFICATE » et « END CERTIFICATE » et le coller dans hello **certificat X.509** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-178">Open hello downloaded certificate from Azure AD in a notepad and copy hello content including "BEGIN CERTIFICATE" and "END CERTIFICATE" and paste it into hello **X.509 Certificate** textbox.</span></span> 

    <span data-ttu-id="7d7e1-179">d.Cliquez sur **Enregistrer les modifications**</span><span class="sxs-lookup"><span data-stu-id="7d7e1-179">d.Click **Save Changes**</span></span>

> [!TIP]
> <span data-ttu-id="7d7e1-180">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="7d7e1-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7d7e1-181">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7d7e1-182">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7d7e1-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7d7e1-183">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="7d7e1-183">Create an Azure AD test user</span></span>

<span data-ttu-id="7d7e1-184">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="7d7e1-186">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7d7e1-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7d7e1-187">Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-187">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-evernote-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="7d7e1-189">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-189">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-evernote-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="7d7e1-191">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-191">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![bouton Ajouter de Hello](./media/active-directory-saas-evernote-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="7d7e1-193">Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="7d7e1-193">In hello **User** dialog box, perform hello following steps:</span></span>

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-evernote-tutorial/create_aaduser_04.png)

    <span data-ttu-id="7d7e1-195">a.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-195">a.</span></span> <span data-ttu-id="7d7e1-196">Bonjour **nom** , tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-196">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7d7e1-197">b.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-197">b.</span></span> <span data-ttu-id="7d7e1-198">Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-198">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="7d7e1-199">c.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-199">c.</span></span> <span data-ttu-id="7d7e1-200">Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-200">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="7d7e1-201">d.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-201">d.</span></span> <span data-ttu-id="7d7e1-202">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-202">Click **Create**.</span></span>
 
### <a name="create-an-evernote-test-user"></a><span data-ttu-id="7d7e1-203">Créer un utilisateur de test Evernote</span><span class="sxs-lookup"><span data-stu-id="7d7e1-203">Create an Evernote test user</span></span>

<span data-ttu-id="7d7e1-204">Dans l’ordre tooenable Azure AD les utilisateurs toolog dans Evernote, ils doivent être configurés dans Evernote.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-204">In order tooenable Azure AD users toolog into Evernote, they must be provisioned into Evernote.</span></span>  
<span data-ttu-id="7d7e1-205">Dans les cas de hello de Evernote, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-205">In hello case of Evernote, provisioning is a manual task.</span></span>

<span data-ttu-id="7d7e1-206">**effectuer des comptes d’utilisateur, tooprovision hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7d7e1-206">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="7d7e1-207">Ouvrez une session dans tooyour Evernote site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-207">Log in tooyour Evernote company site as an administrator.</span></span>

2. <span data-ttu-id="7d7e1-208">Cliquez sur hello **'Console d’administration'**.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-208">Click hello **'Admin Console'**.</span></span>

    ![Admin-Console](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

3. <span data-ttu-id="7d7e1-210">À partir de hello **'Console d’administration'**, accédez trop**ajouter des utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-210">From hello **'Admin Console'**, go too**‘Add users’**.</span></span>

    ![Add-testUser](./media/active-directory-saas-evernote-tutorial/create_aaduser_0001.png)

4. <span data-ttu-id="7d7e1-212">**Ajouter des membres de l’équipe** Bonjour **messagerie** zone de texte, tapez l’adresse de messagerie hello du compte d’utilisateur et cliquez sur **l’invitation.**</span><span class="sxs-lookup"><span data-stu-id="7d7e1-212">**Add team members** in hello **Email** textbox, type hello email address of user account and click **Invite.**</span></span>

    ![Add-testUser](./media/active-directory-saas-evernote-tutorial/create_aaduser_0002.png)
    
5. <span data-ttu-id="7d7e1-214">Après l’envoi de l’invitation, titulaire du compte Azure Active Directory hello recevra un e-mail d’invitation tooaccept hello.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-214">After invitation is sent, hello Azure Active Directory account holder will receive an email tooaccept hello invitation.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="7d7e1-215">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="7d7e1-215">Assign hello Azure AD test user</span></span>

<span data-ttu-id="7d7e1-216">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooEvernote.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEvernote.</span></span>

![Attribuer le rôle d’utilisateur hello][200] 

<span data-ttu-id="7d7e1-218">**tooassign Britta Simon tooEvernote, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7d7e1-218">**tooassign Britta Simon tooEvernote, perform hello following steps:**</span></span>

1. <span data-ttu-id="7d7e1-219">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="7d7e1-221">Dans la liste des applications hello, sélectionnez **Evernote**.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-221">In hello applications list, select **Evernote**.</span></span>

    ![lien de Evernote Hello dans la liste des Applications hello](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_app.png)  

3. <span data-ttu-id="7d7e1-223">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202]

4. <span data-ttu-id="7d7e1-225">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-225">Click **Add** button.</span></span> <span data-ttu-id="7d7e1-226">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="7d7e1-228">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7d7e1-229">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7d7e1-230">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7d7e1-231">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="7d7e1-231">Test single sign-on</span></span>

<span data-ttu-id="7d7e1-232">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-232">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7d7e1-233">Lorsque vous cliquez sur mosaïque Evernote hello hello volet d’accès, vous devez obtenir connecté tooyour Evernote application.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-233">When you click hello Evernote tile in hello Access Panel, you should get signed-on tooyour Evernote application.</span></span> <span data-ttu-id="7d7e1-234">Vous allez être journalisation comme un compte d’organisation mais puis besoin toolog avec votre compte personnel.</span><span class="sxs-lookup"><span data-stu-id="7d7e1-234">You'll be logging in as an Organization account but then need toolog in with your personal account.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7d7e1-235">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="7d7e1-235">Additional resources</span></span>

* [<span data-ttu-id="7d7e1-236">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7d7e1-236">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7d7e1-237">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="7d7e1-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_203.png

