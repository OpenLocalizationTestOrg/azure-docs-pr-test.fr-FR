---
title: "Didacticiel : Intégration d’Azure Active Directory avec Pingboard | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Pingboard."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 008c670a8043da0c67ccefde48d5ef721c75d97c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pingboard"></a><span data-ttu-id="7081a-103">Didacticiel : Intégration d’Azure Active Directory avec Pingboard</span><span class="sxs-lookup"><span data-stu-id="7081a-103">Tutorial: Azure Active Directory integration with Pingboard</span></span>

<span data-ttu-id="7081a-104">Ce didacticiel explique comment intégrer Pingboard avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7081a-104">In this tutorial, you learn how to integrate Pingboard with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7081a-105">L’intégration de Pingboard avec Azure AD offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="7081a-105">Integrating Pingboard with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7081a-106">Dans Azure AD, vous pouvez contrôler qui a accès à Pingboard</span><span class="sxs-lookup"><span data-stu-id="7081a-106">You can control in Azure AD who has access to Pingboard</span></span>
- <span data-ttu-id="7081a-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Pingboard (via l’authentification unique) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="7081a-107">You can enable your users to automatically get signed-on to Pingboard (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7081a-108">Vous pouvez gérer vos comptes de manière centralisée dans le portail de gestion Azure.</span><span class="sxs-lookup"><span data-stu-id="7081a-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="7081a-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7081a-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7081a-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7081a-110">Prerequisites</span></span>

<span data-ttu-id="7081a-111">Pour configurer l’intégration d’Azure AD avec Pingboard, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="7081a-111">To configure Azure AD integration with Pingboard, you need the following items:</span></span>

- <span data-ttu-id="7081a-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="7081a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7081a-113">Un abonnement Pingboard pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="7081a-113">A Pingboard single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7081a-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="7081a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7081a-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="7081a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7081a-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="7081a-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="7081a-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7081a-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7081a-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="7081a-118">Scenario description</span></span>
<span data-ttu-id="7081a-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="7081a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7081a-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="7081a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7081a-121">Ajout de Pingboard à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="7081a-121">Adding Pingboard from the gallery</span></span>
2. <span data-ttu-id="7081a-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="7081a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pingboard-from-the-gallery"></a><span data-ttu-id="7081a-123">Ajout de Pingboard à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="7081a-123">Adding Pingboard from the gallery</span></span>
<span data-ttu-id="7081a-124">Pour configurer l’intégration de Pingboard avec Azure AD, vous devez ajouter Pingboard, disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="7081a-124">To configure the integration of Pingboard into Azure AD, you need to add Pingboard from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7081a-125">**Pour ajouter Pingboard à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7081a-125">**To add Pingboard from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7081a-126">Dans le panneau de navigation gauche du **[Portail de gestion Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7081a-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7081a-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="7081a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7081a-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="7081a-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="7081a-131">Cliquez sur le bouton **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="7081a-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="7081a-133">Dans le champ de recherche, tapez **Pingboard**.</span><span class="sxs-lookup"><span data-stu-id="7081a-133">In the search box, type **Pingboard**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_search.png)

5. <span data-ttu-id="7081a-135">Dans le volet de résultats, sélectionnez **Pingboard**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="7081a-135">In the results panel, select **Pingboard**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7081a-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="7081a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7081a-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Pingboard sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="7081a-138">In this section, you configure and test Azure AD single sign-on with Pingboard based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7081a-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Pingboard équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7081a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Pingboard is to a user in Azure AD.</span></span> <span data-ttu-id="7081a-140">En d’autres termes, une relation doit être établie entre l’utilisateur Azure AD et l’utilisateur Pingboard associé.</span><span class="sxs-lookup"><span data-stu-id="7081a-140">In other words, a link relationship between an Azure AD user and the related user in Pingboard needs to be established.</span></span>

<span data-ttu-id="7081a-141">Pour ce faire, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** dans Pingboard.</span><span class="sxs-lookup"><span data-stu-id="7081a-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Pingboard.</span></span>

