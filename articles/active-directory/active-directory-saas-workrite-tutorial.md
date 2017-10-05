---
title: "Didacticiel : intégration d’Azure Active Directory à Workrite | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Workrite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 2a5c2956-a011-4d5c-877b-80679b6587b5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 4358c4c621634c17cbbd7fa1c72f12746b8e4a2a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workrite"></a><span data-ttu-id="48e08-103">Didacticiel : intégration d’Azure Active Directory à Workrite</span><span class="sxs-lookup"><span data-stu-id="48e08-103">Tutorial: Azure Active Directory integration with Workrite</span></span>

<span data-ttu-id="48e08-104">Dans ce didacticiel, vous allez apprendre à intégrer Workrite à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="48e08-104">In this tutorial, you learn how to integrate Workrite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="48e08-105">L’intégration de Workrite à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="48e08-105">Integrating Workrite with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="48e08-106">Dans Azure AD, vous pouvez contrôler qui a accès à Workrite</span><span class="sxs-lookup"><span data-stu-id="48e08-106">You can control in Azure AD who has access to Workrite.</span></span>
- <span data-ttu-id="48e08-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Workrite (par le biais de l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="48e08-107">You can enable your users to automatically get signed-on to Workrite (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="48e08-108">Vous pouvez gérer vos comptes dans un emplacement central : le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="48e08-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="48e08-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="48e08-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="48e08-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="48e08-110">Prerequisites</span></span>

<span data-ttu-id="48e08-111">Pour configurer l’intégration d’Azure AD à Workrite, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="48e08-111">To configure Azure AD integration with Workrite, you need the following items:</span></span>

- <span data-ttu-id="48e08-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="48e08-112">An Azure AD subscription</span></span>
- <span data-ttu-id="48e08-113">Un abonnement Workrite pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="48e08-113">A Workrite single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="48e08-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="48e08-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="48e08-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="48e08-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="48e08-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="48e08-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="48e08-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="48e08-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="48e08-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="48e08-118">Scenario description</span></span>
<span data-ttu-id="48e08-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="48e08-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="48e08-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="48e08-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="48e08-121">Ajout de Workrite à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="48e08-121">Adding Workrite from the gallery</span></span>
2. <span data-ttu-id="48e08-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="48e08-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workrite-from-the-gallery"></a><span data-ttu-id="48e08-123">Ajout de Workrite à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="48e08-123">Adding Workrite from the gallery</span></span>
<span data-ttu-id="48e08-124">Pour configurer l’intégration de Workrite à Azure AD, vous devez ajouter Workrite à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="48e08-124">To configure the integration of Workrite into Azure AD, you need to add Workrite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="48e08-125">**Pour ajouter Workrite à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="48e08-125">**To add Workrite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="48e08-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="48e08-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Bouton Azure Active Directory][1]

2. <span data-ttu-id="48e08-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="48e08-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="48e08-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="48e08-129">Then go to **All applications**.</span></span>

    ![Panneau Applications d’entreprise][2]
    
3. <span data-ttu-id="48e08-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="48e08-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Bouton Nouvelle application][3]

4. <span data-ttu-id="48e08-133">Dans la zone de recherche, tapez **Workrite**, sélectionnez **Workrite** dans le volet de résultats, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="48e08-133">In the search box, type **Workrite**, select **Workrite** from result panel then click **Add** button to add the application.</span></span>

    ![Workrite dans la liste des résultats](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="48e08-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="48e08-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="48e08-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Workrite, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="48e08-136">In this section, you configure and test Azure AD single sign-on with Workrite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="48e08-137">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Workrite équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48e08-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Workrite is to a user in Azure AD.</span></span> <span data-ttu-id="48e08-138">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Workrite associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="48e08-138">In other words, a link relationship between an Azure AD user and the related user in Workrite needs to be established.</span></span>

<span data-ttu-id="48e08-139">Dans Workrite, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **Username** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="48e08-139">In Workrite, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="48e08-140">Pour configurer et tester l’authentification unique Azure AD avec Workrite, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="48e08-140">To configure and test Azure AD single sign-on with Workrite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="48e08-141">**[Configurer l’authentification unique Azure AD](#configure-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="48e08-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="48e08-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="48e08-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="48e08-143">**[Créer un utilisateur de test Workrite](#create-a-workrite-test-user)** pour avoir un équivalent de Britta Simon dans Workrite lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="48e08-143">**[Create a Workrite test user](#create-a-workrite-test-user)** - to have a counterpart of Britta Simon in Workrite that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="48e08-144">**[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48e08-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="48e08-145">**[Tester l’authentification unique](#test-single-sign-on)** : pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="48e08-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="48e08-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="48e08-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="48e08-147">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Workrite.</span><span class="sxs-lookup"><span data-stu-id="48e08-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workrite application.</span></span>

<span data-ttu-id="48e08-148">**Pour configurer l’authentification unique Azure AD avec Workrite, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="48e08-148">**To configure Azure AD single sign-on with Workrite, perform the following steps:**</span></span>

1. <span data-ttu-id="48e08-149">Dans le portail Azure, dans la page d’intégration de l’application **Workrite**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="48e08-149">In the Azure portal, on the **Workrite** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="48e08-151">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="48e08-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_samlbase.png)

3. <span data-ttu-id="48e08-153">Dans la section **Domaine et URL Workrite**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="48e08-153">On the **Workrite Domain and URLs** section, perform the following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL Workrite](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_url.png)

    <span data-ttu-id="48e08-155">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://app.workrite.co.uk/securelogin/samlgateway.aspx?id=<uniqueid>`</span><span class="sxs-lookup"><span data-stu-id="48e08-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://app.workrite.co.uk/securelogin/samlgateway.aspx?id=<uniqueid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="48e08-156">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="48e08-156">This value is not real.</span></span> <span data-ttu-id="48e08-157">Mettez à jour cette valeur avec l’URL de connexion réelle.</span><span class="sxs-lookup"><span data-stu-id="48e08-157">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="48e08-158">Pour obtenir cette valeur, contactez [l’équipe de support technique de Workrite](mailto:support@workrite.co.uk).</span><span class="sxs-lookup"><span data-stu-id="48e08-158">Contact [Workrite Client support team](mailto:support@workrite.co.uk) to get this value.</span></span>

4. <span data-ttu-id="48e08-159">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="48e08-159">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Lien de téléchargement du certificat](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_certificate.png) 

