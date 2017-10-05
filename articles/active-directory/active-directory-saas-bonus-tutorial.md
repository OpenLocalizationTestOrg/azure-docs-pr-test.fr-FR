---
title: "Didacticiel : Intégration d’Azure Active Directory avec Bonusly | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Bonusly."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 29fea32a-fa20-47b2-9e24-26feb47b0ae6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 29a88b2efdb9f0f33f7933bc654a5a0fdf589c5a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bonusly"></a><span data-ttu-id="559ea-103">Didacticiel : Intégration d’Azure Active Directory avec Bonusly</span><span class="sxs-lookup"><span data-stu-id="559ea-103">Tutorial: Azure Active Directory integration with Bonusly</span></span>

<span data-ttu-id="559ea-104">Dans ce didacticiel, vous allez apprendre à intégrer Bonusly avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="559ea-104">In this tutorial, you learn how to integrate Bonusly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="559ea-105">L’intégration d’Azure AD avec Bonusly offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="559ea-105">Integrating Bonusly with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="559ea-106">Dans Azure AD, vous pouvez contrôler qui a accès à Bonusly.</span><span class="sxs-lookup"><span data-stu-id="559ea-106">You can control in Azure AD who has access to Bonusly</span></span>
- <span data-ttu-id="559ea-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Bonusly (par le biais de l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="559ea-107">You can enable your users to automatically get signed-on to Bonusly (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="559ea-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="559ea-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="559ea-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="559ea-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="559ea-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="559ea-110">Prerequisites</span></span>

<span data-ttu-id="559ea-111">Pour configurer l’intégration d’Azure AD avec Bonusly, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="559ea-111">To configure Azure AD integration with Bonusly, you need the following items:</span></span>

- <span data-ttu-id="559ea-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="559ea-112">An Azure AD subscription</span></span>
- <span data-ttu-id="559ea-113">Un abonnement Bonusly pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="559ea-113">A Bonusly single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="559ea-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="559ea-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="559ea-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="559ea-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="559ea-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="559ea-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="559ea-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="559ea-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="559ea-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="559ea-118">Scenario description</span></span>
<span data-ttu-id="559ea-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="559ea-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="559ea-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="559ea-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="559ea-121">Ajout de Bonusly à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="559ea-121">Adding Bonusly from the gallery</span></span>
2. <span data-ttu-id="559ea-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="559ea-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bonusly-from-the-gallery"></a><span data-ttu-id="559ea-123">Ajout de Bonusly à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="559ea-123">Adding Bonusly from the gallery</span></span>
<span data-ttu-id="559ea-124">Pour configurer l’intégration de Bonusly dans Azure AD, vous devez ajouter Bonusly à votre liste d’applications SaaS gérées à partir de la galerie.</span><span class="sxs-lookup"><span data-stu-id="559ea-124">To configure the integration of Bonusly into Azure AD, you need to add Bonusly from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="559ea-125">**Pour ajouter Bonusly à partir de la galerie, suivez les étapes ci-dessous :**</span><span class="sxs-lookup"><span data-stu-id="559ea-125">**To add Bonusly from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="559ea-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="559ea-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Bouton Azure Active Directory][1]

2. <span data-ttu-id="559ea-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="559ea-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="559ea-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="559ea-129">Then go to **All applications**.</span></span>

    ![Panneau Applications d’entreprise][2]
    
3. <span data-ttu-id="559ea-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="559ea-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Bouton Nouvelle application][3]

