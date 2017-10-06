---
title: "Didacticiel : Intégration d’Azure Active Directory avec SSO SAML pour Confluence de resolution GmbH | Documents Microsoft"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et SAML SSO pour Confluence par résolution GmbH."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6b47d483-d3a3-442d-b123-171e3f0f7486
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: fe50636709857ec49023e24bdc8c6cd8c58e3c7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-confluence-by-resolution-gmbh"></a><span data-ttu-id="ed46f-103">Didacticiel : Intégration d’Azure Active Directory avec SSO SAML pour Confluence de resolution GmbH</span><span class="sxs-lookup"><span data-stu-id="ed46f-103">Tutorial: Azure Active Directory integration with SAML SSO for Confluence by resolution GmbH</span></span>

<span data-ttu-id="ed46f-104">Dans ce didacticiel, vous apprendrez comment toointegrate SAML SSO pour Confluence par résolution GmbH avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ed46f-104">In this tutorial, you learn how toointegrate SAML SSO for Confluence by resolution GmbH with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ed46f-105">Intégration SAML SSO pour Confluence par résolution GmbH avec Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="ed46f-105">Integrating SAML SSO for Confluence by resolution GmbH with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ed46f-106">Vous pouvez contrôler dans Azure AD qui a accès tooSAML SSO pour Confluence par résolution GmbH</span><span class="sxs-lookup"><span data-stu-id="ed46f-106">You can control in Azure AD who has access tooSAML SSO for Confluence by resolution GmbH</span></span>
- <span data-ttu-id="ed46f-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSAML SSO pour Confluence par résolution GmbH (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed46f-107">You can enable your users tooautomatically get signed-on tooSAML SSO for Confluence by resolution GmbH (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ed46f-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="ed46f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ed46f-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ed46f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ed46f-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ed46f-110">Prerequisites</span></span>

<span data-ttu-id="ed46f-111">tooconfigure intégration d’Azure AD avec SAML SSO pour Confluence par résolution GmbH, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="ed46f-111">tooconfigure Azure AD integration with SAML SSO for Confluence by resolution GmbH, you need hello following items:</span></span>

- <span data-ttu-id="ed46f-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed46f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ed46f-113">Une authentification unique SSO SAML pour Confluence de resolution GmbH sur un abonnement activé</span><span class="sxs-lookup"><span data-stu-id="ed46f-113">A SAML SSO for Confluence by resolution GmbH single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ed46f-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="ed46f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ed46f-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="ed46f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ed46f-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="ed46f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ed46f-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ed46f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ed46f-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="ed46f-118">Scenario description</span></span>
<span data-ttu-id="ed46f-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="ed46f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ed46f-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="ed46f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ed46f-121">Ajout de SAML SSO pour Confluence par résolution GmbH à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="ed46f-121">Adding SAML SSO for Confluence by resolution GmbH from hello gallery</span></span>
2. <span data-ttu-id="ed46f-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed46f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-saml-sso-for-confluence-by-resolution-gmbh-from-hello-gallery"></a><span data-ttu-id="ed46f-123">Ajout de SAML SSO pour Confluence par résolution GmbH à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="ed46f-123">Adding SAML SSO for Confluence by resolution GmbH from hello gallery</span></span>

<span data-ttu-id="ed46f-124">tooconfigure hello intégration de SAML SSO pour Confluence par résolution GmbH dans Azure AD, vous devez tooadd SAML SSO pour Confluence par résolution GmbH à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="ed46f-124">tooconfigure hello integration of SAML SSO for Confluence by resolution GmbH into Azure AD, you need tooadd SAML SSO for Confluence by resolution GmbH from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ed46f-125">**tooadd SAML SSO pour Confluence par résolution GmbH à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ed46f-125">**tooadd SAML SSO for Confluence by resolution GmbH from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ed46f-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="ed46f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ed46f-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="ed46f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ed46f-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="ed46f-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="ed46f-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="ed46f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="ed46f-133">Dans la zone de recherche de hello, tapez **SAML SSO pour Confluence par résolution GmbH**.</span><span class="sxs-lookup"><span data-stu-id="ed46f-133">In hello search box, type **SAML SSO for Confluence by resolution GmbH**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_search.png)

5. <span data-ttu-id="ed46f-135">Dans le volet de résultats hello, sélectionnez **SAML SSO pour Confluence par résolution GmbH**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="ed46f-135">In hello results panel, select **SAML SSO for Confluence by resolution GmbH**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ed46f-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed46f-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="ed46f-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec SSO SAML pour Confluence de resolution GmbH, en tirant parti d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="ed46f-138">In this section, you configure and test Azure AD single sign-on with SAML SSO for Confluence by resolution GmbH based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ed46f-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans SAML SSO pour Confluence par résolution GmbH est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ed46f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAML SSO for Confluence by resolution GmbH is tooa user in Azure AD.</span></span> <span data-ttu-id="ed46f-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un hello utilisateur dans SAML SSO pour Confluence par résolution GmbH doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="ed46f-140">In other words, a link relationship between an Azure AD user and hello related user in SAML SSO for Confluence by resolution GmbH needs toobe established.</span></span>

<span data-ttu-id="ed46f-141">Dans SAML SSO pour Confluence par résolution GmbH, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="ed46f-141">In SAML SSO for Confluence by resolution GmbH, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ed46f-142">tooconfigure et tester Azure AD l’authentification unique avec SAML SSO Confluence par résolution GmbH, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="ed46f-142">tooconfigure and test Azure AD single sign-on with SAML SSO for Confluence by resolution GmbH, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ed46f-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="ed46f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ed46f-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ed46f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ed46f-145">**[Création d’un SAML SSO pour Confluence par l’utilisateur de test de résolution GmbH](#creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user)**  -toohave de Britta Simon dans SAML SSO pour Confluence contrepartie par résolution GmbH est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ed46f-145">**[Creating a SAML SSO for Confluence by resolution GmbH test user](#creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user)** - toohave a counterpart of Britta Simon in SAML SSO for Confluence by resolution GmbH that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ed46f-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="ed46f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ed46f-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="ed46f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ed46f-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed46f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ed46f-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre SAML SSO pour Confluence par résolution GmbH application.</span><span class="sxs-lookup"><span data-stu-id="ed46f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAML SSO for Confluence by resolution GmbH application.</span></span>

<span data-ttu-id="ed46f-150">**tooconfigure Azure AD l’authentification unique avec SAML SSO pour Confluence par résolution GmbH, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ed46f-150">**tooconfigure Azure AD single sign-on with SAML SSO for Confluence by resolution GmbH, perform hello following steps:**</span></span>

1. <span data-ttu-id="ed46f-151">Bonjour portail Azure, sur hello **SAML SSO pour Confluence par résolution GmbH** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="ed46f-151">In hello Azure portal, on hello **SAML SSO for Confluence by resolution GmbH** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="ed46f-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="ed46f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_samlbase.png)

3. <span data-ttu-id="ed46f-155">Sur hello **SAML SSO pour Confluence par résolution GmbH domaine et les URL** section, si vous le souhaitez application hello tooconfigure **IDP** en mode initié par :</span><span class="sxs-lookup"><span data-stu-id="ed46f-155">On hello **SAML SSO for Confluence by resolution GmbH Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_url_1.png)

    <span data-ttu-id="ed46f-157">a.</span><span class="sxs-lookup"><span data-stu-id="ed46f-157">a.</span></span> <span data-ttu-id="ed46f-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="ed46f-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

    <span data-ttu-id="ed46f-159">b.</span><span class="sxs-lookup"><span data-stu-id="ed46f-159">b.</span></span> <span data-ttu-id="ed46f-160">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="ed46f-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

