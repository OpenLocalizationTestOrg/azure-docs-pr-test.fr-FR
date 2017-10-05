---
title: "Didacticiel : Intégration d’Azure Active Directory à Heroku | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Heroku."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d7d72ec6-4a60-4524-8634-26d8fbbcc833
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: d30605e4757b484f327a784b73f939b62ef59373
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-heroku"></a><span data-ttu-id="1ad1b-103">Didacticiel : Intégration d’Azure Active Directory à Heroku</span><span class="sxs-lookup"><span data-stu-id="1ad1b-103">Tutorial: Azure Active Directory integration with Heroku</span></span>

<span data-ttu-id="1ad1b-104">Dans ce didacticiel, vous allez apprendre à intégrer Heroku à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1ad1b-104">In this tutorial, you learn how to integrate Heroku with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1ad1b-105">L’intégration de Heroku à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="1ad1b-105">Integrating Heroku with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1ad1b-106">Dans Azure AD, vous pouvez contrôler qui a accès à Heroku.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-106">You can control in Azure AD who has access to Heroku</span></span>
- <span data-ttu-id="1ad1b-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Heroku (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-107">You can enable your users to automatically get signed-on to Heroku (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1ad1b-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="1ad1b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1ad1b-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1ad1b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1ad1b-110">Prérequis</span><span class="sxs-lookup"><span data-stu-id="1ad1b-110">Prerequisites</span></span>

<span data-ttu-id="1ad1b-111">Pour configurer l’intégration d’Azure AD à Heroku, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="1ad1b-111">To configure Azure AD integration with Heroku, you need the following items:</span></span>

- <span data-ttu-id="1ad1b-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ad1b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1ad1b-113">Un abonnement Heroku pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="1ad1b-113">A Heroku single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1ad1b-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1ad1b-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1ad1b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1ad1b-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1ad1b-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1ad1b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1ad1b-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="1ad1b-118">Scenario description</span></span>
<span data-ttu-id="1ad1b-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1ad1b-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="1ad1b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1ad1b-121">Ajout de Heroku à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="1ad1b-121">Adding Heroku from the gallery</span></span>
2. <span data-ttu-id="1ad1b-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ad1b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-heroku-from-the-gallery"></a><span data-ttu-id="1ad1b-123">Ajout de Heroku à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="1ad1b-123">Adding Heroku from the gallery</span></span>
<span data-ttu-id="1ad1b-124">Pour configurer l’intégration de Heroku à Azure AD, vous devez ajouter Heroku à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-124">To configure the integration of Heroku into Azure AD, you need to add Heroku from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1ad1b-125">**Pour ajouter Heroku à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1ad1b-125">**To add Heroku from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1ad1b-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1ad1b-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1ad1b-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="1ad1b-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="1ad1b-133">Dans la zone de recherche, tapez **Heroku**.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-133">In the search box, type **Heroku**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_search.png)

5. <span data-ttu-id="1ad1b-135">Dans le volet de résultats, sélectionnez **Heroku**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-135">In the results panel, select **Heroku**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1ad1b-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ad1b-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="1ad1b-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Heroku avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="1ad1b-138">In this section, you configure and test Azure AD single sign-on with Heroku based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1ad1b-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Heroku équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Heroku is to a user in Azure AD.</span></span> <span data-ttu-id="1ad1b-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Heroku associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-140">In other words, a link relationship between an Azure AD user and the related user in Heroku needs to be established.</span></span>

<span data-ttu-id="1ad1b-141">Dans Heroku, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-141">In Heroku, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1ad1b-142">Pour configurer et tester l’authentification unique Azure AD avec Heroku, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="1ad1b-142">To configure and test Azure AD single sign-on with Heroku, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1ad1b-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1ad1b-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1ad1b-145">**[Création d’un utilisateur de test Heroku](#creating-a-heroku-test-user)** pour avoir un équivalent de Britta Simon dans Heroku lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-145">**[Creating a Heroku test user](#creating-a-heroku-test-user)** - to have a counterpart of Britta Simon in Heroku that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1ad1b-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1ad1b-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1ad1b-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ad1b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1ad1b-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Heroku.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Heroku application.</span></span>

<span data-ttu-id="1ad1b-150">**Pour configurer l’authentification unique Azure AD avec Heroku, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1ad1b-150">**To configure Azure AD single sign-on with Heroku, perform the following steps:**</span></span>

1. <span data-ttu-id="1ad1b-151">Dans le portail Azure, dans la page d’intégration de l’application **Heroku**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-151">In the Azure portal, on the **Heroku** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="1ad1b-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_samlbase.png)

3. <span data-ttu-id="1ad1b-155">Dans la section **Domaine et URL Heroku**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="1ad1b-155">On the **Heroku Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_url.png)

    <span data-ttu-id="1ad1b-157">a.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-157">a.</span></span> <span data-ttu-id="1ad1b-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant :</span><span class="sxs-lookup"><span data-stu-id="1ad1b-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>    
    `https://sso.heroku.com/saml/<company-name>/init`

    <span data-ttu-id="1ad1b-159">b.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-159">b.</span></span> <span data-ttu-id="1ad1b-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant :</span><span class="sxs-lookup"><span data-stu-id="1ad1b-160">In the **Identifier URL** textbox, type a URL using the following pattern:</span></span>            
    `https://sso.heroku.com/saml/<company-name>`

    > [!NOTE]
    ><span data-ttu-id="1ad1b-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-161">These values are not real.</span></span> <span data-ttu-id="1ad1b-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1ad1b-163">C’est l’équipe Heroku qui vous fournit ces valeurs (comme décrit dans les sections suivantes de cet article).</span><span class="sxs-lookup"><span data-stu-id="1ad1b-163">You get these values from Heroku team, which is described in later sections of this article.</span></span> 
        