4. <span data-ttu-id="559ea-133">Dans la zone de recherche, tapez **Bonusly**, sélectionnez **Bonusly** dans le volet de résultats, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="559ea-133">In the search box, type **Bonusly**, select **Bonusly** from result panel then click **Add** button to add the application.</span></span>

    ![Bonusly dans la liste des résultats](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="559ea-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="559ea-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="559ea-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Bonusly avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="559ea-136">In this section, you configure and test Azure AD single sign-on with Bonusly based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="559ea-137">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Bonusly équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="559ea-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Bonusly is to a user in Azure AD.</span></span> <span data-ttu-id="559ea-138">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Bonusly associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="559ea-138">In other words, a link relationship between an Azure AD user and the related user in Bonusly needs to be established.</span></span>

<span data-ttu-id="559ea-139">Dans Bonusly, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="559ea-139">In Bonusly, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="559ea-140">Pour configurer et tester l’authentification unique Azure AD avec Bonusly, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="559ea-140">To configure and test Azure AD single sign-on with Bonusly, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="559ea-141">**[Configurer l’authentification unique Azure AD](#configure-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="559ea-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="559ea-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="559ea-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="559ea-143">**[Création d’un utilisateur de test Bonusly](#create-a-bonusly-test-user)** Permet d’avoir un équivalent de Britta Simon dans Bonusly lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="559ea-143">**[Create a Bonusly test user](#create-a-bonusly-test-user)** - to have a counterpart of Britta Simon in Bonusly that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="559ea-144">**[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="559ea-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="559ea-145">**[Tester l’authentification unique](#test-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="559ea-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="559ea-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="559ea-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="559ea-147">Dans cette section, vous allez activer l’authentification unique Azure AD sur le portail Azure et configurer l’authentification unique dans votre application Bonusly.</span><span class="sxs-lookup"><span data-stu-id="559ea-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Bonusly application.</span></span>

<span data-ttu-id="559ea-148">**Pour configurer l’authentification unique Azure AD avec Bonusly, suivez les étapes ci-dessous :**</span><span class="sxs-lookup"><span data-stu-id="559ea-148">**To configure Azure AD single sign-on with Bonusly, perform the following steps:**</span></span>

1. <span data-ttu-id="559ea-149">Dans le portail Azure, sur la page d’intégration de l’application **Bonusly**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="559ea-149">In the Azure portal, on the **Bonusly** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="559ea-151">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="559ea-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_samlbase.png)

3. <span data-ttu-id="559ea-153">Dans la section **Domaine et URL Bonusly**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="559ea-153">On the **Bonusly Domain and URLs** section, perform the following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL Bonusly](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_url.png)

    <span data-ttu-id="559ea-155">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://Bonus.ly/saml/<tenant-name>`</span><span class="sxs-lookup"><span data-stu-id="559ea-155">In the **Reply URL** textbox, type a URL using the following pattern: `https://Bonus.ly/saml/<tenant-name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="559ea-156">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="559ea-156">The value is not real.</span></span> <span data-ttu-id="559ea-157">Mettez à jour la valeur avec l’URL de réponse réelle.</span><span class="sxs-lookup"><span data-stu-id="559ea-157">Update the value with the actual Reply URL.</span></span> <span data-ttu-id="559ea-158">Pour obtenir cette valeur, contactez [l’équipe de support technique Bonusly](https://Bonusly/contact).</span><span class="sxs-lookup"><span data-stu-id="559ea-158">Contact [Bonusly support team](https://Bonusly/contact) to get the value.</span></span>
 
4. <span data-ttu-id="559ea-159">Dans la section **Certificat de signature SAML**, copiez la valeur **THUMBPRINT** du certificat.</span><span class="sxs-lookup"><span data-stu-id="559ea-159">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value from the certificate.</span></span>

    ![Lien de téléchargement du certificat](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_certificate.png) 

5. <span data-ttu-id="559ea-161">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="559ea-161">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-bonus-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="559ea-163">Dans la section **Configuration de Bonusly**, cliquez sur **Configurer Bonusly** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="559ea-163">On the **Bonusly Configuration** section, click **Configure Bonusly** to open **Configure sign-on** window.</span></span> <span data-ttu-id="559ea-164">Copiez l’**ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="559ea-164">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuration de Bonusly](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_configure.png) 

7. <span data-ttu-id="559ea-166">Dans une autre fenêtre de navigateur, connectez-vous à votre locataire **Bonusly**.</span><span class="sxs-lookup"><span data-stu-id="559ea-166">In a different browser window, log in to your **Bonusly** tenant.</span></span>