<span data-ttu-id="7081a-142">Pour configurer et tester l’authentification unique Azure AD avec Pingboard, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="7081a-142">To configure and test Azure AD single sign-on with Pingboard, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7081a-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="7081a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7081a-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7081a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7081a-145">**[Création d’un utilisateur de test Pingboard](#creating-a-pingboard-test-user)** pour avoir un équivalent de Britta Simon dans Pingboard lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="7081a-145">**[Creating a Pingboard test user](#creating-a-pingboard-test-user)** - to have a counterpart of Britta Simon in Pingboard that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="7081a-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7081a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7081a-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="7081a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7081a-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="7081a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7081a-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail de gestion Azure et configurer l’authentification unique dans votre application Pingboard.</span><span class="sxs-lookup"><span data-stu-id="7081a-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Pingboard application.</span></span>

<span data-ttu-id="7081a-150">**Pour configurer l’authentification unique Azure AD auprès de Pingboard, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7081a-150">**To configure Azure AD single sign-on with Pingboard, perform the following steps:**</span></span>

1. <span data-ttu-id="7081a-151">Dans le portail de gestion Azure, dans la page d’intégration de l’application **Pingboard**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="7081a-151">In the Azure Management portal, on the **Pingboard** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="7081a-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="7081a-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_samlbase.png)

3. <span data-ttu-id="7081a-155">Dans la section **Domaines et URL Pingboard**, suivez les étapes ci-dessous si vous souhaitez configurer l’application en mode initié par **IDP**:</span><span class="sxs-lookup"><span data-stu-id="7081a-155">On the **Pingboard Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_url.png)

    <span data-ttu-id="7081a-157">a.</span><span class="sxs-lookup"><span data-stu-id="7081a-157">a.</span></span> <span data-ttu-id="7081a-158">Dans la zone de texte **Identificateur**, entrez la valeur `http://<entity-id>.pingboard.com/sp`</span><span class="sxs-lookup"><span data-stu-id="7081a-158">In the **Identifier** textbox, type the value as: `http://<entity-id>.pingboard.com/sp`</span></span>

    <span data-ttu-id="7081a-159">b.</span><span class="sxs-lookup"><span data-stu-id="7081a-159">b.</span></span> <span data-ttu-id="7081a-160">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://<entity-id>.pingboard.com/auth/saml/consume`</span><span class="sxs-lookup"><span data-stu-id="7081a-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<entity-id>.pingboard.com/auth/saml/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7081a-161">Notez qu’il ne s’agit pas des valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="7081a-161">Please note that these are not the real values.</span></span> <span data-ttu-id="7081a-162">Vous devez mettre à jour ces valeurs avec l’identificateur et l’URL de réponse réels.</span><span class="sxs-lookup"><span data-stu-id="7081a-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="7081a-163">Nous vous suggérons d’utiliser ici la valeur de chaîne unique dans l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="7081a-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="7081a-164">Pour obtenir ces valeurs, contactez l’[équipe de support technique Pingboard](https://support.pingboard.com/).</span><span class="sxs-lookup"><span data-stu-id="7081a-164">Contact [Pingboard Client support team](https://support.pingboard.com/) to get these values.</span></span> 

4. <span data-ttu-id="7081a-165">Cochez **Afficher les paramètres d’URL avancés** si vous souhaitez configurer l’application en mode lancé par le **fournisseur de service** :</span><span class="sxs-lookup"><span data-stu-id="7081a-165">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_sp_initiated01.png)

    <span data-ttu-id="7081a-167">a.</span><span class="sxs-lookup"><span data-stu-id="7081a-167">a.</span></span> <span data-ttu-id="7081a-168">Dans la zone de texte **URL de connexion**, tapez la valeur suivante : `http://<sub-domain>.pingboard.com/sign_in`</span><span class="sxs-lookup"><span data-stu-id="7081a-168">In the **Sign-on URL** textbox, type the value as: `http://<sub-domain>.pingboard.com/sign_in`</span></span>
     
5. <span data-ttu-id="7081a-169">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier XML sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="7081a-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_certificate.png) 

6. <span data-ttu-id="7081a-171">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="7081a-171">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-pingboard-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="7081a-173">Pour configurer l’authentification unique côté Pingboard, ouvrez une nouvelle fenêtre de navigateur et connectez-vous à votre compte Pingboard.</span><span class="sxs-lookup"><span data-stu-id="7081a-173">To configure SSO on Pingboard side, open a new browser window and log in to your Pingboard Account.</span></span> <span data-ttu-id="7081a-174">Pour configurer l’authentification unique, vous devez être un administrateur Pingboard.</span><span class="sxs-lookup"><span data-stu-id="7081a-174">You must be a Pingboard admin to set up single sign on.</span></span>

