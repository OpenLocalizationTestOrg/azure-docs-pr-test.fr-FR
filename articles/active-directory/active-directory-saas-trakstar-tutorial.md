---
title: "Didacticiel : intégration d’Azure Active Directory à Trakstar | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Trakstar."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 411cb8c3-95c6-4138-acf2-ffc7f663e89a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 757429aa187e6536489b6636a0a11d122c7f9378
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-trakstar"></a><span data-ttu-id="a34bc-103">Didacticiel : Intégration d’Azure Active Directory à Trakstar</span><span class="sxs-lookup"><span data-stu-id="a34bc-103">Tutorial: Azure Active Directory integration with Trakstar</span></span>

<span data-ttu-id="a34bc-104">Dans ce didacticiel, vous allez apprendre à intégrer Trakstar à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a34bc-104">In this tutorial, you learn how to integrate Trakstar with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a34bc-105">L’intégration de Trakstar dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="a34bc-105">Integrating Trakstar with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a34bc-106">Dans Azure AD, vous pouvez contrôler qui a accès à Trakstar</span><span class="sxs-lookup"><span data-stu-id="a34bc-106">You can control in Azure AD who has access to Trakstar</span></span>
- <span data-ttu-id="a34bc-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Trakstar (par le biais de l'authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="a34bc-107">You can enable your users to automatically get signed-on to Trakstar (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a34bc-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="a34bc-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a34bc-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a34bc-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a34bc-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a34bc-110">Prerequisites</span></span>

<span data-ttu-id="a34bc-111">Pour configurer l'intégration d'Azure AD avec Trakstar, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="a34bc-111">To configure Azure AD integration with Trakstar, you need the following items:</span></span>

- <span data-ttu-id="a34bc-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="a34bc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a34bc-113">Un abonnement Trakstar pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="a34bc-113">A Trakstar single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a34bc-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="a34bc-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a34bc-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="a34bc-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a34bc-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="a34bc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a34bc-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a34bc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a34bc-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="a34bc-118">Scenario description</span></span>
<span data-ttu-id="a34bc-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="a34bc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a34bc-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="a34bc-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a34bc-121">Ajout de Trakstar à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="a34bc-121">Adding Trakstar from the gallery</span></span>
2. <span data-ttu-id="a34bc-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a34bc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-trakstar-from-the-gallery"></a><span data-ttu-id="a34bc-123">Ajout de Trakstar à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="a34bc-123">Adding Trakstar from the gallery</span></span>
<span data-ttu-id="a34bc-124">Pour configurer l'intégration de Trakstar avec Azure AD, vous devez ajouter Trakstar à partir de la galerie à votre liste d'applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="a34bc-124">To configure the integration of Trakstar into Azure AD, you need to add Trakstar from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a34bc-125">**Pour ajouter Trakstar à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a34bc-125">**To add Trakstar from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a34bc-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a34bc-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a34bc-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="a34bc-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a34bc-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="a34bc-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="a34bc-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="a34bc-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="a34bc-133">Dans la zone de recherche, tapez **Trakstar**.</span><span class="sxs-lookup"><span data-stu-id="a34bc-133">In the search box, type **Trakstar**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_search.png)

5. <span data-ttu-id="a34bc-135">Dans le panneau de résultats, sélectionnez **Trakstar**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="a34bc-135">In the results panel, select **Trakstar**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a34bc-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a34bc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a34bc-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Trakstar, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="a34bc-138">In this section, you configure and test Azure AD single sign-on with Trakstar based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a34bc-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Trakstar équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a34bc-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Trakstar is to a user in Azure AD.</span></span> <span data-ttu-id="a34bc-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Trakstar associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="a34bc-140">In other words, a link relationship between an Azure AD user and the related user in Trakstar needs to be established.</span></span>

<span data-ttu-id="a34bc-141">Dans Trakstar, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="a34bc-141">In Trakstar, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a34bc-142">Pour configurer et tester l’authentification unique Azure AD avec Trakstar, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="a34bc-142">To configure and test Azure AD single sign-on with Trakstar, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a34bc-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="a34bc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a34bc-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a34bc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a34bc-145">**[Création d'un utilisateur de test Trakstar](#creating-a-trakstar-test-user)** pour avoir un équivalent de Britta Simon dans Trakstar lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="a34bc-145">**[Creating a Trakstar test user](#creating-a-trakstar-test-user)** - to have a counterpart of Britta Simon in Trakstar that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a34bc-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a34bc-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a34bc-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="a34bc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a34bc-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a34bc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a34bc-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le nouveau portail Azure et configurer l’authentification unique dans votre application Trakstar.</span><span class="sxs-lookup"><span data-stu-id="a34bc-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Trakstar application.</span></span>

<span data-ttu-id="a34bc-150">**Pour configurer l'authentification unique Azure AD avec Trakstar, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a34bc-150">**To configure Azure AD single sign-on with Trakstar, perform the following steps:**</span></span>

1. <span data-ttu-id="a34bc-151">Dans le portail Azure, sur la page d’intégration de l’application **Trakstar**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="a34bc-151">In the Azure portal, on the **Trakstar** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="a34bc-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="a34bc-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_samlbase.png)