8. <span data-ttu-id="559ea-167">Dans la barre d’outils située en haut, cliquez sur **Settings**, puis sélectionnez **Integrations and apps**.</span><span class="sxs-lookup"><span data-stu-id="559ea-167">In the toolbar on the top, click **Settings**, and then select **Integrations and apps**.</span></span>
   
    <span data-ttu-id="559ea-168">![Section sociale Bonusly](./media/active-directory-saas-bonus-tutorial/ic773686.png "Bonusly")</span><span class="sxs-lookup"><span data-stu-id="559ea-168">![Bonusly Social Section](./media/active-directory-saas-bonus-tutorial/ic773686.png "Bonusly")</span></span>
9. <span data-ttu-id="559ea-169">Sous **Single Sign-On**, sélectionnez **SAML**.</span><span class="sxs-lookup"><span data-stu-id="559ea-169">Under **Single Sign-On**, select **SAML**.</span></span>

10. <span data-ttu-id="559ea-170">Dans la page de boîte de dialogue **SAML** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="559ea-170">On the **SAML** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="559ea-171">![Page de boîte de dialogue Saml Bonusly](./media/active-directory-saas-bonus-tutorial/ic773687.png "Bonusly")</span><span class="sxs-lookup"><span data-stu-id="559ea-171">![Bonusly Saml Dialog page](./media/active-directory-saas-bonus-tutorial/ic773687.png "Bonusly")</span></span>
   
    <span data-ttu-id="559ea-172">a.</span><span class="sxs-lookup"><span data-stu-id="559ea-172">a.</span></span> <span data-ttu-id="559ea-173">Dans la zone de texte **IdP SSO target URL** (URL cible de l’authentification unique), collez la valeur de **l’URL du service d’authentification unique SAML** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="559ea-173">In the **IdP SSO target URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="559ea-174">b.</span><span class="sxs-lookup"><span data-stu-id="559ea-174">b.</span></span> <span data-ttu-id="559ea-175">Dans la zone de texte **Émetteur IdP**, collez la valeur de **ID d’entité SAML** que vous avez copiée depuis le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="559ea-175">In the **IdP Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="559ea-176">c.</span><span class="sxs-lookup"><span data-stu-id="559ea-176">c.</span></span> <span data-ttu-id="559ea-177">Dans la zone de texte **IdP Login URL** (URL de connexion de fournisseur d’identité), collez la valeur de **l’URL du service d’authentification unique SAML** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="559ea-177">In the **IdP Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="559ea-178">d.</span><span class="sxs-lookup"><span data-stu-id="559ea-178">d.</span></span> <span data-ttu-id="559ea-179">Copiez la valeur située sous **Empreinte** dans le portail Azure, puis collez-la dans la zone de texte **Empreinte du certificat**.</span><span class="sxs-lookup"><span data-stu-id="559ea-179">Paste the **Thumbprint** value copied from Azure portal into the **Cert Fingerprint** textbox.</span></span>
   
