---
title: "Didacticiel : Intégration d’Azure Active Directory à Keeper Password Manager & Digital Vault | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Keeper Password Manager & Digital Vault."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e1a98f6a-2dae-4734-bdbf-4fba742a61d2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 36504a281756b980e3348e7f892ba08821873b52
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-keeper-password-manager--digital-vault"></a><span data-ttu-id="b6f1f-103">Didacticiel : Intégration d’Azure Active Directory à Keeper Password Manager & Digital Vault</span><span class="sxs-lookup"><span data-stu-id="b6f1f-103">Tutorial: Azure Active Directory integration with Keeper Password Manager & Digital Vault</span></span>

<span data-ttu-id="b6f1f-104">Dans ce didacticiel, vous allez apprendre à intégrer Keeper Password Manager & Digital Vault à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b6f1f-104">In this tutorial, you learn how to integrate Keeper Password Manager & Digital Vault with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b6f1f-105">L’intégration de Keeper Password Manager & Digital Vault à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="b6f1f-105">Integrating Keeper Password Manager & Digital Vault with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b6f1f-106">Dans Azure AD, vous pouvez contrôler qui a accès à Keeper Password Manager & Digital Vault.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-106">You can control in Azure AD who has access to Keeper Password Manager & Digital Vault</span></span>
- <span data-ttu-id="b6f1f-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Keeper Password Manager & Digital Vault (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-107">You can enable your users to automatically get signed-on to Keeper Password Manager & Digital Vault (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b6f1f-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="b6f1f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b6f1f-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b6f1f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b6f1f-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b6f1f-110">Prerequisites</span></span>

<span data-ttu-id="b6f1f-111">Pour configurer l’intégration d’Azure AD à Keeper Password Manager & Digital Vault, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="b6f1f-111">To configure Azure AD integration with Keeper Password Manager & Digital Vault, you need the following items:</span></span>

- <span data-ttu-id="b6f1f-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="b6f1f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b6f1f-113">Un abonnement Keeper Password Manager & Digital Vault pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="b6f1f-113">A Keeper Password Manager & Digital Vault single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b6f1f-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b6f1f-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="b6f1f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b6f1f-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b6f1f-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b6f1f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b6f1f-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="b6f1f-118">Scenario description</span></span>
<span data-ttu-id="b6f1f-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b6f1f-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="b6f1f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b6f1f-121">Ajout de Keeper Password Manager & Digital Vault à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="b6f1f-121">Adding Keeper Password Manager & Digital Vault from the gallery</span></span>
2. <span data-ttu-id="b6f1f-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b6f1f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-keeper-password-manager--digital-vault-from-the-gallery"></a><span data-ttu-id="b6f1f-123">Ajout de Keeper Password Manager & Digital Vault à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="b6f1f-123">Adding Keeper Password Manager & Digital Vault from the gallery</span></span>
<span data-ttu-id="b6f1f-124">Pour configurer l’intégration de Keeper Password Manager & Digital Vault à Azure AD, vous devez ajouter Keeper Password Manager & Digital Vault à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-124">To configure the integration of Keeper Password Manager & Digital Vault into Azure AD, you need to add Keeper Password Manager & Digital Vault from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b6f1f-125">**Pour ajouter Keeper Password Manager & Digital Vault à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b6f1f-125">**To add Keeper Password Manager & Digital Vault from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b6f1f-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b6f1f-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b6f1f-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="b6f1f-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="b6f1f-133">Dans la zone de recherche, tapez **Keeper Password Manager & Digital Vault**.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-133">In the search box, type **Keeper Password Manager & Digital Vault**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_search.png)

5. <span data-ttu-id="b6f1f-135">Dans le volet de résultats, sélectionnez **Keeper Password Manager & Digital Vault**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-135">In the results panel, select **Keeper Password Manager & Digital Vault**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b6f1f-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b6f1f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b6f1f-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Keeper Password Manager & Digital Vault avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="b6f1f-138">In this section, you configure and test Azure AD single sign-on with Keeper Password Manager & Digital Vault based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b6f1f-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Keeper Password Manager & Digital Vault équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Keeper Password Manager & Digital Vault is to a user in Azure AD.</span></span> <span data-ttu-id="b6f1f-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Keeper Password Manager & Digital Vault associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-140">In other words, a link relationship between an Azure AD user and the related user in Keeper Password Manager & Digital Vault needs to be established.</span></span>

<span data-ttu-id="b6f1f-141">Dans Keeper Password Manager & Digital Vault, assignez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-141">In Keeper Password Manager & Digital Vault, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b6f1f-142">Pour configurer et tester l’authentification unique Azure AD avec Keeper Password Manager & Digital Vault, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="b6f1f-142">To configure and test Azure AD single sign-on with Keeper Password Manager & Digital Vault, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b6f1f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b6f1f-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b6f1f-145">**[Création d’un utilisateur de test Keeper Password Manager & Digital Vault](#creating-a-keeperpasswordmanager-test-user)** : pour avoir un équivalent de Britta Simon dans Keeper Password Manager & Digital Vault lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-145">**[Creating a Keeper Password Manager & Digital Vault test user](#creating-a-keeperpasswordmanager-test-user)** - to have a counterpart of Britta Simon in Keeper Password Manager & Digital Vault that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b6f1f-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b6f1f-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b6f1f-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b6f1f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b6f1f-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Keeper Password Manager & Digital Vault.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Keeper Password Manager & Digital Vault application.</span></span>

<span data-ttu-id="b6f1f-150">**Pour configurer l’authentification unique Azure AD avec Keeper Password Manager & Digital Vault, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b6f1f-150">**To configure Azure AD single sign-on with Keeper Password Manager & Digital Vault, perform the following steps:**</span></span>

1. <span data-ttu-id="b6f1f-151">Dans le portail Azure, sur la page d’intégration de l’application **Keeper Password Manager & Digital Vault**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-151">In the Azure portal, on the **Keeper Password Manager & Digital Vault** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="b6f1f-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_samlbase.png)

3. <span data-ttu-id="b6f1f-155">Dans la section **Domaine et URL Keeper Password Manager & Digital Vault**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="b6f1f-155">On the **Keeper Password Manager & Digital Vault Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_url.png)

    <span data-ttu-id="b6f1f-157">a.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-157">a.</span></span> <span data-ttu-id="b6f1f-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://{SSO CONNECT SERVER}/sso-connect/saml/login`</span><span class="sxs-lookup"><span data-stu-id="b6f1f-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://{SSO CONNECT SERVER}/sso-connect/saml/login`</span></span>

    <span data-ttu-id="b6f1f-159">b.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-159">b.</span></span> <span data-ttu-id="b6f1f-160">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://{SSO CONNECT SERVER}/sso-connect/saml/sso`</span><span class="sxs-lookup"><span data-stu-id="b6f1f-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://{SSO CONNECT SERVER}/sso-connect/saml/sso`</span></span>

    <span data-ttu-id="b6f1f-161">c.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-161">c.</span></span> <span data-ttu-id="b6f1f-162">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://{SSO CONNECT SERVER}/sso-connect`</span><span class="sxs-lookup"><span data-stu-id="b6f1f-162">In the **Identifier** textbox, type a URL using the following pattern: `https://{SSO CONNECT SERVER}/sso-connect`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b6f1f-163">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-163">These values are not real.</span></span> <span data-ttu-id="b6f1f-164">Mettez à jour ces valeurs avec l’URL de réponse et l’URL de connexion réelles.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-164">Update these values with the actual Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="b6f1f-165">Pour obtenir ces valeurs, contactez [l’équipe de support technique de Keeper Password Manager & Digital Vault](https://keepersecurity.com/contact.html).</span><span class="sxs-lookup"><span data-stu-id="b6f1f-165">Contact [Keeper Password Manager & Digital Vault Client support team](https://keepersecurity.com/contact.html) to get these values.</span></span> 

4. <span data-ttu-id="b6f1f-166">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_certificate.png) 

