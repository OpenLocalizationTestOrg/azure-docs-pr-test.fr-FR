---
title: "Didacticiel : intégration d’Azure Active Directory à la formation de sensibilisation à la sécurité KnowBe4 | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et la formation de sensibilisation à la sécurité KnowBe4."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b80d2212-cc5f-4adb-836c-570640810c39
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: 3b18737112a8aef101fab7fac1904f7c2e194d64
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-knowbe4-security-awareness-training"></a><span data-ttu-id="33637-103">Didacticiel : intégration d’Azure Active Directory à la formation de sensibilisation à la sécurité KnowBe4</span><span class="sxs-lookup"><span data-stu-id="33637-103">Tutorial: Azure Active Directory integration with KnowBe4 Security Awareness Training</span></span>

<span data-ttu-id="33637-104">Dans ce didacticiel, vous allez apprendre à intégrer la formation de sensibilisation à la sécurité KnowBe4 à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="33637-104">In this tutorial, you learn how to integrate KnowBe4 Security Awareness Training with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="33637-105">L’intégration de la formation de sensibilisation à la sécurité KnowBe4 à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="33637-105">Integrating KnowBe4 Security Awareness Training with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="33637-106">Dans Azure AD, vous pouvez contrôler qui a accès à la formation de sensibilisation à la sécurité KnowBe4</span><span class="sxs-lookup"><span data-stu-id="33637-106">You can control in Azure AD who has access to KnowBe4 Security Awareness Training</span></span>
- <span data-ttu-id="33637-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à la formation de sensibilisation à la sécurité KnowBe4 (via l’authentification unique) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="33637-107">You can enable your users to automatically get signed-on to KnowBe4 Security Awareness Training (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="33637-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="33637-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="33637-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="33637-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="33637-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="33637-110">Prerequisites</span></span>

<span data-ttu-id="33637-111">Pour configurer l’intégration d’Azure AD à la formation de sensibilisation à la sécurité KnowBe4, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="33637-111">To configure Azure AD integration with KnowBe4 Security Awareness Training, you need the following items:</span></span>

- <span data-ttu-id="33637-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="33637-112">An Azure AD subscription</span></span>
- <span data-ttu-id="33637-113">Un abonnement à la formation de sensibilisation à la sécurité KnowBe4 pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="33637-113">A KnowBe4 Security Awareness Training single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="33637-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="33637-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="33637-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="33637-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="33637-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="33637-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="33637-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="33637-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="33637-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="33637-118">Scenario description</span></span>
<span data-ttu-id="33637-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="33637-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="33637-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="33637-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="33637-121">Ajout de la formation de sensibilisation à la sécurité KnowBe4 à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="33637-121">Adding KnowBe4 Security Awareness Training from the gallery</span></span>
2. <span data-ttu-id="33637-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="33637-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-knowbe4-security-awareness-training-from-the-gallery"></a><span data-ttu-id="33637-123">Ajout de la formation de sensibilisation à la sécurité KnowBe4 à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="33637-123">Adding KnowBe4 Security Awareness Training from the gallery</span></span>
<span data-ttu-id="33637-124">Pour configurer l’intégration de la formation de sensibilisation à la sécurité KnowBe4 à Azure AD, vous devez ajouter la formation de sensibilisation à la sécurité KnowBe4 à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="33637-124">To configure the integration of KnowBe4 Security Awareness Training into Azure AD, you need to add KnowBe4 Security Awareness Training from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="33637-125">**Pour ajouter la formation de sensibilisation à la sécurité KnowBe4 à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="33637-125">**To add KnowBe4 Security Awareness Training from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="33637-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="33637-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="33637-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="33637-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="33637-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="33637-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="33637-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="33637-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="33637-133">Dans la zone de recherche, tapez **Formation de sensibilisation à la sécurité KnowBe4**.</span><span class="sxs-lookup"><span data-stu-id="33637-133">In the search box, type **KnowBe4 Security Awareness Training**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_search.png)

5. <span data-ttu-id="33637-135">Dans le volet des résultats, sélectionnez **Formation de sensibilisation à la sécurité KnowBe4**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="33637-135">In the results panel, select **KnowBe4 Security Awareness Training**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="33637-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="33637-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="33637-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec la formation de sensibilisation à la sécurité KnowBe4, sur un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="33637-138">In this section, you configure and test Azure AD single sign-on with KnowBe4 Security Awareness Training based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="33637-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur de la formation de sensibilisation à la sécurité KnowBe4 équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="33637-139">For single sign-on to work, Azure AD needs to know what the counterpart user in KnowBe4 Security Awareness Training is to a user in Azure AD.</span></span> <span data-ttu-id="33637-140">En d’autres termes, une relation entre un utilisateur Azure AD et l’utilisateur de la formation de sensibilisation à la sécurité KnowBe4 associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="33637-140">In other words, a link relationship between an Azure AD user and the related user in KnowBe4 Security Awareness Training needs to be established.</span></span>