4. <span data-ttu-id="ed46f-161">Cliquez sur **Afficher les paramètres d’URL avancés**.</span><span class="sxs-lookup"><span data-stu-id="ed46f-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="ed46f-162">Si vous le souhaitez application hello tooconfigure **SP** en mode initié par :</span><span class="sxs-lookup"><span data-stu-id="ed46f-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_url_2.png)

    <span data-ttu-id="ed46f-164">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="ed46f-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="ed46f-165">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="ed46f-165">These values are not real.</span></span> <span data-ttu-id="ed46f-166">Mettre à jour ces valeurs avec hello réel identificateur, URL de réponse et URL de connexion.</span><span class="sxs-lookup"><span data-stu-id="ed46f-166">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="ed46f-167">Contact [équipe de support SAML SSO pour Confluence par résolution GmbH Client](https://www.resolution.de/go/support) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="ed46f-167">Contact [SAML SSO for Confluence by resolution GmbH Client support team](https://www.resolution.de/go/support) tooget these values.</span></span> 

5. <span data-ttu-id="ed46f-168">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="ed46f-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_certificate.png) 

6. <span data-ttu-id="ed46f-170">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="ed46f-170">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_400.png)  
    
7. <span data-ttu-id="ed46f-172">Dans une fenêtre de navigateur web, connectez-vous tooyour **SAML SSO pour Confluence par le portail d’administration résolution GmbH** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="ed46f-172">In a different web browser window, log in tooyour **SAML SSO for Confluence by resolution GmbH admin portal** as an administrator.</span></span>

