---
title: "Didacticiel : Intégration d’Azure Active Directory avec Skillport | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Skillport."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4df349b2-a73f-4b88-a077-ec0fbfc26527
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jeedes
ms.openlocfilehash: 668fc5ae4f964bd776904c3a9dbc2b203689d50c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-skillport"></a><span data-ttu-id="de9f4-103">Didacticiel : Intégration d’Azure AD avec Skillport</span><span class="sxs-lookup"><span data-stu-id="de9f4-103">Tutorial: Azure Active Directory integration with Skillport</span></span>

<span data-ttu-id="de9f4-104">Dans ce didacticiel, vous allez apprendre à intégrer Skillport à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="de9f4-104">In this tutorial, you learn how to integrate Skillport with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="de9f4-105">L’intégration de Skillport dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="de9f4-105">Integrating Skillport with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="de9f4-106">Dans Azure AD, vous pouvez contrôler qui a accès à Skillport.</span><span class="sxs-lookup"><span data-stu-id="de9f4-106">You can control in Azure AD who has access to Skillport</span></span>
- <span data-ttu-id="de9f4-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Skillport (par le biais de l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="de9f4-107">You can enable your users to automatically get signed-on to Skillport (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="de9f4-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="de9f4-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="de9f4-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="de9f4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="de9f4-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="de9f4-110">Prerequisites</span></span>

<span data-ttu-id="de9f4-111">Pour configurer l’intégration d’Azure AD à Skillport, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="de9f4-111">To configure Azure AD integration with Skillport, you need the following items:</span></span>

- <span data-ttu-id="de9f4-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="de9f4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="de9f4-113">Un abonnement Skillport pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="de9f4-113">A Skillport single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="de9f4-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="de9f4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="de9f4-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="de9f4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="de9f4-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="de9f4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="de9f4-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="de9f4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="de9f4-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="de9f4-118">Scenario description</span></span>
<span data-ttu-id="de9f4-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="de9f4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="de9f4-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="de9f4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="de9f4-121">Ajout de Skillport à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="de9f4-121">Adding Skillport from the gallery</span></span>
2. <span data-ttu-id="de9f4-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="de9f4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-skillport-from-the-gallery"></a><span data-ttu-id="de9f4-123">Ajout de Skillport à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="de9f4-123">Adding Skillport from the gallery</span></span>
<span data-ttu-id="de9f4-124">Pour configurer l’intégration de Skillport avec Azure AD, vous devez ajouter Skillport à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="de9f4-124">To configure the integration of Skillport into Azure AD, you need to add Skillport from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="de9f4-125">**Pour ajouter Skillport à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="de9f4-125">**To add Skillport from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="de9f4-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="de9f4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="de9f4-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="de9f4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="de9f4-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="de9f4-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="de9f4-131">Cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="de9f4-131">Click **New Application** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="de9f4-133">Dans la zone de recherche, entrez **Skillport**.</span><span class="sxs-lookup"><span data-stu-id="de9f4-133">In the search box, type **Skillport**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_search.png)

5. <span data-ttu-id="de9f4-135">Dans le volet des résultats, sélectionnez **Skillport**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="de9f4-135">In the results panel, select **Skillport**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="de9f4-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="de9f4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="de9f4-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Skillport avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="de9f4-138">In this section, you configure and test Azure AD single sign-on with Skillport based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="de9f4-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Skillport équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="de9f4-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Skillport is to a user in Azure AD.</span></span> <span data-ttu-id="de9f4-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Skillport associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="de9f4-140">In other words, a link relationship between an Azure AD user and the related user in Skillport needs to be established.</span></span>

<span data-ttu-id="de9f4-141">Pour cela, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** dans Skillport.</span><span class="sxs-lookup"><span data-stu-id="de9f4-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Skillport.</span></span>

