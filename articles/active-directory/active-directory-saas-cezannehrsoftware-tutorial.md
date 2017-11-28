---
title: "Didacticiel : Intégration d’Azure Active Directory avec le logiciel Cezanne HR | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et les logiciels Cezanne HR."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fb8f95bf-c3c1-4e1f-b2b3-3b67526be72d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 3675acd8871d62c2277def8074f7aa39ac46e2a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-cezanne-hr-software"></a><span data-ttu-id="15b4b-103">Didacticiel : Intégration d’Azure Active Directory avec le logiciel Cezanne HR</span><span class="sxs-lookup"><span data-stu-id="15b4b-103">Tutorial: Integrate Azure Active Directory with Cezanne HR software</span></span>

<span data-ttu-id="15b4b-104">Dans ce didacticiel, vous apprendrez comment toointegrate logiciel Cezanne HR avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="15b4b-104">In this tutorial, you learn how toointegrate Cezanne HR software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="15b4b-105">Intégration du logiciel de Cezanne HR avec Azure AD fournit hello avantages suivants.</span><span class="sxs-lookup"><span data-stu-id="15b4b-105">Integrating Cezanne HR software with Azure AD provides you with hello following benefits.</span></span> <span data-ttu-id="15b4b-106">Vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="15b4b-106">You can:</span></span>

- <span data-ttu-id="15b4b-107">Dans Azure AD qui a accès tooCezanne HR logiciel contrôle.</span><span class="sxs-lookup"><span data-stu-id="15b4b-107">Control in Azure AD who has access tooCezanne HR software.</span></span>
- <span data-ttu-id="15b4b-108">Activer vos informations d’identification tooautomatically utilisateurs logiciel tooCezanne HR avec session unique (SSO) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="15b4b-108">Enable your users tooautomatically sign in tooCezanne HR software with single sign-on (SSO) with their Azure AD accounts.</span></span>
- <span data-ttu-id="15b4b-109">Gérer vos comptes dans un emplacement central : hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="15b4b-109">Manage your accounts in one central location: hello Azure portal.</span></span>

<span data-ttu-id="15b4b-110">toolearn savoir plus sur le logiciel en tant qu’une intégration d’application de service (SaaS) avec Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="15b4b-110">toolearn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and SSO with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="15b4b-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="15b4b-111">Prerequisites</span></span>

<span data-ttu-id="15b4b-112">tooconfigure intégration d’Azure AD avec Cezanne HR logiciel, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="15b4b-112">tooconfigure Azure AD integration with Cezanne HR software, you need hello following items:</span></span>

- <span data-ttu-id="15b4b-113">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="15b4b-113">An Azure AD subscription</span></span>
- <span data-ttu-id="15b4b-114">Un abonnement au logiciel Cezanne HR pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="15b4b-114">A Cezanne HR software SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="15b4b-115">tootest hello étapes décrites dans ce didacticiel, nous vous recommandons de ne pas utiliser un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="15b4b-115">tootest hello steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="15b4b-116">étapes de hello tootest dans ce didacticiel, suivez ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="15b4b-116">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="15b4b-117">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="15b4b-117">Don't use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="15b4b-118">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="15b4b-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="15b4b-119">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="15b4b-119">Scenario description</span></span>
<span data-ttu-id="15b4b-120">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="15b4b-120">In this tutorial, you test Azure AD SSO in a test environment.</span></span> 

<span data-ttu-id="15b4b-121">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="15b4b-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="15b4b-122">Ajout d’un logiciel de Cezanne HR à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="15b4b-122">Adding Cezanne HR software from hello gallery</span></span>
* <span data-ttu-id="15b4b-123">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="15b4b-123">Configuring and testing Azure AD SSO</span></span>

