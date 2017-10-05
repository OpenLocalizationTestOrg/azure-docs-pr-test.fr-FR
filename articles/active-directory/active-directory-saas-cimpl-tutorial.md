---
title: "Didacticiel : intégration d’Azure Active Directory à Cimpl | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Cimpl."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 58ee5481-ae40-4e4a-a3c9-86343851fc9a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: 24a0c89966c83e1b32367d4519ead98d76f5ac6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cimpl"></a><span data-ttu-id="6d95e-103">Didacticiel : Intégration d’Azure Active Directory à Cimpl</span><span class="sxs-lookup"><span data-stu-id="6d95e-103">Tutorial: Azure Active Directory integration with Cimpl</span></span>

<span data-ttu-id="6d95e-104">Dans ce didacticiel, vous allez apprendre à intégrer Cimpl à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6d95e-104">In this tutorial, you learn how to integrate Cimpl with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6d95e-105">L’intégration de Cimpl avec Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="6d95e-105">Integrating Cimpl with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6d95e-106">Dans Azure AD, vous pouvez contrôler qui a accès à Cimpl.</span><span class="sxs-lookup"><span data-stu-id="6d95e-106">You can control in Azure AD who has access to Cimpl</span></span>
- <span data-ttu-id="6d95e-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Cimpl (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6d95e-107">You can enable your users to automatically get signed-on to Cimpl (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6d95e-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="6d95e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6d95e-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6d95e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6d95e-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="6d95e-110">Prerequisites</span></span>

<span data-ttu-id="6d95e-111">Pour configurer l’intégration d’Azure AD à Cimpl, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="6d95e-111">To configure Azure AD integration with Cimpl, you need the following items:</span></span>

- <span data-ttu-id="6d95e-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="6d95e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6d95e-113">Un abonnement Cimpl pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="6d95e-113">A Cimpl single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6d95e-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="6d95e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6d95e-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="6d95e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6d95e-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="6d95e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6d95e-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6d95e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6d95e-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="6d95e-118">Scenario description</span></span>
<span data-ttu-id="6d95e-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="6d95e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6d95e-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="6d95e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6d95e-121">Ajout de Cimpl depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="6d95e-121">Adding Cimpl from the gallery</span></span>
2. <span data-ttu-id="6d95e-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="6d95e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cimpl-from-the-gallery"></a><span data-ttu-id="6d95e-123">Ajout de Cimpl depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="6d95e-123">Adding Cimpl from the gallery</span></span>
<span data-ttu-id="6d95e-124">Pour configurer l’intégration de Cimpl à Azure AD, vous devez ajouter Cimpl à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="6d95e-124">To configure the integration of Cimpl into Azure AD, you need to add Cimpl from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6d95e-125">**Pour ajouter Cimpl à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6d95e-125">**To add Cimpl from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6d95e-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6d95e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6d95e-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="6d95e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6d95e-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="6d95e-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="6d95e-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="6d95e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="6d95e-133">Dans la zone de recherche, tapez **Cimpl**.</span><span class="sxs-lookup"><span data-stu-id="6d95e-133">In the search box, type **Cimpl**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cimpl-tutorial/tutorial_cimpl_search.png)

5. <span data-ttu-id="6d95e-135">Dans le volet de résultats, sélectionnez **Cimpl**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="6d95e-135">In the results panel, select **Cimpl**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cimpl-tutorial/tutorial_cimpl_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6d95e-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="6d95e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6d95e-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Cimpl, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="6d95e-138">In this section, you configure and test Azure AD single sign-on with Cimpl based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6d95e-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Cimpl équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6d95e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Cimpl is to a user in Azure AD.</span></span> <span data-ttu-id="6d95e-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Cimpl associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="6d95e-140">In other words, a link relationship between an Azure AD user and the related user in Cimpl needs to be established.</span></span>

