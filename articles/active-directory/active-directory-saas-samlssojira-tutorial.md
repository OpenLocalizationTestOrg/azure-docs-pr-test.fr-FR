---
title: "Didacticiel : Intégration d’Azure Active Directory avec SSO SAML pour Jira par résolution GmbH | Documents Microsoft"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et SSO SAML pour Jira de resolution GmbH."
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
ms.openlocfilehash: cde5983710185d1e46a5601b16bbfb1c0fcae382
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-jira-by-resolution-gmbh"></a><span data-ttu-id="57839-103">Didacticiel : Intégration d’Azure Active Directory avec SSO SAML pour Jira par résolution GmbH</span><span class="sxs-lookup"><span data-stu-id="57839-103">Tutorial: Azure Active Directory integration with SAML SSO for Jira by resolution GmbH</span></span>

<span data-ttu-id="57839-104">Dans ce didacticiel, vous allez apprendre à intégrer SSO SAML pour Jira de resolution GmbH avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="57839-104">In this tutorial, you learn how to integrate SAML SSO for Jira by resolution GmbH with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="57839-105">L’intégration de SSO SAML pour Jira de resolution GmbH avec Azure AD offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="57839-105">Integrating SAML SSO for Jira by resolution GmbH with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="57839-106">Vous pouvez contrôler dans Azure AD qui a accès à SSO SAML pour Jira de resolution GmbH</span><span class="sxs-lookup"><span data-stu-id="57839-106">You can control in Azure AD who has access to SAML SSO for Jira by resolution GmbH</span></span>
- <span data-ttu-id="57839-107">Vous pouvez permettre à vos utilisateurs d’être automatiquement authentifiés auprès de SSO SAML pour Jira de resolution GmbH (authentification unique) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="57839-107">You can enable your users to automatically get signed-on to SAML SSO for Jira by resolution GmbH (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="57839-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="57839-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="57839-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="57839-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="57839-110">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="57839-110">Prerequisites</span></span>

<span data-ttu-id="57839-111">Pour configurer l’intégration d’Azure AD avec SSO SAML pour Jira de resolution GmbH, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="57839-111">To configure Azure AD integration with SAML SSO for Jira by resolution GmbH, you need the following items:</span></span>

- <span data-ttu-id="57839-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="57839-112">An Azure AD subscription</span></span>
- <span data-ttu-id="57839-113">Une authentification unique SSO SAML pour Jira de resolution GmbH sur un abonnement activé</span><span class="sxs-lookup"><span data-stu-id="57839-113">A SAML SSO for Jira by resolution GmbH single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="57839-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="57839-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="57839-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="57839-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="57839-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="57839-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="57839-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="57839-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="57839-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="57839-118">Scenario description</span></span>
<span data-ttu-id="57839-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="57839-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="57839-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="57839-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="57839-121">Ajout de SSO SAML pour Jira de resolution GmbH à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="57839-121">Adding SAML SSO for Jira by resolution GmbH from the gallery</span></span>
2. <span data-ttu-id="57839-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="57839-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-saml-sso-for-jira-by-resolution-gmbh-from-the-gallery"></a><span data-ttu-id="57839-123">Ajout de SSO SAML pour Jira de resolution GmbH à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="57839-123">Adding SAML SSO for Jira by resolution GmbH from the gallery</span></span>
<span data-ttu-id="57839-124">Pour configurer l’intégration de SSO SAML pour Jira de resolution GmbH dans Azure AD, vous devez ajouter SSO SAML pour Jira de resolution GmbH à partir de la galerie dans votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="57839-124">To configure the integration of SAML SSO for Jira by resolution GmbH into Azure AD, you need to add SAML SSO for Jira by resolution GmbH from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="57839-125">**Pour ajouter SSO SAML pour Jira de resolution GmbH à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="57839-125">**To add SAML SSO for Jira by resolution GmbH from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="57839-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="57839-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="57839-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="57839-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="57839-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="57839-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="57839-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="57839-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="57839-133">Dans la boîte de dialogue de recherche, tapez **SSO SAML pour Jira de resolution GmbH**.</span><span class="sxs-lookup"><span data-stu-id="57839-133">In the search box, type **SAML SSO for Jira by resolution GmbH**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_search.png)

