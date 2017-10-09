---
title: "Didacticiel : Intégration d’Azure Active Directory avec SSO SAML pour Jira par résolution GmbH | Documents Microsoft"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et SAML SSO pour Jira par résolution GmbH."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 20e18819-e330-4e40-bd8d-2ff3b98e035f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: a3436a9aa25640e931a61b5ba4a62611e6e07890
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-jira-by-resolution-gmbh"></a><span data-ttu-id="cc36e-103">Didacticiel : Intégration d’Azure Active Directory avec SSO SAML pour Jira par résolution GmbH</span><span class="sxs-lookup"><span data-stu-id="cc36e-103">Tutorial: Azure Active Directory integration with SAML SSO for Jira by resolution GmbH</span></span>

<span data-ttu-id="cc36e-104">Dans ce didacticiel, vous apprendrez comment toointegrate SAML SSO pour Jira par résolution GmbH avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cc36e-104">In this tutorial, you learn how toointegrate SAML SSO for Jira by resolution GmbH with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cc36e-105">Intégration SAML SSO pour Jira par résolution GmbH avec Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="cc36e-105">Integrating SAML SSO for Jira by resolution GmbH with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cc36e-106">Vous pouvez contrôler dans Azure AD qui a accès tooSAML SSO pour Jira par résolution GmbH</span><span class="sxs-lookup"><span data-stu-id="cc36e-106">You can control in Azure AD who has access tooSAML SSO for Jira by resolution GmbH</span></span>
- <span data-ttu-id="cc36e-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSAML SSO pour Jira par résolution GmbH (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc36e-107">You can enable your users tooautomatically get signed-on tooSAML SSO for Jira by resolution GmbH (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cc36e-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="cc36e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="cc36e-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cc36e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc36e-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="cc36e-110">Prerequisites</span></span>

<span data-ttu-id="cc36e-111">tooconfigure intégration d’Azure AD avec SAML SSO pour Jira par résolution GmbH, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="cc36e-111">tooconfigure Azure AD integration with SAML SSO for Jira by resolution GmbH, you need hello following items:</span></span>

- <span data-ttu-id="cc36e-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc36e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cc36e-113">Une authentification unique SSO SAML pour Jira de resolution GmbH sur un abonnement activé</span><span class="sxs-lookup"><span data-stu-id="cc36e-113">A SAML SSO for Jira by resolution GmbH single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cc36e-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="cc36e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cc36e-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="cc36e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cc36e-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="cc36e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cc36e-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cc36e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cc36e-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="cc36e-118">Scenario description</span></span>
<span data-ttu-id="cc36e-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="cc36e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cc36e-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="cc36e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cc36e-121">Ajout de SAML SSO pour Jira par résolution GmbH à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="cc36e-121">Adding SAML SSO for Jira by resolution GmbH from hello gallery</span></span>
2. <span data-ttu-id="cc36e-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc36e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-saml-sso-for-jira-by-resolution-gmbh-from-hello-gallery"></a><span data-ttu-id="cc36e-123">Ajout de SAML SSO pour Jira par résolution GmbH à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="cc36e-123">Adding SAML SSO for Jira by resolution GmbH from hello gallery</span></span>
<span data-ttu-id="cc36e-124">tooconfigure hello intégration de SAML SSO pour Jira par résolution GmbH dans Azure AD, vous devez tooadd SAML SSO pour Jira par résolution GmbH à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="cc36e-124">tooconfigure hello integration of SAML SSO for Jira by resolution GmbH into Azure AD, you need tooadd SAML SSO for Jira by resolution GmbH from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cc36e-125">**tooadd SAML SSO pour Jira par résolution GmbH à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="cc36e-125">**tooadd SAML SSO for Jira by resolution GmbH from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc36e-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="cc36e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cc36e-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="cc36e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cc36e-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="cc36e-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="cc36e-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="cc36e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="cc36e-133">Dans la zone de recherche de hello, tapez **SAML SSO pour Jira par résolution GmbH**.</span><span class="sxs-lookup"><span data-stu-id="cc36e-133">In hello search box, type **SAML SSO for Jira by resolution GmbH**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_search.png)

