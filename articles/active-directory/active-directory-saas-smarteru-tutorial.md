---
title: "Didacticiel : Intégration d’Azure Active Directory à SmarterU | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et SmarterU."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 95fe3212-d052-4ac8-87eb-ac5305227e85
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 129d08c8a7b4228d4d5f1a3b7938ab649b2747a7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-smarteru"></a><span data-ttu-id="0fe45-103">Didacticiel : Intégration d’Azure Active Directory à SmarterU</span><span class="sxs-lookup"><span data-stu-id="0fe45-103">Tutorial: Azure Active Directory integration with SmarterU</span></span>

<span data-ttu-id="0fe45-104">Dans ce didacticiel, vous allez apprendre à intégrer SmarterU à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0fe45-104">In this tutorial, you learn how to integrate SmarterU with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0fe45-105">L’intégration de SmarterU dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="0fe45-105">Integrating SmarterU with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0fe45-106">Dans Azure AD, vous pouvez contrôler qui a accès à SmarterU.</span><span class="sxs-lookup"><span data-stu-id="0fe45-106">You can control in Azure AD who has access to SmarterU</span></span>
- <span data-ttu-id="0fe45-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à SmarterU (par le biais de l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0fe45-107">You can enable your users to automatically get signed-on to SmarterU (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0fe45-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="0fe45-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0fe45-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0fe45-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0fe45-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="0fe45-110">Prerequisites</span></span>

<span data-ttu-id="0fe45-111">Pour configurer l’intégration d’Azure AD à SmarterU, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="0fe45-111">To configure Azure AD integration with SmarterU, you need the following items:</span></span>

- <span data-ttu-id="0fe45-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="0fe45-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0fe45-113">Un abonnement SmarterU pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="0fe45-113">A SmarterU single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0fe45-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="0fe45-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0fe45-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="0fe45-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0fe45-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="0fe45-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0fe45-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0fe45-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0fe45-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="0fe45-118">Scenario description</span></span>
<span data-ttu-id="0fe45-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="0fe45-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0fe45-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="0fe45-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0fe45-121">Ajout de SmarterU à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="0fe45-121">Adding SmarterU from the gallery</span></span>
2. <span data-ttu-id="0fe45-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="0fe45-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-smarteru-from-the-gallery"></a><span data-ttu-id="0fe45-123">Ajout de SmarterU à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="0fe45-123">Adding SmarterU from the gallery</span></span>
<span data-ttu-id="0fe45-124">Pour configurer l’intégration de SmarterU à Azure AD, vous devez ajouter SmarterU à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="0fe45-124">To configure the integration of SmarterU into Azure AD, you need to add SmarterU from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0fe45-125">**Pour ajouter SmarterU à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0fe45-125">**To add SmarterU from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0fe45-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0fe45-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0fe45-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="0fe45-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0fe45-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="0fe45-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="0fe45-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="0fe45-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="0fe45-133">Dans la zone de recherche, entrez **SmarterU**.</span><span class="sxs-lookup"><span data-stu-id="0fe45-133">In the search box, type **SmarterU**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_search.png)

5. <span data-ttu-id="0fe45-135">Dans le volet de résultats, sélectionnez **SmarterU**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="0fe45-135">In the results panel, select **SmarterU**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0fe45-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="0fe45-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0fe45-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec SmarterU, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="0fe45-138">In this section, you configure and test Azure AD single sign-on with SmarterU based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0fe45-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur SmarterU correspondant dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0fe45-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SmarterU is to a user in Azure AD.</span></span> <span data-ttu-id="0fe45-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur SmarterU associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="0fe45-140">In other words, a link relationship between an Azure AD user and the related user in SmarterU needs to be established.</span></span>

