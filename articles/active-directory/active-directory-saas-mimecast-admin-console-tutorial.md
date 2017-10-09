---
title: "Didacticiel : Intégration d’Azure Active Directory à Mimecast Admin Console | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Mimecast Admin Console."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 81c50614-f49b-4bbc-97d5-3cf77154305f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: 5a04a5abd9ff30d484bce0a5c97a1d3e48b69e4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-admin-console"></a><span data-ttu-id="5c76b-103">Didacticiel : Intégration d’Azure Active Directory à Mimecast Admin Console</span><span class="sxs-lookup"><span data-stu-id="5c76b-103">Tutorial: Azure Active Directory integration with Mimecast Admin Console</span></span>

<span data-ttu-id="5c76b-104">Dans ce didacticiel, vous apprendrez comment toointegrate Mimecast Admin Console avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5c76b-104">In this tutorial, you learn how toointegrate Mimecast Admin Console with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5c76b-105">Intégration de Mimecast Admin Console avec Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="5c76b-105">Integrating Mimecast Admin Console with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5c76b-106">Vous pouvez contrôler dans Azure AD qui a accès tooMimecast Console d’administration.</span><span class="sxs-lookup"><span data-stu-id="5c76b-106">You can control in Azure AD who has access tooMimecast Admin Console.</span></span>
- <span data-ttu-id="5c76b-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooMimecast Console d’administration (Single Sign-On) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c76b-107">You can enable your users tooautomatically get signed-on tooMimecast Admin Console (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="5c76b-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5c76b-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="5c76b-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5c76b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c76b-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="5c76b-110">Prerequisites</span></span>

<span data-ttu-id="5c76b-111">tooconfigure intégration d’Azure AD à Mimecast Admin Console, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="5c76b-111">tooconfigure Azure AD integration with Mimecast Admin Console, you need hello following items:</span></span>

- <span data-ttu-id="5c76b-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c76b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5c76b-113">Un abonnement Mimecast Admin Console pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="5c76b-113">A Mimecast Admin Console single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5c76b-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="5c76b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5c76b-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="5c76b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5c76b-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="5c76b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5c76b-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5c76b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5c76b-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="5c76b-118">Scenario description</span></span>
<span data-ttu-id="5c76b-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="5c76b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5c76b-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="5c76b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5c76b-121">Ajout de Mimecast Admin Console à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="5c76b-121">Adding Mimecast Admin Console from hello gallery</span></span>
2. <span data-ttu-id="5c76b-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c76b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mimecast-admin-console-from-hello-gallery"></a><span data-ttu-id="5c76b-123">Ajout de Mimecast Admin Console à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="5c76b-123">Adding Mimecast Admin Console from hello gallery</span></span>
<span data-ttu-id="5c76b-124">intégration de hello tooconfigure de Mimecast Admin Console dans Azure AD, vous devez tooadd Mimecast Admin Console à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="5c76b-124">tooconfigure hello integration of Mimecast Admin Console into Azure AD, you need tooadd Mimecast Admin Console from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5c76b-125">**tooadd Mimecast Admin Console à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5c76b-125">**tooadd Mimecast Admin Console from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5c76b-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="5c76b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="5c76b-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="5c76b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5c76b-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5c76b-129">Then go too**All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="5c76b-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="5c76b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="5c76b-133">Dans la zone de recherche de hello, tapez **Mimecast Admin Console**, sélectionnez **Mimecast Admin Console** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="5c76b-133">In hello search box, type **Mimecast Admin Console**, select **Mimecast Admin Console** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Liste des résultats de Mimecast Admin Console Bonjour](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="5c76b-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c76b-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="5c76b-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Mimecast Admin Console sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="5c76b-136">In this section, you configure and test Azure AD single sign-on with Mimecast Admin Console based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5c76b-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Mimecast Admin Console est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c76b-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Mimecast Admin Console is tooa user in Azure AD.</span></span> <span data-ttu-id="5c76b-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans la Console d’administration Mimecast hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="5c76b-138">In other words, a link relationship between an Azure AD user and hello related user in Mimecast Admin Console needs toobe established.</span></span>

<span data-ttu-id="5c76b-139">Dans la Console d’administration Mimecast, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="5c76b-139">In Mimecast Admin Console, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5c76b-140">tooconfigure et test Azure AD l’authentification unique sur Mimecast Admin Console, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="5c76b-140">tooconfigure and test Azure AD single sign-on with Mimecast Admin Console, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5c76b-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="5c76b-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5c76b-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5c76b-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5c76b-143">**[Créer un utilisateur de test de Mimecast Admin Console](#create-a-mimecast-admin-console-test-user)**  -toohave un équivalent de Britta Simon dans Mimecast Admin Console est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5c76b-143">**[Create a Mimecast Admin Console test user](#create-a-mimecast-admin-console-test-user)** - toohave a counterpart of Britta Simon in Mimecast Admin Console that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5c76b-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5c76b-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5c76b-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="5c76b-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="5c76b-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c76b-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="5c76b-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Mimecast Admin Console.</span><span class="sxs-lookup"><span data-stu-id="5c76b-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Mimecast Admin Console application.</span></span>

<span data-ttu-id="5c76b-148">**tooconfigure Azure AD l’authentification unique sur Mimecast Admin Console, exécutez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5c76b-148">**tooconfigure Azure AD single sign-on with Mimecast Admin Console, perform hello following steps:**</span></span>

1. <span data-ttu-id="5c76b-149">Bonjour portail Azure, sur hello **Mimecast Admin Console** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="5c76b-149">In hello Azure portal, on hello **Mimecast Admin Console** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="5c76b-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5c76b-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_samlbase.png)

3. <span data-ttu-id="5c76b-153">Sur hello **Mimecast Admin Console domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5c76b-153">On hello **Mimecast Admin Console Domain and URLs** section, perform hello following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL Mimecast Admin Console](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_url.png)

    <span data-ttu-id="5c76b-155">Bonjour **URL de connexion** zone de texte, tapez l’URL hello :</span><span class="sxs-lookup"><span data-stu-id="5c76b-155">In hello **Sign-on URL** textbox, type hello URL:</span></span>
    | |
    | -- |
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|

    > [!NOTE] 
    > <span data-ttu-id="5c76b-156">Hello l’URL de connexion est spécifique de la région.</span><span class="sxs-lookup"><span data-stu-id="5c76b-156">hello sign on URL is region specific.</span></span>

4. <span data-ttu-id="5c76b-157">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="5c76b-157">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_certificate.png) 

5. <span data-ttu-id="5c76b-159">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="5c76b-159">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5c76b-161">Sur hello **Mimecast Admin Console Configuration** , cliquez sur **configurer Mimecast Admin Console** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="5c76b-161">On hello **Mimecast Admin Console Configuration** section, click **Configure Mimecast Admin Console** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5c76b-162">Hello de copie **ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="5c76b-162">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuration de Mimecast Admin Console](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_configure.png) 