8. <span data-ttu-id="7081a-175">Dans le menu supérieur, sélectionnez **Applications > Intégrations**</span><span class="sxs-lookup"><span data-stu-id="7081a-175">From the top menu select **Apps > Integrations**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-pingboard-tutorial/Pingboard_integration.png)

9.  <span data-ttu-id="7081a-177">Sur la page **Intégrations**, recherchez la mosaïque **« Azure Active Directory »**, puis cliquez dessus.</span><span class="sxs-lookup"><span data-stu-id="7081a-177">On the **Integrations** page, find the **"Azure Active Directory"** tile, and click it.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-pingboard-tutorial/Pingboard_aad.png)

10. <span data-ttu-id="7081a-179">Dans la fenêtre modale qui suit, cliquez sur **« Configurer »**</span><span class="sxs-lookup"><span data-stu-id="7081a-179">In the modal that follows click **"Configure"**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-pingboard-tutorial/Pingboard_configure.png)

11. <span data-ttu-id="7081a-181">Sur la page suivante, vous remarquerez que « l’intégration Azure SSO est activée ».</span><span class="sxs-lookup"><span data-stu-id="7081a-181">On the following page, you will notice that "Azure SSO Integration is enabled.".</span></span> <span data-ttu-id="7081a-182">Ouvrez le fichier XML de métadonnées téléchargé dans un bloc-notes puis collez le contenu dans **IDP Metadata** (métadonnées du fournisseur d’identité).</span><span class="sxs-lookup"><span data-stu-id="7081a-182">Open the downloaded Metadata XML file in a notepad and paste the content in **IDP Metadata**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-pingboard-tutorial/Pingboard_sso_configure.png)

12. <span data-ttu-id="7081a-184">Le fichier sera validé et, si tout est correct, l’authentification unique sera alors activée</span><span class="sxs-lookup"><span data-stu-id="7081a-184">The file will be validated, and if everything is correct, single sign on will now be enabled</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7081a-185">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="7081a-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="7081a-186">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le Portail de gestion Azure.</span><span class="sxs-lookup"><span data-stu-id="7081a-186">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="7081a-188">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7081a-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7081a-189">Dans le panneau de navigation gauche du **Portail de gestion Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7081a-189">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7081a-191">Accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs** pour afficher la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="7081a-191">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7081a-193">En haut de la boîte de dialogue, cliquez sur **Ajouter** pour ouvrir la boîte de dialogue **Utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="7081a-193">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7081a-195">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="7081a-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7081a-197">a.</span><span class="sxs-lookup"><span data-stu-id="7081a-197">a.</span></span> <span data-ttu-id="7081a-198">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7081a-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7081a-199">b.</span><span class="sxs-lookup"><span data-stu-id="7081a-199">b.</span></span> <span data-ttu-id="7081a-200">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7081a-200">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7081a-201">c.</span><span class="sxs-lookup"><span data-stu-id="7081a-201">c.</span></span> <span data-ttu-id="7081a-202">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="7081a-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7081a-203">d.</span><span class="sxs-lookup"><span data-stu-id="7081a-203">d.</span></span> <span data-ttu-id="7081a-204">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="7081a-204">Click **Create**.</span></span>
 
### <a name="creating-a-pingboard-test-user"></a><span data-ttu-id="7081a-205">Création d’un utilisateur de test Pingboard</span><span class="sxs-lookup"><span data-stu-id="7081a-205">Creating a Pingboard test user</span></span>

<span data-ttu-id="7081a-206">Pour permettre aux utilisateurs Azure AD de se connecter à Pingboard, vous devez les approvisionner dans Pingboard.</span><span class="sxs-lookup"><span data-stu-id="7081a-206">In order to enable Azure AD users to log into Pingboard, they must be provisioned into Pingboard.</span></span>  
<span data-ttu-id="7081a-207">Dans le cas de Pingboard, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="7081a-207">In the case of Pingboard, provisioning is a manual task.</span></span>

<span data-ttu-id="7081a-208">**Pour approvisionner un compte d’utilisateur, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7081a-208">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="7081a-209">Connectez-vous au site d’entreprise Pingboard en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="7081a-209">Log in to your Pingboard company site as an administrator.</span></span>