<span data-ttu-id="33637-141">Dans la formation de sensibilisation à la sécurité KnowBe4, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur**Nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="33637-141">In KnowBe4 Security Awareness Training, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="33637-142">Pour configurer et tester l’authentification unique Azure AD avec la formation de sensibilisation à la sécurité KnowBe4, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="33637-142">To configure and test Azure AD single sign-on with KnowBe4 Security Awareness Training, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="33637-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="33637-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="33637-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="33637-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="33637-145">**[Création d’un utilisateur de test de la formation de sensibilisation à la sécurité KnowBe4](#creating-a-knowbe4-security-awareness-training-test-user)** : pour avoir un équivalent de Britta Simon dans la formation de sensibilisation à la sécurité KnowBe4, lié à la représentation de l’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="33637-145">**[Creating a KnowBe4 Security Awareness Training test user](#creating-a-knowbe4-security-awareness-training-test-user)** - to have a counterpart of Britta Simon in KnowBe4 Security Awareness Training that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="33637-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="33637-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="33637-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="33637-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="33637-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="33637-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="33637-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Formation à la sensibilisation à la sécurité KnowBe4.</span><span class="sxs-lookup"><span data-stu-id="33637-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your KnowBe4 Security Awareness Training application.</span></span>

<span data-ttu-id="33637-150">**Pour configurer l’authentification unique Azure AD avec la formation de sensibilisation à la sécurité KnowBe4, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="33637-150">**To configure Azure AD single sign-on with KnowBe4 Security Awareness Training, perform the following steps:**</span></span>

1. <span data-ttu-id="33637-151">Dans le portail Azure, dans la page d’intégration de l’application **Formation de sensibilisation à la sécurité KnowBe4**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="33637-151">In the Azure portal, on the **KnowBe4 Security Awareness Training** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="33637-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="33637-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_samlbase.png)

3. <span data-ttu-id="33637-155">Dans la section **Domaine et URL de la formation de sensibilisation à la sécurité KnowBe4**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="33637-155">On the **KnowBe4 Security Awareness Training Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_url.png)

    <span data-ttu-id="33637-157">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<companyname>.KnowBe4.com/auth/saml/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="33637-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.KnowBe4.com/auth/saml/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="33637-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="33637-158">The value is not real.</span></span> <span data-ttu-id="33637-159">Mettez à jour la valeur avec l’URL de connexion réelle.</span><span class="sxs-lookup"><span data-stu-id="33637-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="33637-160">Contactez [l’équipe de support client de formation de sensibilisation à la sécurité KnowBe4](mailto:support@KnowBe4.com) pour obtenir la valeur.</span><span class="sxs-lookup"><span data-stu-id="33637-160">Contact [KnowBe4 Security Awareness Training Client support team](mailto:support@KnowBe4.com) to get the value.</span></span> 
 

4. <span data-ttu-id="33637-161">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (brut)**, puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="33637-161">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_certificate.png) 

5. <span data-ttu-id="33637-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="33637-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="33637-165">Dans la section **Configuration de la formation de sensibilisation à la sécurité KnowBe4**, cliquez sur **Configurer la formation de sensibilisation à la sécurité KnowBe4** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="33637-165">On the **KnowBe4 Security Awareness Training Configuration** section, click **Configure KnowBe4 Security Awareness Training** to open **Configure sign-on** window.</span></span> <span data-ttu-id="33637-166">Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="33637-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_configure.png) 

7. <span data-ttu-id="33637-168">Pour configurer l’authentification unique du côté de la **formation de sensibilisation à la sécurité KnowBe4**, vous devez envoyer le **Certificat (brut)** téléchargé et **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à [l’équipe de support client de la formation de sensibilisation à la sécurité KnowBe4](mailto:support@KnowBe4.com).</span><span class="sxs-lookup"><span data-stu-id="33637-168">To configure single sign-on on **KnowBe4 Security Awareness Training** side, you need to send the downloaded **Certificate (Raw)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [KnowBe4 Security Awareness Training Client support team](mailto:support@KnowBe4.com).</span></span>

