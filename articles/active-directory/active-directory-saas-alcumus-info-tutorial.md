---
title: "Didacticiel : Intégration d’Azure Active Directory à Alcumus Info Exchange | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Alcumus Info Exchange."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d26034b8-f0d5-4f65-aa56-0fc168ceec8c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jeedes
ms.openlocfilehash: 1f67682111de0bea1b18fd97d739492661ebbfd9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-alcumus-info-exchange"></a><span data-ttu-id="2f32d-103">Didacticiel : Intégration d’Azure Active Directory avec Alcumus Info Exchange</span><span class="sxs-lookup"><span data-stu-id="2f32d-103">Tutorial: Azure Active Directory integration with Alcumus Info Exchange</span></span>

<span data-ttu-id="2f32d-104">Dans ce didacticiel, vous allez apprendre à intégrer Alcumus Info Exchange à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2f32d-104">In this tutorial, you learn how to integrate Alcumus Info Exchange with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2f32d-105">L’intégration d’Alcumus Info Exchange dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="2f32d-105">Integrating Alcumus Info Exchange with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2f32d-106">Dans Azure AD, vous pouvez contrôler qui a accès à Alcumus Info Exchange.</span><span class="sxs-lookup"><span data-stu-id="2f32d-106">You can control in Azure AD who has access to Alcumus Info Exchange</span></span>
- <span data-ttu-id="2f32d-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Alcumus Info Exchange (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f32d-107">You can enable your users to automatically get signed-on to Alcumus Info Exchange (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2f32d-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="2f32d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2f32d-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2f32d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f32d-110">Prérequis</span><span class="sxs-lookup"><span data-stu-id="2f32d-110">Prerequisites</span></span>

<span data-ttu-id="2f32d-111">Pour configurer l’intégration d’Azure AD avec Alcumus Info Exchange, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="2f32d-111">To configure Azure AD integration with Alcumus Info Exchange, you need the following items:</span></span>

- <span data-ttu-id="2f32d-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f32d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2f32d-113">Un abonnement Alcumus Info Exchange pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="2f32d-113">An Alcumus Info Exchange single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2f32d-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="2f32d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2f32d-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="2f32d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2f32d-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="2f32d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2f32d-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2f32d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2f32d-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="2f32d-118">Scenario description</span></span>
<span data-ttu-id="2f32d-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="2f32d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2f32d-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="2f32d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2f32d-121">Ajout d’Alcumus info Exchange à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="2f32d-121">Adding Alcumus Info Exchange from the gallery</span></span>
2. <span data-ttu-id="2f32d-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f32d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-alcumus-info-exchange-from-the-gallery"></a><span data-ttu-id="2f32d-123">Ajout d’Alcumus info Exchange à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="2f32d-123">Adding Alcumus Info Exchange from the gallery</span></span>
<span data-ttu-id="2f32d-124">Pour configurer l’intégration d’Alcumus Info Exchange dans Azure AD, vous devez ajouter Alcumus Info Exchange, disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="2f32d-124">To configure the integration of Alcumus Info Exchange into Azure AD, you need to add Alcumus Info Exchange from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2f32d-125">**Pour ajouter Alcumus Info Exchange à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2f32d-125">**To add Alcumus Info Exchange from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2f32d-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2f32d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2f32d-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="2f32d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2f32d-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="2f32d-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="2f32d-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="2f32d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="2f32d-133">Dans la zone de recherche, tapez **Alcumus Info Exchange**.</span><span class="sxs-lookup"><span data-stu-id="2f32d-133">In the search box, type **Alcumus Info Exchange**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumusinfoexchange_search.png)

5. <span data-ttu-id="2f32d-135">Dans le volet des résultats, sélectionnez **Alcumus Info Exchange**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="2f32d-135">In the results panel, select **Alcumus Info Exchange**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumusinfoexchange_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2f32d-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f32d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2f32d-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Alcumus Info Exchange avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="2f32d-138">In this section, you configure and test Azure AD single sign-on with Alcumus Info Exchange based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2f32d-139">Pour que l’authentification unique fonctionne, Azure AD doit connaître l’utilisateur Alcumus Info Exchange correspondant à l’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f32d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Alcumus Info Exchange is to a user in Azure AD.</span></span> <span data-ttu-id="2f32d-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Alcumus Info Exchange associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="2f32d-140">In other words, a link relationship between an Azure AD user and the related user in Alcumus Info Exchange needs to be established.</span></span>

