---
title: "Didacticiel : Intégration d’Azure Active Directory à Oneteam | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Oneteam."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2e94916c-64ae-4e1a-a8b5-bc6ef7d28c29
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: c4381ca3166bd75bda1179b9a67b2224ba58ae68
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-oneteam"></a><span data-ttu-id="1502a-103">Didacticiel : Intégration d’Azure Active Directory à Oneteam</span><span class="sxs-lookup"><span data-stu-id="1502a-103">Tutorial: Azure Active Directory integration with Oneteam</span></span>

<span data-ttu-id="1502a-104">Dans ce didacticiel, vous allez apprendre à intégrer Oneteam à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1502a-104">In this tutorial, you learn how to integrate Oneteam with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1502a-105">L’intégration de Oneteam dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="1502a-105">Integrating Oneteam with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1502a-106">Dans Azure AD, vous pouvez contrôler qui a accès à Oneteam.</span><span class="sxs-lookup"><span data-stu-id="1502a-106">You can control in Azure AD who has access to Oneteam</span></span>
- <span data-ttu-id="1502a-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Oneteam (par le biais de l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1502a-107">You can enable your users to automatically get signed-on to Oneteam (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1502a-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="1502a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1502a-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1502a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1502a-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1502a-110">Prerequisites</span></span>

<span data-ttu-id="1502a-111">Pour configurer l’intégration d’Azure AD à Oneteam, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="1502a-111">To configure Azure AD integration with Oneteam, you need the following items:</span></span>

- <span data-ttu-id="1502a-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="1502a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1502a-113">Un abonnement Oneteam pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="1502a-113">A Oneteam single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1502a-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="1502a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1502a-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1502a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1502a-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="1502a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1502a-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1502a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1502a-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="1502a-118">Scenario description</span></span>
<span data-ttu-id="1502a-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="1502a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1502a-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="1502a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1502a-121">Ajout de Oneteam depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="1502a-121">Adding Oneteam from the gallery</span></span>
2. <span data-ttu-id="1502a-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1502a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-oneteam-from-the-gallery"></a><span data-ttu-id="1502a-123">Ajout de Oneteam depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="1502a-123">Adding Oneteam from the gallery</span></span>
<span data-ttu-id="1502a-124">Pour configurer l’intégration de Oneteam à Azure AD, vous devez ajouter Oneteam à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="1502a-124">To configure the integration of Oneteam into Azure AD, you need to add Oneteam from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1502a-125">**Pour ajouter Oneteam à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1502a-125">**To add Oneteam from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1502a-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1502a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1502a-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="1502a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1502a-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1502a-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="1502a-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1502a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="1502a-133">Dans la zone de recherche, tapez **Oneteam**.</span><span class="sxs-lookup"><span data-stu-id="1502a-133">In the search box, type **Oneteam**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_search.png)

5. <span data-ttu-id="1502a-135">Dans le panneau des résultats, sélectionnez **Oneteam**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="1502a-135">In the results panel, select **Oneteam**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1502a-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1502a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1502a-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Oneteam avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="1502a-138">In this section, you configure and test Azure AD single sign-on with Oneteam based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1502a-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Oneteam équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1502a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Oneteam is to a user in Azure AD.</span></span> <span data-ttu-id="1502a-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Oneteam associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="1502a-140">In other words, a link relationship between an Azure AD user and the related user in Oneteam needs to be established.</span></span>

<span data-ttu-id="1502a-141">Dans Oneteam, assignez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="1502a-141">In Oneteam, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1502a-142">Pour configurer et tester l’authentification unique Azure AD avec Oneteam, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="1502a-142">To configure and test Azure AD single sign-on with Oneteam, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1502a-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="1502a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1502a-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1502a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1502a-145">**[Création d’un utilisateur de test Oneteam](#creating-a-oneteam-test-user)** pour obtenir un équivalent de Britta Simon dans Oneteam lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="1502a-145">**[Creating a Oneteam test user](#creating-a-oneteam-test-user)** - to have a counterpart of Britta Simon in Oneteam that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1502a-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1502a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1502a-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="1502a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1502a-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1502a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1502a-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Oneteam.</span><span class="sxs-lookup"><span data-stu-id="1502a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Oneteam application.</span></span>