5. <span data-ttu-id="57839-135">Dans le volet des résultats, sélectionnez **SSO SAML pour Jira de resolution GmbH**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="57839-135">In the results panel, select **SAML SSO for Jira by resolution GmbH**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="57839-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="57839-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="57839-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec SSO SAML pour Jira de resolution GmbH, en tirant parti d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="57839-138">In this section, you configure and test Azure AD single sign-on with SAML SSO for Jira by resolution GmbH based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="57839-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir quel utilisateur SSO SAML pour Jira de resolution GmbH équivaut à un utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="57839-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SAML SSO for Jira by resolution GmbH is to a user in Azure AD.</span></span> <span data-ttu-id="57839-140">En d’autres termes, un lien doit être établi entre un utilisateur Azure AD et l’utilisateur de SSO SAML pour Jira de resolution GmbH associé.</span><span class="sxs-lookup"><span data-stu-id="57839-140">In other words, a link relationship between an Azure AD user and the related user in SAML SSO for Jira by resolution GmbH needs to be established.</span></span>

<span data-ttu-id="57839-141">Dans SSO SAML pour Jira de resolution GmbH, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="57839-141">In SAML SSO for Jira by resolution GmbH, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="57839-142">Pour configurer et tester l’authentification unique Azure AD avec SSO SAML pour Jira de resolution GmbH, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="57839-142">To configure and test Azure AD single sign-on with SAML SSO for Jira by resolution GmbH, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="57839-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="57839-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="57839-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="57839-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="57839-145">**[Création d’un utilisateur de test de SSO SAML pour Jira de resolution GmbH](#creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user)** : pour avoir un équivalent de Britta Simon dans SSO SAML pour Jira de resolution GmbH qui soit lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="57839-145">**[Creating a SAML SSO for Jira by resolution GmbH test user](#creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user)** - to have a counterpart of Britta Simon in SAML SSO for Jira by resolution GmbH that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="57839-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="57839-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="57839-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="57839-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="57839-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="57839-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="57839-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application SSO SAML pour Jira de resolution GmbH.</span><span class="sxs-lookup"><span data-stu-id="57839-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAML SSO for Jira by resolution GmbH application.</span></span>

<span data-ttu-id="57839-150">**Pour configurer l’authentification unique Azure AD avec SSO SAML pour Jira de resolution GmbH, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="57839-150">**To configure Azure AD single sign-on with SAML SSO for Jira by resolution GmbH, perform the following steps:**</span></span>

1. <span data-ttu-id="57839-151">Sur le portail Azure, dans la page intégration de l’application **SSO SAML pour Jira de resolution GmbH**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="57839-151">In the Azure portal, on the **SAML SSO for Jira by resolution GmbH** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="57839-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="57839-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_samlbase.png)

3. <span data-ttu-id="57839-155">Dans la section **SSO SAML pour Jira de resolution GmbH**, si vous souhaitez configurer l’application en mode initié par le **fournisseur d’identité (IDP)**:</span><span class="sxs-lookup"><span data-stu-id="57839-155">On the **SAML SSO for Jira by resolution GmbH Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_1.png)

    <span data-ttu-id="57839-157">a.</span><span class="sxs-lookup"><span data-stu-id="57839-157">a.</span></span> <span data-ttu-id="57839-158">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="57839-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

    <span data-ttu-id="57839-159">b.</span><span class="sxs-lookup"><span data-stu-id="57839-159">b.</span></span> <span data-ttu-id="57839-160">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="57839-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

4. <span data-ttu-id="57839-161">Cliquez sur **Afficher les paramètres d’URL avancés**.</span><span class="sxs-lookup"><span data-stu-id="57839-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="57839-162">Si vous souhaitez configurer l’application en mode initié par le **fournisseur de service** :</span><span class="sxs-lookup"><span data-stu-id="57839-162">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_2.png)

    <span data-ttu-id="57839-164">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="57839-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="57839-165">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="57839-165">These values are not real.</span></span> <span data-ttu-id="57839-166">Mettez à jour ces valeurs avec l’identificateur, l’URL de réponse et l’URL de connexion réels.</span><span class="sxs-lookup"><span data-stu-id="57839-166">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="57839-167">Pour obtenir ces valeurs, contactez l’[équipe de support de SSO SAML pour Jira de resolution GmbH](https://www.resolution.de/go/support).</span><span class="sxs-lookup"><span data-stu-id="57839-167">Contact [SAML SSO for Jira by resolution GmbH Client support team](https://www.resolution.de/go/support) to get these values.</span></span> 

