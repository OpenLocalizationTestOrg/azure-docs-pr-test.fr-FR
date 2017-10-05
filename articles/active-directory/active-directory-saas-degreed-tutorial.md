---
title: "Didacticiel : Intégration d’Azure Active Directory à Degreed | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Degreed."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1eda2d1c-b5e2-4c53-ad46-bbeb91cd119a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: ea96edb25e2d7199981ff126bf4b2a3d93c6840a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-degreed"></a><span data-ttu-id="1567a-103">Didacticiel : Intégration d’Azure AD à Degreed</span><span class="sxs-lookup"><span data-stu-id="1567a-103">Tutorial: Azure Active Directory integration with Degreed</span></span>

<span data-ttu-id="1567a-104">Dans ce didacticiel, vous allez apprendre à intégrer Degreed à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1567a-104">In this tutorial, you learn how to integrate Degreed with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1567a-105">L’intégration de Degreed à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="1567a-105">Integrating Degreed with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1567a-106">Dans Azure AD, vous pouvez contrôler qui a accès à Degreed.</span><span class="sxs-lookup"><span data-stu-id="1567a-106">You can control in Azure AD who has access to Degreed</span></span>
- <span data-ttu-id="1567a-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Degreed (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1567a-107">You can enable your users to automatically get signed-on to Degreed (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1567a-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="1567a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1567a-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1567a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1567a-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1567a-110">Prerequisites</span></span>

<span data-ttu-id="1567a-111">Pour configurer l’intégration d’Azure AD à Degreed, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="1567a-111">To configure Azure AD integration with Degreed, you need the following items:</span></span>

- <span data-ttu-id="1567a-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="1567a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1567a-113">Un abonnement Degreed pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="1567a-113">A Degreed single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1567a-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="1567a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1567a-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1567a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1567a-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="1567a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1567a-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1567a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1567a-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="1567a-118">Scenario description</span></span>
<span data-ttu-id="1567a-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="1567a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1567a-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="1567a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1567a-121">Ajout de Degreed à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="1567a-121">Adding Degreed from the gallery</span></span>
2. <span data-ttu-id="1567a-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1567a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-degreed-from-the-gallery"></a><span data-ttu-id="1567a-123">Ajout de Degreed à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="1567a-123">Adding Degreed from the gallery</span></span>
<span data-ttu-id="1567a-124">Pour configurer l’intégration de Degreed à Azure AD, vous devez ajouter Degreed à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="1567a-124">To configure the integration of Degreed into Azure AD, you need to add Degreed from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1567a-125">**Pour ajouter Degreed à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1567a-125">**To add Degreed from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1567a-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1567a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1567a-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="1567a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1567a-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1567a-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="1567a-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1567a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="1567a-133">Dans la zone de recherche, tapez **Degreed**.</span><span class="sxs-lookup"><span data-stu-id="1567a-133">In the search box, type **Degreed**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-degreed-tutorial/tutorial_degreed_search.png)

5. <span data-ttu-id="1567a-135">Dans le volet de résultats, sélectionnez **Degreed**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="1567a-135">In the results panel, select **Degreed**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-degreed-tutorial/tutorial_degreed_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1567a-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1567a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1567a-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Degreed, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="1567a-138">In this section, you configure and test Azure AD single sign-on with Degreed based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1567a-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Degreed correspondant dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1567a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Degreed is to a user in Azure AD.</span></span> <span data-ttu-id="1567a-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Degreed associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="1567a-140">In other words, a link relationship between an Azure AD user and the related user in Degreed needs to be established.</span></span>

<span data-ttu-id="1567a-141">Dans Degreed, assignez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="1567a-141">In Degreed, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1567a-142">Pour configurer et tester l’authentification unique Azure AD avec Degreed, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="1567a-142">To configure and test Azure AD single sign-on with Degreed, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1567a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="1567a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1567a-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1567a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1567a-145">**[Création d’un utilisateur de test Degreed](#creating-a-degreed-test-user)** pour avoir un équivalent de Britta Simon dans Degreed, lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="1567a-145">**[Creating a Degreed test user](#creating-a-degreed-test-user)** - to have a counterpart of Britta Simon in Degreed that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1567a-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1567a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1567a-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="1567a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1567a-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1567a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1567a-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Degreed.</span><span class="sxs-lookup"><span data-stu-id="1567a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Degreed application.</span></span>

<span data-ttu-id="1567a-150">**Pour configurer l'authentification unique Azure AD avec Degreed, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1567a-150">**To configure Azure AD single sign-on with Degreed, perform the following steps:**</span></span>

1. <span data-ttu-id="1567a-151">Dans le portail Azure, sur la page d’intégration de l’application **Degreed**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="1567a-151">In the Azure portal, on the **Degreed** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="1567a-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="1567a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-degreed-tutorial/tutorial_degreed_samlbase.png)

