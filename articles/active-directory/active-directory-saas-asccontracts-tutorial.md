---
title: "Tutoriel : Intégration d’Azure Active Directory à ASC Contracts | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et ASC Contracts."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f7f54202-1581-4e55-a97e-02633ff9382d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/21/2017
ms.author: jeedes
ms.openlocfilehash: 87ea3cc55f9683e7d5b9912a87d675575cea0347
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-asc-contracts"></a><span data-ttu-id="4f82f-103">Tutoriel : Intégration d’Azure Active Directory à ASC Contracts</span><span class="sxs-lookup"><span data-stu-id="4f82f-103">Tutorial: Azure Active Directory integration with ASC Contracts</span></span>

<span data-ttu-id="4f82f-104">Dans ce tutoriel, vous allez apprendre à intégrer Azure Active Directory (Azure AD) à ASC Contracts.</span><span class="sxs-lookup"><span data-stu-id="4f82f-104">In this tutorial, you learn how to integrate ASC Contracts with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4f82f-105">L’intégration de ASC Contracts à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="4f82f-105">Integrating ASC Contracts with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4f82f-106">Dans Azure AD, vous pouvez contrôler qui a accès à ASC Contracts.</span><span class="sxs-lookup"><span data-stu-id="4f82f-106">You can control in Azure AD who has access to ASC Contracts</span></span>
- <span data-ttu-id="4f82f-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à ASC Contracts (par authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4f82f-107">You can enable your users to automatically get signed-on to ASC Contracts (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4f82f-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="4f82f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4f82f-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4f82f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4f82f-110">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="4f82f-110">Prerequisites</span></span>

<span data-ttu-id="4f82f-111">Pour configurer l’intégration d’Azure AD à ASC Contracts, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="4f82f-111">To configure Azure AD integration with ASC Contracts, you need the following items:</span></span>

- <span data-ttu-id="4f82f-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f82f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4f82f-113">Un abonnement ASC Contracts pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="4f82f-113">An ASC Contracts single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4f82f-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="4f82f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4f82f-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="4f82f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4f82f-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="4f82f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4f82f-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4f82f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4f82f-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="4f82f-118">Scenario description</span></span>
<span data-ttu-id="4f82f-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="4f82f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4f82f-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="4f82f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4f82f-121">Ajout de ASC Contracts à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="4f82f-121">Adding ASC Contracts from the gallery</span></span>
2. <span data-ttu-id="4f82f-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f82f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-asc-contracts-from-the-gallery"></a><span data-ttu-id="4f82f-123">Ajout de ASC Contracts à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="4f82f-123">Adding ASC Contracts from the gallery</span></span>
<span data-ttu-id="4f82f-124">Pour configurer l’intégration d’ASC Contracts à Azure AD, vous devez ajouter ASC Contracts, disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="4f82f-124">To configure the integration of ASC Contracts into Azure AD, you need to add ASC Contracts from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4f82f-125">**Pour ajouter ASC Contracts à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4f82f-125">**To add ASC Contracts from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4f82f-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4f82f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4f82f-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="4f82f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4f82f-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="4f82f-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="4f82f-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="4f82f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="4f82f-133">Dans la zone de recherche, tapez **ASC Contracts**.</span><span class="sxs-lookup"><span data-stu-id="4f82f-133">In the search box, type **ASC Contracts**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_search.png)

5. <span data-ttu-id="4f82f-135">Dans le panneau de résultats, sélectionnez **ASC Contracts**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="4f82f-135">In the results panel, select **ASC Contracts**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4f82f-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f82f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4f82f-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec ASC Contracts, en tirant parti d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="4f82f-138">In this section, you configure and test Azure AD single sign-on with ASC Contracts based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4f82f-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur ASC Contracts équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4f82f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ASC Contracts is to a user in Azure AD.</span></span> <span data-ttu-id="4f82f-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur ASC Contracts associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="4f82f-140">In other words, a link relationship between an Azure AD user and the related user in ASC Contracts needs to be established.</span></span>

<span data-ttu-id="4f82f-141">Pour cela, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** dans ASC Contracts.</span><span class="sxs-lookup"><span data-stu-id="4f82f-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ASC Contracts.</span></span>

<span data-ttu-id="4f82f-142">Pour configurer et tester l’authentification unique Azure AD avec ASC Contracts, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="4f82f-142">To configure and test Azure AD single sign-on with ASC Contracts, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4f82f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="4f82f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4f82f-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4f82f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4f82f-145">**[Création d’un utilisateur de test ASC Contracts](#creating-an-asc-contracts-test-user)** pour avoir un équivalent de Britta Simon dans ASC Contracts lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4f82f-145">**[Creating an ASC Contracts test user](#creating-an-asc-contracts-test-user)** - to have a counterpart of Britta Simon in ASC Contracts that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4f82f-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4f82f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4f82f-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="4f82f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4f82f-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f82f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4f82f-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application ASC Contracts.</span><span class="sxs-lookup"><span data-stu-id="4f82f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ASC Contracts application.</span></span>

<span data-ttu-id="4f82f-150">**Pour configurer l’authentification unique Azure AD avec ASC Contracts, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4f82f-150">**To configure Azure AD single sign-on with ASC Contracts, perform the following steps:**</span></span>

1. <span data-ttu-id="4f82f-151">Dans le portail Azure, sur la page d’intégration de l’application **ASC Contracts**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="4f82f-151">In the Azure portal, on the **ASC Contracts** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="4f82f-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="4f82f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_samlbase.png)

