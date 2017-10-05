---
title: "Didacticiel : intégration d’Azure Active Directory à Intralinks | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Intralinks."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 147f2bf9-166b-402e-adc4-4b19dd336883
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: ee7fd5b88ac806104002ffb41af11bab4fd1b2dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intralinks"></a><span data-ttu-id="84d31-103">Didacticiel : intégration d’Azure Active Directory à Intralinks</span><span class="sxs-lookup"><span data-stu-id="84d31-103">Tutorial: Azure Active Directory integration with Intralinks</span></span>

<span data-ttu-id="84d31-104">Dans ce didacticiel, vous allez apprendre à intégrer Intralinks à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="84d31-104">In this tutorial, you learn how to integrate Intralinks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="84d31-105">L’intégration d’Intralinks à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="84d31-105">Integrating Intralinks with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="84d31-106">Dans Azure AD, vous pouvez déterminer qui a accès à Intralinks.</span><span class="sxs-lookup"><span data-stu-id="84d31-106">You can control in Azure AD who has access to Intralinks</span></span>
- <span data-ttu-id="84d31-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Intralinks (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="84d31-107">You can enable your users to automatically get signed-on to Intralinks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="84d31-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="84d31-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="84d31-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="84d31-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="84d31-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="84d31-110">Prerequisites</span></span>

<span data-ttu-id="84d31-111">Pour configurer l’intégration d’Azure AD à Intralinks, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="84d31-111">To configure Azure AD integration with Intralinks, you need the following items:</span></span>

- <span data-ttu-id="84d31-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="84d31-112">An Azure AD subscription</span></span>
- <span data-ttu-id="84d31-113">Un abonnement Intralinks pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="84d31-113">An Intralinks single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="84d31-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="84d31-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="84d31-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="84d31-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="84d31-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="84d31-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="84d31-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="84d31-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="84d31-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="84d31-118">Scenario description</span></span>
<span data-ttu-id="84d31-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="84d31-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="84d31-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="84d31-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="84d31-121">Ajout d’Intralinks à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="84d31-121">Adding Intralinks from the gallery</span></span>
2. <span data-ttu-id="84d31-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="84d31-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intralinks-from-the-gallery"></a><span data-ttu-id="84d31-123">Ajout d’Intralinks à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="84d31-123">Adding Intralinks from the gallery</span></span>
<span data-ttu-id="84d31-124">Pour configurer son intégration à Azure AD, vous devez ajouter Intralinks à votre liste d’applications SaaS gérées, à partir de la galerie.</span><span class="sxs-lookup"><span data-stu-id="84d31-124">To configure the integration of Intralinks into Azure AD, you need to add Intralinks from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="84d31-125">**Pour ajouter Intralinks à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="84d31-125">**To add Intralinks from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="84d31-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="84d31-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="84d31-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="84d31-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="84d31-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="84d31-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="84d31-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="84d31-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="84d31-133">Dans la zone de recherche, saisissez **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="84d31-133">In the search box, type **Intralinks**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. <span data-ttu-id="84d31-135">Dans le volet de résultats, sélectionnez **Intralinks**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="84d31-135">In the results panel, select **Intralinks**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="84d31-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="84d31-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="84d31-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Intralinks, en tirant parti d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="84d31-138">In this section, you configure and test Azure AD single sign-on with Intralinks based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="84d31-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Intralinks équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="84d31-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Intralinks is to a user in Azure AD.</span></span> <span data-ttu-id="84d31-140">En d’autres termes, une relation doit être établie entre l’utilisateur Azure AD et l’utilisateur Intralinks associé.</span><span class="sxs-lookup"><span data-stu-id="84d31-140">In other words, a link relationship between an Azure AD user and the related user in Intralinks needs to be established.</span></span>

<span data-ttu-id="84d31-141">Dans Intralinks, attribuez la valeur du **nom d’utilisateur** dans Azure AD comme valeur **Nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="84d31-141">In Intralinks, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="84d31-142">Pour configurer et tester l’authentification unique Azure AD avec Intralinks, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="84d31-142">To configure and test Azure AD single sign-on with Intralinks, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="84d31-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="84d31-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="84d31-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="84d31-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="84d31-145">**[Création d’un utilisateur de test Intralinks](#creating-an-intralinks-test-user)** : pour avoir un équivalent de l’utilisateur Britta Simon dans Intralinks qui soit lié à la représentation de l’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="84d31-145">**[Creating an Intralinks test user](#creating-an-intralinks-test-user)** - to have a counterpart of Britta Simon in Intralinks that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="84d31-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="84d31-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="84d31-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="84d31-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="84d31-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="84d31-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="84d31-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Intralinks.</span><span class="sxs-lookup"><span data-stu-id="84d31-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Intralinks application.</span></span>

<span data-ttu-id="84d31-150">**Pour configurer l’authentification unique Azure AD avec Intralinks, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="84d31-150">**To configure Azure AD single sign-on with Intralinks, perform the following steps:**</span></span>

1. <span data-ttu-id="84d31-151">Dans le Portail Azure, sur la page d’intégration de l’application **Intralinks**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="84d31-151">In the Azure portal, on the **Intralinks** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="84d31-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="84d31-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_samlbase.png)