8. <span data-ttu-id="ed46f-173">Pointez sur représentant une roue dentée et cliquez sur hello **modules complémentaires**.</span><span class="sxs-lookup"><span data-stu-id="ed46f-173">Hover on cog and click hello **Add-ons**.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-samlssoconfluence-tutorial/addon1.png)

9. <span data-ttu-id="ed46f-175">Vous êtes redirigé tooAdministrator la page d’accès.</span><span class="sxs-lookup"><span data-stu-id="ed46f-175">You are redirected tooAdministrator Access page.</span></span> <span data-ttu-id="ed46f-176">Entrez le mot de passe hello et cliquez sur **confirmer** bouton.</span><span class="sxs-lookup"><span data-stu-id="ed46f-176">Enter hello password and click **Confirm** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssoconfluence-tutorial/addon2.png)

10. <span data-ttu-id="ed46f-178">Sous **ATLASSIAN MARKETPLACE**, cliquez sur **Find new add-ons** (Trouver de nouveaux modules complémentaires).</span><span class="sxs-lookup"><span data-stu-id="ed46f-178">Under **ATLASSIAN MARKETPLACE** tab, click **Find new add-ons**.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssoconfluence-tutorial/addon.png)

11. <span data-ttu-id="ed46f-180">Recherche **SAML authentification unique (SSO) pour Confluence** et cliquez sur **installer** bouton tooinstall hello nouveau plug-in SAML.</span><span class="sxs-lookup"><span data-stu-id="ed46f-180">Search **SAML Single Sign On (SSO) for Confluence** and click **Install** button tooinstall hello new SAML plugin.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssoconfluence-tutorial/addon7.png)

12. <span data-ttu-id="ed46f-182">installation du plug-in Hello démarre.</span><span class="sxs-lookup"><span data-stu-id="ed46f-182">hello plugin installation will start.</span></span> <span data-ttu-id="ed46f-183">Cliquez sur **Fermer**.</span><span class="sxs-lookup"><span data-stu-id="ed46f-183">Click **Close**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssoconfluence-tutorial/addon8.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssoconfluence-tutorial/addon9.png)

13. <span data-ttu-id="ed46f-186">Cliquez sur **Gérer**.</span><span class="sxs-lookup"><span data-stu-id="ed46f-186">Click **Manage**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssoconfluence-tutorial/addon10.png)
    
14. <span data-ttu-id="ed46f-188">Cliquez sur **configurer** tooconfigure hello nouveau plug-in.</span><span class="sxs-lookup"><span data-stu-id="ed46f-188">Click **Configure** tooconfigure hello new plugin.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssoconfluence-tutorial/addon11.png)

15. <span data-ttu-id="ed46f-190">Ce nouveau plug-in figure également sous l’onglet **UTILISATEURS ET SÉCURITÉ**.</span><span class="sxs-lookup"><span data-stu-id="ed46f-190">This new plugin can also be found under **USERS & SECURITY** tab.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssoconfluence-tutorial/addon3.png)
    
16. <span data-ttu-id="ed46f-192">Sur **SAML SingleSignOn plug-in Configuration** , cliquez sur **ajouter le fournisseur d’identité supplémentaires** bouton Paramètres de hello tooconfigure de fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="ed46f-192">On **SAML SingleSignOn Plugin Configuration** page, click **Add additional Identity Provider** button tooconfigure hello settings of Identity Provider.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssoconfluence-tutorial/addon4.png)

