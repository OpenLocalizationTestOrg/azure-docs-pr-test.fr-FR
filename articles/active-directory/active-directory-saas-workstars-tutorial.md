---
title: "Didacticiel : Intégration d’Azure Active Directory à Workstars | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Workstars."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 51a4a4e4-ff60-4971-b3f8-a0367b70d220
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: 86250d7538f058d2a821ded7dda0b2fc185d80df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workstars"></a><span data-ttu-id="2e515-103">Didacticiel : Intégration d’Azure Active Directory à Workstars</span><span class="sxs-lookup"><span data-stu-id="2e515-103">Tutorial: Azure Active Directory integration with Workstars</span></span>

<span data-ttu-id="2e515-104">Dans ce didacticiel, vous apprendrez comment toointegrate Workstars avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2e515-104">In this tutorial, you learn how toointegrate Workstars with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2e515-105">Intégration Workstars à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="2e515-105">Integrating Workstars with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2e515-106">Vous pouvez contrôler dans Azure AD qui a accès tooWorkstars.</span><span class="sxs-lookup"><span data-stu-id="2e515-106">You can control in Azure AD who has access tooWorkstars.</span></span>
- <span data-ttu-id="2e515-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooWorkstars (Single Sign-On) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2e515-107">You can enable your users tooautomatically get signed-on tooWorkstars (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="2e515-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2e515-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="2e515-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2e515-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2e515-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="2e515-110">Prerequisites</span></span>

<span data-ttu-id="2e515-111">tooconfigure intégration d’Azure AD avec Workstars, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="2e515-111">tooconfigure Azure AD integration with Workstars, you need hello following items:</span></span>

- <span data-ttu-id="2e515-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e515-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2e515-113">Un abonnement Workstars pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="2e515-113">A Workstars single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2e515-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="2e515-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2e515-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="2e515-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2e515-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="2e515-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2e515-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2e515-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2e515-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="2e515-118">Scenario description</span></span>
<span data-ttu-id="2e515-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="2e515-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2e515-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="2e515-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2e515-121">Ajout de Workstars à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="2e515-121">Adding Workstars from hello gallery</span></span>
2. <span data-ttu-id="2e515-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e515-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workstars-from-hello-gallery"></a><span data-ttu-id="2e515-123">Ajout de Workstars à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="2e515-123">Adding Workstars from hello gallery</span></span>
<span data-ttu-id="2e515-124">intégration de hello tooconfigure de Workstars dans Azure AD, vous devez tooadd Workstars à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="2e515-124">tooconfigure hello integration of Workstars into Azure AD, you need tooadd Workstars from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2e515-125">**tooadd Workstars à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2e515-125">**tooadd Workstars from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2e515-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="2e515-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="2e515-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="2e515-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2e515-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="2e515-129">Then go too**All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="2e515-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="2e515-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="2e515-133">Dans la zone de recherche de hello, tapez **Workstars**, sélectionnez **Workstars** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="2e515-133">In hello search box, type **Workstars**, select **Workstars** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Workstars dans la liste des résultats hello](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="2e515-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e515-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="2e515-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Workstars avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="2e515-136">In this section, you configure and test Azure AD single sign-on with Workstars based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2e515-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Workstars est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2e515-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workstars is tooa user in Azure AD.</span></span> <span data-ttu-id="2e515-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Workstars doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="2e515-138">In other words, a link relationship between an Azure AD user and hello related user in Workstars needs toobe established.</span></span>

<span data-ttu-id="2e515-139">Dans Workstars, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="2e515-139">In Workstars, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2e515-140">tooconfigure et test Azure AD l’authentification unique avec Workstars, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="2e515-140">tooconfigure and test Azure AD single sign-on with Workstars, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2e515-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="2e515-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2e515-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2e515-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2e515-143">**[Créer un utilisateur de test Workstars](#create-a-workstars-test-user)**  -toohave un équivalent de Britta Simon dans Workstars est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2e515-143">**[Create a Workstars test user](#create-a-workstars-test-user)** - toohave a counterpart of Britta Simon in Workstars that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2e515-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="2e515-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2e515-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="2e515-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="2e515-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e515-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="2e515-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Workstars.</span><span class="sxs-lookup"><span data-stu-id="2e515-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workstars application.</span></span>

<span data-ttu-id="2e515-148">**tooconfigure Azure AD single sign-on avec Workstars, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2e515-148">**tooconfigure Azure AD single sign-on with Workstars, perform hello following steps:**</span></span>

1. <span data-ttu-id="2e515-149">Bonjour portail Azure, sur hello **Workstars** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="2e515-149">In hello Azure portal, on hello **Workstars** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="2e515-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="2e515-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_samlbase.png)

3. <span data-ttu-id="2e515-153">Sur hello **Workstars domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="2e515-153">On hello **Workstars Domain and URLs** section, perform hello following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_url.png)

    <span data-ttu-id="2e515-155">a.</span><span class="sxs-lookup"><span data-stu-id="2e515-155">a.</span></span> <span data-ttu-id="2e515-156">Bonjour **identificateur** zone de texte, tapez l’URL hello :`https://workstars.com`</span><span class="sxs-lookup"><span data-stu-id="2e515-156">In hello **Identifier** textbox, type hello URL: `https://workstars.com`</span></span>

    <span data-ttu-id="2e515-157">b.</span><span class="sxs-lookup"><span data-stu-id="2e515-157">b.</span></span> <span data-ttu-id="2e515-158">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.workstars.com/saml/login_check`</span><span class="sxs-lookup"><span data-stu-id="2e515-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.workstars.com/saml/login_check`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2e515-159">valeur de Hello n’est pas réelle.</span><span class="sxs-lookup"><span data-stu-id="2e515-159">hello value is not real.</span></span> <span data-ttu-id="2e515-160">Valeur de hello de mise à jour avec hello URL de réponse réelle.</span><span class="sxs-lookup"><span data-stu-id="2e515-160">Update hello value with hello actual Reply URL.</span></span> <span data-ttu-id="2e515-161">Contact [Workstars l’équipe de support](https://support.workstars.com) valeur hello de tooget.</span><span class="sxs-lookup"><span data-stu-id="2e515-161">Contact [Workstars support team](https://support.workstars.com) tooget hello value.</span></span>
 
