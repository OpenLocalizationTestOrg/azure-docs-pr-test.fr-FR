---
title: "Didacticiel : Intégration d’Azure Active Directory à BGS Online | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et BGS Online."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4fd6b29b-1b46-4fd1-9f5e-16b1c9d892cd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: d1abd3f8e2980e03fc092613183a261880fbce38
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bgs-online"></a><span data-ttu-id="6a838-103">Didacticiel : Intégration d’Azure Active Directory à BGS Online</span><span class="sxs-lookup"><span data-stu-id="6a838-103">Tutorial: Azure Active Directory integration with BGS Online</span></span>

<span data-ttu-id="6a838-104">Dans ce didacticiel, vous allez apprendre à intégrer BGS Online avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6a838-104">In this tutorial, you learn how to integrate BGS Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6a838-105">L’intégration de BGS Online avec Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="6a838-105">Integrating BGS Online with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6a838-106">Dans Azure AD, vous pouvez contrôler qui a accès à BGS Online.</span><span class="sxs-lookup"><span data-stu-id="6a838-106">You can control in Azure AD who has access to BGS Online</span></span>
- <span data-ttu-id="6a838-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à BGS Online (authentification unique) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6a838-107">You can enable your users to automatically get signed-on to BGS Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6a838-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="6a838-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6a838-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6a838-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6a838-110">Prérequis</span><span class="sxs-lookup"><span data-stu-id="6a838-110">Prerequisites</span></span>

<span data-ttu-id="6a838-111">Pour configurer l’intégration d’Azure AD à BGS Online, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="6a838-111">To configure Azure AD integration with BGS Online, you need the following items:</span></span>

- <span data-ttu-id="6a838-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a838-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6a838-113">Un abonnement BGS Online pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="6a838-113">A BGS Online single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6a838-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="6a838-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6a838-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="6a838-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6a838-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="6a838-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6a838-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6a838-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6a838-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="6a838-118">Scenario description</span></span>
<span data-ttu-id="6a838-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="6a838-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6a838-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="6a838-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6a838-121">Ajout de BGS Online à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="6a838-121">Adding BGS Online from the gallery</span></span>
2. <span data-ttu-id="6a838-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a838-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bgs-online-from-the-gallery"></a><span data-ttu-id="6a838-123">Ajout de BGS Online à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="6a838-123">Adding BGS Online from the gallery</span></span>
<span data-ttu-id="6a838-124">Pour configurer l’intégration de BGS Online à Azure AD, vous devez ajouter BGS Online à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="6a838-124">To configure the integration of BGS Online into Azure AD, you need to add BGS Online from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6a838-125">**Pour ajouter BGS Online à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6a838-125">**To add BGS Online from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6a838-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6a838-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6a838-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="6a838-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6a838-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="6a838-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="6a838-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="6a838-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="6a838-133">Dans la zone de recherche, tapez **BGS Online**.</span><span class="sxs-lookup"><span data-stu-id="6a838-133">In the search box, type **BGS Online**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_search.png)

5. <span data-ttu-id="6a838-135">Dans le volet de résultats, sélectionnez **BGS Online**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="6a838-135">In the results panel, select **BGS Online**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6a838-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a838-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6a838-138">Dans cette section, vous configurez et testez l’authentification unique Azure AD avec BGS Online au moyen d’un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="6a838-138">In this section, you configure and test Azure AD single sign-on with BGS Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6a838-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir quel utilisateur dans BGS Online équivaut à un utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6a838-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BGS Online is to a user in Azure AD.</span></span> <span data-ttu-id="6a838-140">En d’autres termes, une relation doit être établie entre un utilisateur Azure AD et l’utilisateur associé dans BGS Online.</span><span class="sxs-lookup"><span data-stu-id="6a838-140">In other words, a link relationship between an Azure AD user and the related user in BGS Online needs to be established.</span></span>