5. <span data-ttu-id="b6f1f-168">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="b6f1f-168">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="b6f1f-170">Dans la section **Configuration de Keeper Password Manager & Digital Vault**, cliquez sur **Configurer Keeper Password Manager & Digital Vault** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-170">On the **Keeper Password Manager & Digital Vault Configuration** section, click **Configure Keeper Password Manager & Digital Vault** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b6f1f-171">Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="b6f1f-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_configure.png) 

7. <span data-ttu-id="b6f1f-173">Pour configurer l’authentification unique côté **Keeper Password Manager & Digital Vault**, suivez les instructions fournies dans le [guide de prise en charge de Keeper](https://keepersecurity.com/assets/pdf/SettingupAzurewithKeeperSSOConnect.pdf).</span><span class="sxs-lookup"><span data-stu-id="b6f1f-173">To configure single sign-on on **Keeper Password Manager & Digital Vault Configuration** side, follow the guidelines given at [Keeper Support Guide](https://keepersecurity.com/assets/pdf/SettingupAzurewithKeeperSSOConnect.pdf)</span></span>

> [!TIP]
> <span data-ttu-id="b6f1f-174">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-174">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b6f1f-175">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-175">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b6f1f-176">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b6f1f-176">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b6f1f-177">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="b6f1f-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="b6f1f-178">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-178">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="b6f1f-180">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b6f1f-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b6f1f-181">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-181">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b6f1f-183">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-183">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b6f1f-185">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-185">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b6f1f-187">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="b6f1f-187">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b6f1f-189">a.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-189">a.</span></span> <span data-ttu-id="b6f1f-190">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-190">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b6f1f-191">b.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-191">b.</span></span> <span data-ttu-id="b6f1f-192">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-192">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b6f1f-193">c.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-193">c.</span></span> <span data-ttu-id="b6f1f-194">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-194">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b6f1f-195">d.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-195">d.</span></span> <span data-ttu-id="b6f1f-196">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-196">Click **Create**.</span></span>
 
### <a name="creating-a-keeper-password-manager--digital-vault-test-user"></a><span data-ttu-id="b6f1f-197">Création d’un utilisateur de test Keeper Password Manager & Digital Vault</span><span class="sxs-lookup"><span data-stu-id="b6f1f-197">Creating a Keeper Password Manager & Digital Vault test user</span></span>

<span data-ttu-id="b6f1f-198">Pour se connecter à Keeper Password Manager & Digital Vault, les utilisateurs d’Azure AD doivent être approvisionnés dans Keeper Password Manager & Digital Vault.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-198">To enable Azure AD users to log in to Keeper Password Manager & Digital Vault, they must be provisioned into Keeper Password Manager & Digital Vault.</span></span> <span data-ttu-id="b6f1f-199">L’application prend en charge la configuration d’utilisateur juste-à-temps, et après authentification, les utilisateurs sont créés automatiquement dans l’application.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-199">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span> <span data-ttu-id="b6f1f-200">Si vous voulez configurer des utilisateurs manuellement, vous pouvez contacter le [support de Keeper](https://keepersecurity.com/contact.html).</span><span class="sxs-lookup"><span data-stu-id="b6f1f-200">You can contact [Keeper Support](https://keepersecurity.com/contact.html), if you want to setup users manually.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b6f1f-201">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="b6f1f-201">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b6f1f-202">Dans cette section, vous autorisez Britta Simon à utiliser l’authentification unique Azure en accordant l’accès à Keeper Password Manager & Digital Vault.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Keeper Password Manager & Digital Vault.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="b6f1f-204">**Pour affecter Britta Simon à Keeper Password Manager & Digital Vault, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b6f1f-204">**To assign Britta Simon to Keeper Password Manager & Digital Vault, perform the following steps:**</span></span>

1. <span data-ttu-id="b6f1f-205">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="b6f1f-207">Dans la liste des applications, sélectionnez **Keeper Password Manager & Digital Vault**.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-207">In the applications list, select **Keeper Password Manager & Digital Vault**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_app.png) 

3. <span data-ttu-id="b6f1f-209">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-209">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="b6f1f-211">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-211">Click **Add** button.</span></span> <span data-ttu-id="b6f1f-212">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="b6f1f-214">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b6f1f-215">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b6f1f-216">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b6f1f-217">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="b6f1f-217">Testing single sign-on</span></span>

<span data-ttu-id="b6f1f-218">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-218">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b6f1f-219">Lorsque vous cliquez sur la vignette Keeper Password Manager & Digital Vault dans le volet d’accès, vous devez accéder à la page de connexion de l’application Keeper Password Manager & Digital Vault.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-219">When you click the Keeper Password Manager & Digital Vault tile in the Access Panel, you should get login page of Keeper Password Manager & Digital Vault application.</span></span> <span data-ttu-id="b6f1f-220">Après vous être authentifié, vous devez accéder à l’application.</span><span class="sxs-lookup"><span data-stu-id="b6f1f-220">Upon successful authentication, you should get into the application.</span></span> <span data-ttu-id="b6f1f-221">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b6f1f-221">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b6f1f-222">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="b6f1f-222">Additional resources</span></span>

* [<span data-ttu-id="b6f1f-223">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b6f1f-223">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b6f1f-224">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="b6f1f-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_203.png