7. <span data-ttu-id="5c76b-164">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Mimecast Admin Console en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="5c76b-164">In a different web browser window, log into your Mimecast Admin Console as an administrator.</span></span>

8. <span data-ttu-id="5c76b-165">Accédez trop**Services \> Application**.</span><span class="sxs-lookup"><span data-stu-id="5c76b-165">Go too**Services \> Application**.</span></span>

    <span data-ttu-id="5c76b-166">![Services](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794998.png "Services")</span><span class="sxs-lookup"><span data-stu-id="5c76b-166">![Services](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794998.png "Services")</span></span>

9. <span data-ttu-id="5c76b-167">Cliquez sur **Authentication Profiles**.</span><span class="sxs-lookup"><span data-stu-id="5c76b-167">Click **Authentication Profiles**.</span></span>

    <span data-ttu-id="5c76b-168">![Profils d’authentification](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794999.png "Profils d’authentification")</span><span class="sxs-lookup"><span data-stu-id="5c76b-168">![Authentication Profiles](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794999.png "Authentication Profiles")</span></span>
    
10. <span data-ttu-id="5c76b-169">Cliquez sur **New Authentication Profile**.</span><span class="sxs-lookup"><span data-stu-id="5c76b-169">Click **New Authentication Profile**.</span></span>

    <span data-ttu-id="5c76b-170">![Nouveaux profils d’authentification](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795000.png "Nouveaux profils d’authentification")</span><span class="sxs-lookup"><span data-stu-id="5c76b-170">![New Authentication Profiles](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795000.png "New Authentication Profiles")</span></span>

