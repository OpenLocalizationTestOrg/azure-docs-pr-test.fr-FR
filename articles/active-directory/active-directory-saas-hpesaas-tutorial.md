---
title: "Didacticiel : Intégration d’Azure Active Directory à HPE SaaS | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et HPE SaaS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 314003d6-ca66-4456-88c3-934254d4a9a2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: jeedes
ms.openlocfilehash: 5e6f0da531df85359aa47477248dd020a039e7e3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hpe-saas"></a><span data-ttu-id="40ebf-103">Didacticiel : Intégration d’Azure Active Directory à HPE SaaS</span><span class="sxs-lookup"><span data-stu-id="40ebf-103">Tutorial: Azure Active Directory integration with HPE SaaS</span></span>

<span data-ttu-id="40ebf-104">Dans ce didacticiel, vous allez apprendre à intégrer HPE SaaS dans Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="40ebf-104">In this tutorial, you learn how to integrate HPE SaaS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="40ebf-105">L’intégration de HPE SaaS dans Azure AD offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="40ebf-105">Integrating HPE SaaS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="40ebf-106">Dans Azure AD, vous pouvez contrôler qui a accès à HPE SaaS.</span><span class="sxs-lookup"><span data-stu-id="40ebf-106">You can control in Azure AD who has access to HPE SaaS</span></span>
- <span data-ttu-id="40ebf-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à HPE SaaS (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="40ebf-107">You can enable your users to automatically get signed-on to HPE SaaS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="40ebf-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="40ebf-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="40ebf-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="40ebf-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="40ebf-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="40ebf-110">Prerequisites</span></span>

<span data-ttu-id="40ebf-111">Pour configurer l’intégration d’Azure AD à HPE SaaS, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="40ebf-111">To configure Azure AD integration with HPE SaaS, you need the following items:</span></span>

- <span data-ttu-id="40ebf-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="40ebf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="40ebf-113">Un abonnement HPE SaaS pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="40ebf-113">An HPE SaaS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="40ebf-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="40ebf-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="40ebf-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="40ebf-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="40ebf-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="40ebf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="40ebf-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois ici : [offre d’essai](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="40ebf-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="40ebf-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="40ebf-118">Scenario description</span></span>
<span data-ttu-id="40ebf-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="40ebf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="40ebf-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="40ebf-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="40ebf-121">Ajout de HPE SaaS à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="40ebf-121">Adding HPE SaaS from the gallery</span></span>
2. <span data-ttu-id="40ebf-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="40ebf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hpe-saas-from-the-gallery"></a><span data-ttu-id="40ebf-123">Ajout de HPE SaaS à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="40ebf-123">Adding HPE SaaS from the gallery</span></span>
<span data-ttu-id="40ebf-124">Pour configurer l’intégration de HPE SaaS à Azure AD, vous devez ajouter HPE SaaS à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="40ebf-124">To configure the integration of HPE SaaS into Azure AD, you need to add HPE SaaS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="40ebf-125">**Pour ajouter HPE SaaS à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="40ebf-125">**To add HPE SaaS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="40ebf-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="40ebf-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="40ebf-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="40ebf-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="40ebf-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="40ebf-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="40ebf-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="40ebf-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="40ebf-133">Dans la zone de recherche, tapez **HPE SaaS**.</span><span class="sxs-lookup"><span data-stu-id="40ebf-133">In the search box, type **HPE SaaS**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_search.png)

5. <span data-ttu-id="40ebf-135">Dans le panneau des résultats, sélectionnez **HPE SaaS**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="40ebf-135">In the results panel, select **HPE SaaS**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="40ebf-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="40ebf-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="40ebf-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec HPE SaaS avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="40ebf-138">In this section, you configure and test Azure AD single sign-on with HPE SaaS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="40ebf-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur HPE SaaS équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="40ebf-139">For single sign-on to work, Azure AD needs to know what the counterpart user in HPE SaaS is to a user in Azure AD.</span></span> <span data-ttu-id="40ebf-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur HPE SaaS associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="40ebf-140">In other words, a link relationship between an Azure AD user and the related user in HPE SaaS needs to be established.</span></span>