4. <span data-ttu-id="2e515-162">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="2e515-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_certificate.png) 

5. <span data-ttu-id="2e515-164">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="2e515-164">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-workstars-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2e515-166">Sur hello **Workstars Configuration** , cliquez sur **Workstars de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="2e515-166">On hello **Workstars Configuration** section, click **Configure Workstars** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="2e515-167">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="2e515-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuration de Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_configure.png) 

7. <span data-ttu-id="2e515-169">Dans une autre fenêtre de navigateur, connectez-vous sur le site d’entreprise tooyour Workstars en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="2e515-169">In another browser window, sign on tooyour Workstars company site as an administrator.</span></span>

8. <span data-ttu-id="2e515-170">Dans la barre d’outils principale hello, cliquez sur **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="2e515-170">In hello main toolbar, click **Settings**.</span></span>

    ![Paramètres Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_sett.png)

9. <span data-ttu-id="2e515-172">Accédez trop**authentification** > **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="2e515-172">Go too**Sign On** > **Settings**.</span></span>

    ![Connexion à Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_signon.png)

    ![Paramètres Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_settings.png)

10. <span data-ttu-id="2e515-175">Sur hello **unique signe sur (SAML) - paramètres** page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="2e515-175">On hello **Single Sign On (SAML) - Settings** page, perform hello following steps:</span></span>
    
    ![Workstars saml](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_saml.png)

    <span data-ttu-id="2e515-177">a.</span><span class="sxs-lookup"><span data-stu-id="2e515-177">a.</span></span> <span data-ttu-id="2e515-178">Dans la zone de texte **Identity Provider Name** (Nom du fournisseur d’identité), entrez **Office 365**.</span><span class="sxs-lookup"><span data-stu-id="2e515-178">In **Identity Provider Name** textbox, type **Office 365**.</span></span>

    <span data-ttu-id="2e515-179">b.</span><span class="sxs-lookup"><span data-stu-id="2e515-179">b.</span></span> <span data-ttu-id="2e515-180">Bonjour **Entity ID fournisseur d’identité** zone de texte, valeur hello coller **ID d’entité SAML**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2e515-180">In hello **Identity Provider Entity ID** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="2e515-181">c.</span><span class="sxs-lookup"><span data-stu-id="2e515-181">c.</span></span> <span data-ttu-id="2e515-182">Copie du fichier de certificat téléchargé hello hello dans le bloc-notes, puis collez-le dans hello **x509 certificat** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="2e515-182">Copy hello content of hello downloaded certificate file in notepad, and then paste it into hello **x509 Certificate** textbox.</span></span> 

    <span data-ttu-id="2e515-183">d.</span><span class="sxs-lookup"><span data-stu-id="2e515-183">d.</span></span> <span data-ttu-id="2e515-184">Bonjour **URL SSO SAML** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2e515-184">In hello **SAML SSO URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="2e515-185">e.</span><span class="sxs-lookup"><span data-stu-id="2e515-185">e.</span></span> <span data-ttu-id="2e515-186">Bonjour **URL de déconnexion distante** zone de texte, valeur hello coller **URL de déconnexion**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2e515-186">In hello **Remote Logout URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="2e515-187">f.</span><span class="sxs-lookup"><span data-stu-id="2e515-187">f.</span></span> <span data-ttu-id="2e515-188">Sélectionnez **ID de nom** en tant qu’**adresse électronique (par défaut)**.</span><span class="sxs-lookup"><span data-stu-id="2e515-188">select **Name ID** as **Email (Default)**.</span></span>

    <span data-ttu-id="2e515-189">g.</span><span class="sxs-lookup"><span data-stu-id="2e515-189">g.</span></span> <span data-ttu-id="2e515-190">Cliquez sur **Confirmer**.</span><span class="sxs-lookup"><span data-stu-id="2e515-190">Click **Confirm**.</span></span>
    