4. <span data-ttu-id="1ad1b-164">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_certificate.png) 

5. <span data-ttu-id="1ad1b-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="1ad1b-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-heroku-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1ad1b-168">Pour activer SSO dans Heroku, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1ad1b-168">To enable SSO in Heroku, perform the following steps:</span></span>
   
    <span data-ttu-id="1ad1b-169">a.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-169">a.</span></span> <span data-ttu-id="1ad1b-170">Connectez-vous au compte Heroku en tant qu'administrateur.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-170">Log in to the Heroku account as an administrator.</span></span>

    <span data-ttu-id="1ad1b-171">b.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-171">b.</span></span> <span data-ttu-id="1ad1b-172">Cliquez sur l'onglet **Paramètres** .</span><span class="sxs-lookup"><span data-stu-id="1ad1b-172">Click the **Settings** tab.</span></span>

    <span data-ttu-id="1ad1b-173">c.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-173">c.</span></span> <span data-ttu-id="1ad1b-174">Sur la page **Authentification unique**, cliquez sur **Charger les métadonnées**.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-174">On the **Single Sign On Page**, click **Upload Metadata**.</span></span>

    <span data-ttu-id="1ad1b-175">d.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-175">d.</span></span> <span data-ttu-id="1ad1b-176">Chargez le fichier de métadonnées, que vous avez téléchargé à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-176">Upload the metadata file, which you have downloaded from the Azure portal.</span></span>

    <span data-ttu-id="1ad1b-177">e.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-177">e.</span></span> <span data-ttu-id="1ad1b-178">Quand l’installation réussit, les administrateurs voient une boîte de dialogue de confirmation, et l’URL de l’authentification unique pour les utilisateurs finaux apparaît.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-178">When the setup is successful, administrators see a confirmation dialog and the URL of the SSO Login for end users is displayed.</span></span> 

    <span data-ttu-id="1ad1b-179">f.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-179">f.</span></span> <span data-ttu-id="1ad1b-180">Copiez l’**URL de connexion Heroku** et l’**ID d’entité Heroku**, puis revenez à la section **Domaine et URL Heroku** dans le portail Azure et collez ces valeurs respectivement dans les zones de texte **URL de connexion** et **Identificateur**.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-180">Copy the **Heroku Login URL** and **Heroku Entity ID** values and go back to **Heroku Domain and URLs** section in Azure portal and paste these values into the **Sign-On Url** and **Identifier** textboxes respectively.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_52.png) 
    