<span data-ttu-id="1502a-150">**Pour configurer l’authentification unique Azure AD avec Oneteam, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1502a-150">**To configure Azure AD single sign-on with Oneteam, perform the following steps:**</span></span>

1. <span data-ttu-id="1502a-151">Dans le Portail Azure, sur la page d’intégration de l’application **Oneteam**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="1502a-151">In the Azure portal, on the **Oneteam** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="1502a-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="1502a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_samlbase.png)

3. <span data-ttu-id="1502a-155">Dans la section **Domaines et URL Oneteam**, si vous souhaitez configurer l’application en mode initié par **IDP**, suivez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1502a-155">On the **Oneteam Domain and URLs** section, if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_url.png)

    <span data-ttu-id="1502a-157">a.</span><span class="sxs-lookup"><span data-stu-id="1502a-157">a.</span></span> <span data-ttu-id="1502a-158">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://api.one-team.io/teams/<team name>`</span><span class="sxs-lookup"><span data-stu-id="1502a-158">In the **Identifier** textbox, type a URL using the following pattern: `https://api.one-team.io/teams/<team name>`</span></span>

    <span data-ttu-id="1502a-159">b.</span><span class="sxs-lookup"><span data-stu-id="1502a-159">b.</span></span> <span data-ttu-id="1502a-160">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://api.one-team.io/teams/<team name>/auth/saml/callback`</span><span class="sxs-lookup"><span data-stu-id="1502a-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://api.one-team.io/teams/<team name>/auth/saml/callback`</span></span>