5. <span data-ttu-id="cc36e-135">Dans le volet de résultats hello, sélectionnez **SAML SSO pour Jira par résolution GmbH**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="cc36e-135">In hello results panel, select **SAML SSO for Jira by resolution GmbH**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cc36e-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc36e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cc36e-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec SSO SAML pour Jira de resolution GmbH, en tirant parti d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="cc36e-138">In this section, you configure and test Azure AD single sign-on with SAML SSO for Jira by resolution GmbH based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="cc36e-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans SAML SSO pour Jira par résolution GmbH est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cc36e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAML SSO for Jira by resolution GmbH is tooa user in Azure AD.</span></span> <span data-ttu-id="cc36e-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un hello utilisateur dans SAML SSO pour Jira par résolution GmbH doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="cc36e-140">In other words, a link relationship between an Azure AD user and hello related user in SAML SSO for Jira by resolution GmbH needs toobe established.</span></span>

<span data-ttu-id="cc36e-141">Dans SAML SSO pour Jira par résolution GmbH, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="cc36e-141">In SAML SSO for Jira by resolution GmbH, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="cc36e-142">tooconfigure et tester Azure AD l’authentification unique avec SAML SSO Jira par résolution GmbH, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="cc36e-142">tooconfigure and test Azure AD single sign-on with SAML SSO for Jira by resolution GmbH, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cc36e-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="cc36e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cc36e-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cc36e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cc36e-145">**[Création d’un SAML SSO pour Jira par l’utilisateur de test de résolution GmbH](#creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user)**  -toohave un équivalent de Britta Simon dans SAML SSO pour Jira par résolution GmbH est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="cc36e-145">**[Creating a SAML SSO for Jira by resolution GmbH test user](#creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user)** - toohave a counterpart of Britta Simon in SAML SSO for Jira by resolution GmbH that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cc36e-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="cc36e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cc36e-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="cc36e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cc36e-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc36e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cc36e-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre SAML SSO pour Jira par résolution GmbH application.</span><span class="sxs-lookup"><span data-stu-id="cc36e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAML SSO for Jira by resolution GmbH application.</span></span>

<span data-ttu-id="cc36e-150">**tooconfigure Azure AD l’authentification unique avec SAML SSO pour Jira par résolution GmbH, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="cc36e-150">**tooconfigure Azure AD single sign-on with SAML SSO for Jira by resolution GmbH, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc36e-151">Bonjour portail Azure, sur hello **SAML SSO pour Jira par résolution GmbH** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="cc36e-151">In hello Azure portal, on hello **SAML SSO for Jira by resolution GmbH** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="cc36e-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="cc36e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_samlbase.png)

3. <span data-ttu-id="cc36e-155">Sur hello **SAML SSO pour Jira par résolution GmbH domaine et les URL** section, si vous le souhaitez application hello tooconfigure **IDP** en mode initié par :</span><span class="sxs-lookup"><span data-stu-id="cc36e-155">On hello **SAML SSO for Jira by resolution GmbH Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_1.png)

    <span data-ttu-id="cc36e-157">a.</span><span class="sxs-lookup"><span data-stu-id="cc36e-157">a.</span></span> <span data-ttu-id="cc36e-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="cc36e-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

    <span data-ttu-id="cc36e-159">b.</span><span class="sxs-lookup"><span data-stu-id="cc36e-159">b.</span></span> <span data-ttu-id="cc36e-160">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="cc36e-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

4. <span data-ttu-id="cc36e-161">Cliquez sur **Afficher les paramètres d’URL avancés**.</span><span class="sxs-lookup"><span data-stu-id="cc36e-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="cc36e-162">Si vous le souhaitez application hello tooconfigure **SP** en mode initié par :</span><span class="sxs-lookup"><span data-stu-id="cc36e-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_2.png)

    <span data-ttu-id="cc36e-164">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="cc36e-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="cc36e-165">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="cc36e-165">These values are not real.</span></span> <span data-ttu-id="cc36e-166">Mettre à jour ces valeurs avec hello réel identificateur, URL de réponse et URL de connexion.</span><span class="sxs-lookup"><span data-stu-id="cc36e-166">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="cc36e-167">Contact [équipe de support SAML SSO pour Jira par résolution GmbH Client](https://www.resolution.de/go/support) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="cc36e-167">Contact [SAML SSO for Jira by resolution GmbH Client support team](https://www.resolution.de/go/support) tooget these values.</span></span> 

5. <span data-ttu-id="cc36e-168">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="cc36e-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_certificate.png) 