<span data-ttu-id="6d95e-141">Dans Cimpl, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="6d95e-141">In Cimpl, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6d95e-142">Pour configurer et tester l’authentification unique Azure AD avec Cimpl, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="6d95e-142">To configure and test Azure AD single sign-on with Cimpl, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6d95e-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="6d95e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6d95e-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6d95e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6d95e-145">**[Création d’un utilisateur de test Cimpl](#creating-a-cimpl-test-user)** pour avoir un équivalent de Britta Simon dans Cimpl, lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6d95e-145">**[Creating a Cimpl test user](#creating-a-cimpl-test-user)** - to have a counterpart of Britta Simon in Cimpl that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6d95e-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6d95e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6d95e-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="6d95e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6d95e-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="6d95e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6d95e-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Cimpl.</span><span class="sxs-lookup"><span data-stu-id="6d95e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cimpl application.</span></span>

<span data-ttu-id="6d95e-150">**Pour configurer l’authentification unique Azure AD avec Cimpl, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6d95e-150">**To configure Azure AD single sign-on with Cimpl, perform the following steps:**</span></span>

1. <span data-ttu-id="6d95e-151">Dans le portail Azure, dans la page d’intégration de l’application **Cimpl**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="6d95e-151">In the Azure portal, on the **Cimpl** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="6d95e-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="6d95e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-cimpl-tutorial/tutorial_cimpl_samlbase.png)

3. <span data-ttu-id="6d95e-155">Dans la section **Domaine et URL Cimpl**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="6d95e-155">On the **Cimpl Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cimpl-tutorial/tutorial_cimpl_url.png)

    <span data-ttu-id="6d95e-157">a.</span><span class="sxs-lookup"><span data-stu-id="6d95e-157">a.</span></span> <span data-ttu-id="6d95e-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://sso.etelesolv.com/<TENANTNAME>`</span><span class="sxs-lookup"><span data-stu-id="6d95e-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://sso.etelesolv.com/<TENANTNAME>`</span></span>

    <span data-ttu-id="6d95e-159">b.</span><span class="sxs-lookup"><span data-stu-id="6d95e-159">b.</span></span> <span data-ttu-id="6d95e-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://sso.etelesolv.com/<TENANTNAME>`</span><span class="sxs-lookup"><span data-stu-id="6d95e-160">In the **Identifier** textbox, type a URL using the following pattern: `https://sso.etelesolv.com/<TENANTNAME>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6d95e-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="6d95e-161">These values are not real.</span></span> <span data-ttu-id="6d95e-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="6d95e-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="6d95e-163">Pour obtenir ces valeurs, contactez l’équipe Cimpl en composant le **+1 866-982-8250**.</span><span class="sxs-lookup"><span data-stu-id="6d95e-163">Contact Cimpl team at **+1 866-982-8250** to get these values.</span></span> 
 
4. <span data-ttu-id="6d95e-164">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="6d95e-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cimpl-tutorial/tutorial_cimpl_certificate.png) 

5. <span data-ttu-id="6d95e-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="6d95e-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cimpl-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6d95e-168">Dans la section **Configuration de Cimpl**, cliquez sur **Configurer Cimpl** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="6d95e-168">On the **Cimpl Configuration** section, click **Configure Cimpl** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6d95e-169">Copiez **l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="6d95e-169">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cimpl-tutorial/tutorial_cimpl_configure.png) 

7. <span data-ttu-id="6d95e-171">Pour configurer l’authentification unique côté **Cimpl**, vous devez envoyer le **Certificat (Base64)** téléchargé, **l’URL du service d’authentification unique SAML et l’ID d’entité SAML** à l’équipe du support technique Cimpl en composant le **+1 866-982-8250**.</span><span class="sxs-lookup"><span data-stu-id="6d95e-171">To configure single sign-on on **Cimpl** side, you need to send the downloaded **Certificate (Base64)**, **SAML Entity ID, and SAML Single Sign-On Service URL** to Cimpl support at **+1 866-982-8250**.</span></span>


