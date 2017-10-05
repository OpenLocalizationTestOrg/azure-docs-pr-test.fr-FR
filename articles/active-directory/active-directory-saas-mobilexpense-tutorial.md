---
title: "Didacticiel : Intégration d’Azure Active Directory à MobileXpense | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et MobileXpense."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e649fc4e-3e15-4948-b977-00bfe9f7db13
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: jeedes
ms.openlocfilehash: 030a1fc9f36d6fcfa607552d85ce232e36eaa64b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mobilexpense"></a><span data-ttu-id="57420-103">Didacticiel : Intégration d’Azure Active Directory à MobileXpense</span><span class="sxs-lookup"><span data-stu-id="57420-103">Tutorial: Azure Active Directory integration with MobileXpense</span></span>

<span data-ttu-id="57420-104">Dans ce didacticiel, vous allez apprendre à intégrer MobileXpense à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="57420-104">In this tutorial, you learn how to integrate MobileXpense with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="57420-105">L’intégration de MobileXpense à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="57420-105">Integrating MobileXpense with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="57420-106">Dans Azure AD, vous pouvez contrôler qui a accès à MobileXpense</span><span class="sxs-lookup"><span data-stu-id="57420-106">You can control in Azure AD who has access to MobileXpense</span></span>
- <span data-ttu-id="57420-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à MobileXpense (via l’authentification unique) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="57420-107">You can enable your users to automatically get signed-on to MobileXpense (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="57420-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="57420-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="57420-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="57420-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="57420-110">Prérequis</span><span class="sxs-lookup"><span data-stu-id="57420-110">Prerequisites</span></span>

<span data-ttu-id="57420-111">Pour configurer l’intégration d’Azure AD à MobileXpense, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="57420-111">To configure Azure AD integration with MobileXpense, you need the following items:</span></span>

- <span data-ttu-id="57420-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="57420-112">An Azure AD subscription</span></span>
- <span data-ttu-id="57420-113">Un abonnement MobileXpense pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="57420-113">A MobileXpense single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="57420-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="57420-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="57420-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="57420-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="57420-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="57420-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="57420-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="57420-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="57420-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="57420-118">Scenario description</span></span>
<span data-ttu-id="57420-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="57420-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="57420-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="57420-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="57420-121">Ajout de MobileXpense à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="57420-121">Adding MobileXpense from the gallery</span></span>
2. <span data-ttu-id="57420-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="57420-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mobilexpense-from-the-gallery"></a><span data-ttu-id="57420-123">Ajout de MobileXpense à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="57420-123">Adding MobileXpense from the gallery</span></span>
<span data-ttu-id="57420-124">Pour configurer l’intégration de MobileXpense à Azure AD, vous devez ajouter MobileXpense à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="57420-124">To configure the integration of MobileXpense into Azure AD, you need to add MobileXpense from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="57420-125">**Pour ajouter MobileXpense à partir de la galerie, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="57420-125">**To add MobileXpense from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="57420-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="57420-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="57420-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="57420-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="57420-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="57420-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="57420-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="57420-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="57420-133">Dans la zone de recherche, tapez **MobileXpense**.</span><span class="sxs-lookup"><span data-stu-id="57420-133">In the search box, type **MobileXpense**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_search.png)

5. <span data-ttu-id="57420-135">Dans le volet de résultats, sélectionnez **MobileXpense**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="57420-135">In the results panel, select **MobileXpense**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="57420-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="57420-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="57420-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec MobileXpense pour un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="57420-138">In this section, you configure and test Azure AD single sign-on with MobileXpense based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="57420-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur MobileXpense équivalent à un utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="57420-139">For single sign-on to work, Azure AD needs to know what the counterpart user in MobileXpense is to a user in Azure AD.</span></span> <span data-ttu-id="57420-140">En d’autres termes, une relation doit être établie entre un utilisateur Azure AD et l’utilisateur associé dans MobileXpense.</span><span class="sxs-lookup"><span data-stu-id="57420-140">In other words, a link relationship between an Azure AD user and the related user in MobileXpense needs to be established.</span></span>

