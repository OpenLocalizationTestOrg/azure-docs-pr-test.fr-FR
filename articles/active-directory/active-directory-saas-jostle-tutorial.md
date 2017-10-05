---
title: "Didacticiel : Intégration d’Azure Active Directory à Jostle | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Jostle."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9ca4ca1f-8f68-4225-81a6-1666b486d6a8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 0ca8aca1446a38643ce9f6751b6fe9cae1eaa5b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jostle"></a><span data-ttu-id="b05b5-103">Didacticiel : Intégration d’Azure Active Directory à Jostle</span><span class="sxs-lookup"><span data-stu-id="b05b5-103">Tutorial: Azure Active Directory integration with Jostle</span></span>

<span data-ttu-id="b05b5-104">Dans ce didacticiel, vous allez apprendre à intégrer Jostle à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b05b5-104">In this tutorial, you learn how to integrate Jostle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b05b5-105">L’intégration de Jostle à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="b05b5-105">Integrating Jostle with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b05b5-106">Dans Azure AD, vous pouvez contrôler qui a accès à Jostle.</span><span class="sxs-lookup"><span data-stu-id="b05b5-106">You can control in Azure AD who has access to Jostle</span></span>
- <span data-ttu-id="b05b5-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Jostle (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b05b5-107">You can enable your users to automatically get signed-on to Jostle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b05b5-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="b05b5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b05b5-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b05b5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b05b5-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b05b5-110">Prerequisites</span></span>

<span data-ttu-id="b05b5-111">Pour configurer l’intégration d’Azure AD à Jostle, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="b05b5-111">To configure Azure AD integration with Jostle, you need the following items:</span></span>

- <span data-ttu-id="b05b5-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="b05b5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b05b5-113">Un abonnement Jostle pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="b05b5-113">A Jostle single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b05b5-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="b05b5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b05b5-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="b05b5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b05b5-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="b05b5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b05b5-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b05b5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b05b5-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="b05b5-118">Scenario description</span></span>
<span data-ttu-id="b05b5-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="b05b5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b05b5-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="b05b5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b05b5-121">Ajout de Jostle à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="b05b5-121">Adding Jostle from the gallery</span></span>
2. <span data-ttu-id="b05b5-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b05b5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jostle-from-the-gallery"></a><span data-ttu-id="b05b5-123">Ajout de Jostle à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="b05b5-123">Adding Jostle from the gallery</span></span>
<span data-ttu-id="b05b5-124">Pour configurer l’intégration de Jostle à Azure AD, vous devez ajouter Jostle à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="b05b5-124">To configure the integration of Jostle into Azure AD, you need to add Jostle from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b05b5-125">**Pour ajouter Jostle à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b05b5-125">**To add Jostle from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b05b5-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b05b5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b05b5-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="b05b5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b05b5-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="b05b5-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="b05b5-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="b05b5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="b05b5-133">Dans la zone de recherche, tapez **Jostle**.</span><span class="sxs-lookup"><span data-stu-id="b05b5-133">In the search box, type **Jostle**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jostle-tutorial/tutorial_jostle_search.png)

5. <span data-ttu-id="b05b5-135">Dans le panneau des résultats, sélectionnez **Jostle**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="b05b5-135">In the results panel, select **Jostle**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jostle-tutorial/tutorial_jostle_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b05b5-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b05b5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b05b5-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Jostle avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="b05b5-138">In this section, you configure and test Azure AD single sign-on with Jostle based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b05b5-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Jostle équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b05b5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Jostle is to a user in Azure AD.</span></span> <span data-ttu-id="b05b5-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Jostle associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="b05b5-140">In other words, a link relationship between an Azure AD user and the related user in Jostle needs to be established.</span></span>

<span data-ttu-id="b05b5-141">Dans Jostle, assignez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="b05b5-141">In Jostle, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b05b5-142">Pour configurer et tester l’authentification unique Azure AD avec Jostle, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="b05b5-142">To configure and test Azure AD single sign-on with Jostle, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b05b5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="b05b5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b05b5-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b05b5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b05b5-145">**[Création d’un utilisateur de test Jostle](#creating-a-jostle-test-user)** pour obtenir un équivalent de Britta Simon dans Jostle lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="b05b5-145">**[Creating a Jostle test user](#creating-a-jostle-test-user)** - to have a counterpart of Britta Simon in Jostle that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b05b5-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b05b5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b05b5-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="b05b5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b05b5-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b05b5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b05b5-149">Dans cette section, vous activez l’authentification unique Azure AD dans le portail Azure et configurez l’authentification unique dans votre application Jostle.</span><span class="sxs-lookup"><span data-stu-id="b05b5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Jostle application.</span></span>

<span data-ttu-id="b05b5-150">**Pour configurer l’authentification unique Azure AD avec Jostle, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b05b5-150">**To configure Azure AD single sign-on with Jostle, perform the following steps:**</span></span>

1. <span data-ttu-id="b05b5-151">Dans le portail Azure, sur la page d’intégration de l’application **Jostle**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="b05b5-151">In the Azure portal, on the **Jostle** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="b05b5-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="b05b5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-jostle-tutorial/tutorial_jostle_samlbase.png)