11. <span data-ttu-id="5c76b-171">Bonjour **profil d’authentification** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5c76b-171">In hello **Authentication Profile** section, perform hello following steps:</span></span>

    <span data-ttu-id="5c76b-172">![Profil d’authentification](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795015.png "Profil d’authentification")</span><span class="sxs-lookup"><span data-stu-id="5c76b-172">![Authentication Profile](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795015.png "Authentication Profile")</span></span>
    
    <span data-ttu-id="5c76b-173">a.</span><span class="sxs-lookup"><span data-stu-id="5c76b-173">a.</span></span> <span data-ttu-id="5c76b-174">Bonjour **Description** zone de texte, tapez un nom pour votre configuration.</span><span class="sxs-lookup"><span data-stu-id="5c76b-174">In hello **Description** textbox, type a name for your configuration.</span></span>
    
    <span data-ttu-id="5c76b-175">b.</span><span class="sxs-lookup"><span data-stu-id="5c76b-175">b.</span></span> <span data-ttu-id="5c76b-176">Sélectionnez **Enforce SAML Authentication for Mimecast Admin Console**.</span><span class="sxs-lookup"><span data-stu-id="5c76b-176">Select **Enforce SAML Authentication for Mimecast Admin Console**.</span></span>
    
    <span data-ttu-id="5c76b-177">c.</span><span class="sxs-lookup"><span data-stu-id="5c76b-177">c.</span></span> <span data-ttu-id="5c76b-178">Pour **Provider**, sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5c76b-178">As **Provider**, select **Azure Active Directory**.</span></span>
    
    <span data-ttu-id="5c76b-179">d.</span><span class="sxs-lookup"><span data-stu-id="5c76b-179">d.</span></span> <span data-ttu-id="5c76b-180">Coller **ID d’entité SAML**, lequel vous avez copié à partir de hello portail Azure en hello **URL de l’émetteur** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="5c76b-180">Paste **SAML Entity ID**, which you have copied from hello Azure portal into hello **Issuer URL** textbox.</span></span>
    
    <span data-ttu-id="5c76b-181">e.</span><span class="sxs-lookup"><span data-stu-id="5c76b-181">e.</span></span> <span data-ttu-id="5c76b-182">Coller **SAML Sign-On URL du Service unique**, lequel vous avez copié à partir de hello portail Azure en hello **URL de connexion** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="5c76b-182">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **Login URL** textbox.</span></span>

    <span data-ttu-id="5c76b-183">f.</span><span class="sxs-lookup"><span data-stu-id="5c76b-183">f.</span></span> <span data-ttu-id="5c76b-184">Coller **SAML Sign-On URL du Service unique**, lequel vous avez copié à partir de hello portail Azure en hello **URL de déconnexion** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="5c76b-184">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **Logout URL** textbox.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="5c76b-185">Hello valeur de l’URL de connexion et la valeur de l’URL de déconnexion hello sont pour hello Mimecast Admin Console hello identiques.</span><span class="sxs-lookup"><span data-stu-id="5c76b-185">hello Login URL value and hello Logout URL value are for hello Mimecast Admin Console hello same.</span></span>
    
    <span data-ttu-id="5c76b-186">g.</span><span class="sxs-lookup"><span data-stu-id="5c76b-186">g.</span></span> <span data-ttu-id="5c76b-187">Ouvrez votre certificat de base-64 téléchargé à partir du portail Azure dans le bloc-notes, supprimez la première ligne de hello («*--*») et hello dernière ligne («*--*»), hello copie restant contenu de celui-ci dans le Presse-papiers, puis collez-la toohello **certificat de fournisseur d’identité (métadonnées)** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="5c76b-187">Open your base-64 certificate downloaded from Azure portal in notepad, remove hello first line (“*--*“) and hello last line (“*--*“), copy hello remaining content of it into your clipboard, and then paste it toohello **Identity Provider Certificate (Metadata)** textbox.</span></span>
    
    <span data-ttu-id="5c76b-188">h.</span><span class="sxs-lookup"><span data-stu-id="5c76b-188">h.</span></span> <span data-ttu-id="5c76b-189">Sélectionnez **Allow Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="5c76b-189">Select **Allow Single Sign On**.</span></span>
    
    <span data-ttu-id="5c76b-190">i.</span><span class="sxs-lookup"><span data-stu-id="5c76b-190">i.</span></span> <span data-ttu-id="5c76b-191">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="5c76b-191">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="5c76b-192">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="5c76b-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5c76b-193">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="5c76b-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5c76b-194">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5c76b-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="5c76b-195">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c76b-195">Create an Azure AD test user</span></span>