> [!TIP]
> <span data-ttu-id="2e515-191">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="2e515-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2e515-192">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="2e515-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2e515-193">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2e515-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="2e515-194">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e515-194">Create an Azure AD test user</span></span>

<span data-ttu-id="2e515-195">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="2e515-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="2e515-197">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2e515-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2e515-198">Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.</span><span class="sxs-lookup"><span data-stu-id="2e515-198">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-workstars-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="2e515-200">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="2e515-200">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-workstars-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="2e515-202">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="2e515-202">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![bouton Ajouter de Hello](./media/active-directory-saas-workstars-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="2e515-204">Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="2e515-204">In hello **User** dialog box, perform hello following steps:</span></span>

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-workstars-tutorial/create_aaduser_04.png)

    <span data-ttu-id="2e515-206">a.</span><span class="sxs-lookup"><span data-stu-id="2e515-206">a.</span></span> <span data-ttu-id="2e515-207">Bonjour **nom** , tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2e515-207">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2e515-208">b.</span><span class="sxs-lookup"><span data-stu-id="2e515-208">b.</span></span> <span data-ttu-id="2e515-209">Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2e515-209">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="2e515-210">c.</span><span class="sxs-lookup"><span data-stu-id="2e515-210">c.</span></span> <span data-ttu-id="2e515-211">Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.</span><span class="sxs-lookup"><span data-stu-id="2e515-211">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="2e515-212">d.</span><span class="sxs-lookup"><span data-stu-id="2e515-212">d.</span></span> <span data-ttu-id="2e515-213">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="2e515-213">Click **Create**.</span></span>
  
### <a name="create-a-workstars-test-user"></a><span data-ttu-id="2e515-214">Créer un utilisateur de test Workstars</span><span class="sxs-lookup"><span data-stu-id="2e515-214">Create a Workstars test user</span></span>

<span data-ttu-id="2e515-215">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Workstars.</span><span class="sxs-lookup"><span data-stu-id="2e515-215">In this section, you create a user called Britta Simon in Workstars.</span></span> <span data-ttu-id="2e515-216">Travailler avec [Workstars l’équipe de support](https://support.workstars.com) utilisateurs hello tooadd plate-forme de Workstars hello.</span><span class="sxs-lookup"><span data-stu-id="2e515-216">Work with [Workstars support team](https://support.workstars.com) tooadd hello users in hello Workstars platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="2e515-217">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e515-217">Assign hello Azure AD test user</span></span>

<span data-ttu-id="2e515-218">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooWorkstars.</span><span class="sxs-lookup"><span data-stu-id="2e515-218">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkstars.</span></span>

![Attribuer le rôle d’utilisateur hello][200] 

<span data-ttu-id="2e515-220">**tooassign Britta Simon tooWorkstars, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2e515-220">**tooassign Britta Simon tooWorkstars, perform hello following steps:**</span></span>

1. <span data-ttu-id="2e515-221">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="2e515-221">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="2e515-223">Dans la liste des applications hello, sélectionnez **Workstars**.</span><span class="sxs-lookup"><span data-stu-id="2e515-223">In hello applications list, select **Workstars**.</span></span>

    ![lien de Workstars Hello dans la liste des Applications hello](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_app.png)  

3. <span data-ttu-id="2e515-225">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="2e515-225">In hello menu on hello left, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202]

4. <span data-ttu-id="2e515-227">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="2e515-227">Click **Add** button.</span></span> <span data-ttu-id="2e515-228">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="2e515-228">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="2e515-230">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="2e515-230">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2e515-231">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="2e515-231">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2e515-232">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="2e515-232">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="2e515-233">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="2e515-233">Test single sign-on</span></span>

<span data-ttu-id="2e515-234">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="2e515-234">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2e515-235">Lorsque vous cliquez sur hello Workstars vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour Workstars application.</span><span class="sxs-lookup"><span data-stu-id="2e515-235">When you click hello Workstars tile in hello Access Panel, you should get automatically signed-on tooyour Workstars application.</span></span>
<span data-ttu-id="2e515-236">Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2e515-236">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="2e515-237">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="2e515-237">Additional resources</span></span>

* [<span data-ttu-id="2e515-238">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2e515-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2e515-239">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="2e515-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_203.png