3. <span data-ttu-id="b05b5-155">Dans la section **Domaine et URL Jostle**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="b05b5-155">On the **Jostle Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-jostle-tutorial/tutorial_jostle_url.png)

    <span data-ttu-id="b05b5-157">a.</span><span class="sxs-lookup"><span data-stu-id="b05b5-157">a.</span></span> <span data-ttu-id="b05b5-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<tanent name>.jostle.us/jostle-prod/`</span><span class="sxs-lookup"><span data-stu-id="b05b5-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tanent name>.jostle.us/jostle-prod/`</span></span>

    <span data-ttu-id="b05b5-159">b.</span><span class="sxs-lookup"><span data-stu-id="b05b5-159">b.</span></span> <span data-ttu-id="b05b5-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<tanent name>.jostle.us`</span><span class="sxs-lookup"><span data-stu-id="b05b5-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<tanent name>.jostle.us`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b05b5-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="b05b5-161">These values are not real.</span></span> <span data-ttu-id="b05b5-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="b05b5-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="b05b5-163">Pour obtenir ces valeurs, contactez l’[l’équipe de support technique Jostle](mailto:support@jostle.me).</span><span class="sxs-lookup"><span data-stu-id="b05b5-163">Contact [Jostle support team](mailto:support@jostle.me) to get these values.</span></span> 
 


4. <span data-ttu-id="b05b5-164">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="b05b5-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-jostle-tutorial/tutorial_jostle_certificate.png) 

5. <span data-ttu-id="b05b5-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="b05b5-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-jostle-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="b05b5-168">Pour configurer l’authentification unique du côté Jostle, vous devez envoyer le fichier XML de métadonnées téléchargé à [l’équipe de support technique de Jostle](mailto:support@jostle.me).</span><span class="sxs-lookup"><span data-stu-id="b05b5-168">To configure single sign-on on Jostle side, you need to send the downloaded metadata XML to [Jostle support team](mailto:support@jostle.me).</span></span> <span data-ttu-id="b05b5-169">Celle-ci configure ensuite ce paramètre pour que la connexion SSO SAML soit définie correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="b05b5-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span> 

> [!TIP]
> <span data-ttu-id="b05b5-170">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="b05b5-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b05b5-171">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="b05b5-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b05b5-172">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b05b5-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b05b5-173">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="b05b5-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="b05b5-174">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="b05b5-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="b05b5-176">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b05b5-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b05b5-177">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b05b5-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jostle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b05b5-179">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="b05b5-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jostle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b05b5-181">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="b05b5-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jostle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b05b5-183">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="b05b5-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jostle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b05b5-185">a.</span><span class="sxs-lookup"><span data-stu-id="b05b5-185">a.</span></span> <span data-ttu-id="b05b5-186">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b05b5-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b05b5-187">b.</span><span class="sxs-lookup"><span data-stu-id="b05b5-187">b.</span></span> <span data-ttu-id="b05b5-188">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b05b5-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b05b5-189">c.</span><span class="sxs-lookup"><span data-stu-id="b05b5-189">c.</span></span> <span data-ttu-id="b05b5-190">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="b05b5-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b05b5-191">d.</span><span class="sxs-lookup"><span data-stu-id="b05b5-191">d.</span></span> <span data-ttu-id="b05b5-192">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="b05b5-192">Click **Create**.</span></span>
 
### <a name="creating-a-jostle-test-user"></a><span data-ttu-id="b05b5-193">Création d’un utilisateur de test Jostle</span><span class="sxs-lookup"><span data-stu-id="b05b5-193">Creating a Jostle test user</span></span>

<span data-ttu-id="b05b5-194">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Jostle.</span><span class="sxs-lookup"><span data-stu-id="b05b5-194">In this section, you create a user called Britta Simon in Jostle.</span></span> <span data-ttu-id="b05b5-195">Si vous ne savez pas comment ajouter Britta Simon dans Jostle, veuillez contacter [l’équipe de support Jostle](mailto:support@jostle.me) pour ajouter l’utilisateur de test et activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="b05b5-195">If you don't know how to add Britta Simon in Jostle, please contact with [Jostle support team](mailto:support@jostle.me) to add the test user and enable SSO.</span></span>

> [!NOTE]
> <span data-ttu-id="b05b5-196">Le titulaire du compte Azure Active Directory reçoit un e-mail contenant un lien à suivre pour confirmer son compte et l’activer.</span><span class="sxs-lookup"><span data-stu-id="b05b5-196">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b05b5-197">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="b05b5-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b05b5-198">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Jostle.</span><span class="sxs-lookup"><span data-stu-id="b05b5-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jostle.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="b05b5-200">**Pour affecter Britta Simon à Jostle, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b05b5-200">**To assign Britta Simon to Jostle, perform the following steps:**</span></span>

1. <span data-ttu-id="b05b5-201">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="b05b5-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="b05b5-203">Dans la liste des applications, sélectionnez **Jostle**.</span><span class="sxs-lookup"><span data-stu-id="b05b5-203">In the applications list, select **Jostle**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-jostle-tutorial/tutorial_jostle_app.png) 

3. <span data-ttu-id="b05b5-205">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="b05b5-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="b05b5-207">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="b05b5-207">Click **Add** button.</span></span> <span data-ttu-id="b05b5-208">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="b05b5-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="b05b5-210">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="b05b5-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b05b5-211">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="b05b5-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b05b5-212">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="b05b5-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b05b5-213">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="b05b5-213">Testing single sign-on</span></span>

<span data-ttu-id="b05b5-214">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="b05b5-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b05b5-215">Lorsque vous cliquez sur la vignette Jostle dans le panneau d’accès, vous accédez automatiquement à la page de connexion Jostle.</span><span class="sxs-lookup"><span data-stu-id="b05b5-215">When you click the Jostle tile in the Access Panel, you should get automatically login page of Jostle application.</span></span>
<span data-ttu-id="b05b5-216">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b05b5-216">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b05b5-217">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="b05b5-217">Additional resources</span></span>

* [<span data-ttu-id="b05b5-218">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b05b5-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b05b5-219">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="b05b5-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_203.png