4. <span data-ttu-id="1502a-161">Cochez **Afficher les paramètres d’URL avancés** si vous souhaitez configurer l’application en mode lancé par le **fournisseur de service** :</span><span class="sxs-lookup"><span data-stu-id="1502a-161">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_url1.png)

    <span data-ttu-id="1502a-163">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<team name>.one-team.io/`</span><span class="sxs-lookup"><span data-stu-id="1502a-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<team name>.one-team.io/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="1502a-164">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="1502a-164">These values are not real.</span></span> <span data-ttu-id="1502a-165">Mettez à jour ces valeurs avec l’identificateur, l’URL de réponse et l’URL de connexion réels.</span><span class="sxs-lookup"><span data-stu-id="1502a-165">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="1502a-166">Pour obtenir ces valeurs, contactez l’[équipe de support technique Oneteam](https://support.one-team.com/hc/requests/new).</span><span class="sxs-lookup"><span data-stu-id="1502a-166">Contact [Oneteam Client support team](https://support.one-team.com/hc/requests/new) to get these values.</span></span> 



5. <span data-ttu-id="1502a-167">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="1502a-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_certificate.png) 

6. <span data-ttu-id="1502a-169">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="1502a-169">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-oneteam-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="1502a-171">Pour configurer l’authentification unique pour votre application, vous pouvez ouvrir un ticket de support auprès de [l’équipe Oneteam](https://support.one-team.com/hc/requests/new) et lui fournir les **métadonnées** téléchargées.</span><span class="sxs-lookup"><span data-stu-id="1502a-171">To get SSO configured for your application, you can raise the support ticket with [Oneteam support team](https://support.one-team.com/hc/requests/new) and provide them the downloaded **Metadata**.</span></span> 

> [!TIP]
> <span data-ttu-id="1502a-172">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="1502a-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1502a-173">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="1502a-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1502a-174">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1502a-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1502a-175">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="1502a-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="1502a-176">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1502a-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="1502a-178">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1502a-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1502a-179">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1502a-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-oneteam-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1502a-181">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="1502a-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-oneteam-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1502a-183">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1502a-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-oneteam-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1502a-185">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1502a-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-oneteam-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1502a-187">a.</span><span class="sxs-lookup"><span data-stu-id="1502a-187">a.</span></span> <span data-ttu-id="1502a-188">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1502a-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1502a-189">b.</span><span class="sxs-lookup"><span data-stu-id="1502a-189">b.</span></span> <span data-ttu-id="1502a-190">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1502a-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1502a-191">c.</span><span class="sxs-lookup"><span data-stu-id="1502a-191">c.</span></span> <span data-ttu-id="1502a-192">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="1502a-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1502a-193">d.</span><span class="sxs-lookup"><span data-stu-id="1502a-193">d.</span></span> <span data-ttu-id="1502a-194">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="1502a-194">Click **Create**.</span></span>
 
### <a name="creating-a-oneteam-test-user"></a><span data-ttu-id="1502a-195">Création d’un utilisateur de test Oneteam</span><span class="sxs-lookup"><span data-stu-id="1502a-195">Creating a Oneteam test user</span></span>

<span data-ttu-id="1502a-196">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans Oneteam.</span><span class="sxs-lookup"><span data-stu-id="1502a-196">The objective of this section is to create a user called Britta Simon in Oneteam.</span></span> <span data-ttu-id="1502a-197">Oneteam prend en charge l’approvisionnement de type just-in-time (juste à temps) qui est activé par défaut.</span><span class="sxs-lookup"><span data-stu-id="1502a-197">Oneteam supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="1502a-198">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="1502a-198">There is no action item for you in this section.</span></span> <span data-ttu-id="1502a-199">Un nouvel utilisateur est créé lors d’une tentative d’accès à Oneteam, s’il n’existe pas déjà.</span><span class="sxs-lookup"><span data-stu-id="1502a-199">A new user will be created during an attempt to access Oneteam, if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="1502a-200">Si vous devez créer un utilisateur manuellement, vous pouvez ouvrir un ticket de support auprès de [l’équipe Oneteam](https://support.one-team.com/hc/requests/new).</span><span class="sxs-lookup"><span data-stu-id="1502a-200">If you need to create an user manually, you can raise the support ticket with [Oneteam support team](https://support.one-team.com/hc/requests/new).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1502a-201">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="1502a-201">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1502a-202">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Oneteam.</span><span class="sxs-lookup"><span data-stu-id="1502a-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Oneteam.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="1502a-204">**Pour affecter Britta Simon à Oneteam, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1502a-204">**To assign Britta Simon to Oneteam, perform the following steps:**</span></span>

1. <span data-ttu-id="1502a-205">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1502a-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="1502a-207">Dans la liste des applications, sélectionnez **Oneteam**.</span><span class="sxs-lookup"><span data-stu-id="1502a-207">In the applications list, select **Oneteam**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_app.png) 

3. <span data-ttu-id="1502a-209">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1502a-209">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="1502a-211">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="1502a-211">Click **Add** button.</span></span> <span data-ttu-id="1502a-212">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="1502a-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="1502a-214">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="1502a-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1502a-215">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1502a-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1502a-216">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="1502a-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1502a-217">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="1502a-217">Testing single sign-on</span></span>

<span data-ttu-id="1502a-218">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="1502a-218">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1502a-219">Lorsque vous cliquez sur la mosaïque Oneteam dans le volet d’accès, vous devez être connecté automatiquement à votre application Oneteam.</span><span class="sxs-lookup"><span data-stu-id="1502a-219">When you click the Oneteam tile in the Access Panel, you should get automatically signed-on to your Oneteam application.</span></span>
<span data-ttu-id="1502a-220">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1502a-220">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1502a-221">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="1502a-221">Additional resources</span></span>

* [<span data-ttu-id="1502a-222">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1502a-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1502a-223">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="1502a-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_203.png