6. <span data-ttu-id="cc36e-170">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="cc36e-170">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="cc36e-172">Dans une fenêtre de navigateur web, connectez-vous tooyour **SAML SSO pour Jira par le portail d’administration résolution GmbH** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="cc36e-172">In a different web browser window, log in tooyour **SAML SSO for Jira by resolution GmbH admin portal** as an administrator.</span></span>

8. <span data-ttu-id="cc36e-173">Pointez sur représentant une roue dentée et cliquez sur hello **modules complémentaires**.</span><span class="sxs-lookup"><span data-stu-id="cc36e-173">Hover on cog and click hello **Add-ons**.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/addon1.png)

9. <span data-ttu-id="cc36e-175">Vous êtes redirigé tooAdministrator la page d’accès.</span><span class="sxs-lookup"><span data-stu-id="cc36e-175">You are redirected tooAdministrator Access page.</span></span> <span data-ttu-id="cc36e-176">Entrez hello **mot de passe** et cliquez sur **confirmer** bouton.</span><span class="sxs-lookup"><span data-stu-id="cc36e-176">Enter hello **Password** and click **Confirm** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/addon2.png)

10. <span data-ttu-id="cc36e-178">Sous l’onglet Modules complémentaires, cliquez sur **Find new add-ons** (Trouver de nouveaux modules complémentaires).</span><span class="sxs-lookup"><span data-stu-id="cc36e-178">Under Add-ons tab section, click **Find new add-ons**.</span></span> <span data-ttu-id="cc36e-179">Recherche **SAML authentification unique (SSO) pour JIRA** et cliquez sur **installer** bouton tooinstall hello nouveau plug-in SAML.</span><span class="sxs-lookup"><span data-stu-id="cc36e-179">Search **SAML Single Sign On (SSO) for JIRA** and click **Install** button tooinstall hello new SAML plugin.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/addon7.png)

11. <span data-ttu-id="cc36e-181">installation du plug-in Hello démarre.</span><span class="sxs-lookup"><span data-stu-id="cc36e-181">hello plugin installation will start.</span></span> <span data-ttu-id="cc36e-182">Cliquez sur **Fermer**.</span><span class="sxs-lookup"><span data-stu-id="cc36e-182">Click **Close**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/addon8.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/addon9.png)

12. <span data-ttu-id="cc36e-185">Cliquez sur **Gérer**.</span><span class="sxs-lookup"><span data-stu-id="cc36e-185">Click **Manage**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/addon10.png)
    
13. <span data-ttu-id="cc36e-187">Cliquez sur **configurer** tooconfigure hello nouveau plug-in.</span><span class="sxs-lookup"><span data-stu-id="cc36e-187">Click **Configure** tooconfigure hello new plugin.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/addon11.png)

14. <span data-ttu-id="cc36e-189">Sur **SAML SingleSignOn plug-in Configuration** , cliquez sur **ajouter le fournisseur d’identité supplémentaires** bouton Paramètres de hello tooconfigure de fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="cc36e-189">On **SAML SingleSignOn Plugin Configuration** page, click **Add additional Identity Provider** button tooconfigure hello settings of Identity Provider.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/addon4.png)