5. <span data-ttu-id="57839-168">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="57839-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_certificate.png) 

6. <span data-ttu-id="57839-170">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="57839-170">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="57839-172">Dans une autre fenêtre de navigateur web, connectez-vous à votre **portail d’administration de SSO SAML pour Jira de resolution GmbH** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="57839-172">In a different web browser window, log in to your **SAML SSO for Jira by resolution GmbH admin portal** as an administrator.</span></span>

8. <span data-ttu-id="57839-173">Pointez sur le roue dentée, puis cliquez sur **Modules complémentaires**.</span><span class="sxs-lookup"><span data-stu-id="57839-173">Hover on cog and click the **Add-ons**.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/addon1.png)

9. <span data-ttu-id="57839-175">Vous êtes redirigé vers la page d’accès administrateur.</span><span class="sxs-lookup"><span data-stu-id="57839-175">You are redirected to Administrator Access page.</span></span> <span data-ttu-id="57839-176">Entrez le **mot de passe**, puis cliquez sur le bouton **Confirmer**.</span><span class="sxs-lookup"><span data-stu-id="57839-176">Enter the **Password** and click **Confirm** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/addon2.png)

10. <span data-ttu-id="57839-178">Sous l’onglet Modules complémentaires, cliquez sur **Find new add-ons** (Trouver de nouveaux modules complémentaires).</span><span class="sxs-lookup"><span data-stu-id="57839-178">Under Add-ons tab section, click **Find new add-ons**.</span></span> <span data-ttu-id="57839-179">Recherchez **SAML Single Sign On (SSO) for Jira**, puis cliquez sur le bouton **Install** pour installer le nouveau plug-in SAML.</span><span class="sxs-lookup"><span data-stu-id="57839-179">Search **SAML Single Sign On (SSO) for JIRA** and click **Install** button to install the new SAML plugin.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/addon7.png)

11. <span data-ttu-id="57839-181">L’installation du plug-in démarre.</span><span class="sxs-lookup"><span data-stu-id="57839-181">The plugin installation will start.</span></span> <span data-ttu-id="57839-182">Cliquez sur **Fermer**.</span><span class="sxs-lookup"><span data-stu-id="57839-182">Click **Close**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/addon8.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/addon9.png)

12. <span data-ttu-id="57839-185">Cliquez sur **Gérer**.</span><span class="sxs-lookup"><span data-stu-id="57839-185">Click **Manage**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/addon10.png)
    
13. <span data-ttu-id="57839-187">Cliquez sur **Configurer** pour configurer le nouveau plug-in.</span><span class="sxs-lookup"><span data-stu-id="57839-187">Click **Configure** to configure the new plugin.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/addon11.png)

14. <span data-ttu-id="57839-189">Dans la page **SAML SingleSignOn Plugin Configuration** (Configuration du plug-in d’authentification unique SAML), cliquez sur le bouton **Add additional Identity Provider** (ajouter un fournisseur d’identité) pour configurer les paramètres du fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="57839-189">On **SAML SingleSignOn Plugin Configuration** page, click **Add additional Identity Provider** button to configure the settings of Identity Provider.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/addon4.png)

15. <span data-ttu-id="57839-191">Sur cette page, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="57839-191">Perform following steps on this page:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/addon5.png)
 
    <span data-ttu-id="57839-193">a.</span><span class="sxs-lookup"><span data-stu-id="57839-193">a.</span></span> <span data-ttu-id="57839-194">Ajoutez le **Nom** du fournisseur d’identité (p. ex. Azure AD).</span><span class="sxs-lookup"><span data-stu-id="57839-194">Add **Name** of the Identity Provider (e.g Azure AD).</span></span>
    
    <span data-ttu-id="57839-195">b.</span><span class="sxs-lookup"><span data-stu-id="57839-195">b.</span></span> <span data-ttu-id="57839-196">Ajoutez la **Description** du fournisseur d’identité (p. ex. Azure AD).</span><span class="sxs-lookup"><span data-stu-id="57839-196">Add **Description** of the Identity Provider (e.g Azure AD).</span></span>

    <span data-ttu-id="57839-197">c.</span><span class="sxs-lookup"><span data-stu-id="57839-197">c.</span></span> <span data-ttu-id="57839-198">Cliquez sur **XML**, puis sélectionnez le fichier de **métadonnées** que vous avez téléchargé à partir du portail.</span><span class="sxs-lookup"><span data-stu-id="57839-198">Click **XML** and select the **Metadata** file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="57839-199">d.</span><span class="sxs-lookup"><span data-stu-id="57839-199">d.</span></span> <span data-ttu-id="57839-200">Cliquez sur le bouton **Charger**.</span><span class="sxs-lookup"><span data-stu-id="57839-200">Click **Load** button.</span></span>

    <span data-ttu-id="57839-201">e.</span><span class="sxs-lookup"><span data-stu-id="57839-201">e.</span></span> <span data-ttu-id="57839-202">Les métadonnées d’IdP sont lues et les champs sont renseignés de la manière mise en évidence dans la capture d’écran.</span><span class="sxs-lookup"><span data-stu-id="57839-202">It reads the IdP metadata and populates the fields as highlighted in the screenshot.</span></span> 