11. <span data-ttu-id="559ea-180">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="559ea-180">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="559ea-181">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="559ea-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="559ea-182">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="559ea-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="559ea-183">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="559ea-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="559ea-184">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="559ea-184">Create an Azure AD test user</span></span>
<span data-ttu-id="559ea-185">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="559ea-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="559ea-187">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="559ea-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="559ea-188">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="559ea-188">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bouton Azure Active Directory](./media/active-directory-saas-bonus-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="559ea-190">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="559ea-190">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Liens « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/active-directory-saas-bonus-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="559ea-192">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="559ea-192">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bouton Ajouter](./media/active-directory-saas-bonus-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="559ea-194">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="559ea-194">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Boîte de dialogue Utilisateur](./media/active-directory-saas-bonus-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="559ea-196">a.</span><span class="sxs-lookup"><span data-stu-id="559ea-196">a.</span></span> <span data-ttu-id="559ea-197">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="559ea-197">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="559ea-198">b.</span><span class="sxs-lookup"><span data-stu-id="559ea-198">b.</span></span> <span data-ttu-id="559ea-199">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="559ea-199">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="559ea-200">c.</span><span class="sxs-lookup"><span data-stu-id="559ea-200">c.</span></span> <span data-ttu-id="559ea-201">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="559ea-201">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="559ea-202">d.</span><span class="sxs-lookup"><span data-stu-id="559ea-202">d.</span></span> <span data-ttu-id="559ea-203">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="559ea-203">Click **Create**.</span></span>
 
### <a name="create-a-bonusly-test-user"></a><span data-ttu-id="559ea-204">Création d’un utilisateur de test Bonusly</span><span class="sxs-lookup"><span data-stu-id="559ea-204">Create a Bonusly test user</span></span>

<span data-ttu-id="559ea-205">Pour permettre aux utilisateurs Azure AD de se connecter à Bonusly, vous devez les approvisionner dans Bonusly.</span><span class="sxs-lookup"><span data-stu-id="559ea-205">In order to enable Azure AD users to log in to Bonusly, they must be provisioned into Bonusly.</span></span> <span data-ttu-id="559ea-206">En l’occurrence, cet approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="559ea-206">In the case of Bonusly, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="559ea-207">Vous pouvez utiliser tout autre outil ou n’importe quelle API de création de compte d’utilisateur fournis par Bonusly pour approvisionner des comptes d’utilisateur Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="559ea-207">You can use any other Bonusly user account creation tools or APIs provided by Bonusly to provision AAD user accounts.</span></span>
>  

<span data-ttu-id="559ea-208">**Pour configurer l'approvisionnement des utilisateurs, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="559ea-208">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="559ea-209">Dans une fenêtre de navigateur web, connectez-vous à votre locataire Bonusly.</span><span class="sxs-lookup"><span data-stu-id="559ea-209">In a web browser window, log in to your Bonusly tenant.</span></span>

2. <span data-ttu-id="559ea-210">Cliquez sur **Settings**.</span><span class="sxs-lookup"><span data-stu-id="559ea-210">Click **Settings**.</span></span>
 
    <span data-ttu-id="559ea-211">![Paramètres](./media/active-directory-saas-bonus-tutorial/ic781041.png "Paramètres")</span><span class="sxs-lookup"><span data-stu-id="559ea-211">![Settings](./media/active-directory-saas-bonus-tutorial/ic781041.png "Settings")</span></span>

3. <span data-ttu-id="559ea-212">Cliquez sur l’onglet **Users and bonuses** .</span><span class="sxs-lookup"><span data-stu-id="559ea-212">Click the **Users and bonuses** tab.</span></span>
   
    <span data-ttu-id="559ea-213">![Users and bonuses](./media/active-directory-saas-bonus-tutorial/ic781042.png "Users and bonuses")</span><span class="sxs-lookup"><span data-stu-id="559ea-213">![Users and bonuses](./media/active-directory-saas-bonus-tutorial/ic781042.png "Users and bonuses")</span></span>

4. <span data-ttu-id="559ea-214">Cliquez sur **Manage Users**.</span><span class="sxs-lookup"><span data-stu-id="559ea-214">Click **Manage Users**.</span></span>
   
    <span data-ttu-id="559ea-215">![Gestion des utilisateurs](./media/active-directory-saas-bonus-tutorial/ic781043.png "Gestion des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="559ea-215">![Manage Users](./media/active-directory-saas-bonus-tutorial/ic781043.png "Manage Users")</span></span>

5. <span data-ttu-id="559ea-216">Cliquez sur **Add User**.</span><span class="sxs-lookup"><span data-stu-id="559ea-216">Click **Add User**.</span></span>
   
    <span data-ttu-id="559ea-217">![Ajouter un utilisateur](./media/active-directory-saas-bonus-tutorial/ic781044.png "Ajouter un utilisateur")</span><span class="sxs-lookup"><span data-stu-id="559ea-217">![Add User](./media/active-directory-saas-bonus-tutorial/ic781044.png "Add User")</span></span>

6. <span data-ttu-id="559ea-218">Dans la boîte de dialogue **Ajouter un utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="559ea-218">On the **Add User** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="559ea-219">![Ajouter un utilisateur](./media/active-directory-saas-bonus-tutorial/ic781045.png "Ajouter un utilisateur")</span><span class="sxs-lookup"><span data-stu-id="559ea-219">![Add User](./media/active-directory-saas-bonus-tutorial/ic781045.png "Add User")</span></span>  

    <span data-ttu-id="559ea-220">a.</span><span class="sxs-lookup"><span data-stu-id="559ea-220">a.</span></span> <span data-ttu-id="559ea-221">Dans la zone de texte **First name**, entrez le prénom de l’utilisateur, par exemple **Britta**.</span><span class="sxs-lookup"><span data-stu-id="559ea-221">In the **First name** textbox, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="559ea-222">b.</span><span class="sxs-lookup"><span data-stu-id="559ea-222">b.</span></span> <span data-ttu-id="559ea-223">Dans la zone de texte **Last name**, tapez le nom de l’utilisateur, par exemple **Simon**.</span><span class="sxs-lookup"><span data-stu-id="559ea-223">In the **Last name** textbox, enter the last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="559ea-224">c.</span><span class="sxs-lookup"><span data-stu-id="559ea-224">c.</span></span> <span data-ttu-id="559ea-225">Dans la zone de texte **E-mail**, entrez l’adresse de messagerie de l’utilisateur, par exemple **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="559ea-225">In the **Email** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="559ea-226">d.</span><span class="sxs-lookup"><span data-stu-id="559ea-226">d.</span></span> <span data-ttu-id="559ea-227">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="559ea-227">Click **Save**.</span></span>
   
     >[!NOTE]
     ><span data-ttu-id="559ea-228">Le titulaire du compte Azure AD reçoit alors un e-mail contenant un lien pour confirmer le compte avant qu’il ne soit activé.</span><span class="sxs-lookup"><span data-stu-id="559ea-228">The Azure AD account holder receives an email that includes a link to confirm the account before it becomes active.</span></span>
     >  

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="559ea-229">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="559ea-229">Assign the Azure AD test user</span></span>

<span data-ttu-id="559ea-230">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Bonusly.</span><span class="sxs-lookup"><span data-stu-id="559ea-230">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Bonusly.</span></span>

![Attribuer le rôle d’utilisateur][200] 

<span data-ttu-id="559ea-232">**Pour affecter Britta Simon à Bonusly, suivez les étapes ci-dessous :**</span><span class="sxs-lookup"><span data-stu-id="559ea-232">**To assign Britta Simon to Bonusly, perform the following steps:**</span></span>

1. <span data-ttu-id="559ea-233">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="559ea-233">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="559ea-235">Dans la liste des applications, sélectionnez **Bonusly**.</span><span class="sxs-lookup"><span data-stu-id="559ea-235">In the applications list, select **Bonusly**.</span></span>

    ![Lien Bonusly dans la liste des applications](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_app.png) 

3. <span data-ttu-id="559ea-237">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="559ea-237">In the menu on the left, click **Users and groups**.</span></span>

    ![Lien « Utilisateurs et groupes »][202] 

4. <span data-ttu-id="559ea-239">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="559ea-239">Click **Add** button.</span></span> <span data-ttu-id="559ea-240">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="559ea-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Volet Ajouter une attribution][203]

5. <span data-ttu-id="559ea-242">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="559ea-242">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="559ea-243">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="559ea-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="559ea-244">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="559ea-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="559ea-245">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="559ea-245">Test single sign-on</span></span>

<span data-ttu-id="559ea-246">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="559ea-246">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="559ea-247">Le fait de cliquer sur la vignette Bonusly dans le volet d’accès vous connecte automatiquement à votre application Bonusly.</span><span class="sxs-lookup"><span data-stu-id="559ea-247">When you click the Bonusly tile in the Access Panel, you should get automatically signed-on to your Bonusly application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="559ea-248">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="559ea-248">Additional resources</span></span>

* [<span data-ttu-id="559ea-249">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="559ea-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="559ea-250">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="559ea-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_203.png