3. <span data-ttu-id="4f82f-155">Dans la section **Domaine et URL ASC Contracts**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="4f82f-155">On the **ASC Contracts Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_url.png)

    <span data-ttu-id="4f82f-157">a.</span><span class="sxs-lookup"><span data-stu-id="4f82f-157">a.</span></span> <span data-ttu-id="4f82f-158">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<subdomain>.asccontracts.com/shibboleth`</span><span class="sxs-lookup"><span data-stu-id="4f82f-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.asccontracts.com/shibboleth`</span></span>

    <span data-ttu-id="4f82f-159">b.</span><span class="sxs-lookup"><span data-stu-id="4f82f-159">b.</span></span> <span data-ttu-id="4f82f-160">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://<subdomain>.asccontracts.com/shibboleth.sso/login`</span><span class="sxs-lookup"><span data-stu-id="4f82f-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.asccontracts.com/shibboleth.sso/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4f82f-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="4f82f-161">These values are not real.</span></span> <span data-ttu-id="4f82f-162">Mettez à jour ces valeurs avec l’identificateur et l’URL de réponse réels.</span><span class="sxs-lookup"><span data-stu-id="4f82f-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="4f82f-163">Contactez l’équipe ASC Networks Inc. (ASC) au **613.599.6178** pour obtenir ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="4f82f-163">Contact ASC Networks Inc. (ASC) team at **613.599.6178** to get these values.</span></span>

4. <span data-ttu-id="4f82f-164">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="4f82f-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_certificate.png) 

5. <span data-ttu-id="4f82f-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="4f82f-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-asccontracts-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4f82f-168">Pour configurer l’authentification unique du côté de **ASC Contracts**, appelez ASC Networks Inc. (ASC) au **613.599.6178** et fournissez-leur le fichier **XML de métadonnées** téléchargé.</span><span class="sxs-lookup"><span data-stu-id="4f82f-168">To configure single sign-on on **ASC Contracts** side, call ASC Networks Inc. (ASC) support at **613.599.6178** and provide them with the downloaded **Metadata XML**.</span></span> <span data-ttu-id="4f82f-169">Ils effectuent les réglages nécessaires sur l’application pour que la connexion SSO SAML soit définie correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="4f82f-169">They set this application up to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="4f82f-170">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="4f82f-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4f82f-171">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="4f82f-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4f82f-172">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4f82f-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4f82f-173">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f82f-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="4f82f-174">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="4f82f-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="4f82f-176">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4f82f-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4f82f-177">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4f82f-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4f82f-179">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="4f82f-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4f82f-181">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="4f82f-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4f82f-183">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="4f82f-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4f82f-185">a.</span><span class="sxs-lookup"><span data-stu-id="4f82f-185">a.</span></span> <span data-ttu-id="4f82f-186">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4f82f-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4f82f-187">b.</span><span class="sxs-lookup"><span data-stu-id="4f82f-187">b.</span></span> <span data-ttu-id="4f82f-188">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4f82f-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4f82f-189">c.</span><span class="sxs-lookup"><span data-stu-id="4f82f-189">c.</span></span> <span data-ttu-id="4f82f-190">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="4f82f-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4f82f-191">d.</span><span class="sxs-lookup"><span data-stu-id="4f82f-191">d.</span></span> <span data-ttu-id="4f82f-192">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="4f82f-192">Click **Create**.</span></span>
 
### <a name="creating-an-asc-contracts-test-user"></a><span data-ttu-id="4f82f-193">Création d’un utilisateur de test ASC Contracts</span><span class="sxs-lookup"><span data-stu-id="4f82f-193">Creating an ASC Contracts test user</span></span>

<span data-ttu-id="4f82f-194">Contactez l’équipe de support ASC Networks Inc. (ASC) au **613.599.6178** pour lui demander d’ajouter les utilisateurs dans la plateforme ASC Contracts.</span><span class="sxs-lookup"><span data-stu-id="4f82f-194">Work with ASC Networks Inc. (ASC) support team at **613.599.6178** to get the users added in the ASC Contracts platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4f82f-195">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f82f-195">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4f82f-196">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à ASC Contracts.</span><span class="sxs-lookup"><span data-stu-id="4f82f-196">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ASC Contracts.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="4f82f-198">**Pour affecter Britta Simon à ASC Contracts, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4f82f-198">**To assign Britta Simon to ASC Contracts, perform the following steps:**</span></span>

1. <span data-ttu-id="4f82f-199">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="4f82f-199">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="4f82f-201">Dans la liste des applications, sélectionnez **ASC Contracts**.</span><span class="sxs-lookup"><span data-stu-id="4f82f-201">In the applications list, select **ASC Contracts**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_app.png) 

3. <span data-ttu-id="4f82f-203">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="4f82f-203">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="4f82f-205">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="4f82f-205">Click **Add** button.</span></span> <span data-ttu-id="4f82f-206">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="4f82f-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="4f82f-208">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="4f82f-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4f82f-209">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="4f82f-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4f82f-210">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="4f82f-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4f82f-211">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="4f82f-211">Testing single sign-on</span></span>

<span data-ttu-id="4f82f-212">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="4f82f-212">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4f82f-213">Lorsque vous cliquez sur la vignette ASC Contracts dans le volet d’accès, vous devez être connecté automatiquement à votre application ASC Contracts.</span><span class="sxs-lookup"><span data-stu-id="4f82f-213">When you click the ASC Contracts tile in the Access Panel, you should get automatically signed-on to your ASC Contracts application.</span></span> <span data-ttu-id="4f82f-214">Pour plus d’informations sur le volet d’accès, consultez</span><span class="sxs-lookup"><span data-stu-id="4f82f-214">For more information about the Access Panel, see.</span></span> <span data-ttu-id="4f82f-215">[Présentation du volet d’accès](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="4f82f-215">[Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4f82f-216">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="4f82f-216">Additional resources</span></span>

* [<span data-ttu-id="4f82f-217">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4f82f-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4f82f-218">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="4f82f-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_203.png