5. <span data-ttu-id="48e08-161">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="48e08-161">Click **Save** button.</span></span>

    ![Bouton Enregistrer de Configurer l’authentification unique](./media/active-directory-saas-workrite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="48e08-163">Dans la section **Configuration de Workrite**, cliquez sur **Configurer Workrite** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="48e08-163">On the **Workrite Configuration** section, click **Configure Workrite** to open **Configure sign-on** window.</span></span> <span data-ttu-id="48e08-164">Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="48e08-164">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuration de Workrite](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_configure.png) 

7. <span data-ttu-id="48e08-166">Pour configurer l’authentification unique côté **Workrite**, vous devez envoyer le **Certificat (Base64) téléchargé, l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à l’[équipe de support technique de Workrite](mailto:support@workrite.co.uk).</span><span class="sxs-lookup"><span data-stu-id="48e08-166">To configure single sign-on on **Workrite** side, you need to send the downloaded **Certificate(Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Workrite support team](mailto:support@workrite.co.uk).</span></span>

> [!TIP]
> <span data-ttu-id="48e08-167">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="48e08-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="48e08-168">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="48e08-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="48e08-169">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="48e08-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="48e08-170">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="48e08-170">Create an Azure AD test user</span></span>

<span data-ttu-id="48e08-171">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="48e08-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="48e08-173">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="48e08-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="48e08-174">Dans le volet gauche du Portail Azure, cliquez sur le bouton **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="48e08-174">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Bouton Azure Active Directory](./media/active-directory-saas-workrite-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="48e08-176">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="48e08-176">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Liens « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/active-directory-saas-workrite-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="48e08-178">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="48e08-178">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Bouton Ajouter](./media/active-directory-saas-workrite-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="48e08-180">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="48e08-180">In the **User** dialog box, perform the following steps:</span></span>

    ![Boîte de dialogue Utilisateur](./media/active-directory-saas-workrite-tutorial/create_aaduser_04.png)

    <span data-ttu-id="48e08-182">a.</span><span class="sxs-lookup"><span data-stu-id="48e08-182">a.</span></span> <span data-ttu-id="48e08-183">Dans la zone **Nom**, tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="48e08-183">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="48e08-184">b.</span><span class="sxs-lookup"><span data-stu-id="48e08-184">b.</span></span> <span data-ttu-id="48e08-185">Dans la zone **Nom d’utilisateur** , tapez l’adresse e-mail de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="48e08-185">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="48e08-186">c.</span><span class="sxs-lookup"><span data-stu-id="48e08-186">c.</span></span> <span data-ttu-id="48e08-187">Cochez la case **Afficher le mot de passe**, puis notez la valeur affichée dans le champ **Mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="48e08-187">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="48e08-188">d.</span><span class="sxs-lookup"><span data-stu-id="48e08-188">d.</span></span> <span data-ttu-id="48e08-189">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="48e08-189">Click **Create**.</span></span>
 
### <a name="create-a-workrite-test-user"></a><span data-ttu-id="48e08-190">Créer un utilisateur de test Workrite</span><span class="sxs-lookup"><span data-stu-id="48e08-190">Create a Workrite test user</span></span>

<span data-ttu-id="48e08-191">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans Workrite.</span><span class="sxs-lookup"><span data-stu-id="48e08-191">The objective of this section is to create a user called Britta Simon in Workrite.</span></span>

<span data-ttu-id="48e08-192">**Pour créer un utilisateur appelé Britta Simon dans Workrite, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="48e08-192">**To create a user called Britta Simon in Workrite, perform the following steps:**</span></span>

1. <span data-ttu-id="48e08-193">Connectez-vous à votre site d’entreprise Workrite en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="48e08-193">Sign on to your workrite company site as administrator.</span></span>

2. <span data-ttu-id="48e08-194">Dans le volet de navigation, cliquez sur **Admin**.</span><span class="sxs-lookup"><span data-stu-id="48e08-194">In the navigation pane, click **Admin**.</span></span>
   
    ![Contrôle d’administration][400]

3. <span data-ttu-id="48e08-196">Accédez à Quick Links, puis cliquez sur **Create a User**.</span><span class="sxs-lookup"><span data-stu-id="48e08-196">Go to Quick Links, and then click **Create a User**.</span></span>
   
    ![Section Create User][401]

4. <span data-ttu-id="48e08-198">Dans la boîte de dialogue **Create User** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="48e08-198">On the **Create User** dialog, perform the following steps:</span></span>
   
    ![Boîte de dialogue Create User][402]
    
    <span data-ttu-id="48e08-200">a.</span><span class="sxs-lookup"><span data-stu-id="48e08-200">a.</span></span> <span data-ttu-id="48e08-201">Dans la zone de texte **Email**, tapez l’adresse e-mail d’un utilisateur, par exemple, Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="48e08-201">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="48e08-202">b.</span><span class="sxs-lookup"><span data-stu-id="48e08-202">b.</span></span> <span data-ttu-id="48e08-203">Dans la zone de texte **First Name**, tapez le prénom de l’utilisateur, par exemple Britta.</span><span class="sxs-lookup"><span data-stu-id="48e08-203">In the **First Name** textbox, type the firstname of user like Britta.</span></span>

    <span data-ttu-id="48e08-204">c.</span><span class="sxs-lookup"><span data-stu-id="48e08-204">c.</span></span> <span data-ttu-id="48e08-205">Dans la zone de texte **Surname**, tapez le nom de l’utilisateur, par exemple Simon.</span><span class="sxs-lookup"><span data-stu-id="48e08-205">In the **Surname** textbox, type the surname of user like Simon.</span></span>
    
    <span data-ttu-id="48e08-206">d.</span><span class="sxs-lookup"><span data-stu-id="48e08-206">d.</span></span> <span data-ttu-id="48e08-207">Sélectionnez **Client Administrator** pour **Choose Role**.</span><span class="sxs-lookup"><span data-stu-id="48e08-207">Select **Client Administrator** as **Choose Role**.</span></span>
    
    <span data-ttu-id="48e08-208">e.</span><span class="sxs-lookup"><span data-stu-id="48e08-208">e.</span></span> <span data-ttu-id="48e08-209">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="48e08-209">Click **Save**.</span></span>   

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="48e08-210">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="48e08-210">Assign the Azure AD test user</span></span>

<span data-ttu-id="48e08-211">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Workrite.</span><span class="sxs-lookup"><span data-stu-id="48e08-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workrite.</span></span>

![Attribuer le rôle d’utilisateur][200] 

<span data-ttu-id="48e08-213">**Pour affecter Britta Simon à Workrite, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="48e08-213">**To assign Britta Simon to Workrite, perform the following steps:**</span></span>

1. <span data-ttu-id="48e08-214">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="48e08-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="48e08-216">Dans la liste des applications, sélectionnez **Workrite**.</span><span class="sxs-lookup"><span data-stu-id="48e08-216">In the applications list, select **Workrite**.</span></span>

    ![Lien Workrite dans la liste des applications](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_app.png)  

3. <span data-ttu-id="48e08-218">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="48e08-218">In the menu on the left, click **Users and groups**.</span></span>

    ![Lien « Utilisateurs et groupes »][202]

4. <span data-ttu-id="48e08-220">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="48e08-220">Click **Add** button.</span></span> <span data-ttu-id="48e08-221">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="48e08-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Volet Ajouter une attribution][203]

5. <span data-ttu-id="48e08-223">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="48e08-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="48e08-224">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="48e08-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="48e08-225">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="48e08-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="48e08-226">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="48e08-226">Test single sign-on</span></span>

<span data-ttu-id="48e08-227">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="48e08-227">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="48e08-228">Quand vous cliquez sur la vignette Workrite dans le volet d’accès, vous devez être connecté automatiquement à votre application Workrite.</span><span class="sxs-lookup"><span data-stu-id="48e08-228">When you click the Workrite tile in the Access Panel, you should get automatically signed-on to your Workrite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="48e08-229">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="48e08-229">Additional resources</span></span>

* [<span data-ttu-id="48e08-230">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="48e08-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="48e08-231">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="48e08-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_203.png
[400]: ./media/active-directory-saas-workrite-tutorial/tutorial_workrite_400.png
[401]: ./media/active-directory-saas-workrite-tutorial/tutorial_workrite_401.png
[402]: ./media/active-directory-saas-workrite-tutorial/tutorial_workrite_402.png