<span data-ttu-id="40ebf-141">Dans HPE SaaS, assignez la valeur du **nom d’utilisateur** d’Azure AD comme valeur de **Username** (Nom d’utilisateur) pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="40ebf-141">In HPE SaaS, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="40ebf-142">Pour configurer et tester l’authentification unique Azure AD avec HPE SaaS, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="40ebf-142">To configure and test Azure AD single sign-on with HPE SaaS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="40ebf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="40ebf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="40ebf-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="40ebf-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="40ebf-145">**[Création d’un utilisateur de test HPE SaaS](#creating-an-hpe-saas-test-user)** pour avoir dans HPE SaaS un équivalent de Britta Simon lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="40ebf-145">**[Creating an HPE SaaS test user](#creating-an-hpe-saas-test-user)** - to have a counterpart of Britta Simon in HPE SaaS that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="40ebf-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="40ebf-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="40ebf-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="40ebf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="40ebf-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="40ebf-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="40ebf-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application HPE SaaS.</span><span class="sxs-lookup"><span data-stu-id="40ebf-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your HPE SaaS application.</span></span>

<span data-ttu-id="40ebf-150">**Pour configurer l’authentification unique Azure AD avec HPE SaaS, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="40ebf-150">**To configure Azure AD single sign-on with HPE SaaS, perform the following steps:**</span></span>

1. <span data-ttu-id="40ebf-151">Dans le portail Azure, dans la page d’intégration de l’application **HPE SaaS**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="40ebf-151">In the Azure portal, on the **HPE SaaS** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="40ebf-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="40ebf-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_samlbase.png)

3. <span data-ttu-id="40ebf-155">Dans la section **HPE SaaS Domain and URLs** (Domaine et URL HPE SaaS), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="40ebf-155">On the **HPE SaaS Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_url.png)

    <span data-ttu-id="40ebf-157">a.</span><span class="sxs-lookup"><span data-stu-id="40ebf-157">a.</span></span> <span data-ttu-id="40ebf-158">Dans la zone de texte **URL d’authentification**, tapez l’URL : `https://login.saas.hpe.com/msg`</span><span class="sxs-lookup"><span data-stu-id="40ebf-158">In the **Sign-on URL** textbox, type a URL as: `https://login.saas.hpe.com/msg`</span></span>

    <span data-ttu-id="40ebf-159">b.</span><span class="sxs-lookup"><span data-stu-id="40ebf-159">b.</span></span> <span data-ttu-id="40ebf-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<subdomain>.saas.hpe.com`</span><span class="sxs-lookup"><span data-stu-id="40ebf-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.saas.hpe.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="40ebf-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="40ebf-161">These values are not real.</span></span> <span data-ttu-id="40ebf-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="40ebf-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="40ebf-163">Pour obtenir ces valeurs, contactez l’[équipe de support client HPE SaaS](https://saas.hpe.com/en-us/contact).</span><span class="sxs-lookup"><span data-stu-id="40ebf-163">Contact [HPE SaaS Client support team](https://saas.hpe.com/en-us/contact) to get these values.</span></span> 
 
4. <span data-ttu-id="40ebf-164">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="40ebf-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_certificate.png) 

