---
title: "Didacticiel : Intégration d’Azure Active Directory avec Pagerduty | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de PagerDuty."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0410456a-76f7-42a7-9bb5-f767de75a0e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: c3cfbedac3bf075e2d8cd833d5de7ca0bc9468b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pagerduty"></a><span data-ttu-id="e3ab1-103">Didacticiel : Intégration d’Azure Active Directory à Pagerduty</span><span class="sxs-lookup"><span data-stu-id="e3ab1-103">Tutorial: Azure Active Directory integration with PagerDuty</span></span>

<span data-ttu-id="e3ab1-104">Dans ce didacticiel, vous apprendrez comment toointegrate PagerDuty avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e3ab1-104">In this tutorial, you learn how toointegrate PagerDuty with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e3ab1-105">Intégration de PagerDuty à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="e3ab1-105">Integrating PagerDuty with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e3ab1-106">Vous pouvez contrôler dans Azure AD qui a accès tooPagerDuty</span><span class="sxs-lookup"><span data-stu-id="e3ab1-106">You can control in Azure AD who has access tooPagerDuty</span></span>
- <span data-ttu-id="e3ab1-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooPagerDuty (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3ab1-107">You can enable your users tooautomatically get signed-on tooPagerDuty (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e3ab1-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="e3ab1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e3ab1-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e3ab1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e3ab1-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e3ab1-110">Prerequisites</span></span>

<span data-ttu-id="e3ab1-111">tooconfigure intégration d’Azure AD à PagerDuty, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="e3ab1-111">tooconfigure Azure AD integration with PagerDuty, you need hello following items:</span></span>

- <span data-ttu-id="e3ab1-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3ab1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e3ab1-113">Un abonnement PagerDuty pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="e3ab1-113">A PagerDuty single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e3ab1-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e3ab1-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="e3ab1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e3ab1-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e3ab1-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e3ab1-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e3ab1-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="e3ab1-118">Scenario description</span></span>
<span data-ttu-id="e3ab1-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e3ab1-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="e3ab1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e3ab1-121">Ajout de PagerDuty à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="e3ab1-121">Adding PagerDuty from hello gallery</span></span>
2. <span data-ttu-id="e3ab1-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3ab1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pagerduty-from-hello-gallery"></a><span data-ttu-id="e3ab1-123">Ajout de PagerDuty à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="e3ab1-123">Adding PagerDuty from hello gallery</span></span>
<span data-ttu-id="e3ab1-124">intégration de hello tooconfigure de PagerDuty dans Azure AD, vous devez tooadd PagerDuty à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-124">tooconfigure hello integration of PagerDuty into Azure AD, you need tooadd PagerDuty from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e3ab1-125">**tooadd PagerDuty à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e3ab1-125">**tooadd PagerDuty from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e3ab1-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="e3ab1-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e3ab1-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-129">Then go too**All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="e3ab1-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="e3ab1-133">Dans la zone de recherche de hello, tapez **PagerDuty**, sélectionnez **PagerDuty** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-133">In hello search box, type **PagerDuty**, select  **PagerDuty**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e3ab1-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3ab1-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="e3ab1-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec PagerDuty, par le biais d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="e3ab1-136">In this section, you configure and test Azure AD single sign-on with PagerDuty based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e3ab1-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans PagerDuty est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PagerDuty is tooa user in Azure AD.</span></span> <span data-ttu-id="e3ab1-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans PagerDuty doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-138">In other words, a link relationship between an Azure AD user and hello related user in PagerDuty needs toobe established.</span></span>

<span data-ttu-id="e3ab1-139">Dans PagerDuty, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-139">In PagerDuty, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e3ab1-140">tooconfigure et test Azure AD l’authentification unique à PagerDuty, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="e3ab1-140">tooconfigure and test Azure AD single sign-on with PagerDuty, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e3ab1-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e3ab1-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e3ab1-143">**[Créer un utilisateur de test de PagerDuty](#create-a-pagerduty-test-user)**  -toohave un équivalent de Britta Simon dans PagerDuty est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-143">**[Create a PagerDuty test user](#create-a-pagerduty-test-user)** - toohave a counterpart of Britta Simon in PagerDuty that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e3ab1-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e3ab1-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e3ab1-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3ab1-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e3ab1-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your PagerDuty application.</span></span>

<span data-ttu-id="e3ab1-148">**tooconfigure Azure AD single sign-on avec PagerDuty, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e3ab1-148">**tooconfigure Azure AD single sign-on with PagerDuty, perform hello following steps:**</span></span>

1. <span data-ttu-id="e3ab1-149">Bonjour portail Azure, sur hello **PagerDuty** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-149">In hello Azure portal, on hello **PagerDuty** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="e3ab1-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_samlbase.png)

3. <span data-ttu-id="e3ab1-153">Sur hello **PagerDuty domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e3ab1-153">On hello **PagerDuty Domain and URLs** section, perform hello following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL PagerDuty](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_url.png)

    <span data-ttu-id="e3ab1-155">a.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-155">a.</span></span> <span data-ttu-id="e3ab1-156">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<tenant-name>.pagerduty.com`</span><span class="sxs-lookup"><span data-stu-id="e3ab1-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.pagerduty.com`</span></span>

    <span data-ttu-id="e3ab1-157">b.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-157">b.</span></span> <span data-ttu-id="e3ab1-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<tenant-name>.pagerduty.com`</span><span class="sxs-lookup"><span data-stu-id="e3ab1-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenant-name>.pagerduty.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e3ab1-159">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-159">These values are not real.</span></span> <span data-ttu-id="e3ab1-160">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e3ab1-161">Contact [équipe de support Client de PagerDuty](https://www.pagerduty.com/support/) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-161">Contact [PagerDuty Client support team](https://www.pagerduty.com/support/) tooget these values.</span></span> 

4. <span data-ttu-id="e3ab1-162">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-162">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_certificate.png) 

5. <span data-ttu-id="e3ab1-164">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="e3ab1-164">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-pagerduty-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e3ab1-166">Sur hello **PagerDuty Configuration** , cliquez sur **configurer de PagerDuty** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-166">On hello **PagerDuty Configuration** section, click **Configure PagerDuty** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e3ab1-167">Hello de copie **URL de déconnexion et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="e3ab1-167">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuration de PagerDuty](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_configure.png) 

7. <span data-ttu-id="e3ab1-169">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Pagerduty en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-169">In a different web browser window, log into your Pagerduty company site as an administrator.</span></span>

8. <span data-ttu-id="e3ab1-170">Dans le menu hello haut de hello, cliquez sur **les paramètres de compte**.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-170">In hello menu on hello top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="e3ab1-171">![Paramètres de compte](./media/active-directory-saas-pagerduty-tutorial/ic778535.png "Paramètres de compte")</span><span class="sxs-lookup"><span data-stu-id="e3ab1-171">![Account Settings](./media/active-directory-saas-pagerduty-tutorial/ic778535.png "Account Settings")</span></span>

9. <span data-ttu-id="e3ab1-172">Cliquez sur **Single Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-172">Click **Single Sign-on**.</span></span>
   
    <span data-ttu-id="e3ab1-173">![Authentification unique](./media/active-directory-saas-pagerduty-tutorial/ic778536.png "Authentification unique")</span><span class="sxs-lookup"><span data-stu-id="e3ab1-173">![Single sign-on](./media/active-directory-saas-pagerduty-tutorial/ic778536.png "Single sign-on")</span></span>

10. <span data-ttu-id="e3ab1-174">Sur hello **activer Single Sign-on (SSO)** page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e3ab1-174">On hello **Enable Single Sign-on (SSO)** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="e3ab1-175">![Activer l’authentification unique](./media/active-directory-saas-pagerduty-tutorial/ic778537.png "activer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="e3ab1-175">![Enable single sign-on](./media/active-directory-saas-pagerduty-tutorial/ic778537.png "Enable single sign-on")</span></span>
   
    <span data-ttu-id="e3ab1-176">a.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-176">a.</span></span> <span data-ttu-id="e3ab1-177">Ouvrez votre certificat codé en base 64 téléchargé à partir du portail Azure dans le bloc-notes, hello copie contenu de celui-ci dans le Presse-papiers et le coller ensuite toohello **certificat X.509** zone de texte</span><span class="sxs-lookup"><span data-stu-id="e3ab1-177">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox</span></span>
  
    <span data-ttu-id="e3ab1-178">b.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-178">b.</span></span> <span data-ttu-id="e3ab1-179">Bonjour **URL de connexion** zone de texte, collez **SAML Sign-On URL du Service unique** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-179">In hello **Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="e3ab1-180">c.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-180">c.</span></span> <span data-ttu-id="e3ab1-181">Bonjour **URL de déconnexion** zone de texte, collez **URL de déconnexion** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-181">In hello **Logout URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="e3ab1-182">d.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-182">d.</span></span> <span data-ttu-id="e3ab1-183">Sélectionnez **Turn on Single Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-183">Select **Turn on Single Sign-on**.</span></span>
 
    <span data-ttu-id="e3ab1-184">e.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-184">e.</span></span> <span data-ttu-id="e3ab1-185">Cliquez sur **Enregistrer les modifications**.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-185">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="e3ab1-186">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="e3ab1-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e3ab1-187">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e3ab1-188">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e3ab1-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e3ab1-189">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3ab1-189">Create an Azure AD test user</span></span>

<span data-ttu-id="e3ab1-190">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="e3ab1-192">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e3ab1-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e3ab1-193">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-193">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e3ab1-195">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-195">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e3ab1-197">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-197">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![bouton Ajouter de Hello](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e3ab1-199">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e3ab1-199">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e3ab1-201">a.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-201">a.</span></span> <span data-ttu-id="e3ab1-202">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-202">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e3ab1-203">b.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-203">b.</span></span> <span data-ttu-id="e3ab1-204">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-204">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e3ab1-205">c.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-205">c.</span></span> <span data-ttu-id="e3ab1-206">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-206">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e3ab1-207">d.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-207">d.</span></span> <span data-ttu-id="e3ab1-208">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-208">Click **Create**.</span></span>
 
### <a name="create-a-pagerduty-test-user"></a><span data-ttu-id="e3ab1-209">Créer un utilisateur de test PagerDuty</span><span class="sxs-lookup"><span data-stu-id="e3ab1-209">Create a PagerDuty test user</span></span>

<span data-ttu-id="e3ab1-210">tooenable Azure AD les utilisateurs toolog dans tooPagerDuty, vous devez les configurer dans PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-210">tooenable Azure AD users toolog in tooPagerDuty, they must be provisioned into PagerDuty.</span></span>  
<span data-ttu-id="e3ab1-211">Dans les cas de hello de PagerDuty, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-211">In hello case of PagerDuty, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="e3ab1-212">Vous pouvez utiliser n’importe quel autre Pagerduty utilisateur compte outil de création ou API fournie par Pagerduty tooprovision Azure Active Directory des comptes d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-212">You can use any other Pagerduty user account creation tools or APIs provided by Pagerduty tooprovision Azure Active Directory user accounts.</span></span>

<span data-ttu-id="e3ab1-213">**tooprovision un compte d’utilisateur, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e3ab1-213">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="e3ab1-214">Connectez-vous à tooyour **Pagerduty** client.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-214">Log in tooyour **Pagerduty** tenant.</span></span>

2. <span data-ttu-id="e3ab1-215">Dans le menu hello haut de hello, cliquez sur **utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-215">In hello menu on hello top, click **Users**.</span></span>

3. <span data-ttu-id="e3ab1-216">Cliquez sur **Add Users**.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-216">Click **Add Users**.</span></span>
   
    <span data-ttu-id="e3ab1-217">![Ajouter des utilisateurs](./media/active-directory-saas-pagerduty-tutorial/ic778539.png "ajouter des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="e3ab1-217">![Add Users](./media/active-directory-saas-pagerduty-tutorial/ic778539.png "Add Users")</span></span>

4.  <span data-ttu-id="e3ab1-218">Sur hello **inviter votre équipe** boîte de dialogue, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e3ab1-218">On hello **Invite your team** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="e3ab1-219">![Inviter votre équipe](./media/active-directory-saas-pagerduty-tutorial/ic778540.png "inviter votre équipe")</span><span class="sxs-lookup"><span data-stu-id="e3ab1-219">![Invite your team](./media/active-directory-saas-pagerduty-tutorial/ic778540.png "Invite your team")</span></span>

    <span data-ttu-id="e3ab1-220">a.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-220">a.</span></span> <span data-ttu-id="e3ab1-221">Hello de type **prénom et nom** d’utilisateur comme **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-221">Type hello **First and Last Name** of user like **Britta Simon**.</span></span> 
   
    <span data-ttu-id="e3ab1-222">b.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-222">b.</span></span> <span data-ttu-id="e3ab1-223">Entrez l’**adresse e-mail** d’un utilisateur, par exemple **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-223">Enter **Email** address of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="e3ab1-224">c.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-224">c.</span></span> <span data-ttu-id="e3ab1-225">Cliquez sur **Add**, puis sur **Send Invites**.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-225">Click **Add**, and then click **Send Invites**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="e3ab1-226">Tous les utilisateurs ajoutés reçoivent une invitation de toocreate un compte PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-226">All added users will receive an invite toocreate a PagerDuty account.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="e3ab1-227">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3ab1-227">Assign hello Azure AD test user</span></span>

<span data-ttu-id="e3ab1-228">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooPagerDuty.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPagerDuty.</span></span>

![Attribuer le rôle d’utilisateur hello][200]

<span data-ttu-id="e3ab1-230">**tooassign Britta Simon tooPagerDuty, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e3ab1-230">**tooassign Britta Simon tooPagerDuty, perform hello following steps:**</span></span>

1. <span data-ttu-id="e3ab1-231">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-231">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="e3ab1-233">Dans la liste des applications hello, sélectionnez **PagerDuty**.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-233">In hello applications list, select **PagerDuty**.</span></span>

    ![lien de PagerDuty Hello dans la liste des Applications hello](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_app.png) 

3. <span data-ttu-id="e3ab1-235">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202]

4. <span data-ttu-id="e3ab1-237">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-237">Click **Add** button.</span></span> <span data-ttu-id="e3ab1-238">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="e3ab1-240">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e3ab1-241">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e3ab1-242">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e3ab1-243">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="e3ab1-243">Test single sign-on</span></span>

<span data-ttu-id="e3ab1-244">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-244">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e3ab1-245">Lorsque vous cliquez sur mosaïque PagerDuty hello hello accès Panelyou doit obtenir automatiquement signé sur tooyour PagerDuty application.</span><span class="sxs-lookup"><span data-stu-id="e3ab1-245">When you click hello PagerDuty tile in hello Access Panelyou should get automatically signed-on tooyour PagerDuty application.</span></span>

<span data-ttu-id="e3ab1-246">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e3ab1-246">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e3ab1-247">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="e3ab1-247">Additional resources</span></span>

* [<span data-ttu-id="e3ab1-248">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e3ab1-248">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e3ab1-249">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="e3ab1-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_203.png