3. <span data-ttu-id="1567a-155">Dans la section **Domaine et URL Degreed**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1567a-155">On the **Degreed Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-degreed-tutorial/tutorial_degreed_url.png)

    <span data-ttu-id="1567a-157">a.</span><span class="sxs-lookup"><span data-stu-id="1567a-157">a.</span></span> <span data-ttu-id="1567a-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://degreed.com/?orgsso=<company code>`</span><span class="sxs-lookup"><span data-stu-id="1567a-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://degreed.com/?orgsso=<company code>`</span></span>

    <span data-ttu-id="1567a-159">b.</span><span class="sxs-lookup"><span data-stu-id="1567a-159">b.</span></span> <span data-ttu-id="1567a-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://degreed.com/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="1567a-160">In the **Identifier** textbox, type a URL using the following pattern: `https://degreed.com/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1567a-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="1567a-161">These values are not real.</span></span> <span data-ttu-id="1567a-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="1567a-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1567a-163">Pour obtenir ces valeurs, contactez l’[équipe de support technique de Degreed](mailTo:admin@degreed.com).</span><span class="sxs-lookup"><span data-stu-id="1567a-163">Contact [Degreed Client support team](mailTo:admin@degreed.com) to get these values.</span></span> 
 


4. <span data-ttu-id="1567a-164">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="1567a-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-degreed-tutorial/tutorial_degreed_certificate.png) 

5. <span data-ttu-id="1567a-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="1567a-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-degreed-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1567a-168">Pour configurer l’authentification unique côté **Degreed**, vous devez envoyer le fichier **XML de métadonnées** téléchargé à [l’équipe de support technique de Degreed](mailTo:admin@degreed.com).</span><span class="sxs-lookup"><span data-stu-id="1567a-168">To configure single sign-on on **Degreed** side, you need to send the downloaded **Metadata XML** to [Degreed support team](mailTo:admin@degreed.com).</span></span> <span data-ttu-id="1567a-169">Celle-ci configure ensuite ce paramètre pour que la connexion SSO SAML soit définie correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="1567a-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="1567a-170">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="1567a-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1567a-171">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="1567a-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1567a-172">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1567a-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1567a-173">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="1567a-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="1567a-174">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1567a-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="1567a-176">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1567a-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1567a-177">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1567a-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-degreed-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1567a-179">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="1567a-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-degreed-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1567a-181">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1567a-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-degreed-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1567a-183">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1567a-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-degreed-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1567a-185">a.</span><span class="sxs-lookup"><span data-stu-id="1567a-185">a.</span></span> <span data-ttu-id="1567a-186">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1567a-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1567a-187">b.</span><span class="sxs-lookup"><span data-stu-id="1567a-187">b.</span></span> <span data-ttu-id="1567a-188">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1567a-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1567a-189">c.</span><span class="sxs-lookup"><span data-stu-id="1567a-189">c.</span></span> <span data-ttu-id="1567a-190">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="1567a-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1567a-191">d.</span><span class="sxs-lookup"><span data-stu-id="1567a-191">d.</span></span> <span data-ttu-id="1567a-192">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="1567a-192">Click **Create**.</span></span>
 
### <a name="creating-a-degreed-test-user"></a><span data-ttu-id="1567a-193">Création d’un utilisateur de test Degreed</span><span class="sxs-lookup"><span data-stu-id="1567a-193">Creating a Degreed test user</span></span>

<span data-ttu-id="1567a-194">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans Degreed.</span><span class="sxs-lookup"><span data-stu-id="1567a-194">The objective of this section is to create a user called Britta Simon in Degreed.</span></span> <span data-ttu-id="1567a-195">Degreed prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="1567a-195">Degreed supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="1567a-196">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="1567a-196">There is no action item for you in this section.</span></span> <span data-ttu-id="1567a-197">Un utilisateur est créé lors d’une tentative d’accès à Degreed s’il n’existe pas déjà.</span><span class="sxs-lookup"><span data-stu-id="1567a-197">A new user is created during an attempt to access Degreed if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="1567a-198">Si vous devez créer un utilisateur manuellement, contactez [l’équipe du support technique de Degreed](mailTo:admin@degreed.com).</span><span class="sxs-lookup"><span data-stu-id="1567a-198">If you need to create a user manually, you need to contact the [Degreed support team](mailTo:admin@degreed.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1567a-199">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="1567a-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1567a-200">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Degreed.</span><span class="sxs-lookup"><span data-stu-id="1567a-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Degreed.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="1567a-202">**Pour affecter Britta Simon à Degreed, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1567a-202">**To assign Britta Simon to Degreed, perform the following steps:**</span></span>

1. <span data-ttu-id="1567a-203">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1567a-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="1567a-205">Dans la liste des applications, sélectionnez **Degreed**.</span><span class="sxs-lookup"><span data-stu-id="1567a-205">In the applications list, select **Degreed**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-degreed-tutorial/tutorial_degreed_app.png) 

3. <span data-ttu-id="1567a-207">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1567a-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="1567a-209">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="1567a-209">Click **Add** button.</span></span> <span data-ttu-id="1567a-210">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="1567a-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="1567a-212">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="1567a-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1567a-213">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1567a-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1567a-214">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="1567a-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1567a-215">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="1567a-215">Testing single sign-on</span></span>

<span data-ttu-id="1567a-216">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="1567a-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1567a-217">Lorsque vous cliquez sur la mosaïque Degreed dans le volet d’accès, vous devez être connecté automatiquement à votre application Degreed.</span><span class="sxs-lookup"><span data-stu-id="1567a-217">When you click the Degreed tile in the Access Panel, you should get automatically signed-on to your Degreed application.</span></span>
<span data-ttu-id="1567a-218">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1567a-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1567a-219">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="1567a-219">Additional resources</span></span>

* [<span data-ttu-id="1567a-220">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1567a-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1567a-221">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="1567a-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-degreed-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-degreed-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-degreed-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-degreed-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-degreed-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-degreed-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-degreed-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-degreed-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-degreed-tutorial/tutorial_general_203.png

