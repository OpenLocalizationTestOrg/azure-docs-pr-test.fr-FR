---
title: "Didacticiel : intégration d’Azure Active Directory à Tango Analytics | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Tango Analytics."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2f7555d3-e9ba-40b2-9b3a-2f0ab38a4c08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 46f6facc3c86630a9252340b2e89634368c0263d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tango-analytics"></a><span data-ttu-id="931fd-103">Didacticiel : intégration d’Azure Active Directory à Tango Analytics</span><span class="sxs-lookup"><span data-stu-id="931fd-103">Tutorial: Azure Active Directory integration with Tango Analytics</span></span>

<span data-ttu-id="931fd-104">Dans ce didacticiel, vous allez apprendre à intégrer Tango Analytics à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="931fd-104">In this tutorial, you learn how to integrate Tango Analytics with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="931fd-105">L’intégration de Tango Analytics dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="931fd-105">Integrating Tango Analytics with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="931fd-106">Dans Azure AD, vous pouvez contrôler qui a accès à Tango Analytics</span><span class="sxs-lookup"><span data-stu-id="931fd-106">You can control in Azure AD who has access to Tango Analytics</span></span>
- <span data-ttu-id="931fd-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Tango Analytics (via l’authentification unique) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="931fd-107">You can enable your users to automatically get signed-on to Tango Analytics (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="931fd-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="931fd-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="931fd-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="931fd-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="931fd-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="931fd-110">Prerequisites</span></span>

<span data-ttu-id="931fd-111">Pour configurer l’intégration d’Azure AD à Tango Analytics, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="931fd-111">To configure Azure AD integration with Tango Analytics, you need the following items:</span></span>

- <span data-ttu-id="931fd-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="931fd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="931fd-113">Un abonnement Tango Analytics pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="931fd-113">A Tango Analytics single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="931fd-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="931fd-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="931fd-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="931fd-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="931fd-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="931fd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="931fd-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="931fd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="931fd-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="931fd-118">Scenario description</span></span>
<span data-ttu-id="931fd-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="931fd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="931fd-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="931fd-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="931fd-121">Ajout de Tango Analytique à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="931fd-121">Adding Tango Analytics from the gallery</span></span>
2. <span data-ttu-id="931fd-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="931fd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tango-analytics-from-the-gallery"></a><span data-ttu-id="931fd-123">Ajout de Tango Analytique à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="931fd-123">Adding Tango Analytics from the gallery</span></span>
<span data-ttu-id="931fd-124">Pour configurer l’intégration de Tango Analytics à Azure AD, vous devez ajouter Tango Analytics à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="931fd-124">To configure the integration of Tango Analytics into Azure AD, you need to add Tango Analytics from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="931fd-125">**Pour ajouter Tango Analytics à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="931fd-125">**To add Tango Analytics from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="931fd-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="931fd-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="931fd-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="931fd-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="931fd-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="931fd-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="931fd-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="931fd-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="931fd-133">Dans la zone de recherche, tapez **Tango Analytics**.</span><span class="sxs-lookup"><span data-stu-id="931fd-133">In the search box, type **Tango Analytics**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_tangoanalytics_search.png)

5. <span data-ttu-id="931fd-135">Dans le panneau de résultats, sélectionnez **Tango Analytics**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="931fd-135">In the results panel, select **Tango Analytics**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_tangoanalytics_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="931fd-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="931fd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="931fd-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Tango Analytics avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="931fd-138">In this section, you configure and test Azure AD single sign-on with Tango Analytics based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="931fd-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Tango Analytics équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="931fd-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Tango Analytics is to a user in Azure AD.</span></span> <span data-ttu-id="931fd-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Tango Analytics associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="931fd-140">In other words, a link relationship between an Azure AD user and the related user in Tango Analytics needs to be established.</span></span>

<span data-ttu-id="931fd-141">Dans Tango Analytics, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur **Nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="931fd-141">In Tango Analytics, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="931fd-142">Pour configurer et tester l’authentification unique Azure AD avec Tango Analytics, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="931fd-142">To configure and test Azure AD single sign-on with Tango Analytics, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="931fd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="931fd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="931fd-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="931fd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="931fd-145">**[Création d’un utilisateur de test Tango Analytics](#creating-a-tango-analytics-test-user)** pour avoir un équivalent de Britta Simon dans Tango Analytics lié à la représentation de l’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="931fd-145">**[Creating a Tango Analytics test user](#creating-a-tango-analytics-test-user)** - to have a counterpart of Britta Simon in Tango Analytics that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="931fd-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="931fd-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="931fd-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="931fd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="931fd-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="931fd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="931fd-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Tango Analytics.</span><span class="sxs-lookup"><span data-stu-id="931fd-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Tango Analytics application.</span></span>

<span data-ttu-id="931fd-150">**Pour configurer l’authentification unique Azure AD avec Tango Analytics, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="931fd-150">**To configure Azure AD single sign-on with Tango Analytics, perform the following steps:**</span></span>

1. <span data-ttu-id="931fd-151">Dans le portail Azure, sur la page d’intégration de l’application **Tango Analytics**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="931fd-151">In the Azure portal, on the **Tango Analytics** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="931fd-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="931fd-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_tangoanalytics_samlbase.png)