<span data-ttu-id="0fe45-141">Dans SmarterU, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="0fe45-141">In SmarterU, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0fe45-142">Pour configurer et tester l’authentification unique Azure AD avec SmarterU, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="0fe45-142">To configure and test Azure AD single sign-on with SmarterU, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0fe45-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="0fe45-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0fe45-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0fe45-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0fe45-145">**[Création d’un utilisateur de test SmarterU](#creating-a-smarteru-test-user)** pour avoir un équivalent de Britta Simon dans SmarterU lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0fe45-145">**[Creating a SmarterU test user](#creating-a-smarteru-test-user)** - to have a counterpart of Britta Simon in SmarterU that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0fe45-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0fe45-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0fe45-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="0fe45-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0fe45-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="0fe45-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0fe45-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application SmarterU.</span><span class="sxs-lookup"><span data-stu-id="0fe45-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SmarterU application.</span></span>

<span data-ttu-id="0fe45-150">**Pour configurer l’authentification unique Azure AD avec SmarterU, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0fe45-150">**To configure Azure AD single sign-on with SmarterU, perform the following steps:**</span></span>

1. <span data-ttu-id="0fe45-151">Dans le portail Azure, sur la page d’intégration de l’application **SmarterU**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="0fe45-151">In the Azure portal, on the **SmarterU** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="0fe45-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="0fe45-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_samlbase.png)

3. <span data-ttu-id="0fe45-155">Dans la section **Domaine et URL SmarterU**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="0fe45-155">On the **SmarterU Domain and URLs** section, perform the following steps:</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_url.png)

    <span data-ttu-id="0fe45-157">Dans la zone de texte **Identificateur**, saisissez l’URL : `https://www.smarteru.com/`</span><span class="sxs-lookup"><span data-stu-id="0fe45-157">In the **Identifier** textbox, type the URL: `https://www.smarteru.com/`</span></span>

4. <span data-ttu-id="0fe45-158">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="0fe45-158">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_certificate.png) 

5. <span data-ttu-id="0fe45-160">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="0fe45-160">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-smarteru-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0fe45-162">Dans une autre fenêtre de navigateur web, connectez-vous au site de votre entreprise SmarterU en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="0fe45-162">In a different web browser window, log in to your SmarterU company site as an administrator.</span></span>

7. <span data-ttu-id="0fe45-163">Dans la barre d’outils située en haut, cliquez sur **Account Settings**.</span><span class="sxs-lookup"><span data-stu-id="0fe45-163">In the toolbar on the top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="0fe45-164">![Paramètres de compte](./media/active-directory-saas-smarteru-tutorial/IC777326.png "Paramètres de compte")</span><span class="sxs-lookup"><span data-stu-id="0fe45-164">![Account Settings](./media/active-directory-saas-smarteru-tutorial/IC777326.png "Account Settings")</span></span>

