---
title: "Didacticiel : Intégration d’Azure Active Directory à JIRA SAML SSO by Microsoft | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et l’authentification unique SAML de JIRA par Microsoft."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0dc847b9-eec4-4c31-845e-0144ddedc4a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 178c4c040d9939bca271ac185ca5c2feb14f1247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jira-saml-sso-by-microsoft"></a><span data-ttu-id="1f052-103">Didacticiel : Intégration d’Azure Active Directory à JIRA SAML SSO by Microsoft</span><span class="sxs-lookup"><span data-stu-id="1f052-103">Tutorial: Azure Active Directory integration with JIRA SAML SSO by Microsoft</span></span>

<span data-ttu-id="1f052-104">Dans ce didacticiel, vous apprendrez comment toointegrate SSO SAML de JIRA par Microsoft avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1f052-104">In this tutorial, you learn how toointegrate JIRA SAML SSO by Microsoft with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1f052-105">Intégration de l’authentification unique SAML de JIRA par Microsoft à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="1f052-105">Integrating JIRA SAML SSO by Microsoft with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1f052-106">Vous pouvez contrôler dans Azure AD qui a accès tooJIRA SSO SAML par Microsoft</span><span class="sxs-lookup"><span data-stu-id="1f052-106">You can control in Azure AD who has access tooJIRA SAML SSO by Microsoft</span></span>
- <span data-ttu-id="1f052-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooJIRA SSO SAML par Microsoft (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f052-107">You can enable your users tooautomatically get signed-on tooJIRA SAML SSO by Microsoft (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1f052-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="1f052-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1f052-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1f052-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f052-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1f052-110">Prerequisites</span></span>

<span data-ttu-id="1f052-111">tooconfigure intégration d’Azure AD avec l’authentification unique SAML de JIRA par Microsoft, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="1f052-111">tooconfigure Azure AD integration with JIRA SAML SSO by Microsoft, you need hello following items:</span></span>

- <span data-ttu-id="1f052-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f052-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1f052-113">Application de serveur JIRA installée sur un serveur Windows 64 bits (localement ou sur le cloud hello IaaS infrastructure)</span><span class="sxs-lookup"><span data-stu-id="1f052-113">JIRA server application installed on a Windows 64-bit server (on premise or on hello cloud IaaS infrastructure)</span></span>
- <span data-ttu-id="1f052-114">L’activation du HTTPS dans le serveur JIRA</span><span class="sxs-lookup"><span data-stu-id="1f052-114">JIRA server is HTTPS enabled</span></span>
- <span data-ttu-id="1f052-115">Remarque hello pris en charge les versions du plug-in JIRA sont mentionnées dans section.</span><span class="sxs-lookup"><span data-stu-id="1f052-115">Note hello supported versions for JIRA Plugin are mentioned in below section.</span></span>
- <span data-ttu-id="1f052-116">Serveur JIRA est accessible sur internet particulièrement tooAzure page de connexion d’Active Directory pour l’authentification et doit en mesure de tooreceive hello jeton d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f052-116">JIRA server is reachable on internet particularly tooAzure AD Login page for authentication and should able tooreceive hello token from Azure AD</span></span>
- <span data-ttu-id="1f052-117">La création d’informations d’identification administrateur dans JIRA</span><span class="sxs-lookup"><span data-stu-id="1f052-117">Admin credentials are set up in JIRA</span></span>
- <span data-ttu-id="1f052-118">La désactivation de WebSudo dans JIRA</span><span class="sxs-lookup"><span data-stu-id="1f052-118">WebSudo is disabled in JIRA</span></span>
- <span data-ttu-id="1f052-119">Tester l’utilisateur créé à l’application de serveur JIRA de hello</span><span class="sxs-lookup"><span data-stu-id="1f052-119">Test user created in hello JIRA server application</span></span>

> [!NOTE]
> <span data-ttu-id="1f052-120">les étapes tootest hello dans ce didacticiel, nous déconseillons à l’aide d’un environnement de production de JIRA.</span><span class="sxs-lookup"><span data-stu-id="1f052-120">tootest hello steps in this tutorial, we do not recommend using a production environment of JIRA.</span></span> <span data-ttu-id="1f052-121">Tester l’intégration hello d’abord dans le développement ou l’environnement d’application hello, puis utilisez hello production environnement de mise en lots.</span><span class="sxs-lookup"><span data-stu-id="1f052-121">Test hello integration first in development or staging environment of hello application and then use hello production environment.</span></span>

<span data-ttu-id="1f052-122">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="1f052-122">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1f052-123">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="1f052-123">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1f052-124">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez bénéficier de [l’offre d’essai](https://azure.microsoft.com/pricing/free-trial/) d’un mois.</span><span class="sxs-lookup"><span data-stu-id="1f052-124">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="supported-versions-of-jira"></a><span data-ttu-id="1f052-125">Versions de JIRA prises en charge</span><span class="sxs-lookup"><span data-stu-id="1f052-125">Supported versions of JIRA</span></span> 

<span data-ttu-id="1f052-126">Les versions suivantes de JIRA sont actuellement prises en charge :</span><span class="sxs-lookup"><span data-stu-id="1f052-126">As of now, following versions of JIRA are supported:</span></span>

- <span data-ttu-id="1f052-127">JIRA Core et des logiciels : too7.2.0 6.0</span><span class="sxs-lookup"><span data-stu-id="1f052-127">JIRA Core and Software: 6.0 too7.2.0</span></span>
- <span data-ttu-id="1f052-128">Service d’assistance JIRA : too3.2 3.0</span><span class="sxs-lookup"><span data-stu-id="1f052-128">JIRA Service Desk: 3.0 too3.2</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1f052-129">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="1f052-129">Scenario description</span></span>
<span data-ttu-id="1f052-130">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="1f052-130">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1f052-131">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="1f052-131">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1f052-132">Ajout de l’authentification unique SAML de JIRA par Microsoft à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="1f052-132">Adding JIRA SAML SSO by Microsoft from hello gallery</span></span>
2. <span data-ttu-id="1f052-133">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f052-133">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jira-saml-sso-by-microsoft-from-hello-gallery"></a><span data-ttu-id="1f052-134">Ajout de l’authentification unique SAML de JIRA par Microsoft à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="1f052-134">Adding JIRA SAML SSO by Microsoft from hello gallery</span></span>
<span data-ttu-id="1f052-135">tooconfigure hello intégration de l’authentification unique SAML de JIRA par Microsoft dans Azure AD, vous devez tooadd SSO SAML de JIRA par Microsoft à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="1f052-135">tooconfigure hello integration of JIRA SAML SSO by Microsoft into Azure AD, you need tooadd JIRA SAML SSO by Microsoft from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1f052-136">**tooadd SSO SAML de JIRA par Microsoft à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1f052-136">**tooadd JIRA SAML SSO by Microsoft from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1f052-137">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="1f052-137">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1f052-139">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="1f052-139">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1f052-140">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1f052-140">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="1f052-142">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1f052-142">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="1f052-144">Dans la zone de recherche de hello, tapez **SSO SAML de JIRA par Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="1f052-144">In hello search box, type **JIRA SAML SSO by Microsoft**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_search.png)

5. <span data-ttu-id="1f052-146">Dans le volet de résultats hello, sélectionnez **SSO SAML de JIRA par Microsoft**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="1f052-146">In hello results panel, select **JIRA SAML SSO by Microsoft**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1f052-148">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f052-148">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1f052-149">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec JIRA SAML SSO by Microsoft, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="1f052-149">In this section, you configure and test Azure AD single sign-on with JIRA SAML SSO by Microsoft based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1f052-150">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans l’authentification unique SAML de JIRA par Microsoft est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1f052-150">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in JIRA SAML SSO by Microsoft is tooa user in Azure AD.</span></span> <span data-ttu-id="1f052-151">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans l’authentification unique SAML de JIRA par Microsoft hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="1f052-151">In other words, a link relationship between an Azure AD user and hello related user in JIRA SAML SSO by Microsoft needs toobe established.</span></span>

<span data-ttu-id="1f052-152">Dans l’authentification unique SAML JIRA par Microsoft, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="1f052-152">In JIRA SAML SSO by Microsoft, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1f052-153">tooconfigure et test Azure AD l’authentification unique avec l’authentification unique SAML de JIRA par Microsoft, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="1f052-153">tooconfigure and test Azure AD single sign-on with JIRA SAML SSO by Microsoft, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1f052-154">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="1f052-154">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1f052-155">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1f052-155">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1f052-156">**[Création d’une authentification unique SAML de JIRA par l’utilisateur de test Microsoft](#creating-a-jira-saml-sso-by-microsoft-test-user)**  -toohave un équivalent de Britta Simon dans l’authentification unique SAML de JIRA par Microsoft, qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1f052-156">**[Creating a JIRA SAML SSO by Microsoft test user](#creating-a-jira-saml-sso-by-microsoft-test-user)** - toohave a counterpart of Britta Simon in JIRA SAML SSO by Microsoft that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1f052-157">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="1f052-157">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1f052-158">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="1f052-158">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1f052-159">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f052-159">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1f052-160">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre authentification unique SAML de JIRA par application de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1f052-160">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your JIRA SAML SSO by Microsoft application.</span></span>

<span data-ttu-id="1f052-161">**tooconfigure Azure AD l’authentification unique avec l’authentification unique SAML de JIRA par Microsoft, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1f052-161">**tooconfigure Azure AD single sign-on with JIRA SAML SSO by Microsoft, perform hello following steps:**</span></span>

1. <span data-ttu-id="1f052-162">Bonjour portail Azure, sur hello **SSO SAML de JIRA par Microsoft** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="1f052-162">In hello Azure portal, on hello **JIRA SAML SSO by Microsoft** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="1f052-164">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="1f052-164">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_samlbase.png)

3. <span data-ttu-id="1f052-166">Sur hello **SSO SAML de JIRA par domaine Microsoft et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="1f052-166">On hello **JIRA SAML SSO by Microsoft Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_url.png)

    <span data-ttu-id="1f052-168">a.</span><span class="sxs-lookup"><span data-stu-id="1f052-168">a.</span></span> <span data-ttu-id="1f052-169">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="1f052-169">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    <span data-ttu-id="1f052-170">b.</span><span class="sxs-lookup"><span data-stu-id="1f052-170">b.</span></span> <span data-ttu-id="1f052-171">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<domain:port>/`</span><span class="sxs-lookup"><span data-stu-id="1f052-171">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<domain:port>/`</span></span>

    <span data-ttu-id="1f052-172">c.</span><span class="sxs-lookup"><span data-stu-id="1f052-172">c.</span></span> <span data-ttu-id="1f052-173">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="1f052-173">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1f052-174">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="1f052-174">These values are not real.</span></span> <span data-ttu-id="1f052-175">Mettre à jour ces valeurs avec hello réel identificateur, URL de réponse et URL de connexion.</span><span class="sxs-lookup"><span data-stu-id="1f052-175">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="1f052-176">Le port est facultatif s’il s’agit d’une URL nommée.</span><span class="sxs-lookup"><span data-stu-id="1f052-176">Port is optional in case it’s a named URL.</span></span> <span data-ttu-id="1f052-177">Ces valeurs sont reçus pendant la configuration hello du plug-in Jira, qui est expliquée plus loin dans le didacticiel de hello.</span><span class="sxs-lookup"><span data-stu-id="1f052-177">These values are received during hello configuration of Jira plugin, which is explained later in hello tutorial.</span></span>
 
4. <span data-ttu-id="1f052-178">toogenerate hello **métadonnées** url, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="1f052-178">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="1f052-179">a.</span><span class="sxs-lookup"><span data-stu-id="1f052-179">a.</span></span> <span data-ttu-id="1f052-180">Cliquez sur **Inscriptions des applications**.</span><span class="sxs-lookup"><span data-stu-id="1f052-180">Click **App registrations**.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-jiramicrosoft-tutorial/appregistrations.png)
   
    <span data-ttu-id="1f052-182">b.</span><span class="sxs-lookup"><span data-stu-id="1f052-182">b.</span></span> <span data-ttu-id="1f052-183">Cliquez sur **points de terminaison** tooopen **points de terminaison** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1f052-183">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Configurer l’authentification unique](./media/active-directory-saas-jiramicrosoft-tutorial/endpointicon.png)

    <span data-ttu-id="1f052-185">c.</span><span class="sxs-lookup"><span data-stu-id="1f052-185">c.</span></span> <span data-ttu-id="1f052-186">Cliquez sur hello copie bouton toocopy **DOCUMENT de métadonnées de fédération** url et collez-le dans le bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="1f052-186">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-jiramicrosoft-tutorial/endpoint.png)
     
    <span data-ttu-id="1f052-188">d.</span><span class="sxs-lookup"><span data-stu-id="1f052-188">d.</span></span> <span data-ttu-id="1f052-189">Maintenant accédez toohello page de propriétés de **SSO SAML de JIRA par Microsoft** et copie Bonjour **Id d’Application** à l’aide de **copie** bouton et collez-le dans le bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="1f052-189">Now go toohello property page of **JIRA SAML SSO by Microsoft** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-jiramicrosoft-tutorial/appid.png)

    <span data-ttu-id="1f052-191">e.</span><span class="sxs-lookup"><span data-stu-id="1f052-191">e.</span></span> <span data-ttu-id="1f052-192">Générer hello **URL de métadonnées** à l’aide de hello modèle : `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` et copiez cette valeur dans le bloc-notes, tel qu’il est utilisé ultérieurement pour la configuration de hello du plug-in hello.</span><span class="sxs-lookup"><span data-stu-id="1f052-192">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` and copy this value in notepad as it is used later for hello configuration of hello plugin.</span></span>

5. <span data-ttu-id="1f052-193">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="1f052-193">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1f052-195">Contact [Microsoft](mailto:waadpartners@microsoft.com) avec hello informations pour le plug-in de hello JIRA suivantes.</span><span class="sxs-lookup"><span data-stu-id="1f052-195">Contact [Microsoft](mailto:waadpartners@microsoft.com) with hello following information for hello JIRA plugin.</span></span>
    
    *   <span data-ttu-id="1f052-196">Nom du client :</span><span class="sxs-lookup"><span data-stu-id="1f052-196">Customer Name:</span></span>
    *   <span data-ttu-id="1f052-197">Nom du domaine principal :</span><span class="sxs-lookup"><span data-stu-id="1f052-197">Primary domain name:</span></span>
    *   <span data-ttu-id="1f052-198">Azure AD Premium : Oui/non (plug-in sera disponible tooall client de hello gratuit, Basic et Premium SKU)</span><span class="sxs-lookup"><span data-stu-id="1f052-198">Azure AD Premium: Yes/No (Plugin will be available tooall     hello customer Free, Basic, and Premium SKU)</span></span>
    *   <span data-ttu-id="1f052-199">Nombre d’utilisateurs qui vont utiliser cette intégration :</span><span class="sxs-lookup"><span data-stu-id="1f052-199">Number of users who will be using this integration:</span></span>
    *   <span data-ttu-id="1f052-200">Version JIRA :</span><span class="sxs-lookup"><span data-stu-id="1f052-200">JIRA Version:</span></span>
    *   <span data-ttu-id="1f052-201">Commentaires :</span><span class="sxs-lookup"><span data-stu-id="1f052-201">Comments:</span></span>

7. <span data-ttu-id="1f052-202">Dans une fenêtre de navigateur web, ouvrez une session dans l’instance JIRA tooyour en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="1f052-202">In a different web browser window, log in tooyour JIRA instance as an administrator.</span></span>

8. <span data-ttu-id="1f052-203">Pointez sur représentant une roue dentée et cliquez sur hello **modules complémentaires**.</span><span class="sxs-lookup"><span data-stu-id="1f052-203">Hover on cog and click hello **Add-ons**.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-jiramicrosoft-tutorial/addon1.png)

9. <span data-ttu-id="1f052-205">Sous l’onglet Add-ons (Modules complémentaires), cliquez sur **Manage add-ons** (Gérer les modules complémentaires).</span><span class="sxs-lookup"><span data-stu-id="1f052-205">Under Add-ons tab section, click **Manage add-ons**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-jiramicrosoft-tutorial/addon7.png)

10. <span data-ttu-id="1f052-207">Charger manuellement les plug-in hello fourni par Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1f052-207">Manually upload hello plugin provided by Microsoft.</span></span> <span data-ttu-id="1f052-208">Une fois que le plug-in hello est installé, il apparaît dans **utilisateur installé** section modules complémentaires de **gérer le module complémentaire** section.</span><span class="sxs-lookup"><span data-stu-id="1f052-208">Once hello plugin is installed, it appears in **User Installed** add-ons section of **Manage Add-on** section.</span></span>

11. <span data-ttu-id="1f052-209">Cliquez sur **configurer** tooconfigure hello nouveau plug-in.</span><span class="sxs-lookup"><span data-stu-id="1f052-209">Click **Configure** tooconfigure hello new plugin.</span></span>

12. <span data-ttu-id="1f052-210">Effectuez les opérations suivantes dans la page de configuration :</span><span class="sxs-lookup"><span data-stu-id="1f052-210">Perform following steps on configuration page:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-jiramicrosoft-tutorial/addon5.png)
 
    <span data-ttu-id="1f052-212">a.</span><span class="sxs-lookup"><span data-stu-id="1f052-212">a.</span></span> <span data-ttu-id="1f052-213">Dans **URL de métadonnées** coller hello **URL de métadonnées** généré à partir d’Azure AD et cliquez sur hello **résoudre** bouton.</span><span class="sxs-lookup"><span data-stu-id="1f052-213">In **Metadata URL** paste hello **Metadata URL** generated from Azure AD and click hello **Resolve** button.</span></span> <span data-ttu-id="1f052-214">Il lit les URL des métadonnées IdP hello et remplit toutes les informations de champs hello.</span><span class="sxs-lookup"><span data-stu-id="1f052-214">It reads hello IdP metadata URL and populates all hello fields information.</span></span>

    > [!Note]
    > <span data-ttu-id="1f052-215">Par défaut, l’emplacement de l’identificateur d’utilisateur SAML est défini sur l’élément NameIdentifier.</span><span class="sxs-lookup"><span data-stu-id="1f052-215">Default SAML User ID location is Name Identifier.</span></span> <span data-ttu-id="1f052-216">Vous pouvez modifier cette option d’attribut tooan et entrez le nom de l’attribut approprié hello.</span><span class="sxs-lookup"><span data-stu-id="1f052-216">You can change this tooan attribute option and enter hello appropriate attribute name.</span></span>

    > [!TIP]
    > <span data-ttu-id="1f052-217">Vérifiez qu’un seul certificat mappé par rapport à l’application hello afin qu’il n’existe aucune erreur dans la résolution des métadonnées de hello.</span><span class="sxs-lookup"><span data-stu-id="1f052-217">Ensure that there is only one certificate mapped against hello app so that there is no error in resolving hello metadata.</span></span> <span data-ttu-id="1f052-218">S’il existe plusieurs certificats, lors de la résolution des métadonnées de hello, admin Obtient une erreur.</span><span class="sxs-lookup"><span data-stu-id="1f052-218">If there are multiple certificates, upon resolving hello metadata, admin gets an error.</span></span>
    
    <span data-ttu-id="1f052-219">b.</span><span class="sxs-lookup"><span data-stu-id="1f052-219">b.</span></span> <span data-ttu-id="1f052-220">Hello de copie **identificateur, URL de réponse et l’URL de connexion** les valeurs et les coller dans **identificateur, URL de réponse et l’URL de connexion** zones de texte respectivement dans **SSO SAML de JIRA par domaine Microsoft et les URL** section sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1f052-220">Copy hello **Identifier, Reply URL and Sign on URL** values and paste them in **Identifier, Reply URL and Sign on URL** textboxes respectively in **JIRA SAML SSO by Microsoft Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="1f052-221">c.</span><span class="sxs-lookup"><span data-stu-id="1f052-221">c.</span></span> <span data-ttu-id="1f052-222">Dans **nom de bouton de connexion** nom de type hello du bouton de votre organisation souhaite toosee des utilisateurs hello sur l’écran de connexion.</span><span class="sxs-lookup"><span data-stu-id="1f052-222">In **Login Button Name** type hello name of button your organization wants hello users toosee on login screen.</span></span>

    <span data-ttu-id="1f052-223">d.</span><span class="sxs-lookup"><span data-stu-id="1f052-223">d.</span></span> <span data-ttu-id="1f052-224">Dans **les emplacements des ID utilisateur SAML** sélectionnez **ID d’utilisateur est dans l’élément NameIdentifier de hello Hello Subject statement** ou **ID utilisateur est dans un élément Attribute**.</span><span class="sxs-lookup"><span data-stu-id="1f052-224">In **SAML User ID Locations** select either **User ID is in hello NameIdentifier element of hello Subject statement** or **User ID is in an Attribute element**.</span></span>  <span data-ttu-id="1f052-225">Ce code a un id d’utilisateur JIRA toobe hello. Si l’id d’utilisateur hello n’est pas mis en correspondance, système ne permet pas de toolog d’utilisateurs dans.</span><span class="sxs-lookup"><span data-stu-id="1f052-225">This ID has toobe hello JIRA user id. If hello user id is not matched, then system will not allow users toolog in.</span></span> 
    
    <span data-ttu-id="1f052-226">e.</span><span class="sxs-lookup"><span data-stu-id="1f052-226">e.</span></span> <span data-ttu-id="1f052-227">Si vous sélectionnez **ID utilisateur est dans un élément Attribute** option, puis dans **nom de l’attribut** nom de hello de type zone de texte d’attribut hello lorsque l’Id d’utilisateur est attendu.</span><span class="sxs-lookup"><span data-stu-id="1f052-227">If you select **User ID is in an Attribute element** option, then in **Attribute name** textbox type hello name of hello attribute where User Id is expected.</span></span> 

    <span data-ttu-id="1f052-228">f.</span><span class="sxs-lookup"><span data-stu-id="1f052-228">f.</span></span> <span data-ttu-id="1f052-229">Si vous utilisez un domaine fédéré de hello (par exemple, ADFS, etc.) auprès d’Azure AD, puis cliquez sur hello **activer la découverte de domaine d’accueil** option et configurer hello **nom de domaine**.</span><span class="sxs-lookup"><span data-stu-id="1f052-229">If you are using hello federated domain (like ADFS etc.) with Azure AD, then click on hello **Enable Home Realm Discovery** option and configure hello **Domain Name**.</span></span>
    
    <span data-ttu-id="1f052-230">g.</span><span class="sxs-lookup"><span data-stu-id="1f052-230">g.</span></span> <span data-ttu-id="1f052-231">Dans **nom de domaine** hello domaine nom de type ici en cas de connexion de base de ADFS hello.</span><span class="sxs-lookup"><span data-stu-id="1f052-231">In **Domain Name** type hello domain name here in case of hello ADFS-based login.</span></span>

    <span data-ttu-id="1f052-232">h.</span><span class="sxs-lookup"><span data-stu-id="1f052-232">h.</span></span> <span data-ttu-id="1f052-233">Vérifiez **activer la déconnexion unique** si vous souhaitez toolog out d’Azure AD quand un utilisateur se déconnecte de JIRA.</span><span class="sxs-lookup"><span data-stu-id="1f052-233">Check **Enable Single Sign out** if you wish toolog out from Azure AD when a user logs out from JIRA.</span></span> 

    <span data-ttu-id="1f052-234">i.</span><span class="sxs-lookup"><span data-stu-id="1f052-234">i.</span></span> <span data-ttu-id="1f052-235">Cliquez sur **enregistrer** bouton Paramètres de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="1f052-235">Click **Save** button toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="1f052-236">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="1f052-236">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1f052-237">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="1f052-237">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1f052-238">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1f052-238">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1f052-239">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f052-239">Creating an Azure AD test user</span></span>
<span data-ttu-id="1f052-240">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="1f052-240">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="1f052-242">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1f052-242">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1f052-243">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="1f052-243">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1f052-245">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="1f052-245">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1f052-247">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="1f052-247">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1f052-249">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="1f052-249">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1f052-251">a.</span><span class="sxs-lookup"><span data-stu-id="1f052-251">a.</span></span> <span data-ttu-id="1f052-252">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1f052-252">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1f052-253">b.</span><span class="sxs-lookup"><span data-stu-id="1f052-253">b.</span></span> <span data-ttu-id="1f052-254">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1f052-254">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1f052-255">c.</span><span class="sxs-lookup"><span data-stu-id="1f052-255">c.</span></span> <span data-ttu-id="1f052-256">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="1f052-256">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1f052-257">d.</span><span class="sxs-lookup"><span data-stu-id="1f052-257">d.</span></span> <span data-ttu-id="1f052-258">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="1f052-258">Click **Create**.</span></span>
 
### <a name="creating-a-jira-saml-sso-by-microsoft-test-user"></a><span data-ttu-id="1f052-259">Création d’un utilisateur de test JIRA SAML SSO by Microsoft</span><span class="sxs-lookup"><span data-stu-id="1f052-259">Creating a JIRA SAML SSO by Microsoft test user</span></span>

<span data-ttu-id="1f052-260">toolog d’utilisateurs tooenable Azure AD dans le serveur local de tooJIRA, ils doivent être configurés dans JIRA SAML SSO par Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1f052-260">tooenable Azure AD users toolog in tooJIRA on-premise server, they must be provisioned into JIRA SAML SSO by Microsoft.</span></span> <span data-ttu-id="1f052-261">Pour JIRA SAML SSO by Microsoft, l’attribution des utilisateurs se fait manuellement.</span><span class="sxs-lookup"><span data-stu-id="1f052-261">For JIRA SAML SSO by Microsoft, provisioning is a manual task.</span></span>

<span data-ttu-id="1f052-262">**tooprovision un compte d’utilisateur, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1f052-262">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="1f052-263">Ouvrez une session dans tooyour JIRA sur site serveur en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="1f052-263">Log in tooyour JIRA on-premise server as an administrator.</span></span>

2. <span data-ttu-id="1f052-264">Pointez sur représentant une roue dentée et cliquez sur hello **gestion des utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="1f052-264">Hover on cog and click hello **User management**.</span></span>

    ![Ajouter un employé](./media/active-directory-saas-jiramicrosoft-tutorial/user1.png) 

3. <span data-ttu-id="1f052-266">Vous êtes redirigé tooAdministrator accès page tooenter **mot de passe** et cliquez sur **confirmer** bouton.</span><span class="sxs-lookup"><span data-stu-id="1f052-266">You are redirected tooAdministrator Access page tooenter **Password** and click **Confirm** button.</span></span>

    ![Ajouter un employé](./media/active-directory-saas-jiramicrosoft-tutorial/user2.png) 

4. <span data-ttu-id="1f052-268">Sous l’onglet **User management** (Gestion des utilisateurs), cliquez sur **Create user** (Créer un utilisateur).</span><span class="sxs-lookup"><span data-stu-id="1f052-268">Under **User management** tab section, click **create user**.</span></span>

    ![Ajouter un employé](./media/active-directory-saas-jiramicrosoft-tutorial/user3.png) 

5. <span data-ttu-id="1f052-270">Sur hello **« Créer un utilisateur »** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="1f052-270">On hello **“Create new user”** dialog page, perform hello following steps:</span></span>

    ![Ajouter un employé](./media/active-directory-saas-jiramicrosoft-tutorial/user4.png) 

    <span data-ttu-id="1f052-272">a.</span><span class="sxs-lookup"><span data-stu-id="1f052-272">a.</span></span> <span data-ttu-id="1f052-273">Bonjour **adresse de messagerie** adresse de messagerie de type hello d’utilisateur de zone de texte, comme Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="1f052-273">In hello **Email address** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="1f052-274">b.</span><span class="sxs-lookup"><span data-stu-id="1f052-274">b.</span></span> <span data-ttu-id="1f052-275">Bonjour **nom complet** zone de texte, nom complet du type d’utilisateur hello comme Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1f052-275">In hello **Full Name** textbox, type full name of hello user like Britta Simon.</span></span>

    <span data-ttu-id="1f052-276">c.</span><span class="sxs-lookup"><span data-stu-id="1f052-276">c.</span></span> <span data-ttu-id="1f052-277">Bonjour **nom d’utilisateur** par courrier électronique de type hello d’utilisateur de zone de texte, comme Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="1f052-277">In hello **Username** textbox, type hello email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="1f052-278">d.</span><span class="sxs-lookup"><span data-stu-id="1f052-278">d.</span></span> <span data-ttu-id="1f052-279">Bonjour **mot de passe** zone de texte, un mot de passe hello type d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1f052-279">In hello **Password** textbox, type hello password of user.</span></span>

    <span data-ttu-id="1f052-280">e.</span><span class="sxs-lookup"><span data-stu-id="1f052-280">e.</span></span> <span data-ttu-id="1f052-281">Cliquez sur **Create User** (Créer un utilisateur).</span><span class="sxs-lookup"><span data-stu-id="1f052-281">Click **Create user**.</span></span>   

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1f052-282">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f052-282">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1f052-283">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooJIRA SSO SAML par Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1f052-283">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooJIRA SAML SSO by Microsoft.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="1f052-285">**tooassign Britta Simon tooJIRA SSO SAML par Microsoft, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1f052-285">**tooassign Britta Simon tooJIRA SAML SSO by Microsoft, perform hello following steps:**</span></span>

1. <span data-ttu-id="1f052-286">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1f052-286">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="1f052-288">Dans la liste des applications hello, sélectionnez **SSO SAML de JIRA par Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="1f052-288">In hello applications list, select **JIRA SAML SSO by Microsoft**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_app.png) 

3. <span data-ttu-id="1f052-290">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1f052-290">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="1f052-292">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="1f052-292">Click **Add** button.</span></span> <span data-ttu-id="1f052-293">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="1f052-293">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="1f052-295">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="1f052-295">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1f052-296">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1f052-296">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1f052-297">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="1f052-297">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1f052-298">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="1f052-298">Testing single sign-on</span></span>

<span data-ttu-id="1f052-299">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="1f052-299">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1f052-300">Lorsque vous cliquez sur hello JIRA SAML SSO par vignette Microsoft Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour JIRA SAML SSO par application de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1f052-300">When you click hello JIRA SAML SSO by Microsoft tile in hello Access Panel, you should get automatically signed-on tooyour JIRA SAML SSO by Microsoft application.</span></span>
<span data-ttu-id="1f052-301">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1f052-301">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1f052-302">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="1f052-302">Additional resources</span></span>

* [<span data-ttu-id="1f052-303">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1f052-303">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1f052-304">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="1f052-304">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_203.png