8. <span data-ttu-id="1ad1b-182">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-182">Click **Next**.</span></span>

> [!TIP]
> <span data-ttu-id="1ad1b-183">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1ad1b-184">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-184">After adding this app from the **Active Directory Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1ad1b-185">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1ad1b-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1ad1b-186">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ad1b-186">Creating an Azure AD test user</span></span>

<span data-ttu-id="1ad1b-187">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="1ad1b-189">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1ad1b-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1ad1b-190">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-heroku-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1ad1b-192">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-heroku-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1ad1b-194">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-heroku-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1ad1b-196">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1ad1b-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-heroku-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1ad1b-198">a.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-198">a.</span></span> <span data-ttu-id="1ad1b-199">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1ad1b-200">b.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-200">b.</span></span> <span data-ttu-id="1ad1b-201">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1ad1b-202">c.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-202">c.</span></span> <span data-ttu-id="1ad1b-203">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1ad1b-204">d.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-204">d.</span></span> <span data-ttu-id="1ad1b-205">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-205">Click **Create**.</span></span>
 
### <a name="creating-a-heroku-test-user"></a><span data-ttu-id="1ad1b-206">Création d’un utilisateur de test Heroku</span><span class="sxs-lookup"><span data-stu-id="1ad1b-206">Creating a Heroku test user</span></span>

<span data-ttu-id="1ad1b-207">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Heroku.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-207">In this section, you create a user called Britta Simon in Heroku.</span></span> <span data-ttu-id="1ad1b-208">Heroku prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-208">Heroku supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="1ad1b-209">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-209">There is no action item for you in this section.</span></span> <span data-ttu-id="1ad1b-210">Un nouvel utilisateur est créé lors de l’accès Heroku si l’utilisateur n’existe pas encore.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-210">A new user is created when accessing Heroku if the user doesn't exist yet.</span></span> <span data-ttu-id="1ad1b-211">Une fois le compte approvisionné, l’utilisateur final reçoit un message de vérification et doit cliquer sur le lien d’accusé de réception.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-211">After the account is provisioned, the end user receives a verification email and needs to click the acknowledgement link.</span></span>

>[!NOTE]
><span data-ttu-id="1ad1b-212">Si vous devez créer un utilisateur manuellement, contactez l’[équipe de support technique Heroku](https://www.heroku.com/support).</span><span class="sxs-lookup"><span data-stu-id="1ad1b-212">If you need to create a user manually, you need to contact the [Heroku Client support team](https://www.heroku.com/support).</span></span>
>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1ad1b-213">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ad1b-213">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1ad1b-214">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Heroku.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Heroku.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="1ad1b-216">**Pour affecter Britta Simon à Heroku, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1ad1b-216">**To assign Britta Simon to Heroku, perform the following steps:**</span></span>

1. <span data-ttu-id="1ad1b-217">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="1ad1b-219">Dans la liste des applications, sélectionnez **Heroku**.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-219">In the applications list, select **Heroku**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_app.png) 

3. <span data-ttu-id="1ad1b-221">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-221">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="1ad1b-223">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-223">Click **Add** button.</span></span> <span data-ttu-id="1ad1b-224">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="1ad1b-226">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1ad1b-227">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1ad1b-228">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1ad1b-229">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="1ad1b-229">Testing single sign-on</span></span>

<span data-ttu-id="1ad1b-230">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1ad1b-231">Lorsque vous cliquez sur la mosaïque Heroku dans le volet d’accès, vous devez être connecté automatiquement à votre application Heroku.</span><span class="sxs-lookup"><span data-stu-id="1ad1b-231">When you click the Heroku tile in the Access Panel, you should get automatically signed-on to your Heroku application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1ad1b-232">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="1ad1b-232">Additional resources</span></span>

* [<span data-ttu-id="1ad1b-233">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1ad1b-233">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1ad1b-234">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="1ad1b-234">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_203.png