17. <span data-ttu-id="ed46f-194">Sur cette page, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ed46f-194">Perform following steps on this page:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssoconfluence-tutorial/addon5.png)
 
    <span data-ttu-id="ed46f-196">a.</span><span class="sxs-lookup"><span data-stu-id="ed46f-196">a.</span></span> <span data-ttu-id="ed46f-197">Ajouter **nom** Hello fournisseur d’identité (par exemple, Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ed46f-197">Add **Name** of hello Identity Provider (e.g Azure AD).</span></span>
    
    <span data-ttu-id="ed46f-198">b.</span><span class="sxs-lookup"><span data-stu-id="ed46f-198">b.</span></span> <span data-ttu-id="ed46f-199">Ajouter **Description** Hello fournisseur d’identité (par exemple, Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ed46f-199">Add **Description** of hello Identity Provider (e.g Azure AD).</span></span>

    <span data-ttu-id="ed46f-200">c.</span><span class="sxs-lookup"><span data-stu-id="ed46f-200">c.</span></span> <span data-ttu-id="ed46f-201">Cliquez sur **XML** et sélectionnez hello **métadonnées** fichier que vous avez téléchargé à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ed46f-201">Click **XML** and select hello **Metadata** file that you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="ed46f-202">d.</span><span class="sxs-lookup"><span data-stu-id="ed46f-202">d.</span></span> <span data-ttu-id="ed46f-203">Cliquez sur le bouton **Charger**.</span><span class="sxs-lookup"><span data-stu-id="ed46f-203">Click **Load** button.</span></span>

    <span data-ttu-id="ed46f-204">e.</span><span class="sxs-lookup"><span data-stu-id="ed46f-204">e.</span></span> <span data-ttu-id="ed46f-205">Il lit les métadonnées de IdP hello et renseigne les champs hello en surbrillance dans la capture d’écran de hello.</span><span class="sxs-lookup"><span data-stu-id="ed46f-205">It reads hello IdP metadata and populates hello fields as highlighted in hello screenshot.</span></span>   
18. <span data-ttu-id="ed46f-206">Cliquez sur **enregistrer les paramètres** bouton Paramètres de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="ed46f-206">Click **Save settings** button toosave hello settings.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssoconfluence-tutorial/addon6.png)

> [!TIP]
> <span data-ttu-id="ed46f-208">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="ed46f-208">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ed46f-209">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="ed46f-209">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ed46f-210">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ed46f-210">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ed46f-211">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed46f-211">Creating an Azure AD test user</span></span>
<span data-ttu-id="ed46f-212">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="ed46f-212">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="ed46f-214">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ed46f-214">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ed46f-215">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="ed46f-215">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ed46f-217">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="ed46f-217">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ed46f-219">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="ed46f-219">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ed46f-221">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="ed46f-221">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ed46f-223">a.</span><span class="sxs-lookup"><span data-stu-id="ed46f-223">a.</span></span> <span data-ttu-id="ed46f-224">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ed46f-224">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ed46f-225">b.</span><span class="sxs-lookup"><span data-stu-id="ed46f-225">b.</span></span> <span data-ttu-id="ed46f-226">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ed46f-226">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ed46f-227">c.</span><span class="sxs-lookup"><span data-stu-id="ed46f-227">c.</span></span> <span data-ttu-id="ed46f-228">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="ed46f-228">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ed46f-229">d.</span><span class="sxs-lookup"><span data-stu-id="ed46f-229">d.</span></span> <span data-ttu-id="ed46f-230">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="ed46f-230">Click **Create**.</span></span>
 
### <a name="creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user"></a><span data-ttu-id="ed46f-231">Création d’un utilisateur de test pour SSO SAML pour Confluence de resolution GmbH</span><span class="sxs-lookup"><span data-stu-id="ed46f-231">Creating a SAML SSO for Confluence by resolution GmbH test user</span></span>

<span data-ttu-id="ed46f-232">tooenable Azure AD les utilisateurs toolog dans tooSAML SSO pour Confluence par résolution GmbH, ils doivent être configurés dans SAML SSO pour Confluence par résolution GmbH.</span><span class="sxs-lookup"><span data-stu-id="ed46f-232">tooenable Azure AD users toolog in tooSAML SSO for Confluence by resolution GmbH, they must be provisioned into SAML SSO for Confluence by resolution GmbH.</span></span>  
<span data-ttu-id="ed46f-233">Dans SSO SAML pour Confluence de resolution GmbH, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="ed46f-233">In SAML SSO for Confluence by resolution GmbH, provisioning is a manual task.</span></span>

<span data-ttu-id="ed46f-234">**tooprovision un compte d’utilisateur, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ed46f-234">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="ed46f-235">Ouvrez une session dans tooyour SAML SSO pour Confluence par site d’entreprise GmbH résolution en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="ed46f-235">Log in tooyour SAML SSO for Confluence by resolution GmbH company site as an administrator.</span></span>

2. <span data-ttu-id="ed46f-236">Pointez sur représentant une roue dentée et cliquez sur hello **gestion des utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="ed46f-236">Hover on cog and click hello **User management**.</span></span>

    ![Ajouter un employé](./media/active-directory-saas-samlssoconfluence-tutorial/user1.png) 

3. <span data-ttu-id="ed46f-238">Dans la section Utilisateurs, cliquez sur l’onglet **Add users** (Ajouter des utilisateurs). Sur hello **« Ajouter un utilisateur »** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="ed46f-238">Under Users section, click **Add users** tab. On hello **“Add a User”** dialog page, perform hello following steps:</span></span>

    ![Ajouter un employé](./media/active-directory-saas-samlssoconfluence-tutorial/user2.png) 

    <span data-ttu-id="ed46f-240">a.</span><span class="sxs-lookup"><span data-stu-id="ed46f-240">a.</span></span> <span data-ttu-id="ed46f-241">Bonjour **nom d’utilisateur** zone de texte, par courrier électronique de type hello d’utilisateur comme Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ed46f-241">In hello **Username** textbox, type hello email of user like Britta Simon.</span></span>

    <span data-ttu-id="ed46f-242">b.</span><span class="sxs-lookup"><span data-stu-id="ed46f-242">b.</span></span> <span data-ttu-id="ed46f-243">Bonjour **nom complet** zone de texte, nom complet de type hello d’utilisateur comme Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ed46f-243">In hello **Full Name** textbox, type hello full name of user like Britta Simon.</span></span>

    <span data-ttu-id="ed46f-244">c.</span><span class="sxs-lookup"><span data-stu-id="ed46f-244">c.</span></span> <span data-ttu-id="ed46f-245">Bonjour **messagerie** adresse de messagerie de type hello d’utilisateur de zone de texte, comme Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="ed46f-245">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="ed46f-246">d.</span><span class="sxs-lookup"><span data-stu-id="ed46f-246">d.</span></span> <span data-ttu-id="ed46f-247">Bonjour **mot de passe** zone de texte, type hello mot de passe Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ed46f-247">In hello **Password** textbox, type hello password for Britta Simon.</span></span>

    <span data-ttu-id="ed46f-248">e.</span><span class="sxs-lookup"><span data-stu-id="ed46f-248">e.</span></span> <span data-ttu-id="ed46f-249">Cliquez sur **confirmer le mot de passe** entrer à nouveau le mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="ed46f-249">Click **Confirm Password** reenter hello password.</span></span>
    
    <span data-ttu-id="ed46f-250">f.</span><span class="sxs-lookup"><span data-stu-id="ed46f-250">f.</span></span> <span data-ttu-id="ed46f-251">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="ed46f-251">Click **Add** button.</span></span>    

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ed46f-252">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed46f-252">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ed46f-253">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooSAML SSO pour Confluence par résolution GmbH.</span><span class="sxs-lookup"><span data-stu-id="ed46f-253">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAML SSO for Confluence by resolution GmbH.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="ed46f-255">**tooassign Britta Simon tooSAML SSO pour Confluence par résolution GmbH, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ed46f-255">**tooassign Britta Simon tooSAML SSO for Confluence by resolution GmbH, perform hello following steps:**</span></span>

1. <span data-ttu-id="ed46f-256">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="ed46f-256">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="ed46f-258">Dans la liste des applications hello, sélectionnez **SAML SSO pour Confluence par résolution GmbH**.</span><span class="sxs-lookup"><span data-stu-id="ed46f-258">In hello applications list, select **SAML SSO for Confluence by resolution GmbH**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_app.png) 

3. <span data-ttu-id="ed46f-260">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="ed46f-260">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="ed46f-262">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="ed46f-262">Click **Add** button.</span></span> <span data-ttu-id="ed46f-263">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="ed46f-263">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="ed46f-265">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="ed46f-265">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ed46f-266">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="ed46f-266">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ed46f-267">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="ed46f-267">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ed46f-268">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="ed46f-268">Testing single sign-on</span></span>

<span data-ttu-id="ed46f-269">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="ed46f-269">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ed46f-270">Lorsque vous cliquez sur hello SAML SSO pour Confluence en mosaïque GmbH résolution hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour SAML SSO pour Confluence par résolution GmbH application.</span><span class="sxs-lookup"><span data-stu-id="ed46f-270">When you click hello SAML SSO for Confluence by resolution GmbH tile in hello Access Panel, you should get automatically signed-on tooyour SAML SSO for Confluence by resolution GmbH application.</span></span>
<span data-ttu-id="ed46f-271">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ed46f-271">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ed46f-272">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="ed46f-272">Additional resources</span></span>

* [<span data-ttu-id="ed46f-273">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ed46f-273">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ed46f-274">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="ed46f-274">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_203.png

