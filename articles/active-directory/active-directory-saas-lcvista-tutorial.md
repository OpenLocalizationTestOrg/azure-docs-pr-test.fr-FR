---
title: "Tutoriel : intégration d’Azure Active Directory à LCVista | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et LCVista."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8db80d6e-3275-419f-aa39-6115a7bc9800
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: jeedes
ms.openlocfilehash: c19f81da495eb7116b62797d1755d312a23f3805
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lcvista"></a><span data-ttu-id="ac375-103">Tutoriel : Intégration d’Azure Active Directory à LCVista</span><span class="sxs-lookup"><span data-stu-id="ac375-103">Tutorial: Azure Active Directory integration with LCVista</span></span>

<span data-ttu-id="ac375-104">Dans ce tutoriel, vous allez apprendre à intégrer Azure Active Directory (Azure AD) dans LCVista.</span><span class="sxs-lookup"><span data-stu-id="ac375-104">In this tutorial, you learn how to integrate LCVista with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ac375-105">L’intégration de LCVista dans Azure AD offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="ac375-105">Integrating LCVista with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ac375-106">Azure AD vous permet de contrôler l’accès à LCVista</span><span class="sxs-lookup"><span data-stu-id="ac375-106">You can control in Azure AD who has access to LCVista</span></span>
- <span data-ttu-id="ac375-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à LCVista (via l'authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="ac375-107">You can enable your users to automatically get signed-on to LCVista (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ac375-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="ac375-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ac375-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ac375-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ac375-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ac375-110">Prerequisites</span></span>

<span data-ttu-id="ac375-111">Pour configurer l'intégration d'Azure AD avec LCVista, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="ac375-111">To configure Azure AD integration with LCVista, you need the following items:</span></span>

- <span data-ttu-id="ac375-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="ac375-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ac375-113">Un abonnement LCVista pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="ac375-113">A LCVista single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ac375-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="ac375-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ac375-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ac375-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ac375-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="ac375-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ac375-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ac375-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ac375-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="ac375-118">Scenario description</span></span>
<span data-ttu-id="ac375-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="ac375-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ac375-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="ac375-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ac375-121">Ajout de LCVista à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="ac375-121">Adding LCVista from the gallery</span></span>
2. <span data-ttu-id="ac375-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ac375-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lcvista-from-the-gallery"></a><span data-ttu-id="ac375-123">Ajout de LCVista à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="ac375-123">Adding LCVista from the gallery</span></span>
<span data-ttu-id="ac375-124">Pour configurer l'intégration de LCVista avec Azure AD, vous devez ajouter LCVista disponible dans la galerie, à votre liste d'applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="ac375-124">To configure the integration of LCVista into Azure AD, you need to add LCVista from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ac375-125">**Pour ajouter LCVista à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ac375-125">**To add LCVista from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ac375-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ac375-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ac375-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="ac375-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ac375-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="ac375-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="ac375-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="ac375-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="ac375-133">Dans la zone de recherche, entrez **LCVista**.</span><span class="sxs-lookup"><span data-stu-id="ac375-133">In the search box, type **LCVista**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_search.png)

5. <span data-ttu-id="ac375-135">Dans le panneau des résultats, sélectionnez **LCVista**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="ac375-135">In the results panel, select **LCVista**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ac375-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ac375-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ac375-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec LCVista, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="ac375-138">In this section, you configure and test Azure AD single sign-on with LCVista based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ac375-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur LCVista équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ac375-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LCVista is to a user in Azure AD.</span></span> <span data-ttu-id="ac375-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur LCVista associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="ac375-140">In other words, a link relationship between an Azure AD user and the related user in LCVista needs to be established.</span></span>

<span data-ttu-id="ac375-141">Pour ce faire, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **Username** (NomUtilisateur) dans LCVista.</span><span class="sxs-lookup"><span data-stu-id="ac375-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LCVista.</span></span>

<span data-ttu-id="ac375-142">Pour configurer et tester l’authentification unique Azure AD avec LCVista, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="ac375-142">To configure and test Azure AD single sign-on with LCVista, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ac375-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="ac375-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ac375-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ac375-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ac375-145">**[Création d’un utilisateur de test LCVista](#creating-a-lcvista-test-user)** pour avoir un équivalent de Britta Simon dans LCVista lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ac375-145">**[Creating a LCVista test user](#creating-a-lcvista-test-user)** - to have a counterpart of Britta Simon in LCVista that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ac375-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ac375-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ac375-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="ac375-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ac375-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ac375-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ac375-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application LCVista.</span><span class="sxs-lookup"><span data-stu-id="ac375-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LCVista application.</span></span>

<span data-ttu-id="ac375-150">**Pour configurer l’authentification unique Azure AD avec LCVista, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ac375-150">**To configure Azure AD single sign-on with LCVista, perform the following steps:**</span></span>

1. <span data-ttu-id="ac375-151">Dans le portail Azure, sur la page d’intégration de l’application **LCVista**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="ac375-151">In the Azure portal, on the **LCVista** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="ac375-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="ac375-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_samlbase.png)