2. <span data-ttu-id="7081a-210">Cliquez sur le bouton **« Ajouter un employé »** sur la page **Annuaire**.</span><span class="sxs-lookup"><span data-stu-id="7081a-210">Click **“Add Employee”** button on **Directory** page.</span></span>

    ![Ajouter un employé](./media/active-directory-saas-pingboard-tutorial/create_testuser_add.png)

3. <span data-ttu-id="7081a-212">Dans la boîte de dialogue **Ajouter un employé** , procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="7081a-212">On the **“Add Employee”** dialog page, perform the following steps.</span></span>

    ![Inviter des personnes](./media/active-directory-saas-pingboard-tutorial/create_testuser_name.png)

    <span data-ttu-id="7081a-214">a.</span><span class="sxs-lookup"><span data-stu-id="7081a-214">a.</span></span> <span data-ttu-id="7081a-215">Dans la zone de texte **Nom complet**, tapez Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7081a-215">In the **Full Name** textbox, type the full name of Britta Simon.</span></span>

    <span data-ttu-id="7081a-216">b.</span><span class="sxs-lookup"><span data-stu-id="7081a-216">b.</span></span> <span data-ttu-id="7081a-217">Dans la zone de texte **E-mail** , tapez l’adresse de messagerie du compte de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7081a-217">In the **Email** textbox, type the email address of Britta Simon account.</span></span>

    <span data-ttu-id="7081a-218">c.</span><span class="sxs-lookup"><span data-stu-id="7081a-218">c.</span></span> <span data-ttu-id="7081a-219">Dans la zone de texte **Fonction**, tapez la fonction de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7081a-219">In the **Job Title** textbox, type the job title of Britta Simon.</span></span>

    <span data-ttu-id="7081a-220">d.</span><span class="sxs-lookup"><span data-stu-id="7081a-220">d.</span></span> <span data-ttu-id="7081a-221">Dans la liste déroulante **Emplacement**, sélectionnez l’emplacement de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7081a-221">In the **Location** dropdown, select the location  of Britta Simon.</span></span>
    
    <span data-ttu-id="7081a-222">e.</span><span class="sxs-lookup"><span data-stu-id="7081a-222">e.</span></span> <span data-ttu-id="7081a-223">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="7081a-223">Click **Add**.</span></span>   

4. <span data-ttu-id="7081a-224">Un écran de confirmation s’affichera pour confirmer l’ajout de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7081a-224">A confirmation screen will come up to confirm the addition of user.</span></span>
    
    ![Confirmer](./media/active-directory-saas-pingboard-tutorial/create_testuser_confirm.png)
        
    > [!NOTE]
    > <span data-ttu-id="7081a-226">Le titulaire du compte Azure Active Directory reçoit un message électronique contenant un lien à suivre pour confirmer son compte et l’activer.</span><span class="sxs-lookup"><span data-stu-id="7081a-226">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7081a-227">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="7081a-227">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7081a-228">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Pingboard.</span><span class="sxs-lookup"><span data-stu-id="7081a-228">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Pingboard.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="7081a-230">**Pour affecter Britta Simon à Pingboard, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7081a-230">**To assign Britta Simon to Pingboard, perform the following steps:**</span></span>

1. <span data-ttu-id="7081a-231">Dans le portail de gestion Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="7081a-231">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="7081a-233">Dans la liste des applications, sélectionnez **Pingboard**.</span><span class="sxs-lookup"><span data-stu-id="7081a-233">In the applications list, select **Pingboard**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_app.png) 

3. <span data-ttu-id="7081a-235">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="7081a-235">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="7081a-237">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="7081a-237">Click **Add** button.</span></span> <span data-ttu-id="7081a-238">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="7081a-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="7081a-240">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="7081a-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7081a-241">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="7081a-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7081a-242">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="7081a-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7081a-243">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="7081a-243">Testing single sign-on</span></span>

<span data-ttu-id="7081a-244">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="7081a-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7081a-245">Lorsque vous cliquez sur la mosaïque Pingboard dans le volet d’accès, vous devez être connecté automatiquement à votre application Pingboard.</span><span class="sxs-lookup"><span data-stu-id="7081a-245">When you click the Pingboard tile in the Access Panel, you should get automatically signed-on to your Pingboard application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7081a-246">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="7081a-246">Additional resources</span></span>

* [<span data-ttu-id="7081a-247">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7081a-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7081a-248">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="7081a-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_203.png