16. <span data-ttu-id="57839-203">Cliquez sur le bouton **Enregistrer les paramètres** pour enregistrer les paramètres.</span><span class="sxs-lookup"><span data-stu-id="57839-203">Click **Save settings** button to save the settings.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/addon6.png)

> [!TIP]
> <span data-ttu-id="57839-205">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="57839-205">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="57839-206">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="57839-206">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="57839-207">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="57839-207">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="57839-208">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="57839-208">Creating an Azure AD test user</span></span>
<span data-ttu-id="57839-209">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="57839-209">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="57839-211">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="57839-211">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="57839-212">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="57839-212">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="57839-214">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="57839-214">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="57839-216">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="57839-216">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="57839-218">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="57839-218">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="57839-220">a.</span><span class="sxs-lookup"><span data-stu-id="57839-220">a.</span></span> <span data-ttu-id="57839-221">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="57839-221">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="57839-222">b.</span><span class="sxs-lookup"><span data-stu-id="57839-222">b.</span></span> <span data-ttu-id="57839-223">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="57839-223">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="57839-224">c.</span><span class="sxs-lookup"><span data-stu-id="57839-224">c.</span></span> <span data-ttu-id="57839-225">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="57839-225">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="57839-226">d.</span><span class="sxs-lookup"><span data-stu-id="57839-226">d.</span></span> <span data-ttu-id="57839-227">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="57839-227">Click **Create**.</span></span>
 
### <a name="creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user"></a><span data-ttu-id="57839-228">Création d’un utilisateur de test pour SSO SAML pour Jira de resolution GmbH</span><span class="sxs-lookup"><span data-stu-id="57839-228">Creating a SAML SSO for Jira by resolution GmbH test user</span></span>

<span data-ttu-id="57839-229">Pour permettre à des utilisateurs d’Azure AD de se connecter à SSO SAML pour Jira de resolution GmbH, vous devez configurer ceux-ci dans SSO SAML pour Jira de resolution GmbH.</span><span class="sxs-lookup"><span data-stu-id="57839-229">To enable Azure AD users to log in to SAML SSO for Jira by resolution GmbH, they must be provisioned into SAML SSO for Jira by resolution GmbH.</span></span>  
<span data-ttu-id="57839-230">Dans SSO SAML pour Jira de resolution GmbH, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="57839-230">In SAML SSO for Jira by resolution GmbH, provisioning is a manual task.</span></span>

<span data-ttu-id="57839-231">**Pour approvisionner un compte d’utilisateur, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="57839-231">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="57839-232">Connectez-vous à votre site d’entreprise SSO SAML pour Jira de resolution GmbH en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="57839-232">Log in to your SAML SSO for Jira by resolution GmbH company site as an administrator.</span></span>

2. <span data-ttu-id="57839-233">Pointez sur la roue dentée, puis cliquez sur **Gestion des utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="57839-233">Hover on cog and click the **User management**.</span></span>

    ![Ajouter un employé](./media/active-directory-saas-samlssojira-tutorial/user1.png) 

3. <span data-ttu-id="57839-235">Vous êtes redirigé vers la page d’accès administrateur dans laquelle vous entrez le **mot de passe**, puis cliquez sur le bouton **Confirmer**.</span><span class="sxs-lookup"><span data-stu-id="57839-235">You are redirected to Administrator Access page to enter **Password** and click **Confirm** button.</span></span>

    ![Ajouter un employé](./media/active-directory-saas-samlssojira-tutorial/user2.png) 