<span data-ttu-id="5c76b-196">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="5c76b-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="5c76b-198">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5c76b-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5c76b-199">Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.</span><span class="sxs-lookup"><span data-stu-id="5c76b-199">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="5c76b-201">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="5c76b-201">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="5c76b-203">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="5c76b-203">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![bouton Ajouter de Hello](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="5c76b-205">Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5c76b-205">In hello **User** dialog box, perform hello following steps:</span></span>

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_04.png)

    <span data-ttu-id="5c76b-207">a.</span><span class="sxs-lookup"><span data-stu-id="5c76b-207">a.</span></span> <span data-ttu-id="5c76b-208">Bonjour **nom** , tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5c76b-208">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5c76b-209">b.</span><span class="sxs-lookup"><span data-stu-id="5c76b-209">b.</span></span> <span data-ttu-id="5c76b-210">Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5c76b-210">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="5c76b-211">c.</span><span class="sxs-lookup"><span data-stu-id="5c76b-211">c.</span></span> <span data-ttu-id="5c76b-212">Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.</span><span class="sxs-lookup"><span data-stu-id="5c76b-212">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="5c76b-213">d.</span><span class="sxs-lookup"><span data-stu-id="5c76b-213">d.</span></span> <span data-ttu-id="5c76b-214">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="5c76b-214">Click **Create**.</span></span>
 
### <a name="create-a-mimecast-admin-console-test-user"></a><span data-ttu-id="5c76b-215">Créer un utilisateur de test Mimecast Admin Console</span><span class="sxs-lookup"><span data-stu-id="5c76b-215">Create a Mimecast Admin Console test user</span></span>

<span data-ttu-id="5c76b-216">Dans l’ordre tooenable Azure AD les utilisateurs toolog à Mimecast Admin Console, vous devez les configurer dans Mimecast Admin Console.</span><span class="sxs-lookup"><span data-stu-id="5c76b-216">In order tooenable Azure AD users toolog into Mimecast Admin Console, they must be provisioned into Mimecast Admin Console.</span></span> <span data-ttu-id="5c76b-217">Dans les cas de hello de Mimecast Admin Console, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="5c76b-217">In hello case of Mimecast Admin Console, provisioning is a manual task.</span></span>

* <span data-ttu-id="5c76b-218">Vous devez tooregister un domaine avant de pouvoir créer des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="5c76b-218">You need tooregister a domain before you can create users.</span></span>

<span data-ttu-id="5c76b-219">**configuration, de l’utilisateur tooconfigure effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5c76b-219">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="5c76b-220">Ouverture de session tooyour **Mimecast Admin Console** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="5c76b-220">Sign on tooyour **Mimecast Admin Console** as administrator.</span></span>
2. <span data-ttu-id="5c76b-221">Accédez trop**répertoires \> interne**.</span><span class="sxs-lookup"><span data-stu-id="5c76b-221">Go too**Directories \> Internal**.</span></span>
   
   <span data-ttu-id="5c76b-222">![Répertoires](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795003.png "Répertoires")</span><span class="sxs-lookup"><span data-stu-id="5c76b-222">![Directories](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795003.png "Directories")</span></span>
3. <span data-ttu-id="5c76b-223">Cliquez sur **Register New Domain**.</span><span class="sxs-lookup"><span data-stu-id="5c76b-223">Click **Register New Domain**.</span></span>
   
   <span data-ttu-id="5c76b-224">![Enregistrer un nouveau domaine](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795004.png "Enregistrer un nouveau domaine")</span><span class="sxs-lookup"><span data-stu-id="5c76b-224">![Register New Domain](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795004.png "Register New Domain")</span></span>