15. <span data-ttu-id="cc36e-191">Sur cette page, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="cc36e-191">Perform following steps on this page:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/addon5.png)
 
    <span data-ttu-id="cc36e-193">a.</span><span class="sxs-lookup"><span data-stu-id="cc36e-193">a.</span></span> <span data-ttu-id="cc36e-194">Ajouter **nom** Hello fournisseur d’identité (par exemple, Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cc36e-194">Add **Name** of hello Identity Provider (e.g Azure AD).</span></span>
    
    <span data-ttu-id="cc36e-195">b.</span><span class="sxs-lookup"><span data-stu-id="cc36e-195">b.</span></span> <span data-ttu-id="cc36e-196">Ajouter **Description** Hello fournisseur d’identité (par exemple, Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cc36e-196">Add **Description** of hello Identity Provider (e.g Azure AD).</span></span>

    <span data-ttu-id="cc36e-197">c.</span><span class="sxs-lookup"><span data-stu-id="cc36e-197">c.</span></span> <span data-ttu-id="cc36e-198">Cliquez sur **XML** et sélectionnez hello **métadonnées** fichier, qui vous avez téléchargé à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="cc36e-198">Click **XML** and select hello **Metadata** file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="cc36e-199">d.</span><span class="sxs-lookup"><span data-stu-id="cc36e-199">d.</span></span> <span data-ttu-id="cc36e-200">Cliquez sur le bouton **Charger**.</span><span class="sxs-lookup"><span data-stu-id="cc36e-200">Click **Load** button.</span></span>

    <span data-ttu-id="cc36e-201">e.</span><span class="sxs-lookup"><span data-stu-id="cc36e-201">e.</span></span> <span data-ttu-id="cc36e-202">Il lit les métadonnées de IdP hello et renseigne les champs hello en surbrillance dans la capture d’écran de hello.</span><span class="sxs-lookup"><span data-stu-id="cc36e-202">It reads hello IdP metadata and populates hello fields as highlighted in hello screenshot.</span></span>   

16. <span data-ttu-id="cc36e-203">Cliquez sur **enregistrer les paramètres** bouton Paramètres de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="cc36e-203">Click **Save settings** button toosave hello settings.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/addon6.png)

> [!TIP]
> <span data-ttu-id="cc36e-205">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="cc36e-205">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cc36e-206">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="cc36e-206">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cc36e-207">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cc36e-207">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cc36e-208">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc36e-208">Creating an Azure AD test user</span></span>
<span data-ttu-id="cc36e-209">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="cc36e-209">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="cc36e-211">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="cc36e-211">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc36e-212">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="cc36e-212">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cc36e-214">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="cc36e-214">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cc36e-216">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="cc36e-216">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cc36e-218">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="cc36e-218">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cc36e-220">a.</span><span class="sxs-lookup"><span data-stu-id="cc36e-220">a.</span></span> <span data-ttu-id="cc36e-221">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cc36e-221">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cc36e-222">b.</span><span class="sxs-lookup"><span data-stu-id="cc36e-222">b.</span></span> <span data-ttu-id="cc36e-223">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cc36e-223">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cc36e-224">c.</span><span class="sxs-lookup"><span data-stu-id="cc36e-224">c.</span></span> <span data-ttu-id="cc36e-225">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="cc36e-225">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cc36e-226">d.</span><span class="sxs-lookup"><span data-stu-id="cc36e-226">d.</span></span> <span data-ttu-id="cc36e-227">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="cc36e-227">Click **Create**.</span></span>
 
### <a name="creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user"></a><span data-ttu-id="cc36e-228">Création d’un utilisateur de test pour SSO SAML pour Jira de resolution GmbH</span><span class="sxs-lookup"><span data-stu-id="cc36e-228">Creating a SAML SSO for Jira by resolution GmbH test user</span></span>

<span data-ttu-id="cc36e-229">tooenable Azure AD les utilisateurs toolog dans tooSAML SSO pour Jira par résolution GmbH, ils doivent être configurés dans SAML SSO pour Jira par résolution GmbH.</span><span class="sxs-lookup"><span data-stu-id="cc36e-229">tooenable Azure AD users toolog in tooSAML SSO for Jira by resolution GmbH, they must be provisioned into SAML SSO for Jira by resolution GmbH.</span></span>  
<span data-ttu-id="cc36e-230">Dans SSO SAML pour Jira de resolution GmbH, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="cc36e-230">In SAML SSO for Jira by resolution GmbH, provisioning is a manual task.</span></span>

<span data-ttu-id="cc36e-231">**tooprovision un compte d’utilisateur, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="cc36e-231">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc36e-232">Ouvrez une session dans tooyour SAML SSO pour Jira par le site d’entreprise GmbH résolution en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="cc36e-232">Log in tooyour SAML SSO for Jira by resolution GmbH company site as an administrator.</span></span>

2. <span data-ttu-id="cc36e-233">Pointez sur représentant une roue dentée et cliquez sur hello **gestion des utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="cc36e-233">Hover on cog and click hello **User management**.</span></span>

    ![Ajouter un employé](./media/active-directory-saas-samlssojira-tutorial/user1.png) 

3. <span data-ttu-id="cc36e-235">Vous êtes redirigé tooAdministrator accès page tooenter **mot de passe** et cliquez sur **confirmer** bouton.</span><span class="sxs-lookup"><span data-stu-id="cc36e-235">You are redirected tooAdministrator Access page tooenter **Password** and click **Confirm** button.</span></span>

    ![Ajouter un employé](./media/active-directory-saas-samlssojira-tutorial/user2.png) 

4. <span data-ttu-id="cc36e-237">Sous l’onglet **User management** (Gestion des utilisateurs), cliquez sur **Create user** (Créer un utilisateur).</span><span class="sxs-lookup"><span data-stu-id="cc36e-237">Under **User management** tab section, click **create user**.</span></span>

    ![Ajouter un employé](./media/active-directory-saas-samlssojira-tutorial/user3.png) 

5. <span data-ttu-id="cc36e-239">Sur hello **« Créer un utilisateur »** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="cc36e-239">On hello **“Create new user”** dialog page, perform hello following steps:</span></span>

    ![Ajouter un employé](./media/active-directory-saas-samlssojira-tutorial/user4.png) 

    <span data-ttu-id="cc36e-241">a.</span><span class="sxs-lookup"><span data-stu-id="cc36e-241">a.</span></span> <span data-ttu-id="cc36e-242">Bonjour **adresse de messagerie** adresse de messagerie de type hello d’utilisateur de zone de texte, comme Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="cc36e-242">In hello **Email address** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="cc36e-243">b.</span><span class="sxs-lookup"><span data-stu-id="cc36e-243">b.</span></span> <span data-ttu-id="cc36e-244">Bonjour **nom complet** zone de texte, nom complet du type d’utilisateur hello comme Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cc36e-244">In hello **Full Name** textbox, type full name of hello user like Britta Simon.</span></span>

    <span data-ttu-id="cc36e-245">c.</span><span class="sxs-lookup"><span data-stu-id="cc36e-245">c.</span></span> <span data-ttu-id="cc36e-246">Bonjour **nom d’utilisateur** par courrier électronique de type hello d’utilisateur de zone de texte, comme Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="cc36e-246">In hello **Username** textbox, type hello email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="cc36e-247">d.</span><span class="sxs-lookup"><span data-stu-id="cc36e-247">d.</span></span> <span data-ttu-id="cc36e-248">Bonjour **mot de passe** zone de texte, un mot de passe hello type d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="cc36e-248">In hello **Password** textbox, type hello password of user.</span></span>

    <span data-ttu-id="cc36e-249">e.</span><span class="sxs-lookup"><span data-stu-id="cc36e-249">e.</span></span> <span data-ttu-id="cc36e-250">Cliquez sur **Create User** (Créer un utilisateur).</span><span class="sxs-lookup"><span data-stu-id="cc36e-250">Click **Create user**.</span></span>   

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cc36e-251">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc36e-251">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cc36e-252">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooSAML SSO pour Jira par résolution GmbH.</span><span class="sxs-lookup"><span data-stu-id="cc36e-252">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAML SSO for Jira by resolution GmbH.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="cc36e-254">**tooassign Britta Simon tooSAML SSO pour Jira par résolution GmbH, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="cc36e-254">**tooassign Britta Simon tooSAML SSO for Jira by resolution GmbH, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc36e-255">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="cc36e-255">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="cc36e-257">Dans la liste des applications hello, sélectionnez **SAML SSO pour Jira par résolution GmbH**.</span><span class="sxs-lookup"><span data-stu-id="cc36e-257">In hello applications list, select **SAML SSO for Jira by resolution GmbH**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_app.png) 

3. <span data-ttu-id="cc36e-259">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="cc36e-259">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="cc36e-261">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="cc36e-261">Click **Add** button.</span></span> <span data-ttu-id="cc36e-262">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="cc36e-262">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="cc36e-264">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="cc36e-264">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cc36e-265">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="cc36e-265">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cc36e-266">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="cc36e-266">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cc36e-267">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="cc36e-267">Testing single sign-on</span></span>

<span data-ttu-id="cc36e-268">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="cc36e-268">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="cc36e-269">Lorsque vous cliquez sur hello SAML SSO pour Jira en mosaïque GmbH résolution hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour SAML SSO pour Jira par résolution GmbH application.</span><span class="sxs-lookup"><span data-stu-id="cc36e-269">When you click hello SAML SSO for Jira by resolution GmbH tile in hello Access Panel, you should get automatically signed-on tooyour SAML SSO for Jira by resolution GmbH application.</span></span>
<span data-ttu-id="cc36e-270">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cc36e-270">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="cc36e-271">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="cc36e-271">Additional resources</span></span>

* [<span data-ttu-id="cc36e-272">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cc36e-272">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cc36e-273">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="cc36e-273">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_203.png