4. <span data-ttu-id="57839-237">Sous l’onglet **User management** (Gestion des utilisateurs), cliquez sur **Create user** (Créer un utilisateur).</span><span class="sxs-lookup"><span data-stu-id="57839-237">Under **User management** tab section, click **create user**.</span></span>

    ![Ajouter un employé](./media/active-directory-saas-samlssojira-tutorial/user3.png) 

5. <span data-ttu-id="57839-239">Dans la page de boîte de dialogue **Create New User** (Créer un utilisateur), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="57839-239">On the **“Create new user”** dialog page, perform the following steps:</span></span>

    ![Ajouter un employé](./media/active-directory-saas-samlssojira-tutorial/user4.png) 

    <span data-ttu-id="57839-241">a.</span><span class="sxs-lookup"><span data-stu-id="57839-241">a.</span></span> <span data-ttu-id="57839-242">Dans la zone de texte **Email address** (Adresse e-mail), tapez l’adresse e-mail d’un utilisateur, par exemple, Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="57839-242">In the **Email address** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="57839-243">b.</span><span class="sxs-lookup"><span data-stu-id="57839-243">b.</span></span> <span data-ttu-id="57839-244">Dans la zone de texte **Full Name** (Nom complet), tapez le nom complet d’un utilisateur, par exemple, Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="57839-244">In the **Full Name** textbox, type full name of the user like Britta Simon.</span></span>

    <span data-ttu-id="57839-245">c.</span><span class="sxs-lookup"><span data-stu-id="57839-245">c.</span></span> <span data-ttu-id="57839-246">Dans la zone de texte **Username** (Nom d’utilisateur), tapez l’e-mail d’un utilisateur, par exemple, Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="57839-246">In the **Username** textbox, type the email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="57839-247">d.</span><span class="sxs-lookup"><span data-stu-id="57839-247">d.</span></span> <span data-ttu-id="57839-248">Dans la zone de texte **Password** (Mot de passe), tapez le mot de passe de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="57839-248">In the **Password** textbox, type the password of user.</span></span>

    <span data-ttu-id="57839-249">e.</span><span class="sxs-lookup"><span data-stu-id="57839-249">e.</span></span> <span data-ttu-id="57839-250">Cliquez sur **Create User** (Créer un utilisateur).</span><span class="sxs-lookup"><span data-stu-id="57839-250">Click **Create user**.</span></span>   

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="57839-251">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="57839-251">Assigning the Azure AD test user</span></span>

<span data-ttu-id="57839-252">Dans cette section, vous activez Britta Simon pour utiliser l’authentification unique Azure en accordant l’accès à SSO SAML pour Jira de resolution GmbH.</span><span class="sxs-lookup"><span data-stu-id="57839-252">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAML SSO for Jira by resolution GmbH.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="57839-254">**Pour affecter Britta Simon à SSO SAML pour Jira de resolution GmbH, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="57839-254">**To assign Britta Simon to SAML SSO for Jira by resolution GmbH, perform the following steps:**</span></span>

1. <span data-ttu-id="57839-255">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="57839-255">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="57839-257">Dans la liste des applications, sélectionnez **SSO SAML pour Jira de resolution GmbH**.</span><span class="sxs-lookup"><span data-stu-id="57839-257">In the applications list, select **SAML SSO for Jira by resolution GmbH**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_app.png) 

3. <span data-ttu-id="57839-259">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="57839-259">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="57839-261">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="57839-261">Click **Add** button.</span></span> <span data-ttu-id="57839-262">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="57839-262">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="57839-264">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="57839-264">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="57839-265">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="57839-265">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="57839-266">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="57839-266">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="57839-267">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="57839-267">Testing single sign-on</span></span>

<span data-ttu-id="57839-268">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="57839-268">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="57839-269">Lorsque vous cliquez sur la vignette SSO SAML pour Jira de resolution GmbH dans le panneau d’accès, vous devez être automatiquement authentifiés auprès de votre application SSO SAML pour Jira de resolution GmbH.</span><span class="sxs-lookup"><span data-stu-id="57839-269">When you click the SAML SSO for Jira by resolution GmbH tile in the Access Panel, you should get automatically signed-on to your SAML SSO for Jira by resolution GmbH application.</span></span>
<span data-ttu-id="57839-270">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="57839-270">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="57839-271">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="57839-271">Additional resources</span></span>

* [<span data-ttu-id="57839-272">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="57839-272">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="57839-273">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="57839-273">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



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