8. <span data-ttu-id="0fe45-165">Dans la page de configuration du compte, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="0fe45-165">On the account configuration page, perform the following steps:</span></span>
   
    <span data-ttu-id="0fe45-166">![Autorisation externe](./media/active-directory-saas-smarteru-tutorial/IC777327.png "Autorisation externe")</span><span class="sxs-lookup"><span data-stu-id="0fe45-166">![External Authorization](./media/active-directory-saas-smarteru-tutorial/IC777327.png "External Authorization")</span></span> 
 
      <span data-ttu-id="0fe45-167">a.</span><span class="sxs-lookup"><span data-stu-id="0fe45-167">a.</span></span> <span data-ttu-id="0fe45-168">Sélectionnez **Enable External Authorization**.</span><span class="sxs-lookup"><span data-stu-id="0fe45-168">Select **Enable External Authorization**.</span></span>
  
      <span data-ttu-id="0fe45-169">b.</span><span class="sxs-lookup"><span data-stu-id="0fe45-169">b.</span></span> <span data-ttu-id="0fe45-170">Dans la section **Master Login Control**, cliquez sur l’onglet **SmarterU**.</span><span class="sxs-lookup"><span data-stu-id="0fe45-170">In the **Master Login Control** section, select the **SmarterU** tab.</span></span>
  
      <span data-ttu-id="0fe45-171">c.</span><span class="sxs-lookup"><span data-stu-id="0fe45-171">c.</span></span> <span data-ttu-id="0fe45-172">Dans la section **User Default Login**, cliquez sur l’onglet **SmarterU**.</span><span class="sxs-lookup"><span data-stu-id="0fe45-172">In the **User Default Login** section, select the **SmarterU** tab.</span></span>
  
      <span data-ttu-id="0fe45-173">d.</span><span class="sxs-lookup"><span data-stu-id="0fe45-173">d.</span></span> <span data-ttu-id="0fe45-174">Sélectionnez **Enable Okta**.</span><span class="sxs-lookup"><span data-stu-id="0fe45-174">Select **Enable Okta**.</span></span>
  
      <span data-ttu-id="0fe45-175">e.</span><span class="sxs-lookup"><span data-stu-id="0fe45-175">e.</span></span> <span data-ttu-id="0fe45-176">Copiez le contenu du fichier de métadonnées téléchargé et collez-le dans la zone de texte **Okta Metadata** .</span><span class="sxs-lookup"><span data-stu-id="0fe45-176">Copy the content of the downloaded metadata file, and then paste it into the **Okta Metadata** textbox.</span></span>
  
      <span data-ttu-id="0fe45-177">f.</span><span class="sxs-lookup"><span data-stu-id="0fe45-177">f.</span></span> <span data-ttu-id="0fe45-178">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="0fe45-178">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="0fe45-179">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="0fe45-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0fe45-180">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="0fe45-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0fe45-181">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0fe45-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0fe45-182">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="0fe45-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="0fe45-183">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0fe45-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="0fe45-185">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0fe45-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0fe45-186">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0fe45-186">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-smarteru-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0fe45-188">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="0fe45-188">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-smarteru-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0fe45-190">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="0fe45-190">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-smarteru-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0fe45-192">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="0fe45-192">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-smarteru-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0fe45-194">a.</span><span class="sxs-lookup"><span data-stu-id="0fe45-194">a.</span></span> <span data-ttu-id="0fe45-195">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0fe45-195">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0fe45-196">b.</span><span class="sxs-lookup"><span data-stu-id="0fe45-196">b.</span></span> <span data-ttu-id="0fe45-197">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0fe45-197">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0fe45-198">c.</span><span class="sxs-lookup"><span data-stu-id="0fe45-198">c.</span></span> <span data-ttu-id="0fe45-199">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="0fe45-199">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0fe45-200">d.</span><span class="sxs-lookup"><span data-stu-id="0fe45-200">d.</span></span> <span data-ttu-id="0fe45-201">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="0fe45-201">Click **Create**.</span></span>
 
### <a name="creating-a-smarteru-test-user"></a><span data-ttu-id="0fe45-202">Création d’un utilisateur de test SmarterU</span><span class="sxs-lookup"><span data-stu-id="0fe45-202">Creating a SmarterU test user</span></span>

<span data-ttu-id="0fe45-203">Pour se connecter à SmarterU, les utilisateurs d’Azure AD doivent être approvisionnés dans SmarterU.</span><span class="sxs-lookup"><span data-stu-id="0fe45-203">To enable Azure AD users to log in to SmarterU, they must be provisioned into SmarterU.</span></span>

<span data-ttu-id="0fe45-204">Pour SmarterU, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="0fe45-204">When SmarterU, provisioning is a manual task.</span></span>

<span data-ttu-id="0fe45-205">**Pour approvisionner un compte d’utilisateur, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0fe45-205">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="0fe45-206">Connectez-vous à votre locataire **SmarterU** .</span><span class="sxs-lookup"><span data-stu-id="0fe45-206">Log in to your **SmarterU** tenant.</span></span>

2. <span data-ttu-id="0fe45-207">Accédez à **Users**.</span><span class="sxs-lookup"><span data-stu-id="0fe45-207">Go to **Users**.</span></span>