3. <span data-ttu-id="931fd-155">Dans la section **Domaine et URL Tango Analytics**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="931fd-155">On the **Tango Analytics Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_tangoanalytics_url.png)

    <span data-ttu-id="931fd-157">a.</span><span class="sxs-lookup"><span data-stu-id="931fd-157">a.</span></span> <span data-ttu-id="931fd-158">Dans la zone de texte **Identificateur**, entrez la valeur `TACORE_SSO`</span><span class="sxs-lookup"><span data-stu-id="931fd-158">In the **Identifier** textbox, type the value `TACORE_SSO`</span></span>

    <span data-ttu-id="931fd-159">b.</span><span class="sxs-lookup"><span data-stu-id="931fd-159">b.</span></span> <span data-ttu-id="931fd-160">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://mts.tangoanalytics.com/saml2/sp/acs/post`</span><span class="sxs-lookup"><span data-stu-id="931fd-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://mts.tangoanalytics.com/saml2/sp/acs/post`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="931fd-161">La valeur de l’URL de réponse n’est pas réelle.</span><span class="sxs-lookup"><span data-stu-id="931fd-161">The Reply URL value is not real.</span></span> <span data-ttu-id="931fd-162">Mettez à jour la valeur avec l’URL de réponse réelle.</span><span class="sxs-lookup"><span data-stu-id="931fd-162">Update this with the actual Reply URL.</span></span> <span data-ttu-id="931fd-163">Pour obtenir cette valeur, contactez [l’équipe de support technique de Tango Analytics](mailto:support@tangoanalytics.com).</span><span class="sxs-lookup"><span data-stu-id="931fd-163">Contact [Tango Analytics support team](mailto:support@tangoanalytics.com) to get this value.</span></span>

4. <span data-ttu-id="931fd-164">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="931fd-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_tangoanalytics_certificate.png) 

5. <span data-ttu-id="931fd-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="931fd-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="931fd-168">Pour configurer l’authentification unique du côté de **Tango Analytics**, vous devez envoyer le fichier **XML de métadonnées** téléchargé à [l’équipe de support technique Tango Analytics](mailto:support@tangoanalytics.com).</span><span class="sxs-lookup"><span data-stu-id="931fd-168">To configure single sign-on on **Tango Analytics** side, you need to send the downloaded **Metadata XML** to [Tango Analytics support team](mailto:support@tangoanalytics.com).</span></span> <span data-ttu-id="931fd-169">Celles-ci configurent ensuite ce paramètre pour que la connexion SSO SAML soit définie correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="931fd-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="931fd-170">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="931fd-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="931fd-171">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="931fd-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="931fd-172">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="931fd-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="931fd-173">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="931fd-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="931fd-174">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="931fd-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="931fd-176">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="931fd-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="931fd-177">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="931fd-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tangoanalytics-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="931fd-179">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="931fd-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tangoanalytics-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="931fd-181">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="931fd-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tangoanalytics-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="931fd-183">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="931fd-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tangoanalytics-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="931fd-185">a.</span><span class="sxs-lookup"><span data-stu-id="931fd-185">a.</span></span> <span data-ttu-id="931fd-186">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="931fd-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="931fd-187">b.</span><span class="sxs-lookup"><span data-stu-id="931fd-187">b.</span></span> <span data-ttu-id="931fd-188">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="931fd-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="931fd-189">c.</span><span class="sxs-lookup"><span data-stu-id="931fd-189">c.</span></span> <span data-ttu-id="931fd-190">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="931fd-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="931fd-191">d.</span><span class="sxs-lookup"><span data-stu-id="931fd-191">d.</span></span> <span data-ttu-id="931fd-192">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="931fd-192">Click **Create**.</span></span>
 
### <a name="creating-a-tango-analytics-test-user"></a><span data-ttu-id="931fd-193">Création d’un utilisateur de test Tango Analytics</span><span class="sxs-lookup"><span data-stu-id="931fd-193">Creating a Tango Analytics test user</span></span>

<span data-ttu-id="931fd-194">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Tango Analytics.</span><span class="sxs-lookup"><span data-stu-id="931fd-194">In this section, you create a user called Britta Simon in Tango Analytics.</span></span> <span data-ttu-id="931fd-195">Travailler avec [l’équipe de support technique Tango Analytics](mailto:support@tangoanalytics.com) pour ajouter des utilisateurs dans la plateforme Tango Analytics.</span><span class="sxs-lookup"><span data-stu-id="931fd-195">Work with [Tango Analytics support team](mailto:support@tangoanalytics.com) to add the users in the Tango Analytics platform.</span></span> <span data-ttu-id="931fd-196">Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="931fd-196">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="931fd-197">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="931fd-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="931fd-198">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Tango Analytics.</span><span class="sxs-lookup"><span data-stu-id="931fd-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Tango Analytics.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="931fd-200">**Pour affecter Britta Simon à Tango Analytics, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="931fd-200">**To assign Britta Simon to Tango Analytics, perform the following steps:**</span></span>

1. <span data-ttu-id="931fd-201">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="931fd-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="931fd-203">Dans la liste des applications, sélectionnez **Tango Analytics**.</span><span class="sxs-lookup"><span data-stu-id="931fd-203">In the applications list, select **Tango Analytics**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_tangoanalytics_app.png) 

3. <span data-ttu-id="931fd-205">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="931fd-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="931fd-207">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="931fd-207">Click **Add** button.</span></span> <span data-ttu-id="931fd-208">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="931fd-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="931fd-210">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="931fd-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="931fd-211">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="931fd-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="931fd-212">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="931fd-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="931fd-213">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="931fd-213">Testing single sign-on</span></span>

<span data-ttu-id="931fd-214">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="931fd-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="931fd-215">Si vous cliquez sur la vignette Tango Analytics dans le volet d’accès, vous devez vous connecter automatiquement à votre application Tango Analytics.</span><span class="sxs-lookup"><span data-stu-id="931fd-215">When you click the Tango Analytics tile in the Access Panel, you should get automatically signed-on to your Tango Analytics application.</span></span>
<span data-ttu-id="931fd-216">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="931fd-216">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="931fd-217">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="931fd-217">Additional resources</span></span>

* [<span data-ttu-id="931fd-218">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="931fd-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="931fd-219">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="931fd-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_203.png

