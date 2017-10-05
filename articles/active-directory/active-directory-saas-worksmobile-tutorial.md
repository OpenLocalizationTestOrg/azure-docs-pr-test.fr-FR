---
title: "Didacticiel : Intégration d’Azure Active Directory à WORKS MOBILE | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et WORKS MOBILE."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 725f32fd-d0ad-49c7-b137-1cc246bf85d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 139a1968a59424eae278de3e7fa227ad340a1eb8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-works-mobile"></a><span data-ttu-id="4d7dd-103">Didacticiel : Intégration d’Azure Active Directory à WORKS MOBILE</span><span class="sxs-lookup"><span data-stu-id="4d7dd-103">Tutorial: Azure Active Directory integration with WORKS MOBILE</span></span>

<span data-ttu-id="4d7dd-104">Dans ce didacticiel, vous découvrez comment intégrer WORKS MOBILE à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4d7dd-104">In this tutorial, you learn how to integrate WORKS MOBILE with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4d7dd-105">L’intégration de WORKS MOBILE à Azure AD vous procure les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="4d7dd-105">Integrating WORKS MOBILE with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4d7dd-106">Vous pouvez contrôler dans Azure AD qui a accès à WORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-106">You can control in Azure AD who has access to WORKS MOBILE</span></span>
- <span data-ttu-id="4d7dd-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à WORKS MOBILE (par le biais de l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-107">You can enable your users to automatically get signed-on to WORKS MOBILE (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4d7dd-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="4d7dd-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4d7dd-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4d7dd-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4d7dd-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="4d7dd-110">Prerequisites</span></span>

<span data-ttu-id="4d7dd-111">Pour configurer l’intégration d’Azure AD à WORKS MOBILE, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="4d7dd-111">To configure Azure AD integration with WORKS MOBILE, you need the following items:</span></span>

- <span data-ttu-id="4d7dd-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d7dd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4d7dd-113">Un abonnement WORKS MOBILE pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="4d7dd-113">A WORKS MOBILE single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4d7dd-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4d7dd-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="4d7dd-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4d7dd-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4d7dd-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4d7dd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4d7dd-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="4d7dd-118">Scenario description</span></span>
<span data-ttu-id="4d7dd-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4d7dd-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="4d7dd-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4d7dd-121">Ajout de WORKS MOBILE à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="4d7dd-121">Adding WORKS MOBILE from the gallery</span></span>
2. <span data-ttu-id="4d7dd-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d7dd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-works-mobile-from-the-gallery"></a><span data-ttu-id="4d7dd-123">Ajout de WORKS MOBILE à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="4d7dd-123">Adding WORKS MOBILE from the gallery</span></span>
<span data-ttu-id="4d7dd-124">Pour configurer l’intégration de WORKS MOBILE dans Azure AD, vous devez ajouter WORKS MOBILE à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-124">To configure the integration of WORKS MOBILE into Azure AD, you need to add WORKS MOBILE from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4d7dd-125">**Pour ajouter WORKS MOBILE à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4d7dd-125">**To add WORKS MOBILE from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4d7dd-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4d7dd-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4d7dd-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="4d7dd-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="4d7dd-133">Dans la zone de recherche, tapez **WORKS MOBILE**.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-133">In the search box, type **WORKS MOBILE**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_search.png)

5. <span data-ttu-id="4d7dd-135">Dans le volet de résultats, sélectionnez **WORKS MOBILE**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-135">In the results panel, select **WORKS MOBILE**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4d7dd-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d7dd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4d7dd-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec WORKS MOBILE grâce à un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="4d7dd-138">In this section, you configure and test Azure AD single sign-on with WORKS MOBILE based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4d7dd-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur WORKS MOBILE équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-139">For single sign-on to work, Azure AD needs to know what the counterpart user in WORKS MOBILE is to a user in Azure AD.</span></span> <span data-ttu-id="4d7dd-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur WORKS MOBILE associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-140">In other words, a link relationship between an Azure AD user and the related user in WORKS MOBILE needs to be established.</span></span>

<span data-ttu-id="4d7dd-141">Pour ce faire, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur de **Username** dans WORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in WORKS MOBILE.</span></span>

<span data-ttu-id="4d7dd-142">Pour configurer et tester l’authentification unique Azure AD avec WORKS MOBILE, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="4d7dd-142">To configure and test Azure AD single sign-on with WORKS MOBILE, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4d7dd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4d7dd-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4d7dd-145">**[Création d’un utilisateur de test WORKS MOBILE](#creating-a-works-mobile-test-user)** pour avoir un équivalent de Britta Simon dans WORKS MOBILE qui est lié à la représentation d’un utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-145">**[Creating a WORKS MOBILE test user](#creating-a-works-mobile-test-user)** - to have a counterpart of Britta Simon in WORKS MOBILE that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4d7dd-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4d7dd-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4d7dd-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d7dd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4d7dd-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application WORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your WORKS MOBILE application.</span></span>

<span data-ttu-id="4d7dd-150">**Pour configurer l’authentification unique Azure AD avec WORKS MOBILE, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4d7dd-150">**To configure Azure AD single sign-on with WORKS MOBILE, perform the following steps:**</span></span>

1. <span data-ttu-id="4d7dd-151">Dans le portail Azure, sur la page d’intégration de l’application **WORKS MOBILE**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-151">In the Azure portal, on the **WORKS MOBILE** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="4d7dd-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_samlbase.png)

3. <span data-ttu-id="4d7dd-155">Dans la section **Domaine et URL WORKS MOBILE**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="4d7dd-155">On the **WORKS MOBILE Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_url.png)

    <span data-ttu-id="4d7dd-157">a.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-157">a.</span></span> <span data-ttu-id="4d7dd-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<subdomain>.worksmobile.com/jp/myservice`</span><span class="sxs-lookup"><span data-stu-id="4d7dd-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.worksmobile.com/jp/myservice`</span></span>

    <span data-ttu-id="4d7dd-159">b.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-159">b.</span></span> <span data-ttu-id="4d7dd-160">Dans la zone de texte **Identificateur**, entrez la valeur `worksmobile.com`.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-160">In the **Identifier** textbox, type the value as `worksmobile.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4d7dd-161">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-161">This value is not real.</span></span> <span data-ttu-id="4d7dd-162">Mettez à jour cette valeur avec l’URL de connexion réelle.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-162">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="4d7dd-163">Pour obtenir cette valeur, contactez [l’équipe de support technique WORKS MOBILE](mailto:dl_ssoinfo@worksmobile.com).</span><span class="sxs-lookup"><span data-stu-id="4d7dd-163">Contact [WORKS MOBILE Client support team](mailto:dl_ssoinfo@worksmobile.com) to get this value.</span></span> 
 
4. <span data-ttu-id="4d7dd-164">Dans la section **Certificat de signature SAML**, cliquez sur **Certificat (brut)**, puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-164">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_certificate.png) 

5. <span data-ttu-id="4d7dd-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="4d7dd-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-worksmobile-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4d7dd-168">Dans la section **Configuration de WORKS MOBILE** , cliquez sur **Configurer WORKS MOBILE** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-168">On the **WORKS MOBILE Configuration** section, click **Configure WORKS MOBILE** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4d7dd-169">Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="4d7dd-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_configure.png) 

7. <span data-ttu-id="4d7dd-171">Pour obtenir la configuration de l’authentification unique pour votre application, contactez [l’équipe de support WORKS MOBILE](mailto:dl_ssoinfo@worksmobile.com) et fournissez-lui les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="4d7dd-171">To get SSO configured for your application, contact [WORKS MOBILE support team](mailto:dl_ssoinfo@worksmobile.com) and provide them with the following information:</span></span> 

    <span data-ttu-id="4d7dd-172">• Le **fichier de certificat** téléchargé</span><span class="sxs-lookup"><span data-stu-id="4d7dd-172">• The downloaded **Certificate file**</span></span>

    <span data-ttu-id="4d7dd-173">• **L’URL du service d’authentification unique SAML**</span><span class="sxs-lookup"><span data-stu-id="4d7dd-173">• The **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="4d7dd-174">• **L’ID d’entité SAML**</span><span class="sxs-lookup"><span data-stu-id="4d7dd-174">• The **SAML Entity ID**</span></span>

    <span data-ttu-id="4d7dd-175">• **L’URL de déconnexion**</span><span class="sxs-lookup"><span data-stu-id="4d7dd-175">• The **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="4d7dd-176">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-176">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4d7dd-177">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-177">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4d7dd-178">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4d7dd-178">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4d7dd-179">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d7dd-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="4d7dd-180">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-180">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="4d7dd-182">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4d7dd-182">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4d7dd-183">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-183">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4d7dd-185">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-185">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4d7dd-187">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-187">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4d7dd-189">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="4d7dd-189">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4d7dd-191">a.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-191">a.</span></span> <span data-ttu-id="4d7dd-192">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-192">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4d7dd-193">b.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-193">b.</span></span> <span data-ttu-id="4d7dd-194">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-194">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4d7dd-195">c.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-195">c.</span></span> <span data-ttu-id="4d7dd-196">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-196">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4d7dd-197">d.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-197">d.</span></span> <span data-ttu-id="4d7dd-198">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-198">Click **Create**.</span></span>
 
### <a name="creating-a-works-mobile-test-user"></a><span data-ttu-id="4d7dd-199">Création d’un utilisateur de test WORKS MOBILE</span><span class="sxs-lookup"><span data-stu-id="4d7dd-199">Creating a WORKS MOBILE test user</span></span>

 <span data-ttu-id="4d7dd-200">Dans cette section, vous créez un utilisateur appelé Britta Simon dans WORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-200">In this section, you create a user called Britta Simon in WORKS MOBILE.</span></span> <span data-ttu-id="4d7dd-201">Collaborez avec [l’équipe du support technique WORKS MOBILE](mailto:dl_ssoinfo@worksmobile.com) pour ajouter des utilisateurs dans la plateforme WORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-201">Please work with [WORKS MOBILE support team](mailto:dl_ssoinfo@worksmobile.com) to add the users in the WORKS MOBILE platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4d7dd-202">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d7dd-202">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4d7dd-203">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à WORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-203">In this section, you enable Britta Simon to use Azure single sign-on by granting access to WORKS MOBILE.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="4d7dd-205">**Pour affecter Britta Simon à WORKS MOBILE, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4d7dd-205">**To assign Britta Simon to WORKS MOBILE, perform the following steps:**</span></span>

1. <span data-ttu-id="4d7dd-206">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-206">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="4d7dd-208">Dans la liste des applications, sélectionnez **WORKS MOBILE**.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-208">In the applications list, select **WORKS MOBILE**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_app.png) 

3. <span data-ttu-id="4d7dd-210">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-210">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="4d7dd-212">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-212">Click **Add** button.</span></span> <span data-ttu-id="4d7dd-213">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="4d7dd-215">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-215">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4d7dd-216">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4d7dd-217">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4d7dd-218">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="4d7dd-218">Testing single sign-on</span></span>

<span data-ttu-id="4d7dd-219">Dans cette section, vous allez tester la configuration SSO Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-219">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="4d7dd-220">Quand vous cliquez sur la vignette WORKS MOBILE dans le panneau d’accès, vous devez être connecté automatiquement à votre application WORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="4d7dd-220">When you click the WORKS MOBILE tile in the Access Panel, you should get automatically signed-on to your WORKS MOBILE application.</span></span>
<span data-ttu-id="4d7dd-221">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4d7dd-221">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4d7dd-222">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="4d7dd-222">Additional resources</span></span>

* [<span data-ttu-id="4d7dd-223">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4d7dd-223">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4d7dd-224">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="4d7dd-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_203.png