3. <span data-ttu-id="0fe45-208">Dans la section Users, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="0fe45-208">In the user section, perform the following steps:</span></span>
   
    <span data-ttu-id="0fe45-209">![Nouvel utilisateur](./media/active-directory-saas-smarteru-tutorial/IC777329.png "Nouvel utilisateur")</span><span class="sxs-lookup"><span data-stu-id="0fe45-209">![New User](./media/active-directory-saas-smarteru-tutorial/IC777329.png "New User")</span></span>  

    <span data-ttu-id="0fe45-210">a.</span><span class="sxs-lookup"><span data-stu-id="0fe45-210">a.</span></span> <span data-ttu-id="0fe45-211">Cliquez sur **+User**.</span><span class="sxs-lookup"><span data-stu-id="0fe45-211">Click **+User**.</span></span>
    
    <span data-ttu-id="0fe45-212">b.</span><span class="sxs-lookup"><span data-stu-id="0fe45-212">b.</span></span> <span data-ttu-id="0fe45-213">Saisissez les valeurs d’attribut associées au compte d’utilisateur Azure AD dans les zones de texte **Primary Email**, **Employee ID**, **Password**, **Verify Password**, **Given Name** et **Surname**.</span><span class="sxs-lookup"><span data-stu-id="0fe45-213">Type the related attribute values of the Azure AD user account into the following textboxes: **Primary Email**, **Employee ID**, **Password**, **Verify Password**, **Given Name**, **Surname**.</span></span>
    
    <span data-ttu-id="0fe45-214">c.</span><span class="sxs-lookup"><span data-stu-id="0fe45-214">c.</span></span> <span data-ttu-id="0fe45-215">Cliquez sur **Active**.</span><span class="sxs-lookup"><span data-stu-id="0fe45-215">Click **Active**.</span></span> 
    
    <span data-ttu-id="0fe45-216">d.</span><span class="sxs-lookup"><span data-stu-id="0fe45-216">d.</span></span> <span data-ttu-id="0fe45-217">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="0fe45-217">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="0fe45-218">Vous pouvez utiliser n’importe quel outil ou API de création de compte d’utilisateur, fourni par SmarterU, pour approvisionner des comptes utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="0fe45-218">You can use any other SmarterU user account creation tools or APIs provided by SmarterU to provision AAD user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0fe45-219">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="0fe45-219">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0fe45-220">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à SmarterU.</span><span class="sxs-lookup"><span data-stu-id="0fe45-220">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SmarterU.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="0fe45-222">**Pour affecter Britta Simon à SmarterU, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0fe45-222">**To assign Britta Simon to SmarterU, perform the following steps:**</span></span>

1. <span data-ttu-id="0fe45-223">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="0fe45-223">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="0fe45-225">Dans la liste des applications, sélectionnez **SmarterU**.</span><span class="sxs-lookup"><span data-stu-id="0fe45-225">In the applications list, select **SmarterU**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_app.png) 

3. <span data-ttu-id="0fe45-227">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="0fe45-227">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="0fe45-229">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="0fe45-229">Click **Add** button.</span></span> <span data-ttu-id="0fe45-230">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="0fe45-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="0fe45-232">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="0fe45-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0fe45-233">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="0fe45-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0fe45-234">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="0fe45-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0fe45-235">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="0fe45-235">Testing single sign-on</span></span>

<span data-ttu-id="0fe45-236">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="0fe45-236">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
 
<span data-ttu-id="0fe45-237">Quand vous cliquez sur la vignette SmarterU dans le volet d’accès, vous devez être connecté automatiquement à votre application SmarterU.</span><span class="sxs-lookup"><span data-stu-id="0fe45-237">When you click the SmarterU tile in the Access Panel, you should get automatically signed-on to your SmarterU application.</span></span>
<span data-ttu-id="0fe45-238">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0fe45-238">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 


## <a name="additional-resources"></a><span data-ttu-id="0fe45-239">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="0fe45-239">Additional resources</span></span>

* [<span data-ttu-id="0fe45-240">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0fe45-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0fe45-241">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="0fe45-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_203.png