3. <span data-ttu-id="84d31-155">Dans la section **Domaine et URL Intralinks**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="84d31-155">On the **Intralinks Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_url.png)

    <span data-ttu-id="84d31-157">Dans la zone de texte **URL d’authentification**, tapez une URL en utilisant le modèle suivant : `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`</span><span class="sxs-lookup"><span data-stu-id="84d31-157">In the **Sign-on URL** textbox, type a URL using the following pattern:  `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="84d31-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="84d31-158">This value is not real.</span></span> <span data-ttu-id="84d31-159">Mettez à jour cette valeur avec l’URL d’authentification réelle.</span><span class="sxs-lookup"><span data-stu-id="84d31-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="84d31-160">Contactez [l’équipe de support client Intralinks](https://www.intralinks.com/contact-1) pour obtenir cette valeur.</span><span class="sxs-lookup"><span data-stu-id="84d31-160">Contact [Intralinks Client support team](https://www.intralinks.com/contact-1) to get this value.</span></span> 
 
4. <span data-ttu-id="84d31-161">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="84d31-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_certificate.png) 

5. <span data-ttu-id="84d31-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="84d31-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="84d31-165">Pour configurer l’authentification unique du côté de **Intralinks**, vous devez envoyer le **XML de métadonnées** téléchargé à [l’équipe de support d’Intralinks](https://www.intralinks.com/contact-1).</span><span class="sxs-lookup"><span data-stu-id="84d31-165">To configure single sign-on on **Intralinks** side, you need to send the downloaded **Metadata XML** [Intralinks support team](https://www.intralinks.com/contact-1).</span></span> <span data-ttu-id="84d31-166">Celle-ci configure ensuite ce paramètre pour que la connexion SSO SAML soit définie correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="84d31-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="84d31-167">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="84d31-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="84d31-168">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="84d31-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="84d31-169">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="84d31-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="84d31-170">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="84d31-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="84d31-171">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="84d31-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="84d31-173">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="84d31-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="84d31-174">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="84d31-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="84d31-176">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="84d31-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="84d31-178">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="84d31-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="84d31-180">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="84d31-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="84d31-182">a.</span><span class="sxs-lookup"><span data-stu-id="84d31-182">a.</span></span> <span data-ttu-id="84d31-183">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="84d31-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="84d31-184">b.</span><span class="sxs-lookup"><span data-stu-id="84d31-184">b.</span></span> <span data-ttu-id="84d31-185">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="84d31-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="84d31-186">c.</span><span class="sxs-lookup"><span data-stu-id="84d31-186">c.</span></span> <span data-ttu-id="84d31-187">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="84d31-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="84d31-188">d.</span><span class="sxs-lookup"><span data-stu-id="84d31-188">d.</span></span> <span data-ttu-id="84d31-189">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="84d31-189">Click **Create**.</span></span>
 
### <a name="creating-an-intralinks-test-user"></a><span data-ttu-id="84d31-190">Création d’un utilisateur de test Intralinks</span><span class="sxs-lookup"><span data-stu-id="84d31-190">Creating an Intralinks test user</span></span>

<span data-ttu-id="84d31-191">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Intralinks.</span><span class="sxs-lookup"><span data-stu-id="84d31-191">In this section, you create a user called Britta Simon in Intralinks.</span></span> <span data-ttu-id="84d31-192">Collaborez avec [l’équipe du support technique Intralinks](https://www.intralinks.com/contact-1) pour ajouter des utilisateurs sur la plateforme Intralinks.</span><span class="sxs-lookup"><span data-stu-id="84d31-192">Please work with [Intralinks support team](https://www.intralinks.com/contact-1) to add the users in the Intralinks platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="84d31-193">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="84d31-193">Assigning the Azure AD test user</span></span>

<span data-ttu-id="84d31-194">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Intralinks.</span><span class="sxs-lookup"><span data-stu-id="84d31-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Intralinks.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="84d31-196">**Pour affecter Britta Simon à Intralinks, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="84d31-196">**To assign Britta Simon to Intralinks, perform the following steps:**</span></span>

1. <span data-ttu-id="84d31-197">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="84d31-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="84d31-199">Dans la liste des applications, sélectionnez **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="84d31-199">In the applications list, select **Intralinks**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_app.png) 

3. <span data-ttu-id="84d31-201">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="84d31-201">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="84d31-203">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="84d31-203">Click **Add** button.</span></span> <span data-ttu-id="84d31-204">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="84d31-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="84d31-206">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="84d31-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="84d31-207">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="84d31-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="84d31-208">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="84d31-208">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="add-intralinks-via-or-elite-application"></a><span data-ttu-id="84d31-209">Ajouter une application Intralinks VIA ou Elite</span><span class="sxs-lookup"><span data-stu-id="84d31-209">Add Intralinks VIA or Elite application</span></span>

<span data-ttu-id="84d31-210">Intralinks utilise la même plateforme d’identité pour l’authentification unique quelle que soit l’application Intralinks, à l’exception de Dealnexus.</span><span class="sxs-lookup"><span data-stu-id="84d31-210">Intralinks uses the same SSO identity platform for all other Intralinks applications excluding Deal Nexus application.</span></span> <span data-ttu-id="84d31-211">Par conséquent, si vous envisagez d’utiliser une autre application Intralinks, vous devez d’abord configurer l’authentification unique pour une application Intralinks principale, en suivant la procédure décrite ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="84d31-211">So if you plan to use any other Intralinks application then first you have to configure SSO for one Primary Intralinks application using the procedure described above.</span></span>

<span data-ttu-id="84d31-212">Après cela, vous pouvez suivre la procédure ci-dessous pour ajouter une autre application Intralinks dans votre client, afin de pouvoir tirer parti de cette application principale pour l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="84d31-212">After that you can follow the below procedure to add another Intralinks application in your tenant which can leverage this primary application for SSO.</span></span> 

>[!NOTE]
><span data-ttu-id="84d31-213">Cette fonctionnalité est uniquement disponible pour les clients de la référence SKU Azure AD Premium. Les clients dotés de la SKU gratuite ou de base du logiciel ne peuvent pas l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="84d31-213">This feature is available only to Azure AD Premium SKU Customers and not available for Free or Basic SKU customers.</span></span>

1. <span data-ttu-id="84d31-214">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="84d31-214">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]


2. <span data-ttu-id="84d31-216">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="84d31-216">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="84d31-217">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="84d31-217">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="84d31-219">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="84d31-219">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="84d31-221">Dans la zone de recherche, saisissez **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="84d31-221">In the search box, type **Intralinks**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. <span data-ttu-id="84d31-223">Sur **l’application Ajout Intralinks** procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="84d31-223">On **Intralinks Add app** perform the following steps:</span></span>

    ![Ajout d’une application Intralinks VIA ou Elite](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addapp.png)

    <span data-ttu-id="84d31-225">a.</span><span class="sxs-lookup"><span data-stu-id="84d31-225">a.</span></span> <span data-ttu-id="84d31-226">Dans la zone de texte **Nom**, entrez un nom de l’application approprié, par exemple **Intralinks Elite**.</span><span class="sxs-lookup"><span data-stu-id="84d31-226">In **Name** textbox, enter appropriate name of the application e.g. **Intralinks Elite**.</span></span>

    <span data-ttu-id="84d31-227">b.</span><span class="sxs-lookup"><span data-stu-id="84d31-227">b.</span></span> <span data-ttu-id="84d31-228">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="84d31-228">Click **Add** button.</span></span>

6.  <span data-ttu-id="84d31-229">Dans le Portail Azure, sur la page d’intégration de l’application **Intralinks**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="84d31-229">In the Azure portal, on the **Intralinks** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

7. <span data-ttu-id="84d31-231">Dans la boîte de dialogue **Authentification unique**, sélectionnez **Mode** en tant que **Authentification liée**.</span><span class="sxs-lookup"><span data-stu-id="84d31-231">On the **Single sign-on** dialog, select **Mode** as **Linked Sign-on**.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_linkedsignon.png)

8. <span data-ttu-id="84d31-233">Récupérez l’URL d’authentification unique initiée par le fournisseur de services depuis [l’équipe Intralinks](https://www.intralinks.com/contact-1) pour l’autre application Intralinks. Saisissez l’URL ainsi obtenue dans **Configurer l’URL d’authentification** comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="84d31-233">Get the the SP Initiated SSO URL from [Intralinks team](https://www.intralinks.com/contact-1) for the other Intralinks application and enter it in **Configure Sign-on URL** as shown below.</span></span> 
    
     ![Configurer l’authentification unique](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_customappurl.png)
    
     <span data-ttu-id="84d31-235">Dans la zone de texte URL de connexion, saisissez l’URL utilisée par les utilisateurs pour se connecter à votre application Intralinks en utilisant le modèle suivant :</span><span class="sxs-lookup"><span data-stu-id="84d31-235">In the Sign On URL textbox, type the URL used by your users to sign-on to your Intralinks application using the following pattern:</span></span>
   
    `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`

9. <span data-ttu-id="84d31-236">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="84d31-236">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

10. <span data-ttu-id="84d31-238">Affectez l’application à un utilisateur ou à un groupe, comme l’indique la section **[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)**.</span><span class="sxs-lookup"><span data-stu-id="84d31-238">Assign the application to user or groups as shown in the section **[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)**.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="84d31-239">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="84d31-239">Testing single sign-on</span></span>

<span data-ttu-id="84d31-240">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="84d31-240">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="84d31-241">Lorsque vous cliquez sur la vignette Intralinks dans le volet d’accès, vous devez être connecté automatiquement à votre application Intralinks.</span><span class="sxs-lookup"><span data-stu-id="84d31-241">When you click the Intralinks tile in the Access Panel, you should get automatically signed-on to your Intralinks application.</span></span>
<span data-ttu-id="84d31-242">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="84d31-242">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="84d31-243">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="84d31-243">Additional resources</span></span>

* [<span data-ttu-id="84d31-244">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="84d31-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="84d31-245">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="84d31-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_203.png