> [!TIP]
> <span data-ttu-id="6d95e-172">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="6d95e-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6d95e-173">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="6d95e-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6d95e-174">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6d95e-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6d95e-175">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="6d95e-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="6d95e-176">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="6d95e-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="6d95e-178">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6d95e-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6d95e-179">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6d95e-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cimpl-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6d95e-181">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="6d95e-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cimpl-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6d95e-183">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="6d95e-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cimpl-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6d95e-185">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="6d95e-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cimpl-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6d95e-187">a.</span><span class="sxs-lookup"><span data-stu-id="6d95e-187">a.</span></span> <span data-ttu-id="6d95e-188">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6d95e-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6d95e-189">b.</span><span class="sxs-lookup"><span data-stu-id="6d95e-189">b.</span></span> <span data-ttu-id="6d95e-190">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6d95e-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6d95e-191">c.</span><span class="sxs-lookup"><span data-stu-id="6d95e-191">c.</span></span> <span data-ttu-id="6d95e-192">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="6d95e-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6d95e-193">d.</span><span class="sxs-lookup"><span data-stu-id="6d95e-193">d.</span></span> <span data-ttu-id="6d95e-194">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="6d95e-194">Click **Create**.</span></span>
 
### <a name="creating-a-cimpl-test-user"></a><span data-ttu-id="6d95e-195">Création d’un utilisateur de test Cimpl</span><span class="sxs-lookup"><span data-stu-id="6d95e-195">Creating a Cimpl test user</span></span>

<span data-ttu-id="6d95e-196">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans Cimpl.</span><span class="sxs-lookup"><span data-stu-id="6d95e-196">The objective of this section is to create a user called Britta Simon in Cimpl.</span></span> <span data-ttu-id="6d95e-197">Collaborez avec l’équipe du support technique Cimpl en composant le **+1 866-982-8250** pour ajouter les utilisateurs au compte Cimpl.</span><span class="sxs-lookup"><span data-stu-id="6d95e-197">Work with Cimpl support at **+1 866-982-8250** to add the users in the Cimpl account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6d95e-198">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="6d95e-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6d95e-199">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Cimpl.</span><span class="sxs-lookup"><span data-stu-id="6d95e-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cimpl.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="6d95e-201">**Pour affecter Britta Simon à Cimpl, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6d95e-201">**To assign Britta Simon to Cimpl, perform the following steps:**</span></span>

1. <span data-ttu-id="6d95e-202">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="6d95e-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="6d95e-204">Dans la liste des applications, sélectionnez **Cimpl**.</span><span class="sxs-lookup"><span data-stu-id="6d95e-204">In the applications list, select **Cimpl**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cimpl-tutorial/tutorial_cimpl_app.png) 

3. <span data-ttu-id="6d95e-206">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="6d95e-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="6d95e-208">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="6d95e-208">Click **Add** button.</span></span> <span data-ttu-id="6d95e-209">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="6d95e-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="6d95e-211">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="6d95e-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6d95e-212">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="6d95e-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6d95e-213">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="6d95e-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6d95e-214">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="6d95e-214">Testing single sign-on</span></span>

<span data-ttu-id="6d95e-215">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="6d95e-215">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  <span data-ttu-id="6d95e-216">Lorsque vous cliquez sur la vignette Cimpl dans le volet d’accès, vous devez être connecté automatiquement à votre application Cimpl.</span><span class="sxs-lookup"><span data-stu-id="6d95e-216">When you click the Cimpl tile in the Access Panel, you should get automatically signed-on to your Cimpl application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6d95e-217">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="6d95e-217">Additional resources</span></span>

* [<span data-ttu-id="6d95e-218">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6d95e-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6d95e-219">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="6d95e-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cimpl-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cimpl-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cimpl-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cimpl-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cimpl-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cimpl-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cimpl-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cimpl-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cimpl-tutorial/tutorial_general_203.png

