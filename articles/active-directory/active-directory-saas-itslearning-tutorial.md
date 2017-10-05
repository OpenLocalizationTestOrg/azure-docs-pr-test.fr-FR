---
title: "Didacticiel : Intégration d’Azure Active Directory à itslearning | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et itslearning."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 60587ba3-1396-4b8a-9ac1-e22a98e5e0ac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 32c8a8dff533f726784fb52b9496c2cb50ecfde7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-itslearning"></a><span data-ttu-id="e59f5-103">Didacticiel : Intégration d’Azure Active Directory à itslearning</span><span class="sxs-lookup"><span data-stu-id="e59f5-103">Tutorial: Azure Active Directory integration with itslearning</span></span>

<span data-ttu-id="e59f5-104">Dans ce didacticiel, vous allez apprendre à intégrer itslearning à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e59f5-104">In this tutorial, you learn how to integrate itslearning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e59f5-105">L’intégration d’itslearning à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="e59f5-105">Integrating itslearning with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e59f5-106">Dans Azure AD, vous pouvez contrôler qui a accès à itslearning.</span><span class="sxs-lookup"><span data-stu-id="e59f5-106">You can control in Azure AD who has access to itslearning</span></span>
- <span data-ttu-id="e59f5-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à itslearning (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e59f5-107">You can enable your users to automatically get signed-on to itslearning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e59f5-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="e59f5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e59f5-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e59f5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e59f5-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e59f5-110">Prerequisites</span></span>

<span data-ttu-id="e59f5-111">Pour configurer l’intégration d’Azure AD à itslearning, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="e59f5-111">To configure Azure AD integration with itslearning, you need the following items:</span></span>

- <span data-ttu-id="e59f5-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="e59f5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e59f5-113">Un abonnement itslearning pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="e59f5-113">An itslearning single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e59f5-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="e59f5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e59f5-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="e59f5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e59f5-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e59f5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e59f5-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e59f5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e59f5-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="e59f5-118">Scenario description</span></span>
<span data-ttu-id="e59f5-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="e59f5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e59f5-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="e59f5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e59f5-121">Ajout d’itslearning à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="e59f5-121">Adding itslearning from the gallery</span></span>
2. <span data-ttu-id="e59f5-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e59f5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-itslearning-from-the-gallery"></a><span data-ttu-id="e59f5-123">Ajout d’itslearning à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="e59f5-123">Adding itslearning from the gallery</span></span>
<span data-ttu-id="e59f5-124">Pour configurer l’intégration d’itslearning à Azure AD, vous devez ajouter itslearning à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="e59f5-124">To configure the integration of itslearning into Azure AD, you need to add itslearning from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e59f5-125">**Pour ajouter itslearning à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e59f5-125">**To add itslearning from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e59f5-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e59f5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e59f5-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="e59f5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e59f5-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="e59f5-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="e59f5-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="e59f5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="e59f5-133">Dans la zone de recherche, tapez **itslearning**.</span><span class="sxs-lookup"><span data-stu-id="e59f5-133">In the search box, type **itslearning**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_search.png)

5. <span data-ttu-id="e59f5-135">Dans le panneau de résultats, sélectionnez **itslearning**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="e59f5-135">In the results panel, select **itslearning**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e59f5-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e59f5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e59f5-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec itslearning avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="e59f5-138">In this section, you configure and test Azure AD single sign-on with itslearning based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e59f5-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur itslearning équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e59f5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in itslearning is to a user in Azure AD.</span></span> <span data-ttu-id="e59f5-140">En d’autres termes, une relation entre un utilisateur Azure AD et l’utilisateur itslearning associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="e59f5-140">In other words, a link relationship between an Azure AD user and the related user in itslearning needs to be established.</span></span>

<span data-ttu-id="e59f5-141">Dans itslearning, attribuez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="e59f5-141">In itslearning, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e59f5-142">Pour configurer et tester l’authentification unique Azure AD avec itslearning, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="e59f5-142">To configure and test Azure AD single sign-on with itslearning, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e59f5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="e59f5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e59f5-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e59f5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e59f5-145">**[Création d’un utilisateur de test itslearning](#creating-an-itslearning-test-user)** pour avoir un équivalent de Britta Simon dans itslearning lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e59f5-145">**[Creating an itslearning test user](#creating-an-itslearning-test-user)** - to have a counterpart of Britta Simon in itslearning that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e59f5-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e59f5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e59f5-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="e59f5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e59f5-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e59f5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e59f5-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application itslearning.</span><span class="sxs-lookup"><span data-stu-id="e59f5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your itslearning application.</span></span>

<span data-ttu-id="e59f5-150">**Pour configurer l’authentification unique Azure AD avec itslearning, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e59f5-150">**To configure Azure AD single sign-on with itslearning, perform the following steps:**</span></span>

1. <span data-ttu-id="e59f5-151">Dans le portail Azure, sur la page d’intégration de l’application **itslearning**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="e59f5-151">In the Azure portal, on the **itslearning** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="e59f5-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="e59f5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_samlbase.png)