<span data-ttu-id="57420-141">Dans MobileXpense, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="57420-141">In MobileXpense, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="57420-142">Pour configurer et tester l’authentification unique Azure AD avec MobileXpense, vous devez effectuer les deux actions essentielles suivantes :</span><span class="sxs-lookup"><span data-stu-id="57420-142">To configure and test Azure AD single sign-on with MobileXpense, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="57420-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="57420-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="57420-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="57420-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="57420-145">**[Création d’un utilisateur de test MobileXpense](#creating-a-mobilexpense-test-user)** pour avoir un équivalent de Britta Simon dans MobileXpense lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="57420-145">**[Creating a MobileXpense test user](#creating-a-mobilexpense-test-user)** - to have a counterpart of Britta Simon in MobileXpense that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="57420-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="57420-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="57420-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="57420-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="57420-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="57420-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="57420-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application MobileXpense.</span><span class="sxs-lookup"><span data-stu-id="57420-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your MobileXpense application.</span></span>

<span data-ttu-id="57420-150">**Pour configurer l’authentification unique Azure AD avec MobileXpense, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="57420-150">**To configure Azure AD single sign-on with MobileXpense, perform the following steps:**</span></span>

1. <span data-ttu-id="57420-151">Dans le portail Azure, sur la page d’intégration de l’application **MobileXpense**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="57420-151">In the Azure portal, on the **MobileXpense** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="57420-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="57420-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_samlbase.png)

3. <span data-ttu-id="57420-155">Dans la section **Domaines et URL MobileXpense**, si vous souhaitez configurer l’application en mode initié par le **fournisseur d’identité (IDP)** :</span><span class="sxs-lookup"><span data-stu-id="57420-155">On the **MobileXpense Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_url11.png)

    <span data-ttu-id="57420-157">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://<sub domain>.mobilexpense.com/SSO/SAML20/SAML/AssertionConsumerService.aspx`</span><span class="sxs-lookup"><span data-stu-id="57420-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<sub domain>.mobilexpense.com/SSO/SAML20/SAML/AssertionConsumerService.aspx`</span></span>

4. <span data-ttu-id="57420-158">Cochez **Afficher les paramètres d’URL avancés** si vous souhaitez configurer l’application en mode initié par le **fournisseur de service** :</span><span class="sxs-lookup"><span data-stu-id="57420-158">Check **Show advanced URL settings**, If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_url22.png)

<span data-ttu-id="57420-160">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<sub domain>.mobilexpense.com/<customername>`</span><span class="sxs-lookup"><span data-stu-id="57420-160">In the **Sign-on URL** textbox, type a URL using the following pattern:: `https://<sub domain>.mobilexpense.com/<customername>`</span></span>

> [!NOTE] 
> <span data-ttu-id="57420-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="57420-161">These values are not real.</span></span> <span data-ttu-id="57420-162">Mettez à jour ces valeurs avec l’URL de réponse et l’URL de connexion réelles.</span><span class="sxs-lookup"><span data-stu-id="57420-162">Update these values with the actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="57420-163">Pour obtenir ces valeurs, contactez l’[équipe de support technique MobileXpense](http://www.mobilexpense.net/contact).</span><span class="sxs-lookup"><span data-stu-id="57420-163">Contact [MobileXpense Client support team](http://www.mobilexpense.net/contact) to get these values.</span></span> 

5. <span data-ttu-id="57420-164">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="57420-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_certificate.png) 