<span data-ttu-id="2f32d-141">Dans Alcumus Info Exchange, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="2f32d-141">In Alcumus Info Exchange, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="2f32d-142">Pour configurer et tester l’authentification unique Azure AD avec Alcumus Info Exchange, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="2f32d-142">To configure and test Azure AD single sign-on with Alcumus Info Exchange, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2f32d-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="2f32d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2f32d-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2f32d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2f32d-145">**[Création d’un utilisateur de test Alcumus Info Exchange](#creating-an-alcumus-info-exchange-test-user)** pour avoir un équivalent de Britta Simon dans Alcumus Info Exchange lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2f32d-145">**[Creating an Alcumus Info Exchange test user](#creating-an-alcumus-info-exchange-test-user)** - to have a counterpart of Britta Simon in Alcumus Info Exchange that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2f32d-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f32d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2f32d-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="2f32d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2f32d-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f32d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2f32d-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Alcumus Info Exchange.</span><span class="sxs-lookup"><span data-stu-id="2f32d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Alcumus Info Exchange application.</span></span>

<span data-ttu-id="2f32d-150">**Pour configurer l’authentification unique Azure AD avec Alcumus Info Exchange, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2f32d-150">**To configure Azure AD single sign-on with Alcumus Info Exchange, perform the following steps:**</span></span>

1. <span data-ttu-id="2f32d-151">Dans le portail Azure, dans la page d’intégration de l’application **Alcumus Info Exchange**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="2f32d-151">In the Azure portal, on the **Alcumus Info Exchange** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="2f32d-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="2f32d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumusinfoexchange_samlbase.png)

3. <span data-ttu-id="2f32d-155">Dans la section **Domaine et URL Alcumus Info Exchange**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="2f32d-155">On the **Alcumus Info Exchange Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumusinfoexchange_url.png)

    <span data-ttu-id="2f32d-157">a.</span><span class="sxs-lookup"><span data-stu-id="2f32d-157">a.</span></span> <span data-ttu-id="2f32d-158">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<subdomain>.info-exchange.com`</span><span class="sxs-lookup"><span data-stu-id="2f32d-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.info-exchange.com`</span></span>

    <span data-ttu-id="2f32d-159">b.</span><span class="sxs-lookup"><span data-stu-id="2f32d-159">b.</span></span> <span data-ttu-id="2f32d-160">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://<subdomain>.info-exchange.com/Auth/`</span><span class="sxs-lookup"><span data-stu-id="2f32d-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.info-exchange.com/Auth/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2f32d-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="2f32d-161">These values are not real.</span></span> <span data-ttu-id="2f32d-162">Mettez à jour ces valeurs avec l’identificateur et l’URL de réponse réels.</span><span class="sxs-lookup"><span data-stu-id="2f32d-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="2f32d-163">Pour obtenir ces valeurs, contactez [l’équipe du support Alcumus Info Exchange](mailto:helpdesk@alcumusgroup.com).</span><span class="sxs-lookup"><span data-stu-id="2f32d-163">Contact [Alcumus Info Exchange support team](mailto:helpdesk@alcumusgroup.com) to get these values.</span></span>
 
4. <span data-ttu-id="2f32d-164">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="2f32d-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumusinfoexchange_certificate.png) 

5. <span data-ttu-id="2f32d-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="2f32d-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2f32d-168">Pour configurer l’authentification unique côté **Alcumus Info Exchange**, vous devez envoyer le fichier **XML de métadonnées** téléchargé à [l’équipe du support Alcumus Info Exchange](mailto:helpdesk@alcumusgroup.com).</span><span class="sxs-lookup"><span data-stu-id="2f32d-168">To configure single sign-on on **Alcumus Info Exchange** side, you need to send the downloaded **Metadata XML** to [Alcumus Info Exchange support team](mailto:helpdesk@alcumusgroup.com).</span></span>