4. <span data-ttu-id="5c76b-225">Après avoir créé votre domaine, cliquez sur **New Address**.</span><span class="sxs-lookup"><span data-stu-id="5c76b-225">After your new domain has been created, click **New Address**.</span></span>
   
   <span data-ttu-id="5c76b-226">![Nouvelle adresse](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795005.png "Nouvelle adresse")</span><span class="sxs-lookup"><span data-stu-id="5c76b-226">![New Address](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795005.png "New Address")</span></span>
5. <span data-ttu-id="5c76b-227">Dans hello adresse boîte de dialogue Nouveau, effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5c76b-227">In hello new address dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="5c76b-228">![Enregistrer](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795006.png "enregistrer")</span><span class="sxs-lookup"><span data-stu-id="5c76b-228">![Save](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795006.png "Save")</span></span>
   
   <span data-ttu-id="5c76b-229">a.</span><span class="sxs-lookup"><span data-stu-id="5c76b-229">a.</span></span> <span data-ttu-id="5c76b-230">Hello de type **adresse de messagerie**, **nom Global**, **mot de passe**, et **confirmer le mot de passe** compte les attributs d’un Azure AD valide que vous souhaitez tooprovision dans hello relatives des zones de texte.</span><span class="sxs-lookup"><span data-stu-id="5c76b-230">Type hello **Email Address**, **Global Name**, **Password**, and **Confirm Password** attributes of a valid Azure AD account you want tooprovision into hello related textboxes.</span></span>

   <span data-ttu-id="5c76b-231">b.</span><span class="sxs-lookup"><span data-stu-id="5c76b-231">b.</span></span> <span data-ttu-id="5c76b-232">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="5c76b-232">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="5c76b-233">Vous pouvez utiliser tout autre outil de création de compte utilisateur Mimecast Admin Console ou API fournie par les comptes d’utilisateur Mimecast Admin Console tooprovision Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c76b-233">You can use any other Mimecast Admin Console user account creation tools or APIs provided by Mimecast Admin Console tooprovision Azure AD user accounts.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="5c76b-234">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c76b-234">Assign hello Azure AD test user</span></span>

<span data-ttu-id="5c76b-235">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooMimecast Console d’administration.</span><span class="sxs-lookup"><span data-stu-id="5c76b-235">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMimecast Admin Console.</span></span>

![Attribuer le rôle d’utilisateur hello][200] 

<span data-ttu-id="5c76b-237">**tooassign Britta Simon tooMimecast Console d’administration, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5c76b-237">**tooassign Britta Simon tooMimecast Admin Console, perform hello following steps:**</span></span>

1. <span data-ttu-id="5c76b-238">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5c76b-238">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="5c76b-240">Dans la liste des applications hello, sélectionnez **Mimecast Admin Console**.</span><span class="sxs-lookup"><span data-stu-id="5c76b-240">In hello applications list, select **Mimecast Admin Console**.</span></span>

    ![lien de Mimecast Admin Console Hello dans la liste des Applications hello](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_app.png)  

3. <span data-ttu-id="5c76b-242">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5c76b-242">In hello menu on hello left, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202]

4. <span data-ttu-id="5c76b-244">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="5c76b-244">Click **Add** button.</span></span> <span data-ttu-id="5c76b-245">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5c76b-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="5c76b-247">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="5c76b-247">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5c76b-248">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5c76b-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5c76b-249">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5c76b-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="5c76b-250">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="5c76b-250">Test single sign-on</span></span>

<span data-ttu-id="5c76b-251">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="5c76b-251">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5c76b-252">Lorsque vous cliquez sur mosaïque Mimecast Admin Console hello hello volet d’accès, vous devez obtenir l’application de Mimecast Admin Console automatiquement signé sur tooyour.</span><span class="sxs-lookup"><span data-stu-id="5c76b-252">When you click hello Mimecast Admin Console tile in hello Access Panel, you should get automatically signed-on tooyour Mimecast Admin Console application.</span></span>
<span data-ttu-id="5c76b-253">Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5c76b-253">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5c76b-254">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="5c76b-254">Additional resources</span></span>

* [<span data-ttu-id="5c76b-255">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5c76b-255">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5c76b-256">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="5c76b-256">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_203.png