3. <span data-ttu-id="ac375-155">Dans la section **Domaine et URL LCVista**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ac375-155">On the **LCVista Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_url.png)

    <span data-ttu-id="ac375-157">a.</span><span class="sxs-lookup"><span data-stu-id="ac375-157">a.</span></span> <span data-ttu-id="ac375-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<subdomain>.lcvista.com/rainier/login`</span><span class="sxs-lookup"><span data-stu-id="ac375-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.lcvista.com/rainier/login`</span></span>

    <span data-ttu-id="ac375-159">b.</span><span class="sxs-lookup"><span data-stu-id="ac375-159">b.</span></span> <span data-ttu-id="ac375-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<subdomain>.lcvista.com`</span><span class="sxs-lookup"><span data-stu-id="ac375-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.lcvista.com`</span></span> 
     
    > [!NOTE] 
    > <span data-ttu-id="ac375-161">Il ne s’agit pas des valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="ac375-161">These values are not the real.</span></span> <span data-ttu-id="ac375-162">Mettez à jour ces valeurs avec l’identificateur et l’URL de connexion réels.</span><span class="sxs-lookup"><span data-stu-id="ac375-162">Update these values with the actual Identifier and Sign-On URL.</span></span> <span data-ttu-id="ac375-163">Pour obtenir ces valeurs, contactez l’[équipe de support technique LCVista](https://lcvista.com/contact).</span><span class="sxs-lookup"><span data-stu-id="ac375-163">Contact [LCVista Client support team](https://lcvista.com/contact) to get these values.</span></span> 

4. <span data-ttu-id="ac375-164">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="ac375-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_certificate.png) 

5. <span data-ttu-id="ac375-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="ac375-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lcvista-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="ac375-168">Dans la section **Configuration de LCVista**, cliquez sur **Configurer LCVista** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="ac375-168">On the **LCVista Configuration** section, click **Configure LCVista** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ac375-169">Copiez **l’ID d’entité SAML** et **l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="ac375-169">Copy the **SAML Entity ID** and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_configure.png) 

7.  <span data-ttu-id="ac375-171">Connectez-vous à votre application LCVista en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="ac375-171">Sign on to your LCVista application as an administrator.</span></span>

8. <span data-ttu-id="ac375-172">Dans la section **SAML Config** (Configuration SAML), cochez la case **Enable SAML login** (Activer la connexion SAML), puis entrez les informations détaillées, comme indiqué dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="ac375-172">In the **SAML Config** section, check the **Enable SAML login** and enter the details as mentioned in below image.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_config.png)

    <span data-ttu-id="ac375-174">a.</span><span class="sxs-lookup"><span data-stu-id="ac375-174">a.</span></span> <span data-ttu-id="ac375-175">Collez l’**URL de l’émetteur** que vous avez copiée à partir d’Azure AD dans la section **ID d’entité**.</span><span class="sxs-lookup"><span data-stu-id="ac375-175">Paste the **Issuer URL** which you have copied from Azure AD in the **Entity ID** section.</span></span> 

    <span data-ttu-id="ac375-176">b.</span><span class="sxs-lookup"><span data-stu-id="ac375-176">b.</span></span> <span data-ttu-id="ac375-177">Collez l’**URL du service d’authentification unique** que vous avez copiée à partir d’Azure AD dans la section **URL**.</span><span class="sxs-lookup"><span data-stu-id="ac375-177">Paste the **Single Sign-On Service URL** which you have copied from Azure AD in the **URL** section.</span></span>

    <span data-ttu-id="ac375-178">c.</span><span class="sxs-lookup"><span data-stu-id="ac375-178">c.</span></span> <span data-ttu-id="ac375-179">Dans le fichier de métadonnées (XML) que vous avez téléchargé à partir du portail Azure, copiez la valeur de l’objet **X509Certificate** et collez-la dans la section **Certificat x509**.</span><span class="sxs-lookup"><span data-stu-id="ac375-179">From Metadata (XML) which you have downloaded from Azure portal, copy the value **X509Certificate** and paste it in the **x509 Certificate** section.</span></span>

    <span data-ttu-id="ac375-180">d.</span><span class="sxs-lookup"><span data-stu-id="ac375-180">d.</span></span> <span data-ttu-id="ac375-181">Dans la zone de texte **First Name Attribute** (Attribut de prénom) entrez la valeur `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="ac375-181">In the **First name attribute** textbox, paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>

    <span data-ttu-id="ac375-182">e.</span><span class="sxs-lookup"><span data-stu-id="ac375-182">e.</span></span> <span data-ttu-id="ac375-183">Dans la zone de texte **Last name attribute** (Attribut de nom), collez la valeur `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="ac375-183">In the **Last name attribute** textbox, paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>

    <span data-ttu-id="ac375-184">f.</span><span class="sxs-lookup"><span data-stu-id="ac375-184">f.</span></span> <span data-ttu-id="ac375-185">Dans la zone de texte **Email attribute** (Attribut d’email), collez la valeur `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="ac375-185">In the **Email attribute** textbox, paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="ac375-186">g.</span><span class="sxs-lookup"><span data-stu-id="ac375-186">g.</span></span> <span data-ttu-id="ac375-187">Dans la zone de texte **Username attribute** (Attribut de nom d’utilisateur), collez la valeur `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="ac375-187">In the **Username attribute** textbox, paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>

    <span data-ttu-id="ac375-188">e.</span><span class="sxs-lookup"><span data-stu-id="ac375-188">e.</span></span> <span data-ttu-id="ac375-189">Cliquez sur **Enregistrer** pour enregistrer les paramètres.</span><span class="sxs-lookup"><span data-stu-id="ac375-189">Click **Save** to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="ac375-190">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="ac375-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ac375-191">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="ac375-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ac375-192">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ac375-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ac375-193">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="ac375-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="ac375-194">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ac375-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="ac375-196">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ac375-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ac375-197">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ac375-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lcvista-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ac375-199">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="ac375-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lcvista-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ac375-201">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="ac375-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lcvista-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ac375-203">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ac375-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lcvista-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ac375-205">a.</span><span class="sxs-lookup"><span data-stu-id="ac375-205">a.</span></span> <span data-ttu-id="ac375-206">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ac375-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ac375-207">b.</span><span class="sxs-lookup"><span data-stu-id="ac375-207">b.</span></span> <span data-ttu-id="ac375-208">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ac375-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ac375-209">c.</span><span class="sxs-lookup"><span data-stu-id="ac375-209">c.</span></span> <span data-ttu-id="ac375-210">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="ac375-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ac375-211">d.</span><span class="sxs-lookup"><span data-stu-id="ac375-211">d.</span></span> <span data-ttu-id="ac375-212">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="ac375-212">Click **Create**.</span></span>
 