> [!TIP]
> <span data-ttu-id="33637-169">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="33637-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="33637-170">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="33637-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="33637-171">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="33637-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="33637-172">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="33637-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="33637-173">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="33637-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="33637-175">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="33637-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="33637-176">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="33637-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-KnowBe4-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="33637-178">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="33637-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-KnowBe4-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="33637-180">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="33637-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-KnowBe4-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="33637-182">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="33637-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-KnowBe4-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="33637-184">a.</span><span class="sxs-lookup"><span data-stu-id="33637-184">a.</span></span> <span data-ttu-id="33637-185">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="33637-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="33637-186">b.</span><span class="sxs-lookup"><span data-stu-id="33637-186">b.</span></span> <span data-ttu-id="33637-187">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="33637-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="33637-188">c.</span><span class="sxs-lookup"><span data-stu-id="33637-188">c.</span></span> <span data-ttu-id="33637-189">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="33637-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="33637-190">d.</span><span class="sxs-lookup"><span data-stu-id="33637-190">d.</span></span> <span data-ttu-id="33637-191">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="33637-191">Click **Create**.</span></span>
 
### <a name="creating-a-knowbe4-security-awareness-training-test-user"></a><span data-ttu-id="33637-192">Création d’un utilisateur de test de la formation de sensibilisation à la sécurité KnowBe4</span><span class="sxs-lookup"><span data-stu-id="33637-192">Creating a KnowBe4 Security Awareness Training test user</span></span>

<span data-ttu-id="33637-193">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans la formation de sensibilisation à la sécurité KnowBe4.</span><span class="sxs-lookup"><span data-stu-id="33637-193">The objective of this section is to create a user called Britta Simon in KnowBe4 Security Awareness Training.</span></span> <span data-ttu-id="33637-194">La formation de sensibilisation à la sécurité KnowBe4 prend en charge l’approvisionnement juste à temps, activé par défaut.</span><span class="sxs-lookup"><span data-stu-id="33637-194">KnowBe4 Security Awareness Training supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="33637-195">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="33637-195">There is no action item for you in this section.</span></span> <span data-ttu-id="33637-196">Un nouvel utilisateur est créé lors d’une tentative d’accès à la formation de sensibilisation à la sécurité KnowBe4 s’il n’existe pas déjà.</span><span class="sxs-lookup"><span data-stu-id="33637-196">A new user is created during an attempt to access KnowBe4 Security Awareness Training if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="33637-197">Si vous devez créer un utilisateur manuellement, contactez [l’équipe du support technique de formation de sensibilisation à la sécurité KnowBe4](mailto:support@KnowBe4.com).</span><span class="sxs-lookup"><span data-stu-id="33637-197">If you need to create a user manually, you need to contact the [KnowBe4 Security Awareness Training support team](mailto:support@KnowBe4.com).</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="33637-198">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="33637-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="33637-199">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à la formation de sensibilisation à la sécurité KnowBe4.</span><span class="sxs-lookup"><span data-stu-id="33637-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to KnowBe4 Security Awareness Training.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="33637-201">**Pour affecter la formation de sensibilisation à la sécurité KnowBe4 à Britta Simon, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="33637-201">**To assign Britta Simon to KnowBe4 Security Awareness Training, perform the following steps:**</span></span>

1. <span data-ttu-id="33637-202">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="33637-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="33637-204">Dans la liste des applications, sélectionnez **Formation de sensibilisation à la sécurité KnowBe4**.</span><span class="sxs-lookup"><span data-stu-id="33637-204">In the applications list, select **KnowBe4 Security Awareness Training**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_app.png) 

3. <span data-ttu-id="33637-206">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="33637-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="33637-208">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="33637-208">Click **Add** button.</span></span> <span data-ttu-id="33637-209">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="33637-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="33637-211">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="33637-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="33637-212">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="33637-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="33637-213">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="33637-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="33637-214">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="33637-214">Testing single sign-on</span></span>

<span data-ttu-id="33637-215">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="33637-215">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>
  
<span data-ttu-id="33637-216">Lorsque vous cliquez sur la vignette Formation de sensibilisation à la sécurité KnowBe4 dans le volet d’accès, vous devez être connecté automatiquement à votre application Formation de sensibilisation à la sécurité KnowBe4.</span><span class="sxs-lookup"><span data-stu-id="33637-216">When you click the KnowBe4 Security Awareness Training tile in the Access Panel, you should get automatically signed-on to your KnowBe4 Security Awareness Training application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="33637-217">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="33637-217">Additional resources</span></span>

* [<span data-ttu-id="33637-218">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="33637-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="33637-219">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="33637-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_203.png