5. <span data-ttu-id="40ebf-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="40ebf-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hpesaas-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="40ebf-168">Pour configurer l’authentification unique du côté **HPE SaaS**, vous devez envoyer le **XML des métadonnées** téléchargé à [l’équipe de support HPE SaaS](https://saas.hpe.com/en-us/contact).</span><span class="sxs-lookup"><span data-stu-id="40ebf-168">To configure single sign-on on **HPE SaaS** side, you need to send the downloaded **Metadata XML** to [HPE SaaS support team](https://saas.hpe.com/en-us/contact).</span></span> <span data-ttu-id="40ebf-169">Celles-ci configurent ensuite ce paramètre pour que la connexion SSO SAML soit définie correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="40ebf-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="40ebf-170">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="40ebf-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="40ebf-171">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="40ebf-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="40ebf-172">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="40ebf-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="40ebf-173">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="40ebf-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="40ebf-174">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="40ebf-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="40ebf-176">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="40ebf-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="40ebf-177">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="40ebf-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hpesaas-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="40ebf-179">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="40ebf-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hpesaas-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="40ebf-181">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="40ebf-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hpesaas-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="40ebf-183">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="40ebf-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hpesaas-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="40ebf-185">a.</span><span class="sxs-lookup"><span data-stu-id="40ebf-185">a.</span></span> <span data-ttu-id="40ebf-186">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="40ebf-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="40ebf-187">b.</span><span class="sxs-lookup"><span data-stu-id="40ebf-187">b.</span></span> <span data-ttu-id="40ebf-188">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="40ebf-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="40ebf-189">c.</span><span class="sxs-lookup"><span data-stu-id="40ebf-189">c.</span></span> <span data-ttu-id="40ebf-190">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="40ebf-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="40ebf-191">d.</span><span class="sxs-lookup"><span data-stu-id="40ebf-191">d.</span></span> <span data-ttu-id="40ebf-192">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="40ebf-192">Click **Create**.</span></span>
 
### <a name="creating-an-hpe-saas-test-user"></a><span data-ttu-id="40ebf-193">Création d’un utilisateur de test HPE SaaS</span><span class="sxs-lookup"><span data-stu-id="40ebf-193">Creating an HPE SaaS test user</span></span>

<span data-ttu-id="40ebf-194">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans HPE SaaS.</span><span class="sxs-lookup"><span data-stu-id="40ebf-194">The objective of this section is to create a user called Britta Simon in HPE SaaS.</span></span> <span data-ttu-id="40ebf-195">Pour ajouter des utilisateurs au compte HPE SaaS, contactez l’[équipe de support HPE SaaS](https://saas.hpe.com/en-us/contact).</span><span class="sxs-lookup"><span data-stu-id="40ebf-195">Please work with [HPE SaaS support team](https://saas.hpe.com/en-us/contact) to add the users in the HPE SaaS account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="40ebf-196">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="40ebf-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="40ebf-197">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à HPE SaaS.</span><span class="sxs-lookup"><span data-stu-id="40ebf-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to HPE SaaS.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="40ebf-199">**Pour affecter Britta Simon à HPE SaaS, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="40ebf-199">**To assign Britta Simon to HPE SaaS, perform the following steps:**</span></span>

1. <span data-ttu-id="40ebf-200">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="40ebf-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="40ebf-202">Dans la liste des applications, sélectionnez **HPE SaaS**.</span><span class="sxs-lookup"><span data-stu-id="40ebf-202">In the applications list, select **HPE SaaS**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_app.png) 

3. <span data-ttu-id="40ebf-204">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="40ebf-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="40ebf-206">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="40ebf-206">Click **Add** button.</span></span> <span data-ttu-id="40ebf-207">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="40ebf-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="40ebf-209">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="40ebf-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="40ebf-210">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="40ebf-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="40ebf-211">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="40ebf-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="40ebf-212">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="40ebf-212">Testing single sign-on</span></span>

<span data-ttu-id="40ebf-213">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="40ebf-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="40ebf-214">Quand vous cliquez sur la vignette HPE SaaS dans le volet d’accès, vous devez être connecté automatiquement à votre application HPE SaaS.</span><span class="sxs-lookup"><span data-stu-id="40ebf-214">When you click the HPE SaaS tile in the Access Panel, you should get automatically signed-on to your HPE SaaS application.</span></span>
<span data-ttu-id="40ebf-215">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="40ebf-215">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="40ebf-216">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="40ebf-216">Additional resources</span></span>

* [<span data-ttu-id="40ebf-217">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="40ebf-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="40ebf-218">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="40ebf-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_203.png