<span data-ttu-id="de9f4-142">Pour configurer et tester l’authentification unique Azure AD avec Skillport, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="de9f4-142">To configure and test Azure AD single sign-on with Skillport, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="de9f4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="de9f4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="de9f4-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="de9f4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="de9f4-145">**[Création d’un utilisateur de test Skillport](#creating-a-skillport-test-user)** pour avoir un équivalent de Britta Simon dans Skillport lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="de9f4-145">**[Creating a Skillport test user](#creating-a-skillport-test-user)** - to have a counterpart of Britta Simon in Skillport that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="de9f4-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="de9f4-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="de9f4-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="de9f4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="de9f4-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="de9f4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="de9f4-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Skillport.</span><span class="sxs-lookup"><span data-stu-id="de9f4-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Skillport application.</span></span>

<span data-ttu-id="de9f4-150">**Pour configurer l’authentification unique Azure AD avec Skillport, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="de9f4-150">**To configure Azure AD single sign-on with Skillport, perform the following steps:**</span></span>

1. <span data-ttu-id="de9f4-151">Dans le portail Azure, sur la page d’intégration de l’application **Skillport**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="de9f4-151">In the Azure  portal, on the **Skillport** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="de9f4-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="de9f4-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_samlbase.png)

3. <span data-ttu-id="de9f4-155">Dans la section **Domaine et URL Skillport**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="de9f4-155">On the **Skillport Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_url.png)

    <span data-ttu-id="de9f4-157">a.</span><span class="sxs-lookup"><span data-stu-id="de9f4-157">a.</span></span> <span data-ttu-id="de9f4-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant :</span><span class="sxs-lookup"><span data-stu-id="de9f4-158">In the **Sign-on URL** textbox, type a URL using the following patterns:</span></span>
      
      <span data-ttu-id="de9f4-159">Centre de données Europe : `https://<subdomain>.skillport.eu`</span><span class="sxs-lookup"><span data-stu-id="de9f4-159">EU Datacenter: `https://<subdomain>.skillport.eu`</span></span>
   
      <span data-ttu-id="de9f4-160">Centre de données États-Unis : `https://<subdomain>.skillport.com`</span><span class="sxs-lookup"><span data-stu-id="de9f4-160">US Datacenter: `https://<subdomain>.skillport.com`</span></span>
   
    <span data-ttu-id="de9f4-161">b.</span><span class="sxs-lookup"><span data-stu-id="de9f4-161">b.</span></span> <span data-ttu-id="de9f4-162">Dans la zone de texte **URL de réponse** , tapez une URL en respectant les formats suivants :</span><span class="sxs-lookup"><span data-stu-id="de9f4-162">In the **Reply URL** textbox, type a URL using the following patterns:</span></span>
    
      <span data-ttu-id="de9f4-163">Centre de données Europe : `https://<subdomain>.skillport.eu/adfs/ls/`</span><span class="sxs-lookup"><span data-stu-id="de9f4-163">EU Datacenter: `https://<subdomain>.skillport.eu/adfs/ls/`</span></span>
    
      <span data-ttu-id="de9f4-164">Centre de données États-Unis : `https://<subdomain>.skillport.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="de9f4-164">US Datacenter: `https://<subdomain>.skillport.com/sp/ACS.saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="de9f4-165">Il ne s’agit pas des valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="de9f4-165">These values are not the real.</span></span> <span data-ttu-id="de9f4-166">Mettez à jour ces valeurs avec l’URL de réponse et l’URL de connexion réelles.</span><span class="sxs-lookup"><span data-stu-id="de9f4-166">Update these values with the actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="de9f4-167">Pour obtenir ces valeurs, contactez l’[équipe de support technique de Skillport](https://www.skillsoft.com/contact.asp).</span><span class="sxs-lookup"><span data-stu-id="de9f4-167">Contact [Skillport Client support team](https://www.skillsoft.com/contact.asp) to get these values.</span></span>
 
4. <span data-ttu-id="de9f4-168">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier XML sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="de9f4-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_certificate.png) 