> [!TIP]
> <span data-ttu-id="2f32d-169">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="2f32d-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2f32d-170">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="2f32d-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2f32d-171">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2f32d-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2f32d-172">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f32d-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="2f32d-173">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2f32d-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="2f32d-175">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2f32d-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2f32d-176">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2f32d-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-alcumus-info-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2f32d-178">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="2f32d-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-alcumus-info-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2f32d-180">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="2f32d-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-alcumus-info-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2f32d-182">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="2f32d-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-alcumus-info-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2f32d-184">a.</span><span class="sxs-lookup"><span data-stu-id="2f32d-184">a.</span></span> <span data-ttu-id="2f32d-185">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2f32d-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2f32d-186">b.</span><span class="sxs-lookup"><span data-stu-id="2f32d-186">b.</span></span> <span data-ttu-id="2f32d-187">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2f32d-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2f32d-188">c.</span><span class="sxs-lookup"><span data-stu-id="2f32d-188">c.</span></span> <span data-ttu-id="2f32d-189">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="2f32d-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2f32d-190">d.</span><span class="sxs-lookup"><span data-stu-id="2f32d-190">d.</span></span> <span data-ttu-id="2f32d-191">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="2f32d-191">Click **Create**.</span></span>
 
### <a name="creating-an-alcumus-info-exchange-test-user"></a><span data-ttu-id="2f32d-192">Création d’un utilisateur de test Alcumus Info Exchange</span><span class="sxs-lookup"><span data-stu-id="2f32d-192">Creating an Alcumus Info Exchange test user</span></span>

<span data-ttu-id="2f32d-193">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans Alcumus Info Exchange.</span><span class="sxs-lookup"><span data-stu-id="2f32d-193">The objective of this section is to create a user called Britta Simon in Alcumus Info Exchange.</span></span>

<span data-ttu-id="2f32d-194">Pour créer un utilisateur appelé Britta Simon dans Alcumus Info Exchange, contactez [l’équipe du support Alcumus informations Exchange](mailto:helpdesk@alcumusgroup.com).</span><span class="sxs-lookup"><span data-stu-id="2f32d-194">To create a user called Britta Simon in Alcumus Info Exchange, Contact the [Alcumus Info Exchange support team](mailto:helpdesk@alcumusgroup.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2f32d-195">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f32d-195">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2f32d-196">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Alcumus Info Exchange.</span><span class="sxs-lookup"><span data-stu-id="2f32d-196">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Alcumus Info Exchange.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="2f32d-198">**Pour attribuer Britta Simon à Alcumus Info Exchange, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2f32d-198">**To assign Britta Simon to Alcumus Info Exchange, perform the following steps:**</span></span>

1. <span data-ttu-id="2f32d-199">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="2f32d-199">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="2f32d-201">Dans la liste des applications, sélectionnez **Alcumus Info Exchange**.</span><span class="sxs-lookup"><span data-stu-id="2f32d-201">In the applications list, select **Alcumus Info Exchange**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumusinfoexchange_app.png) 

3. <span data-ttu-id="2f32d-203">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="2f32d-203">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="2f32d-205">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="2f32d-205">Click **Add** button.</span></span> <span data-ttu-id="2f32d-206">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="2f32d-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="2f32d-208">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="2f32d-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2f32d-209">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="2f32d-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2f32d-210">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="2f32d-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2f32d-211">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="2f32d-211">Testing single sign-on</span></span>

<span data-ttu-id="2f32d-212">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="2f32d-212">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="2f32d-213">Lorsque vous cliquez sur la vignette Alcumus Info Exchange dans le volet d’accès, vous devez vous connecter automatiquement à votre application Alcumus Info Exchange.</span><span class="sxs-lookup"><span data-stu-id="2f32d-213">When you click the Alcumus Info Exchange tile in the Access Panel, you should get automatically signed-on to your Alcumus Info Exchange application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2f32d-214">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="2f32d-214">Additional resources</span></span>

* [<span data-ttu-id="2f32d-215">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2f32d-215">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2f32d-216">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="2f32d-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_203.png