### <a name="creating-a-lcvista-test-user"></a><span data-ttu-id="ac375-213">Création d’un utilisateur de test LCVista</span><span class="sxs-lookup"><span data-stu-id="ac375-213">Creating a LCVista test user</span></span>

<span data-ttu-id="ac375-214">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans LCVista.</span><span class="sxs-lookup"><span data-stu-id="ac375-214">In this section, you create a user called Britta Simon in LCVista.</span></span> <span data-ttu-id="ac375-215">Vous devez contactez l’[équipe de support technique LCVista](https://lcvista.com/contact) pour ajouter des utilisateurs dans l’application LCVista.</span><span class="sxs-lookup"><span data-stu-id="ac375-215">You need to contact [LCVista Client support team](https://lcvista.com/contact) to add the users in the LCVista application.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ac375-216">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="ac375-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ac375-217">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à LCVista.</span><span class="sxs-lookup"><span data-stu-id="ac375-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LCVista.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="ac375-219">**Pour affecter Britta Simon à LCVista, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ac375-219">**To assign Britta Simon to LCVista, perform the following steps:**</span></span>

1. <span data-ttu-id="ac375-220">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="ac375-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="ac375-222">Dans la liste des applications, sélectionnez **LCVista**.</span><span class="sxs-lookup"><span data-stu-id="ac375-222">In the applications list, select **LCVista**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_app.png) 

3. <span data-ttu-id="ac375-224">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="ac375-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="ac375-226">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="ac375-226">Click **Add** button.</span></span> <span data-ttu-id="ac375-227">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="ac375-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="ac375-229">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="ac375-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ac375-230">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="ac375-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ac375-231">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="ac375-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ac375-232">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="ac375-232">Testing single sign-on</span></span>

<span data-ttu-id="ac375-233">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="ac375-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span> <span data-ttu-id="ac375-234">Cliquez sur la vignette LCVista dans le volet d’accès. Vous êtes redirigé vers la page Organization sign on (Authentification d’organisation).</span><span class="sxs-lookup"><span data-stu-id="ac375-234">Click the LCVista tile in the Access Panel, you will be redirected to Organization sign on page.</span></span> <span data-ttu-id="ac375-235">Une fois authentifié, vous êtes connecté à votre application LCVista.</span><span class="sxs-lookup"><span data-stu-id="ac375-235">After successful login, you will be signed-on to your LCVista application.</span></span> <span data-ttu-id="ac375-236">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="ac375-236">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ac375-237">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="ac375-237">Additional resources</span></span>

* [<span data-ttu-id="ac375-238">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ac375-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ac375-239">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="ac375-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_203.png