3. <span data-ttu-id="e59f5-155">Dans la section **itslearning Domain and URLs** (Domaine et URL itslearning), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="e59f5-155">On the **itslearning Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_url.png)

    <span data-ttu-id="e59f5-157">a.</span><span class="sxs-lookup"><span data-stu-id="e59f5-157">a.</span></span> <span data-ttu-id="e59f5-158">Dans la zone de texte **URL d’authentification**, tapez une URL comme :</span><span class="sxs-lookup"><span data-stu-id="e59f5-158">In the **Sign-on URL** textbox, type a URL as:</span></span>
    | |
    |--| 
    | `https://www.itslearning.com/index.aspx`|
    | `https://us1.itslearning.com/index.aspx`|

    <span data-ttu-id="e59f5-159">b.</span><span class="sxs-lookup"><span data-stu-id="e59f5-159">b.</span></span> <span data-ttu-id="e59f5-160">Dans la zone de texte **Identificateur**, tapez une URL comme : `urn:mace:saml2v2.no:services:com.itslearning`</span><span class="sxs-lookup"><span data-stu-id="e59f5-160">In the **Identifier** textbox, type a URL as: `urn:mace:saml2v2.no:services:com.itslearning`</span></span>

4. <span data-ttu-id="e59f5-161">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="e59f5-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_certificate.png) 

5. <span data-ttu-id="e59f5-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="e59f5-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-itslearning-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e59f5-165">Pour configurer l’authentification unique du côté **itslearning**, vous devez envoyer le fichier **XML de métadonnées** téléchargé à [l’équipe de support technique itslearning](mailto:support@itslearning.com).</span><span class="sxs-lookup"><span data-stu-id="e59f5-165">To configure single sign-on on **itslearning** side, you need to send the downloaded **Metadata XML** to [itslearning support team](mailto:support@itslearning.com).</span></span> <span data-ttu-id="e59f5-166">Elle configure ce paramètre pour que la connexion SSO SAML soit définie correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="e59f5-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="e59f5-167">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="e59f5-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e59f5-168">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="e59f5-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e59f5-169">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e59f5-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e59f5-170">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="e59f5-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="e59f5-171">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e59f5-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="e59f5-173">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e59f5-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e59f5-174">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e59f5-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-itslearning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e59f5-176">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="e59f5-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-itslearning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e59f5-178">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="e59f5-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-itslearning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e59f5-180">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="e59f5-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-itslearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e59f5-182">a.</span><span class="sxs-lookup"><span data-stu-id="e59f5-182">a.</span></span> <span data-ttu-id="e59f5-183">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e59f5-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e59f5-184">b.</span><span class="sxs-lookup"><span data-stu-id="e59f5-184">b.</span></span> <span data-ttu-id="e59f5-185">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e59f5-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e59f5-186">c.</span><span class="sxs-lookup"><span data-stu-id="e59f5-186">c.</span></span> <span data-ttu-id="e59f5-187">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="e59f5-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e59f5-188">d.</span><span class="sxs-lookup"><span data-stu-id="e59f5-188">d.</span></span> <span data-ttu-id="e59f5-189">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="e59f5-189">Click **Create**.</span></span>
 
### <a name="creating-an-itslearning-test-user"></a><span data-ttu-id="e59f5-190">Création d’un utilisateur de test itslearning</span><span class="sxs-lookup"><span data-stu-id="e59f5-190">Creating an itslearning test user</span></span>

<span data-ttu-id="e59f5-191">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans itslearning.</span><span class="sxs-lookup"><span data-stu-id="e59f5-191">In this section, you create a user called Britta Simon in itslearning.</span></span> <span data-ttu-id="e59f5-192">Travaillez avec [l’équipe de support technique itslearning](mailto:support@itslearning.com) pour ajouter les utilisateurs à la plateforme itslearning.</span><span class="sxs-lookup"><span data-stu-id="e59f5-192">Work with [itslearning Client support team](mailto:support@itslearning.com) to add the users in the itslearning platform.</span></span> <span data-ttu-id="e59f5-193">Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="e59f5-193">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e59f5-194">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="e59f5-194">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e59f5-195">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à itslearning.</span><span class="sxs-lookup"><span data-stu-id="e59f5-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to itslearning.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="e59f5-197">**Pour affecter Britta Simon à itslearning, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e59f5-197">**To assign Britta Simon to itslearning, perform the following steps:**</span></span>

1. <span data-ttu-id="e59f5-198">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="e59f5-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="e59f5-200">Dans la liste des applications, sélectionnez **itslearning**.</span><span class="sxs-lookup"><span data-stu-id="e59f5-200">In the applications list, select **itslearning**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_app.png) 

3. <span data-ttu-id="e59f5-202">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="e59f5-202">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="e59f5-204">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="e59f5-204">Click **Add** button.</span></span> <span data-ttu-id="e59f5-205">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="e59f5-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="e59f5-207">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="e59f5-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e59f5-208">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="e59f5-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e59f5-209">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="e59f5-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e59f5-210">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="e59f5-210">Testing single sign-on</span></span>

<span data-ttu-id="e59f5-211">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="e59f5-211">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e59f5-212">Lorsque vous cliquez sur la vignette itslearning dans le panneau d’accès, la page de connexion de l’application itslearning doit apparaître.</span><span class="sxs-lookup"><span data-stu-id="e59f5-212">When you click the itslearning tile in the Access Panel, you should get login page of itslearning application.</span></span> <span data-ttu-id="e59f5-213">Cliquez sur **Log in with Windows Azure ACS1** (Se connecter avec Windows Azure ACS1) pour vous connecter à l’application.</span><span class="sxs-lookup"><span data-stu-id="e59f5-213">Click **Log in with Windows Azure ACS1** for successful login into the application.</span></span>

  ![Connexion](./media/active-directory-saas-itslearning-tutorial/login.png)

<span data-ttu-id="e59f5-215">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e59f5-215">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e59f5-216">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="e59f5-216">Additional resources</span></span>

* [<span data-ttu-id="e59f5-217">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e59f5-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e59f5-218">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="e59f5-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_203.png