5. <span data-ttu-id="de9f4-170">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="de9f4-170">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-skillport-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="de9f4-172">Pour configurer l’authentification unique côté **Skillport**, vous devez envoyer le fichier **XML des métadonnées** téléchargé à l’[équipe de support technique de Skillport](https://www.skillsoft.com/contact.asp).</span><span class="sxs-lookup"><span data-stu-id="de9f4-172">To configure single sign-on on **Skillport** side, you need to send the downloaded **Metadata XML** to [Skillport support team](https://www.skillsoft.com/contact.asp).</span></span> <span data-ttu-id="de9f4-173">Ils configurent les éléments pour que la connexion SSO SAML soit définie correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="de9f4-173">They will set it up to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="de9f4-174">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="de9f4-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="de9f4-175">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="de9f4-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="de9f4-177">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="de9f4-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="de9f4-178">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="de9f4-178">In the **Azure  portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-skillport-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="de9f4-180">Accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs** pour afficher la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="de9f4-180">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-skillport-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="de9f4-182">En haut de la boîte de dialogue, cliquez sur **Ajouter** pour ouvrir la boîte de dialogue **Utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="de9f4-182">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-skillport-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="de9f4-184">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="de9f4-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-skillport-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="de9f4-186">a.</span><span class="sxs-lookup"><span data-stu-id="de9f4-186">a.</span></span> <span data-ttu-id="de9f4-187">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="de9f4-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="de9f4-188">b.</span><span class="sxs-lookup"><span data-stu-id="de9f4-188">b.</span></span> <span data-ttu-id="de9f4-189">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="de9f4-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="de9f4-190">c.</span><span class="sxs-lookup"><span data-stu-id="de9f4-190">c.</span></span> <span data-ttu-id="de9f4-191">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="de9f4-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="de9f4-192">d.</span><span class="sxs-lookup"><span data-stu-id="de9f4-192">d.</span></span> <span data-ttu-id="de9f4-193">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="de9f4-193">Click **Create**.</span></span>
 
### <a name="creating-a-skillport-test-user"></a><span data-ttu-id="de9f4-194">Création d’un utilisateur de test Skillport</span><span class="sxs-lookup"><span data-stu-id="de9f4-194">Creating a Skillport test user</span></span>

<span data-ttu-id="de9f4-195">Pour créer un utilisateur de test Skillport, vous devez contacter [l’équipe de support Skillport](https://www.skillsoft.com/contact.asp), qui dispose de plusieurs scénarios d’entreprise en fonction des exigences de l’utilisateur final.</span><span class="sxs-lookup"><span data-stu-id="de9f4-195">In order to create Skillport test user, you need to contact [Skillport support team](https://www.skillsoft.com/contact.asp) as they have multiple business scenarios according to the requirement of end user.</span></span> <span data-ttu-id="de9f4-196">Ils configureront les éléments après avoir discuté avec les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="de9f4-196">They will configure it after discussion with the users.</span></span>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="de9f4-197">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="de9f4-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="de9f4-198">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Skillport.</span><span class="sxs-lookup"><span data-stu-id="de9f4-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Skillport.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="de9f4-200">**Pour affecter Britta Simon à Skillport, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="de9f4-200">**To assign Britta Simon to Skillport, perform the following steps:**</span></span>

1. <span data-ttu-id="de9f4-201">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="de9f4-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="de9f4-203">Dans la liste des applications, sélectionnez **Skillport**.</span><span class="sxs-lookup"><span data-stu-id="de9f4-203">In the applications list, select **Skillport**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_app.png) 

3. <span data-ttu-id="de9f4-205">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="de9f4-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="de9f4-207">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="de9f4-207">Click **Add** button.</span></span> <span data-ttu-id="de9f4-208">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="de9f4-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="de9f4-210">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="de9f4-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="de9f4-211">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="de9f4-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="de9f4-212">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="de9f4-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="de9f4-213">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="de9f4-213">Testing single sign-on</span></span>

<span data-ttu-id="de9f4-214">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="de9f4-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="de9f4-215">Quand vous cliquez sur la vignette Skillport dans le volet d’accès, vous devez être connecté automatiquement à votre application Skillport.</span><span class="sxs-lookup"><span data-stu-id="de9f4-215">When you click the Skillport tile in the Access Panel, you should get automatically signed-on to your Skillport application.</span></span>
<span data-ttu-id="de9f4-216">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="de9f4-216">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="de9f4-217">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="de9f4-217">Additional resources</span></span>

* [<span data-ttu-id="de9f4-218">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="de9f4-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="de9f4-219">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="de9f4-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_203.png