<span data-ttu-id="6a838-141">Dans BGS Online, affectez la valeur du **nom d’utilisateur** indiquée dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="6a838-141">In BGS Online, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6a838-142">Pour configurer et tester l’authentification unique Azure AD avec BGS Online, vous devez suivre les instructions des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="6a838-142">To configure and test Azure AD single sign-on with BGS Online, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6a838-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="6a838-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6a838-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6a838-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6a838-145">**[Création d’un utilisateur de test BGS Online](#creating-a-bgs-online-test-user)** pour avoir dans BGS Online un équivalent de Britta Simon lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6a838-145">**[Creating a BGS Online test user](#creating-a-bgs-online-test-user)** - to have a counterpart of Britta Simon in BGS Online that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6a838-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6a838-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6a838-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="6a838-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6a838-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a838-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6a838-149">Dans cette section, vous activez l’authentification unique Azure AD dans le portail Azure et configurez l’authentification unique dans votre application BGS Online.</span><span class="sxs-lookup"><span data-stu-id="6a838-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BGS Online application.</span></span>

<span data-ttu-id="6a838-150">**Procédez comme suit pour configurer l’authentification unique Azure AD avec BGS Online :**</span><span class="sxs-lookup"><span data-stu-id="6a838-150">**To configure Azure AD single sign-on with BGS Online, perform the following steps:**</span></span>

1. <span data-ttu-id="6a838-151">Dans le portail Azure, sur la page d’intégration de l’application **BGS Online**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="6a838-151">In the Azure portal, on the **BGS Online** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="6a838-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="6a838-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_samlbase.png)