## <a name="add-cezanne-hr-software-from-hello-gallery"></a><span data-ttu-id="15b4b-124">Ajouter le logiciel de Cezanne HR à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="15b4b-124">Add Cezanne HR software from hello gallery</span></span>
<span data-ttu-id="15b4b-125">intégration de hello tooconfigure du logiciel de Cezanne HR dans Azure AD, ajoutez le logiciel de Cezanne HR à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="15b4b-125">tooconfigure hello integration of Cezanne HR software into Azure AD, add Cezanne HR software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="15b4b-126">tooadd Cezanne HR des logiciels à partir de la galerie hello, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="15b4b-126">tooadd Cezanne HR software from hello gallery, do hello following:</span></span>

1. <span data-ttu-id="15b4b-127">Bonjour  **[portail Azure](https://portal.azure.com)**hello du volet gauche, dans Sélectionnez hello **Azure Active Directory** bouton.</span><span class="sxs-lookup"><span data-stu-id="15b4b-127">In hello **[Azure portal](https://portal.azure.com)**, in hello left pane, select hello **Azure Active Directory** button.</span></span> 

    ![bouton de « Azure Active Directory » Hello][1]

2. <span data-ttu-id="15b4b-129">Sélectionnez **Applications d’entreprise** > **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="15b4b-129">Select **Enterprise applications** > **All applications**.</span></span>

    ![lient Hello « Toutes les applications »][2]
    
3. <span data-ttu-id="15b4b-131">tooadd une nouvelle application, en haut de hello Hello **toutes les applications** boîte de dialogue, sélectionnez **nouvelle application**.</span><span class="sxs-lookup"><span data-stu-id="15b4b-131">tooadd a new application, at hello top of hello **All applications** dialog box, select **New application**.</span></span>

    ![Hello « Nouvelle application » bouton][3]

4. <span data-ttu-id="15b4b-133">Dans la zone de recherche de hello, tapez **Cezanne HR logiciel**.</span><span class="sxs-lookup"><span data-stu-id="15b4b-133">In hello search box, type **Cezanne HR Software**.</span></span>

    ![zone de recherche Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_search.png)

5. <span data-ttu-id="15b4b-135">Dans la liste des résultats hello, sélectionnez **Cezanne HR logiciel** , puis sélectionnez hello **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="15b4b-135">In hello results list, select **Cezanne HR Software** and then select hello **Add** button tooadd hello application.</span></span>

    ![liste des résultats Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="15b4b-137">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="15b4b-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="15b4b-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec le logiciel Cezanne HR, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="15b4b-138">In this section, you configure and test Azure AD SSO with Cezanne HR software based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="15b4b-139">Pour l’authentification unique toowork, Azure AD doit tooknow hello Cezanne HR équivalent toohello Azure AD utilisateur.</span><span class="sxs-lookup"><span data-stu-id="15b4b-139">For SSO toowork, Azure AD needs tooknow hello Cezanne HR software counterpart toohello Azure AD user.</span></span> <span data-ttu-id="15b4b-140">En d’autres termes, vous devez établir une relation de lien entre un utilisateur Azure AD et un utilisateur hello Bonjour Cezanne HR logiciel.</span><span class="sxs-lookup"><span data-stu-id="15b4b-140">In other words, you must establish a link relationship between an Azure AD user and hello related user in hello Cezanne HR software.</span></span>

<span data-ttu-id="15b4b-141">relation de lien de hello tooestablish, affecter hello Cezanne HR logiciel **nom d’utilisateur** valeur comme hello Azure AD **nom d’utilisateur** valeur.</span><span class="sxs-lookup"><span data-stu-id="15b4b-141">tooestablish hello link relationship, assign hello Cezanne HR software **user name** value as hello Azure AD **Username** value.</span></span>

<span data-ttu-id="15b4b-142">tooconfigure et test de l’authentification unique de Azure AD à l’aide de logiciels Cezanne HR, hello terminée après les blocs de construction.</span><span class="sxs-lookup"><span data-stu-id="15b4b-142">tooconfigure and test Azure AD SSO by using Cezanne HR software, complete hello following building blocks.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="15b4b-143">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="15b4b-143">Configure Azure AD SSO</span></span>

<span data-ttu-id="15b4b-144">Dans cette section, vous pouvez activer l’authentification unique de Azure AD Bonjour portail Azure et configurer l’authentification unique dans votre application Cezanne HR de manière hello suivante :</span><span class="sxs-lookup"><span data-stu-id="15b4b-144">In this section, you can enable Azure AD SSO in hello Azure portal and configure SSO in your Cezanne HR software application by doing hello following:</span></span>

1. <span data-ttu-id="15b4b-145">Bonjour portail Azure, sur hello **Cezanne HR logiciel** page d’intégration d’application, sélectionnez **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="15b4b-145">In hello Azure portal, on hello **Cezanne HR Software** application integration page, select **Single sign-on**.</span></span>

    ![Hello « Sur l’authentification unique » de commande][4]

2. <span data-ttu-id="15b4b-147">tooenable SSO, Bonjour **l’authentification unique** boîte de dialogue, sélectionnez hello **Mode** en tant que **SAML-authentification**.</span><span class="sxs-lookup"><span data-stu-id="15b4b-147">tooenable SSO, in hello **Single sign-on** dialog box, select hello **Mode** as **SAML-based Sign-on**.</span></span>
 
    ![zone de « Mode » Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_samlbase.png)

3. <span data-ttu-id="15b4b-149">Sous **Cezanne HR logiciel domaine et les URL**, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="15b4b-149">Under **Cezanne HR Software Domain and URLs**, do hello following:</span></span>

    ![Hello « Cezanne HR logiciel et les URL de domaines » section](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_url.png)

    <span data-ttu-id="15b4b-151">a.</span><span class="sxs-lookup"><span data-stu-id="15b4b-151">a.</span></span> <span data-ttu-id="15b4b-152">Bonjour **URL de connexion** zone, tapez une URL qui a hello selon la syntaxe :`https://w3.cezanneondemand.com/cezannehr/-/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="15b4b-152">In hello **Sign-on URL** box, type a URL that has hello following syntax: `https://w3.cezanneondemand.com/cezannehr/-/<tenant id>`</span></span>

    <span data-ttu-id="15b4b-153">b.</span><span class="sxs-lookup"><span data-stu-id="15b4b-153">b.</span></span> <span data-ttu-id="15b4b-154">Bonjour **URL de réponse** zone, tapez une URL qui a hello selon la syntaxe :`https://w3.cezanneondemand.com:443/<tenantid>`</span><span class="sxs-lookup"><span data-stu-id="15b4b-154">In hello **Reply URL** box, type a URL that has hello following syntax: `https://w3.cezanneondemand.com:443/<tenantid>`</span></span>    
     
    > [!NOTE] 
    > <span data-ttu-id="15b4b-155">Hello les valeurs précédentes ne sont pas réelles.</span><span class="sxs-lookup"><span data-stu-id="15b4b-155">hello preceding values are not real.</span></span> <span data-ttu-id="15b4b-156">Mettre à jour les URL de réponse réelle hello et URL de connexion hello.</span><span class="sxs-lookup"><span data-stu-id="15b4b-156">Update them with hello actual reply URL and hello sign-on URL.</span></span> <span data-ttu-id="15b4b-157">les valeurs hello tooobtain, contact hello [équipe du support client Cezanne HR logiciel](mailto:info@cezannehr.com).</span><span class="sxs-lookup"><span data-stu-id="15b4b-157">tooobtain hello values, contact hello [Cezanne HR software client support team](mailto:info@cezannehr.com).</span></span>

4. <span data-ttu-id="15b4b-158">Sous **le certificat de signature SAML**, sélectionnez **certificat (Base64)**, puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="15b4b-158">Under **SAML Signing Certificate**, select **Certificate (Base64)**, and then save hello certificate file on your computer.</span></span>

    ![Hello section « Certificat de signature SAML »](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_certificate.png) 

5. <span data-ttu-id="15b4b-160">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="15b4b-160">Select **Save**.</span></span>

    ![bouton « Enregistrer » de Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="15b4b-162">Sous **Cezanne HR logiciel Configuration**, sélectionnez **configurer le logiciel HR Cezanne** tooopen hello **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="15b4b-162">Under **Cezanne HR Software Configuration**, select **Configure Cezanne HR Software** tooopen hello **Configure sign-on** window.</span></span> <span data-ttu-id="15b4b-163">Hello de copie **ID d’entité SAML** et **SAML Single Sign-On Service** URL à partir de hello **aide-mémoire** section.</span><span class="sxs-lookup"><span data-stu-id="15b4b-163">Copy hello **SAML Entity ID** and **SAML Single Sign-On Service** URL from hello **Quick Reference** section.</span></span>

    ![Hello section « Configuration de logiciels Cezanne HR »](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_configure.png) 

7. <span data-ttu-id="15b4b-165">Dans une fenêtre de navigateur web, connectez-vous sur le client de logiciel tooyour Cezanne HR en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="15b4b-165">In a different web browser window, sign on tooyour Cezanne HR software tenant as an administrator.</span></span>

8. <span data-ttu-id="15b4b-166">Dans le volet gauche de hello, sélectionnez **le programme d’installation du système**.</span><span class="sxs-lookup"><span data-stu-id="15b4b-166">In hello left pane, select **System Setup**.</span></span> <span data-ttu-id="15b4b-167">Sélectionnez **Paramètres de sécurité** > **Configuration d’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="15b4b-167">Select **Security Settings** > **Single Sign-On Configuration**.</span></span>

    ![lien de « Seule Configuration d’authentification » Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_000.png)

9. <span data-ttu-id="15b4b-169">Bonjour **autoriser toolog les utilisateurs à l’aide de hello suivant les services Single Sign-On (SSO)** volet, sélectionnez hello **SAML 2.0** case à cocher et sélectionnez hello **Configuration avancée** option.</span><span class="sxs-lookup"><span data-stu-id="15b4b-169">In hello **Allow users toolog in using hello following Single Sign-On (SSO) services** pane, select hello **SAML 2.0** check box and select hello **Advanced Configuration** option.</span></span>

    ![Options des services d’authentification unique](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_001.png)

10. <span data-ttu-id="15b4b-171">Sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="15b4b-171">Select **Add New**.</span></span>

    ![bouton « Nouveau » de Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_002.png)

11. <span data-ttu-id="15b4b-173">Sous **fournisseurs d’identité SAML 2.0**, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="15b4b-173">Under **SAML 2.0 Identity Providers**, do hello following:</span></span>

    ![Hello section « Fournisseurs d’identité SAML 2.0 »](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_003.png)
    
    <span data-ttu-id="15b4b-175">a.</span><span class="sxs-lookup"><span data-stu-id="15b4b-175">a.</span></span> <span data-ttu-id="15b4b-176">Bonjour **nom d’affichage** , entrez le nom hello de votre fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="15b4b-176">In hello **Display Name** box, enter hello name of your identity provider.</span></span>

    <span data-ttu-id="15b4b-177">b.</span><span class="sxs-lookup"><span data-stu-id="15b4b-177">b.</span></span> <span data-ttu-id="15b4b-178">Bonjour **identificateur d’entité** zone, collez hello **ID d’entité SAML** que vous avez copié à partir de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="15b4b-178">In hello **Entity Identifier** box, paste hello **SAML Entity ID** that you copied from hello Azure portal.</span></span> 

    <span data-ttu-id="15b4b-179">c.</span><span class="sxs-lookup"><span data-stu-id="15b4b-179">c.</span></span> <span data-ttu-id="15b4b-180">Bonjour **SAML liaison** zone de liste, sélectionnez **POST**.</span><span class="sxs-lookup"><span data-stu-id="15b4b-180">In hello **SAML Binding** list box, select **POST**.</span></span>

    <span data-ttu-id="15b4b-181">d.</span><span class="sxs-lookup"><span data-stu-id="15b4b-181">d.</span></span> <span data-ttu-id="15b4b-182">Bonjour **point de terminaison Service de jeton de sécurité** zone, collez hello **SAML Single Sign-On Service** URL que vous avez copié à partir de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="15b4b-182">In hello **Security Token Service Endpoint** box, paste hello **SAML Single Sign-On Service** URL that you copied from hello Azure portal.</span></span> 
    
    <span data-ttu-id="15b4b-183">e.</span><span class="sxs-lookup"><span data-stu-id="15b4b-183">e.</span></span> <span data-ttu-id="15b4b-184">Bonjour **nom de l’attribut ID utilisateur** , entrez `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="15b4b-184">In hello **User ID Attribute Name** box, enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
    
    <span data-ttu-id="15b4b-185">f.</span><span class="sxs-lookup"><span data-stu-id="15b4b-185">f.</span></span> <span data-ttu-id="15b4b-186">hello de tooupload téléchargé le certificat à partir d’Azure AD, sélectionnez hello **télécharger** bouton.</span><span class="sxs-lookup"><span data-stu-id="15b4b-186">tooupload hello downloaded certificate from Azure AD, select hello **Upload** button.</span></span>
    
    <span data-ttu-id="15b4b-187">g.</span><span class="sxs-lookup"><span data-stu-id="15b4b-187">g.</span></span> <span data-ttu-id="15b4b-188">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="15b4b-188">Select **OK**.</span></span> 

12. <span data-ttu-id="15b4b-189">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="15b4b-189">Select **Save**.</span></span>

    ![bouton « Enregistrer » de Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_004.png)

> [!TIP]
> <span data-ttu-id="15b4b-191">Lorsque vous définissez application hello, vous pouvez lire une version concise de hello précédant les instructions dans hello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="15b4b-191">As you set up hello app, you can read a concise version of hello preceding instructions in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="15b4b-192">Après avoir ajouté l’application hello de hello **Active Directory** > **des applications d’entreprise** section, sélectionnez hello **l’authentification unique** onglet. Hello d’accès incorporée documentation hello **Configuration** section.</span><span class="sxs-lookup"><span data-stu-id="15b4b-192">After you add hello app from hello **Active Directory** > **Enterprise applications** section, select hello **Single sign-on** tab. Then access hello embedded documentation from hello **Configuration** section.</span></span> 

<span data-ttu-id="15b4b-193">toolearn en savoir plus sur la fonctionnalité de documentation embedded hello, consultez [AD Azure incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="15b4b-193">toolearn more about hello embedded documentation feature, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="15b4b-194">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="15b4b-194">Create an Azure AD test user</span></span>
<span data-ttu-id="15b4b-195">Dans cette section, vous créez utilisateur test Britta Simon Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="15b4b-195">In this section, you create test user Britta Simon in hello Azure portal.</span></span>

![utilisateur de test Hello Britta Simon][100]

<span data-ttu-id="15b4b-197">toocreate un utilisateur test dans Azure AD, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="15b4b-197">toocreate a test user in Azure AD, do hello following:</span></span>

1. <span data-ttu-id="15b4b-198">Bonjour **portail Azure**hello du volet gauche, dans Sélectionnez hello **Azure Active Directory** bouton.</span><span class="sxs-lookup"><span data-stu-id="15b4b-198">In hello **Azure portal**, in hello left pane, select hello **Azure Active Directory** button.</span></span>

    ![bouton de « Azure Active Directory » Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="15b4b-200">liste de hello toodisplay d’utilisateurs, sélectionnez **utilisateurs et groupes** > **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="15b4b-200">toodisplay hello list of users, select **Users and groups** > **All users**.</span></span>
    
    ![lien Hello « Tous les utilisateurs »](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_02.png) 
    
    <span data-ttu-id="15b4b-202">Hello **tous les utilisateurs** boîte de dialogue s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="15b4b-202">hello **All users** dialog box opens.</span></span>

3. <span data-ttu-id="15b4b-203">tooopen hello **utilisateur** boîte de dialogue, sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="15b4b-203">tooopen hello **User** dialog box, select **Add**.</span></span>
 
    ![bouton « Ajouter » de Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="15b4b-205">Bonjour **utilisateur** boîte de dialogue zone, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="15b4b-205">In hello **User** dialog box, do hello following:</span></span>
 
    ![boîte de dialogue Hello « Utilisateur »](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="15b4b-207">a.</span><span class="sxs-lookup"><span data-stu-id="15b4b-207">a.</span></span> <span data-ttu-id="15b4b-208">Bonjour **nom** , tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="15b4b-208">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="15b4b-209">b.</span><span class="sxs-lookup"><span data-stu-id="15b4b-209">b.</span></span> <span data-ttu-id="15b4b-210">Bonjour **nom d’utilisateur** zone utilisateur Britta Simon **adresse de messagerie**.</span><span class="sxs-lookup"><span data-stu-id="15b4b-210">In hello **User name** box, type user Britta Simon's **email address**.</span></span>

    <span data-ttu-id="15b4b-211">c.</span><span class="sxs-lookup"><span data-stu-id="15b4b-211">c.</span></span> <span data-ttu-id="15b4b-212">Sélectionnez hello **afficher le mot de passe** case à cocher, puis sur valeur hello Remarque qui a été générée dans hello **mot de passe** boîte.</span><span class="sxs-lookup"><span data-stu-id="15b4b-212">Select hello **Show Password** check box, and then note hello value that was generated in hello **Password** box.</span></span>

    <span data-ttu-id="15b4b-213">d.</span><span class="sxs-lookup"><span data-stu-id="15b4b-213">d.</span></span> <span data-ttu-id="15b4b-214">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="15b4b-214">Select **Create**.</span></span>
 
### <a name="create-a-cezanne-hr-software-test-user"></a><span data-ttu-id="15b4b-215">Créer un utilisateur de test pour le logiciel Cezanne HR</span><span class="sxs-lookup"><span data-stu-id="15b4b-215">Create a Cezanne HR software test user</span></span>

<span data-ttu-id="15b4b-216">tooenable Azure AD les utilisateurs toosign dans tooCezanne HR logiciel, vous devez les configurer dans Cezanne HR logiciel.</span><span class="sxs-lookup"><span data-stu-id="15b4b-216">tooenable Azure AD users toosign in tooCezanne HR software, they must be provisioned into Cezanne HR software.</span></span> <span data-ttu-id="15b4b-217">Dans les cas de hello du logiciel de Cezanne HR, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="15b4b-217">In hello case of Cezanne HR software, provisioning is a manual task.</span></span>

<span data-ttu-id="15b4b-218">Configurer un compte d’utilisateur de manière hello suivante :</span><span class="sxs-lookup"><span data-stu-id="15b4b-218">Provision a user account by doing hello following:</span></span>

1.  <span data-ttu-id="15b4b-219">Se connecter tooyour site d’entreprise Cezanne HR software en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="15b4b-219">Sign in tooyour Cezanne HR software company site as an administrator.</span></span>

2.  <span data-ttu-id="15b4b-220">Dans le volet gauche de hello, sélectionnez **le programme d’installation de système** > **gérer les utilisateurs** > **ajouter un nouvel utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="15b4b-220">In hello left pane, select **System Setup** > **Manage Users** > **Add New User**.</span></span>

    <span data-ttu-id="15b4b-221">![lien de « Ajouter un nouvel utilisateur » Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "nouvel utilisateur")</span><span class="sxs-lookup"><span data-stu-id="15b4b-221">![hello "Add New User" link](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "New User")</span></span>

3.  <span data-ttu-id="15b4b-222">Sous **détails de la personne**, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="15b4b-222">Under **Person Details**, do hello following:</span></span>

    <span data-ttu-id="15b4b-223">![Hello section « Détails de la personne »](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "nouvel utilisateur")</span><span class="sxs-lookup"><span data-stu-id="15b4b-223">![hello "Person Details" section](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "New User")</span></span>
    
    <span data-ttu-id="15b4b-224">a.</span><span class="sxs-lookup"><span data-stu-id="15b4b-224">a.</span></span> <span data-ttu-id="15b4b-225">Paramétrez **Utilisateur interne** sur **Désactivé**.</span><span class="sxs-lookup"><span data-stu-id="15b4b-225">Set **Internal User** as **OFF**.</span></span>
    
    <span data-ttu-id="15b4b-226">b.</span><span class="sxs-lookup"><span data-stu-id="15b4b-226">b.</span></span> <span data-ttu-id="15b4b-227">Bonjour **prénom** zone, l’utilisateur de type hello prénom, par exemple, **Brian**.</span><span class="sxs-lookup"><span data-stu-id="15b4b-227">In hello **First Name** box, type hello user's first name, for example, **Britta**.</span></span>  
 
    <span data-ttu-id="15b4b-228">c.</span><span class="sxs-lookup"><span data-stu-id="15b4b-228">c.</span></span> <span data-ttu-id="15b4b-229">Bonjour **nom** boîte, de type hello nom de l’utilisateur, par exemple, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="15b4b-229">In hello **Last Name** box, type hello user's last name, for example, **Simon**.</span></span>
    
    <span data-ttu-id="15b4b-230">d.</span><span class="sxs-lookup"><span data-stu-id="15b4b-230">d.</span></span> <span data-ttu-id="15b4b-231">Bonjour **messagerie** , tapez Bonjour son adresse électronique, par exemple, Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="15b4b-231">In hello **E-mail** box, type hello user's email address, for example, Brittasimon@contoso.com.</span></span>

4.  <span data-ttu-id="15b4b-232">Sous **les informations de compte**, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="15b4b-232">Under **Account Information**, do hello following:</span></span>

    <span data-ttu-id="15b4b-233">![Hello section « Informations de compte »](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "nouvel utilisateur")</span><span class="sxs-lookup"><span data-stu-id="15b4b-233">![hello "Account Information" section](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "New User")</span></span>
    
    <span data-ttu-id="15b4b-234">a.</span><span class="sxs-lookup"><span data-stu-id="15b4b-234">a.</span></span> <span data-ttu-id="15b4b-235">Bonjour **nom d’utilisateur** , tapez Bonjour son adresse électronique, par exemple, Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="15b4b-235">In hello **Username** box, type hello user's email address, for example, Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="15b4b-236">b.</span><span class="sxs-lookup"><span data-stu-id="15b4b-236">b.</span></span> <span data-ttu-id="15b4b-237">Bonjour **mot de passe** , tapez le mot de passe de l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="15b4b-237">In hello **Password** box, type hello user's password.</span></span>
    
    <span data-ttu-id="15b4b-238">c.</span><span class="sxs-lookup"><span data-stu-id="15b4b-238">c.</span></span> <span data-ttu-id="15b4b-239">Bonjour **rôle de sécurité** boîte, sélectionnez **HR Professionnel**.</span><span class="sxs-lookup"><span data-stu-id="15b4b-239">In hello **Security Role** box, select **HR Professional**.</span></span>
    
    <span data-ttu-id="15b4b-240">d.</span><span class="sxs-lookup"><span data-stu-id="15b4b-240">d.</span></span> <span data-ttu-id="15b4b-241">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="15b4b-241">Select **OK**.</span></span>

5. <span data-ttu-id="15b4b-242">Sur hello **l’authentification unique** onglet hello **SAML 2.0 identificateurs** section, sélectionnez **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="15b4b-242">On hello **Single sign-on** tab, in hello **SAML 2.0 Identifiers** section, select **Add New**.</span></span>

    <span data-ttu-id="15b4b-243">![bouton « Nouveau » de Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "utilisateur")</span><span class="sxs-lookup"><span data-stu-id="15b4b-243">![hello "Add New" button](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "User")</span></span>

6. <span data-ttu-id="15b4b-244">Bonjour **fournisseur d’identité** zone de liste, sélectionnez votre fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="15b4b-244">In hello **Identity Provider** list box, select your identity provider.</span></span> <span data-ttu-id="15b4b-245">Bonjour **identificateur de l’utilisateur** , entrez l’adresse de messagerie hello pour le compte de test utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="15b4b-245">In hello **User Identifier** box, enter hello email address for test user Britta Simon's account.</span></span>

    <span data-ttu-id="15b4b-246">![Hello zones « Fournisseur d’identité » et « Identificateur d’utilisateur »](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "utilisateur")</span><span class="sxs-lookup"><span data-stu-id="15b4b-246">![hello "Identity Provider" and "User Identifier" boxes](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "User")</span></span>
    
7. <span data-ttu-id="15b4b-247">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="15b4b-247">Select **Save**.</span></span>

    <span data-ttu-id="15b4b-248">![bouton « Enregistrer » de Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "utilisateur")</span><span class="sxs-lookup"><span data-stu-id="15b4b-248">![hello "Save" button](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "User")</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="15b4b-249">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="15b4b-249">Assign hello Azure AD test user</span></span>

<span data-ttu-id="15b4b-250">Dans cette section, vous activez l’utilisateur de test Britta Simon toouse Azure SSO en accordant l’accès tooCezanne HR logiciel.</span><span class="sxs-lookup"><span data-stu-id="15b4b-250">In this section, you enable test user Britta Simon toouse Azure SSO by granting access tooCezanne HR software.</span></span>

![Accès de l’utilisateur de test][200] 

1. <span data-ttu-id="15b4b-252">Bonjour portail Azure, ouvrez la vue des applications hello et passez toohello vue d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="15b4b-252">In hello Azure portal, open hello applications view and then go toohello directory view.</span></span> <span data-ttu-id="15b4b-253">Sélectionnez **Applications d’entreprise** > **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="15b4b-253">Select **Enterprise applications** > **All applications**.</span></span>

    ![lient Hello « Toutes les applications »][201] 

2. <span data-ttu-id="15b4b-255">Dans la liste des applications hello, sélectionnez **Cezanne HR logiciel**.</span><span class="sxs-lookup"><span data-stu-id="15b4b-255">In hello applications list, select **Cezanne HR Software**.</span></span>

    ![liste des « Applications » Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_app.png) 

3. <span data-ttu-id="15b4b-257">Dans le menu hello hello gauche, sélectionnez **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="15b4b-257">In hello menu on hello left, select **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="15b4b-259">Sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="15b4b-259">Select **Add**.</span></span> <span data-ttu-id="15b4b-260">Ensuite, dans hello **ajouter l’affectation** boîte de dialogue, sélectionnez **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="15b4b-260">Then in hello **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![Lien Utilisateurs et groupes][203]

5. <span data-ttu-id="15b4b-262">Bonjour **utilisateurs et groupes** la boîte de dialogue hello **utilisateurs** liste, sélectionnez **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="15b4b-262">In hello **Users and groups** dialog box, in hello **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="15b4b-263">Bonjour **utilisateurs et groupes** boîte de dialogue, sélectionnez **sélectionnez**.</span><span class="sxs-lookup"><span data-stu-id="15b4b-263">In hello **Users and groups** dialog box, select **Select**.</span></span>

7. <span data-ttu-id="15b4b-264">Bonjour **ajouter l’affectation** boîte de dialogue, sélectionnez **affecter**.</span><span class="sxs-lookup"><span data-stu-id="15b4b-264">In hello **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-sso"></a><span data-ttu-id="15b4b-265">Tester l’authentification unique (SSO)</span><span class="sxs-lookup"><span data-stu-id="15b4b-265">Test SSO</span></span>

<span data-ttu-id="15b4b-266">Dans cette section, vous testez votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="15b4b-266">In this section, you test your Azure AD SSO configuration by using hello Access Panel.</span></span>

<span data-ttu-id="15b4b-267">Lorsque vous sélectionnez la vignette de logiciel Cezanne HR hello Bonjour volet d’accès, vous vous connectez sur automatiquement tooyour application logicielle de Cezanne HR.</span><span class="sxs-lookup"><span data-stu-id="15b4b-267">When you select hello Cezanne HR software tile in hello Access Panel, you sign on automatically tooyour Cezanne HR software application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="15b4b-268">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="15b4b-268">Next steps</span></span>

* [<span data-ttu-id="15b4b-269">Liste des didacticiels sur la façon de toointegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="15b4b-269">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="15b4b-270">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="15b4b-270">What is application access and SSO with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_203.png