6. <span data-ttu-id="57420-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="57420-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="57420-168">Pour configurer l’authentification unique côté **MobileXpense**, vous devez envoyer le fichier **XML de métadonnées** téléchargé à l’[équipe de support technique MobileXpense](http://www.mobilexpense.net/contact).</span><span class="sxs-lookup"><span data-stu-id="57420-168">To configure single sign-on on **MobileXpense** side, you need to send the downloaded **Metadata XML** to [MobileXpense support team](http://www.mobilexpense.net/contact).</span></span>

> [!TIP]
> <span data-ttu-id="57420-169">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="57420-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="57420-170">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="57420-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="57420-171">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="57420-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="57420-172">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="57420-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="57420-173">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="57420-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="57420-175">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="57420-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="57420-176">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="57420-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mobilexpense-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="57420-178">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="57420-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mobilexpense-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="57420-180">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="57420-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mobilexpense-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="57420-182">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="57420-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mobilexpense-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="57420-184">a.</span><span class="sxs-lookup"><span data-stu-id="57420-184">a.</span></span> <span data-ttu-id="57420-185">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="57420-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="57420-186">b.</span><span class="sxs-lookup"><span data-stu-id="57420-186">b.</span></span> <span data-ttu-id="57420-187">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="57420-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="57420-188">c.</span><span class="sxs-lookup"><span data-stu-id="57420-188">c.</span></span> <span data-ttu-id="57420-189">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="57420-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="57420-190">d.</span><span class="sxs-lookup"><span data-stu-id="57420-190">d.</span></span> <span data-ttu-id="57420-191">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="57420-191">Click **Create**.</span></span>
 
### <a name="creating-a-mobilexpense-test-user"></a><span data-ttu-id="57420-192">Création d’un utilisateur de test MobileXpense</span><span class="sxs-lookup"><span data-stu-id="57420-192">Creating a MobileXpense test user</span></span>

<span data-ttu-id="57420-193">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans MobileXpense.</span><span class="sxs-lookup"><span data-stu-id="57420-193">In this section, you create a user called Britta Simon in MobileXpense.</span></span> <span data-ttu-id="57420-194">Collaborez avec l’[équipe du support technique MobileXpense](http://www.mobilexpense.net/contact) pour ajouter des utilisateurs dans la plateforme MobileXpense.</span><span class="sxs-lookup"><span data-stu-id="57420-194">work with [MobileXpense support team](http://www.mobilexpense.net/contact) to add the users in the MobileXpense platform.</span></span> <span data-ttu-id="57420-195">Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="57420-195">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="57420-196">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="57420-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="57420-197">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en accordant l’accès à MobileXpense.</span><span class="sxs-lookup"><span data-stu-id="57420-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to MobileXpense.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="57420-199">**Pour affecter Britta Simon à MobileXpense, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="57420-199">**To assign Britta Simon to MobileXpense, perform the following steps:**</span></span>

1. <span data-ttu-id="57420-200">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="57420-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="57420-202">Dans la liste des applications, sélectionnez **MobileXpense**.</span><span class="sxs-lookup"><span data-stu-id="57420-202">In the applications list, select **MobileXpense**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_app.png) 

3. <span data-ttu-id="57420-204">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="57420-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="57420-206">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="57420-206">Click **Add** button.</span></span> <span data-ttu-id="57420-207">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="57420-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="57420-209">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="57420-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="57420-210">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="57420-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="57420-211">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="57420-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="57420-212">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="57420-212">Testing single sign-on</span></span>

<span data-ttu-id="57420-213">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="57420-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="57420-214">Quand vous cliquez sur la mosaïque MobileXpense dans le volet d’accès, vous devez être automatiquement connecté à votre application MobileXpense.</span><span class="sxs-lookup"><span data-stu-id="57420-214">When you click the MobileXpense tile in the Access Panel, you should get automatically signed-on to your MobileXpense application.</span></span>
<span data-ttu-id="57420-215">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="57420-215">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="57420-216">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="57420-216">Additional resources</span></span>

* [<span data-ttu-id="57420-217">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="57420-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="57420-218">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="57420-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_203.png

