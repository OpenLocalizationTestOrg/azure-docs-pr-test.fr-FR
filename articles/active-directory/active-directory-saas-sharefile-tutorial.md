---
title: "Didacticiel : Intégration d’Azure Active Directory à Citrix ShareFile | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Citrix ShareFile."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: e14fc310-bac4-4f09-99ef-87e5c77288b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2017
ms.author: jeedes
ms.openlocfilehash: d7eaf140e56c40f9f621062849dd8558588ffd1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-sharefile"></a><span data-ttu-id="6612d-103">Didacticiel : Intégration d’Azure Active Directory à Citrix ShareFile</span><span class="sxs-lookup"><span data-stu-id="6612d-103">Tutorial: Azure Active Directory integration with Citrix ShareFile</span></span>

<span data-ttu-id="6612d-104">Dans ce didacticiel, vous apprendrez comment toointegrate Citrix ShareFile avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6612d-104">In this tutorial, you learn how toointegrate Citrix ShareFile with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6612d-105">Intégration de Citrix ShareFile à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="6612d-105">Integrating Citrix ShareFile with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6612d-106">Vous pouvez contrôler dans Azure AD qui a accès tooCitrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="6612d-106">You can control in Azure AD who has access tooCitrix ShareFile.</span></span>
- <span data-ttu-id="6612d-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooCitrix ShareFile (Single Sign-On) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6612d-107">You can enable your users tooautomatically get signed-on tooCitrix ShareFile (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="6612d-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="6612d-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="6612d-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6612d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6612d-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="6612d-110">Prerequisites</span></span>

<span data-ttu-id="6612d-111">tooconfigure intégration d’Azure AD avec Citrix ShareFile, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="6612d-111">tooconfigure Azure AD integration with Citrix ShareFile, you need hello following items:</span></span>

- <span data-ttu-id="6612d-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="6612d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6612d-113">Un abonnement Citrix ShareFile pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="6612d-113">A Citrix ShareFile single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6612d-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="6612d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6612d-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="6612d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6612d-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="6612d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6612d-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6612d-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6612d-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="6612d-118">Scenario description</span></span>
<span data-ttu-id="6612d-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="6612d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6612d-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="6612d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6612d-121">Ajouter Citrix ShareFile à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="6612d-121">Add Citrix ShareFile from hello gallery</span></span>
2. <span data-ttu-id="6612d-122">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="6612d-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-citrix-sharefile-from-hello-gallery"></a><span data-ttu-id="6612d-123">Ajouter Citrix ShareFile à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="6612d-123">Add Citrix ShareFile from hello gallery</span></span>
<span data-ttu-id="6612d-124">tooconfigure hello intégration de Citrix ShareFile dans Azure AD, vous devez tooadd Citrix ShareFile à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="6612d-124">tooconfigure hello integration of Citrix ShareFile into Azure AD, you need tooadd Citrix ShareFile from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6612d-125">**tooadd Citrix ShareFile à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6612d-125">**tooadd Citrix ShareFile from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6612d-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="6612d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="6612d-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="6612d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6612d-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="6612d-129">Then go too**All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="6612d-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="6612d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="6612d-133">Dans la zone de recherche de hello, tapez **Citrix ShareFile**, sélectionnez **Citrix ShareFile** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="6612d-133">In hello search box, type **Citrix ShareFile**, select **Citrix ShareFile** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Liste des résultats de Citrix ShareFile Bonjour](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="6612d-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="6612d-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="6612d-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Citrix ShareFile avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="6612d-136">In this section, you configure and test Azure AD single sign-on with Citrix ShareFile based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6612d-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Citrix ShareFile est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6612d-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Citrix ShareFile is tooa user in Azure AD.</span></span> <span data-ttu-id="6612d-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Citrix ShareFile doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="6612d-138">In other words, a link relationship between an Azure AD user and hello related user in Citrix ShareFile needs toobe established.</span></span>

<span data-ttu-id="6612d-139">Dans Citrix ShareFile, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="6612d-139">In Citrix ShareFile, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6612d-140">tooconfigure et test Azure AD l’authentification unique avec Citrix ShareFile, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="6612d-140">tooconfigure and test Azure AD single sign-on with Citrix ShareFile, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6612d-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="6612d-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6612d-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6612d-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6612d-143">**[Créer un utilisateur de test de Citrix ShareFile](#create-a-citrix-sharefile-test-user)**  -toohave un équivalent de Britta Simon dans Citrix ShareFile qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6612d-143">**[Create a Citrix ShareFile test user](#create-a-citrix-sharefile-test-user)** - toohave a counterpart of Britta Simon in Citrix ShareFile that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6612d-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="6612d-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6612d-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="6612d-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="6612d-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="6612d-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="6612d-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="6612d-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Citrix ShareFile application.</span></span>

<span data-ttu-id="6612d-148">**tooconfigure Azure AD single sign-on avec Citrix ShareFile, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6612d-148">**tooconfigure Azure AD single sign-on with Citrix ShareFile, perform hello following steps:**</span></span>

1. <span data-ttu-id="6612d-149">Bonjour portail Azure, sur hello **Citrix ShareFile** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="6612d-149">In hello Azure portal, on hello **Citrix ShareFile** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="6612d-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="6612d-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_samlbase.png)

3. <span data-ttu-id="6612d-153">Sur hello **Citrix ShareFile domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="6612d-153">On hello **Citrix ShareFile Domain and URLs** section, perform hello following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL Citrix ShareFile](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_url.png)
    
    <span data-ttu-id="6612d-155">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<tenant-name>.sharefile.com/saml/login`</span><span class="sxs-lookup"><span data-stu-id="6612d-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.sharefile.com/saml/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6612d-156">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="6612d-156">This value is not real.</span></span> <span data-ttu-id="6612d-157">Mettre à jour de cette valeur avec hello URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="6612d-157">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="6612d-158">Contact [équipe de support du Client Citrix ShareFile](https://www.citrix.co.in/products/sharefile/support.html) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="6612d-158">Contact [Citrix ShareFile Client support team](https://www.citrix.co.in/products/sharefile/support.html) tooget this value.</span></span> 

4. <span data-ttu-id="6612d-159">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="6612d-159">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_certificate.png) 

5. <span data-ttu-id="6612d-161">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="6612d-161">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-sharefile-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6612d-163">Sur hello **Configuration de Citrix ShareFile** , cliquez sur **configurer Citrix ShareFile** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="6612d-163">On hello **Citrix ShareFile Configuration** section, click **Configure Citrix ShareFile** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="6612d-164">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="6612d-164">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuration de Citrix ShareFile](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_configure.png) 

7. <span data-ttu-id="6612d-166">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise **Citrix ShareFile** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="6612d-166">In a different web browser window, log into your **Citrix ShareFile** company site as an administrator.</span></span>

8. <span data-ttu-id="6612d-167">Dans la barre d’outils de hello en haut de hello, cliquez sur **Admin**.</span><span class="sxs-lookup"><span data-stu-id="6612d-167">In hello toolbar on hello top, click **Admin**.</span></span>

9. <span data-ttu-id="6612d-168">Dans le volet de navigation gauche hello, sélectionnez **configurer l’authentification unique sur**.</span><span class="sxs-lookup"><span data-stu-id="6612d-168">In hello left navigation pane, select **Configure Single Sign-On**.</span></span>
   
    <span data-ttu-id="6612d-169">![Compte d’administration](./media/active-directory-saas-sharefile-tutorial/ic773627.png "Compte d’administration")</span><span class="sxs-lookup"><span data-stu-id="6612d-169">![Account Administration](./media/active-directory-saas-sharefile-tutorial/ic773627.png "Account Administration")</span></span>

10. <span data-ttu-id="6612d-170">Sur hello **Single Sign-On / Configuration de SAML 2.0** page de boîte de dialogue sous **les paramètres de base**, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="6612d-170">On hello **Single Sign-On/ SAML 2.0 Configuration** dialog page under **Basic Settings**, perform hello following steps:</span></span>
   
    <span data-ttu-id="6612d-171">![Authentification unique](./media/active-directory-saas-sharefile-tutorial/ic773628.png "Authentification unique")</span><span class="sxs-lookup"><span data-stu-id="6612d-171">![Single sign-on](./media/active-directory-saas-sharefile-tutorial/ic773628.png "Single sign-on")</span></span>
   
    <span data-ttu-id="6612d-172">a.</span><span class="sxs-lookup"><span data-stu-id="6612d-172">a.</span></span> <span data-ttu-id="6612d-173">Cliquez sur **Enable SAML**.</span><span class="sxs-lookup"><span data-stu-id="6612d-173">Click **Enable SAML**.</span></span>
    
    <span data-ttu-id="6612d-174">b.</span><span class="sxs-lookup"><span data-stu-id="6612d-174">b.</span></span> <span data-ttu-id="6612d-175">Dans **votre émetteur IDP / ID d’entité** zone de texte, valeur hello coller **ID d’entité SAML** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="6612d-175">In **Your IDP Issuer/ Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="6612d-176">c.</span><span class="sxs-lookup"><span data-stu-id="6612d-176">c.</span></span> <span data-ttu-id="6612d-177">Cliquez sur **modification** toohello suivant **certificat X.509** champ, puis vous avez téléchargé à partir de télécharger le certificat hello hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="6612d-177">Click **Change** next toohello **X.509 Certificate** field and then upload hello certificate you downloaded from hello Azure portal.</span></span>
    
    <span data-ttu-id="6612d-178">d.</span><span class="sxs-lookup"><span data-stu-id="6612d-178">d.</span></span> <span data-ttu-id="6612d-179">Dans **URL de connexion** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="6612d-179">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="6612d-180">e.</span><span class="sxs-lookup"><span data-stu-id="6612d-180">e.</span></span> <span data-ttu-id="6612d-181">Dans **URL de déconnexion** zone de texte, valeur hello coller **URL de déconnexion** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="6612d-181">In **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

11. <span data-ttu-id="6612d-182">Cliquez sur **enregistrer** sur hello portail de gestion de Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="6612d-182">Click **Save** on hello Citrix ShareFile management portal.</span></span>

> [!TIP]
> <span data-ttu-id="6612d-183">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="6612d-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6612d-184">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="6612d-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6612d-185">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6612d-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="6612d-186">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="6612d-186">Create an Azure AD test user</span></span>

<span data-ttu-id="6612d-187">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="6612d-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="6612d-189">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6612d-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6612d-190">Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.</span><span class="sxs-lookup"><span data-stu-id="6612d-190">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-sharefile-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="6612d-192">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="6612d-192">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-sharefile-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="6612d-194">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="6612d-194">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![bouton Ajouter de Hello](./media/active-directory-saas-sharefile-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="6612d-196">Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="6612d-196">In hello **User** dialog box, perform hello following steps:</span></span>

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-sharefile-tutorial/create_aaduser_04.png)

    <span data-ttu-id="6612d-198">a.</span><span class="sxs-lookup"><span data-stu-id="6612d-198">a.</span></span> <span data-ttu-id="6612d-199">Bonjour **nom** , tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6612d-199">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6612d-200">b.</span><span class="sxs-lookup"><span data-stu-id="6612d-200">b.</span></span> <span data-ttu-id="6612d-201">Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6612d-201">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="6612d-202">c.</span><span class="sxs-lookup"><span data-stu-id="6612d-202">c.</span></span> <span data-ttu-id="6612d-203">Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.</span><span class="sxs-lookup"><span data-stu-id="6612d-203">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="6612d-204">d.</span><span class="sxs-lookup"><span data-stu-id="6612d-204">d.</span></span> <span data-ttu-id="6612d-205">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="6612d-205">Click **Create**.</span></span>
 
### <a name="create-a-citrix-sharefile-test-user"></a><span data-ttu-id="6612d-206">Créer un utilisateur de test Citrix ShareFile</span><span class="sxs-lookup"><span data-stu-id="6612d-206">Create a Citrix ShareFile test user</span></span>

<span data-ttu-id="6612d-207">Dans l’ordre tooenable le toolog d’utilisateurs Azure AD à Citrix ShareFile, ils doivent être configurés dans Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="6612d-207">In order tooenable Azure AD users toolog into Citrix ShareFile, they must be provisioned into Citrix ShareFile.</span></span> <span data-ttu-id="6612d-208">Dans les cas de hello de Citrix ShareFile, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="6612d-208">In hello case of Citrix ShareFile, provisioning is a manual task.</span></span>

<span data-ttu-id="6612d-209">**tooprovision un compte d’utilisateur, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6612d-209">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="6612d-210">Connectez-vous à tooyour **Citrix ShareFile** client.</span><span class="sxs-lookup"><span data-stu-id="6612d-210">Log in tooyour **Citrix ShareFile** tenant.</span></span>

2. <span data-ttu-id="6612d-211">Cliquez sur **Manage Users \> Manage Users Home \> + Create Employee**.</span><span class="sxs-lookup"><span data-stu-id="6612d-211">Click **Manage Users \> Manage Users Home \> + Create Employee**.</span></span>
   
   <span data-ttu-id="6612d-212">![Create Employee](./media/active-directory-saas-sharefile-tutorial/IC781050.png "Create Employee")</span><span class="sxs-lookup"><span data-stu-id="6612d-212">![Create Employee](./media/active-directory-saas-sharefile-tutorial/IC781050.png "Create Employee")</span></span>

3. <span data-ttu-id="6612d-213">Sur hello **des informations de base** section, suivez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="6612d-213">On hello **Basic Information** section, perform below steps:</span></span>
   
   <span data-ttu-id="6612d-214">![Informations de base](./media/active-directory-saas-sharefile-tutorial/IC799951.png "Informations de base")</span><span class="sxs-lookup"><span data-stu-id="6612d-214">![Basic Information](./media/active-directory-saas-sharefile-tutorial/IC799951.png "Basic Information")</span></span>
   
   <span data-ttu-id="6612d-215">a.</span><span class="sxs-lookup"><span data-stu-id="6612d-215">a.</span></span> <span data-ttu-id="6612d-216">Bonjour **adresse de messagerie** zone de texte, adresse de messagerie de type hello de Britta Simon comme  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="6612d-216">In hello **Email Address** textbox, type hello email address of Britta Simon as **brittasimon@contoso.com**.</span></span>
   
   <span data-ttu-id="6612d-217">b.</span><span class="sxs-lookup"><span data-stu-id="6612d-217">b.</span></span> <span data-ttu-id="6612d-218">Bonjour **prénom** zone de texte, type **prénom** d’utilisateur en tant que **Brian**.</span><span class="sxs-lookup"><span data-stu-id="6612d-218">In hello **First Name** textbox, type **first name** of user as **Britta**.</span></span>
   
   <span data-ttu-id="6612d-219">c.</span><span class="sxs-lookup"><span data-stu-id="6612d-219">c.</span></span> <span data-ttu-id="6612d-220">Bonjour **nom** zone de texte, type **nom** d’utilisateur en tant que **Simon**.</span><span class="sxs-lookup"><span data-stu-id="6612d-220">In hello **Last Name** textbox, type **last name** of user as **Simon**.</span></span>

4. <span data-ttu-id="6612d-221">Cliquez sur **Add User**.</span><span class="sxs-lookup"><span data-stu-id="6612d-221">Click **Add User**.</span></span>
  
   >[!NOTE]
   ><span data-ttu-id="6612d-222">titulaire du compte Azure AD Hello sera reçoivent un e-mail et suivez les leur compte d’un tooconfirm lien avant son activation. Vous pouvez utiliser n’importe quel autre Citrix ShareFile utilisateur compte outil de création ou API fournie par Citrix ShareFile tooprovision comptes d’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6612d-222">hello Azure AD account holder will receive an email and follow a link tooconfirm their account before it becomes active.You can use any other Citrix ShareFile user account creation tools or APIs provided by Citrix ShareFile tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="6612d-223">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="6612d-223">Assign hello Azure AD test user</span></span>

<span data-ttu-id="6612d-224">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooCitrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="6612d-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCitrix ShareFile.</span></span>

![Attribuer le rôle d’utilisateur hello][200] 

<span data-ttu-id="6612d-226">**tooassign Britta Simon tooCitrix ShareFile, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6612d-226">**tooassign Britta Simon tooCitrix ShareFile, perform hello following steps:**</span></span>

1. <span data-ttu-id="6612d-227">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="6612d-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="6612d-229">Dans la liste des applications hello, sélectionnez **Citrix ShareFile**.</span><span class="sxs-lookup"><span data-stu-id="6612d-229">In hello applications list, select **Citrix ShareFile**.</span></span>

    ![Hello lien Citrix ShareFile dans la liste des Applications hello](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_app.png)  

3. <span data-ttu-id="6612d-231">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="6612d-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202]

4. <span data-ttu-id="6612d-233">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="6612d-233">Click **Add** button.</span></span> <span data-ttu-id="6612d-234">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="6612d-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="6612d-236">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="6612d-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6612d-237">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="6612d-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6612d-238">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="6612d-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="6612d-239">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="6612d-239">Test single sign-on</span></span>

<span data-ttu-id="6612d-240">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="6612d-240">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6612d-241">Lorsque vous cliquez sur hello Citrix ShareFile vignette Bonjour volet d’accès, vous devez obtenir tooyour automatiquement signé sur Citrix ShareFile application.</span><span class="sxs-lookup"><span data-stu-id="6612d-241">When you click hello Citrix ShareFile tile in hello Access Panel, you should get automatically signed-on tooyour Citrix ShareFile application.</span></span>
<span data-ttu-id="6612d-242">Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6612d-242">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6612d-243">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="6612d-243">Additional resources</span></span>

* [<span data-ttu-id="6612d-244">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6612d-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6612d-245">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="6612d-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_203.png