3. <span data-ttu-id="6a838-155">Dans la section **Domaine et URL BGS Online**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="6a838-155">On the **BGS Online Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_url.png)

    <span data-ttu-id="6a838-157">a.</span><span class="sxs-lookup"><span data-stu-id="6a838-157">a.</span></span> <span data-ttu-id="6a838-158">Dans la zone de texte **Identificateur**, tapez une URL au format suivant :</span><span class="sxs-lookup"><span data-stu-id="6a838-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>

    <span data-ttu-id="6a838-159">Pour un environnement de production, utilisez ce modèle `https://<company name>.millwardbrown.report`</span><span class="sxs-lookup"><span data-stu-id="6a838-159">For production environment, use this pattern `https://<company name>.millwardbrown.report`</span></span> 

    <span data-ttu-id="6a838-160">Pour un environnement de test, utilisez ce modèle `https://millwardbrown.marketingtracker.nl/mt5/`</span><span class="sxs-lookup"><span data-stu-id="6a838-160">For test environment, use this pattern `https://millwardbrown.marketingtracker.nl/mt5/`</span></span>

    <span data-ttu-id="6a838-161">b.</span><span class="sxs-lookup"><span data-stu-id="6a838-161">b.</span></span> <span data-ttu-id="6a838-162">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant :</span><span class="sxs-lookup"><span data-stu-id="6a838-162">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    
    <span data-ttu-id="6a838-163">Pour un environnement de production, utilisez ce modèle `https://<company name>.millwardbrown.report/sso/saml/AssertionConsumerService.aspx`</span><span class="sxs-lookup"><span data-stu-id="6a838-163">For production environment, use this pattern `https://<company name>.millwardbrown.report/sso/saml/AssertionConsumerService.aspx`</span></span> 
      
    <span data-ttu-id="6a838-164">Pour un environnement de test, utilisez ce modèle `https://millwardbrown.marketingtracker.nl/mt5/sso/saml/AssertionConsumerService.aspx`</span><span class="sxs-lookup"><span data-stu-id="6a838-164">For test environment, use this pattern `https://millwardbrown.marketingtracker.nl/mt5/sso/saml/AssertionConsumerService.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6a838-165">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="6a838-165">These values are not real.</span></span> <span data-ttu-id="6a838-166">Mettez à jour ces valeurs avec l’identificateur et l’URL de réponse réels.</span><span class="sxs-lookup"><span data-stu-id="6a838-166">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="6a838-167">Pour obtenir ces valeurs, contactez [l’équipe du support technique de BGS Online](mailTo:bgsdashboardteam@millwardbrown.com).</span><span class="sxs-lookup"><span data-stu-id="6a838-167">Contact [BGS Online support team](mailTo:bgsdashboardteam@millwardbrown.com) to get these values.</span></span>
 

4. <span data-ttu-id="6a838-168">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="6a838-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_certificate.png) 

5. <span data-ttu-id="6a838-170">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="6a838-170">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bgsonline-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6a838-172">Dans la section **Configuration BGS Online**, cliquez sur **Configurer BGS Online** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="6a838-172">On the **BGS Online Configuration** section, click **Configure BGS Online** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6a838-173">Copiez l**’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="6a838-173">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_configure.png) 

7. <span data-ttu-id="6a838-175">Pour configurer l’authentification unique du côté de **BGS Online**, vous devez envoyer le fichier **XML de métadonnées** et **l’URL du service d’authentification unique SAML** téléchargés à [l’équipe du support technique de BGS Online](mailto:bgsdashboardteam@millwardbrown.com).</span><span class="sxs-lookup"><span data-stu-id="6a838-175">To configure single sign-on on **BGS Online** side, you need to send the downloaded **Metadata XML** and **SAML Single Sign-On Service URL** to [BGS Online support team](mailto:bgsdashboardteam@millwardbrown.com).</span></span> 


> [!TIP]
> <span data-ttu-id="6a838-176">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="6a838-176">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6a838-177">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="6a838-177">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6a838-178">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6a838-178">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6a838-179">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a838-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="6a838-180">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="6a838-180">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="6a838-182">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6a838-182">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6a838-183">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6a838-183">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6a838-185">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="6a838-185">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6a838-187">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="6a838-187">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6a838-189">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="6a838-189">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6a838-191">a.</span><span class="sxs-lookup"><span data-stu-id="6a838-191">a.</span></span> <span data-ttu-id="6a838-192">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6a838-192">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6a838-193">b.</span><span class="sxs-lookup"><span data-stu-id="6a838-193">b.</span></span> <span data-ttu-id="6a838-194">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6a838-194">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6a838-195">c.</span><span class="sxs-lookup"><span data-stu-id="6a838-195">c.</span></span> <span data-ttu-id="6a838-196">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="6a838-196">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6a838-197">d.</span><span class="sxs-lookup"><span data-stu-id="6a838-197">d.</span></span> <span data-ttu-id="6a838-198">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="6a838-198">Click **Create**.</span></span>
 
### <a name="creating-a-bgs-online-test-user"></a><span data-ttu-id="6a838-199">Création d’un utilisateur de test BGS Online</span><span class="sxs-lookup"><span data-stu-id="6a838-199">Creating a BGS Online test user</span></span>

<span data-ttu-id="6a838-200">Dans cette section, vous allez créer un utilisateur nommé Britta Simon dans BGS Online.</span><span class="sxs-lookup"><span data-stu-id="6a838-200">In this section, you create a user called Britta Simon in BGS Online.</span></span> <span data-ttu-id="6a838-201">Contactez [l’équipe du support technique de BGS Online](mailto:bgsdashboardteam@millwardbrown.com) pour ajouter des utilisateurs à la plateforme BGS Online.</span><span class="sxs-lookup"><span data-stu-id="6a838-201">Work with [BGS Online support team](mailto:bgsdashboardteam@millwardbrown.com) to add the users in the BGS Online platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6a838-202">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a838-202">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6a838-203">Dans cette section, vous autorisez Britta Simon à utiliser l’authentification unique Azure en accordant l’accès à BGS Online.</span><span class="sxs-lookup"><span data-stu-id="6a838-203">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BGS Online.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="6a838-205">**Pour affecter Britta Simon à BGS Online, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6a838-205">**To assign Britta Simon to BGS Online, perform the following steps:**</span></span>

1. <span data-ttu-id="6a838-206">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="6a838-206">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="6a838-208">Dans la liste des applications, sélectionnez **BGS Online**.</span><span class="sxs-lookup"><span data-stu-id="6a838-208">In the applications list, select **BGS Online**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_app.png) 

3. <span data-ttu-id="6a838-210">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="6a838-210">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="6a838-212">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="6a838-212">Click **Add** button.</span></span> <span data-ttu-id="6a838-213">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="6a838-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="6a838-215">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="6a838-215">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6a838-216">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="6a838-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6a838-217">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="6a838-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6a838-218">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="6a838-218">Testing single sign-on</span></span>

<span data-ttu-id="6a838-219">Dans cette section, vous allez tester la configuration SSO Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="6a838-219">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="6a838-220">Quand vous cliquez sur la vignette BGS Online dans le volet d’accès, vous devez être authentifié automatiquement auprès de votre application BGS Online.</span><span class="sxs-lookup"><span data-stu-id="6a838-220">When you click the BGS Online tile in the Access Panel, you should get automatically signed-on to your BGS Online application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6a838-221">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="6a838-221">Additional resources</span></span>

* [<span data-ttu-id="6a838-222">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6a838-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6a838-223">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="6a838-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_203.png