3. <span data-ttu-id="a34bc-155">Dans la section **Domaine et URL Trakstar**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="a34bc-155">On the **Trakstar Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_url.png)

    <span data-ttu-id="a34bc-157">a.</span><span class="sxs-lookup"><span data-stu-id="a34bc-157">a.</span></span> <span data-ttu-id="a34bc-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://app.trakstar.com/auth/saml/callback?namespace=<NAMESPACE>`</span><span class="sxs-lookup"><span data-stu-id="a34bc-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://app.trakstar.com/auth/saml/callback?namespace=<NAMESPACE>`</span></span>

    <span data-ttu-id="a34bc-159">b.</span><span class="sxs-lookup"><span data-stu-id="a34bc-159">b.</span></span> <span data-ttu-id="a34bc-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<subdomain>.trakstar.com`</span><span class="sxs-lookup"><span data-stu-id="a34bc-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.trakstar.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a34bc-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="a34bc-161">These values are not real.</span></span> <span data-ttu-id="a34bc-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="a34bc-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a34bc-163">Pour obtenir ces valeurs, contactez l’[équipe de support technique Trakstar](mailto:integrations@trakstar.com).</span><span class="sxs-lookup"><span data-stu-id="a34bc-163">Contact [Trakstar Client support team](mailto:integrations@trakstar.com) to get these values.</span></span> 
 
4. <span data-ttu-id="a34bc-164">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="a34bc-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_certificate.png) 

5. <span data-ttu-id="a34bc-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="a34bc-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-trakstar-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a34bc-168">Dans la section **Configuration de Trakstar**, cliquez sur **Configurer Trakstar** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="a34bc-168">On the **Trakstar Configuration** section, click **Configure Trakstar** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a34bc-169">Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="a34bc-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_configure.png) 

7. <span data-ttu-id="a34bc-171">Pour configurer l’authentification unique côté **Trakstar**, vous devez envoyer le **Certificat (Base64)** téléchargé, l’**URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à l’[équipe de support Trakstar](mailto:integrations@trakstar.com).</span><span class="sxs-lookup"><span data-stu-id="a34bc-171">To configure single sign-on on **Trakstar** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Trakstar support team](mailto:integrations@trakstar.com).</span></span> 

> [!TIP]
> <span data-ttu-id="a34bc-172">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="a34bc-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a34bc-173">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="a34bc-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a34bc-174">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a34bc-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a34bc-175">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="a34bc-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="a34bc-176">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a34bc-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="a34bc-178">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a34bc-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a34bc-179">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a34bc-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-trakstar-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a34bc-181">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="a34bc-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-trakstar-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a34bc-183">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="a34bc-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-trakstar-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a34bc-185">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="a34bc-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-trakstar-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a34bc-187">a.</span><span class="sxs-lookup"><span data-stu-id="a34bc-187">a.</span></span> <span data-ttu-id="a34bc-188">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a34bc-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a34bc-189">b.</span><span class="sxs-lookup"><span data-stu-id="a34bc-189">b.</span></span> <span data-ttu-id="a34bc-190">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a34bc-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a34bc-191">c.</span><span class="sxs-lookup"><span data-stu-id="a34bc-191">c.</span></span> <span data-ttu-id="a34bc-192">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="a34bc-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a34bc-193">d.</span><span class="sxs-lookup"><span data-stu-id="a34bc-193">d.</span></span> <span data-ttu-id="a34bc-194">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="a34bc-194">Click **Create**.</span></span>
 
### <a name="creating-a-trakstar-test-user"></a><span data-ttu-id="a34bc-195">Création d'un utilisateur de test Trakstar</span><span class="sxs-lookup"><span data-stu-id="a34bc-195">Creating a Trakstar test user</span></span>

<span data-ttu-id="a34bc-196">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans Trakstar.</span><span class="sxs-lookup"><span data-stu-id="a34bc-196">The objective of this section is to create a user called Britta Simon in Trakstar.</span></span> <span data-ttu-id="a34bc-197">Collaborez avec l’[équipe du support technique Trakstar](mailto:integrations@trakstar.com) pour ajouter des utilisateurs dans le compte Trakstar.</span><span class="sxs-lookup"><span data-stu-id="a34bc-197">Work with [Trakstar support team](mailto:integrations@trakstar.com) to add the users in the Trakstar account.</span></span> 


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a34bc-198">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="a34bc-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a34bc-199">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Trakstar.</span><span class="sxs-lookup"><span data-stu-id="a34bc-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Trakstar.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="a34bc-201">**Pour affecter Britta Simon à Trakstar, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a34bc-201">**To assign Britta Simon to Trakstar, perform the following steps:**</span></span>

1. <span data-ttu-id="a34bc-202">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="a34bc-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="a34bc-204">Dans la liste des applications, sélectionnez **Trakstar**.</span><span class="sxs-lookup"><span data-stu-id="a34bc-204">In the applications list, select **Trakstar**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_app.png) 

3. <span data-ttu-id="a34bc-206">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="a34bc-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="a34bc-208">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="a34bc-208">Click **Add** button.</span></span> <span data-ttu-id="a34bc-209">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="a34bc-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="a34bc-211">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="a34bc-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a34bc-212">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="a34bc-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a34bc-213">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="a34bc-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a34bc-214">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="a34bc-214">Testing single sign-on</span></span>

<span data-ttu-id="a34bc-215">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="a34bc-215">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="a34bc-216">Lorsque vous cliquez sur la mosaïque Trakstar dans le volet d'accès, vous devez être connecté automatiquement à votre application Trakstar.</span><span class="sxs-lookup"><span data-stu-id="a34bc-216">When you click the Trakstar tile in the Access Panel, you should get automatically signed-on to your Trakstar application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a34bc-217">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="a34bc-217">Additional resources</span></span>

* [<span data-ttu-id="a34bc-218">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a34bc-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a34bc-219">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="a34bc-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_203.png

