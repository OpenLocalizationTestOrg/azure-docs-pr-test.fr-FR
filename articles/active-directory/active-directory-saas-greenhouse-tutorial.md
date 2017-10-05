---
title: "Didacticiel : intégration d’Azure Active Directory à Greenhouse | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Greenhouse."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 78ec1766-4f79-4f16-9a66-d5584c4b6151
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: d3aba4aab8ded8749db2bf8197f57a6763008c60
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-greenhouse"></a><span data-ttu-id="f1104-103">Didacticiel : Intégration d’Azure Active Directory avec Greenhouse</span><span class="sxs-lookup"><span data-stu-id="f1104-103">Tutorial: Azure Active Directory integration with Greenhouse</span></span>

<span data-ttu-id="f1104-104">Ce didacticiel explique comment intégrer Greenhouse avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f1104-104">In this tutorial, you learn how to integrate Greenhouse with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f1104-105">L’intégration de Greenhouse avec Azure AD offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="f1104-105">Integrating Greenhouse with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f1104-106">Dans Azure AD, vous pouvez contrôler qui a accès à Greenhouse.</span><span class="sxs-lookup"><span data-stu-id="f1104-106">You can control in Azure AD who has access to Greenhouse.</span></span>
- <span data-ttu-id="f1104-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Greenhouse (via l’authentification unique) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f1104-107">You can enable your users to automatically get signed-on to Greenhouse (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="f1104-108">Vous pouvez gérer vos comptes dans un emplacement central : le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f1104-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="f1104-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f1104-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f1104-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f1104-110">Prerequisites</span></span>

<span data-ttu-id="f1104-111">Pour configurer l’intégration d’Azure AD avec Greenhouse, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f1104-111">To configure Azure AD integration with Greenhouse, you need the following items:</span></span>

- <span data-ttu-id="f1104-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1104-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f1104-113">Un abonnement Greenhouse pour lequel l’authentification unique (SSO) est activée</span><span class="sxs-lookup"><span data-stu-id="f1104-113">A Greenhouse single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f1104-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="f1104-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f1104-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="f1104-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f1104-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="f1104-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f1104-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f1104-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f1104-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="f1104-118">Scenario description</span></span>
<span data-ttu-id="f1104-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="f1104-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f1104-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="f1104-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f1104-121">Ajout de Greenhouse à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="f1104-121">Adding Greenhouse from the gallery</span></span>
2. <span data-ttu-id="f1104-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1104-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-greenhouse-from-the-gallery"></a><span data-ttu-id="f1104-123">Ajout de Greenhouse à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="f1104-123">Adding Greenhouse from the gallery</span></span>
<span data-ttu-id="f1104-124">Pour configurer l’intégration de à partir de la galerie avec Azure AD, vous devez ajouter à partir de la galerie à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="f1104-124">To configure the integration of Greenhouse into Azure AD, you need to add Greenhouse from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f1104-125">**Pour ajouter Greenhouse à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f1104-125">**To add Greenhouse from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f1104-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f1104-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Bouton Azure Active Directory][1]

2. <span data-ttu-id="f1104-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="f1104-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f1104-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="f1104-129">Then go to **All applications**.</span></span>

    ![Panneau Applications d’entreprise][2]
    
3. <span data-ttu-id="f1104-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="f1104-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Bouton Nouvelle application][3]

4. <span data-ttu-id="f1104-133">Dans la zone de recherche, tapez **Greenhouse**, sélectionnez **dans le panneau** de résultats, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="f1104-133">In the search box, type **Greenhouse**, select **Greenhouse** from result panel then click **Add** button to add the application.</span></span>

    ![Greenhouse dans la liste des résultats](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f1104-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1104-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="f1104-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Greenhouse, sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="f1104-136">In this section, you configure and test Azure AD single sign-on with Greenhouse based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f1104-137">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Greenhouse équivalent à un utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f1104-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Greenhouse is to a user in Azure AD.</span></span> <span data-ttu-id="f1104-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur Greenhouse associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="f1104-138">In other words, a link relationship between an Azure AD user and the related user in Greenhouse needs to be established.</span></span>

<span data-ttu-id="f1104-139">Dans Greenhouse, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **Username** pour établir la relation de lien.</span><span class="sxs-lookup"><span data-stu-id="f1104-139">In Greenhouse, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f1104-140">Pour configurer et tester l’authentification unique Azure AD avec Greenhouse, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="f1104-140">To configure and test Azure AD single sign-on with Greenhouse, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f1104-141">**[Configurer l’authentification unique Azure AD](#configure-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="f1104-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f1104-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f1104-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f1104-143">**[Créer un utilisateur de test Fuse](#create-a-greenhouse-test-user)** pour avoir dans Greenhouse un équivalent de Britta Simon lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="f1104-143">**[Create a Greenhouse test user](#create-a-greenhouse-test-user)** - to have a counterpart of Britta Simon in Greenhouse that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f1104-144">**[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f1104-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f1104-145">**[Tester l’authentification unique](#test-single-sign-on)** : pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="f1104-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="f1104-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1104-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="f1104-147">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Greenhouse.</span><span class="sxs-lookup"><span data-stu-id="f1104-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Greenhouse application.</span></span>

<span data-ttu-id="f1104-148">**Pour configurer l’authentification unique Azure AD avec Greenhouse, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f1104-148">**To configure Azure AD single sign-on with Greenhouse, perform the following steps:**</span></span>

1. <span data-ttu-id="f1104-149">Dans le portail Azure, sur la page d’intégration de l’application **Greenhouse**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="f1104-149">In the Azure portal, on the **Greenhouse** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="f1104-151">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="f1104-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_samlbase.png)

3. <span data-ttu-id="f1104-153">Dans la section **Domaine et URL Greenhouse**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f1104-153">On the **Greenhouse Domain and URLs** section, perform the following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL Greenhouse](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_url.png)

    <span data-ttu-id="f1104-155">a.</span><span class="sxs-lookup"><span data-stu-id="f1104-155">a.</span></span> <span data-ttu-id="f1104-156">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<companyname>.greenhouse.io`</span><span class="sxs-lookup"><span data-stu-id="f1104-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.greenhouse.io`</span></span>

    <span data-ttu-id="f1104-157">b.</span><span class="sxs-lookup"><span data-stu-id="f1104-157">b.</span></span> <span data-ttu-id="f1104-158">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<companyname>.greenhouse.io`</span><span class="sxs-lookup"><span data-stu-id="f1104-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.greenhouse.io`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f1104-159">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="f1104-159">These values are not real.</span></span> <span data-ttu-id="f1104-160">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="f1104-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f1104-161">Pour obtenir ces valeurs, contactez l’[équipe de support technique Greenhouse](https://www.greenhouse.io/contact).</span><span class="sxs-lookup"><span data-stu-id="f1104-161">Contact [Greenhouse Client support team](https://www.greenhouse.io/contact) to get these values.</span></span> 
 


4. <span data-ttu-id="f1104-162">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="f1104-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Lien Téléchargement de certificat](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_certificate.png) 

5. <span data-ttu-id="f1104-164">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="f1104-164">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-greenhouse-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f1104-166">Pour configurer l’authentification unique côté **Greenhouse**, vous devez envoyer le **XML de métadonnées** téléchargé à [l’équipe de support technique Greenhouse](http://www.greenhouse.io/contact).</span><span class="sxs-lookup"><span data-stu-id="f1104-166">To configure single sign-on on **Greenhouse** side, you need to send the downloaded **Metadata XML** to [Greenhouse support team](http://www.greenhouse.io/contact).</span></span>

> [!TIP]
> <span data-ttu-id="f1104-167">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="f1104-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f1104-168">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="f1104-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f1104-169">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f1104-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f1104-170">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1104-170">Create an Azure AD test user</span></span>

<span data-ttu-id="f1104-171">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f1104-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="f1104-173">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f1104-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f1104-174">Dans le volet gauche du Portail Azure, cliquez sur le bouton **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f1104-174">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Bouton Azure Active Directory](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="f1104-176">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="f1104-176">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Liens « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="f1104-178">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="f1104-178">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Bouton Ajouter](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="f1104-180">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f1104-180">In the **User** dialog box, perform the following steps:</span></span>

    ![Boîte de dialogue Utilisateur](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_04.png)

    <span data-ttu-id="f1104-182">a.</span><span class="sxs-lookup"><span data-stu-id="f1104-182">a.</span></span> <span data-ttu-id="f1104-183">Dans la zone **Nom**, tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f1104-183">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f1104-184">b.</span><span class="sxs-lookup"><span data-stu-id="f1104-184">b.</span></span> <span data-ttu-id="f1104-185">Dans la zone **Nom d’utilisateur** , tapez l’adresse e-mail de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f1104-185">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="f1104-186">c.</span><span class="sxs-lookup"><span data-stu-id="f1104-186">c.</span></span> <span data-ttu-id="f1104-187">Cochez la case **Afficher le mot de passe**, puis notez la valeur affichée dans le champ **Mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="f1104-187">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="f1104-188">d.</span><span class="sxs-lookup"><span data-stu-id="f1104-188">d.</span></span> <span data-ttu-id="f1104-189">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="f1104-189">Click **Create**.</span></span>
 
### <a name="create-a-greenhouse-test-user"></a><span data-ttu-id="f1104-190">Créer un utilisateur de test Greenhouse</span><span class="sxs-lookup"><span data-stu-id="f1104-190">Create a Greenhouse test user</span></span>

<span data-ttu-id="f1104-191">Pour se connecter à Greenhouse, les utilisateurs d’Azure AD doivent être approvisionnés dans Greenhouse.</span><span class="sxs-lookup"><span data-stu-id="f1104-191">In order to enable Azure AD users to log into Greenhouse, they must be provisioned into Greenhouse.</span></span> <span data-ttu-id="f1104-192">Dans le cas de Greenhouse, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="f1104-192">In the case of Greenhouse, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="f1104-193">Vous pouvez utiliser tout autre outil ou n’importe quelle API de création de compte d’utilisateur fournis par Greenhouse pour approvisionner des comptes d’utilisateur Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f1104-193">You can use any other Greenhouse user account creation tools or APIs provided by Greenhouse to provision AAD user accounts.</span></span> 

<span data-ttu-id="f1104-194">**Pour approvisionner un compte d’utilisateur, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f1104-194">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="f1104-195">Connectez-vous au site d’entreprise **Greenhouse** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="f1104-195">Log in to your **Greenhouse** company site as an administrator.</span></span>

2. <span data-ttu-id="f1104-196">Dans le menu situé en haut, cliquez sur **Configure (Configurer)**, puis sur **Users (Utilisateurs)**.</span><span class="sxs-lookup"><span data-stu-id="f1104-196">In the menu on the top, click **Configure**, and then click **Users**.</span></span>
   
   <span data-ttu-id="f1104-197">![Utilisateurs](./media/active-directory-saas-greenhouse-tutorial/ic790791.png "Utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="f1104-197">![Users](./media/active-directory-saas-greenhouse-tutorial/ic790791.png "Users")</span></span>

3. <span data-ttu-id="f1104-198">Cliquez sur **New Users**.</span><span class="sxs-lookup"><span data-stu-id="f1104-198">Click **New Users**.</span></span>
   
   <span data-ttu-id="f1104-199">![Nouvel utilisateur](./media/active-directory-saas-greenhouse-tutorial/ic790792.png "Nouvel utilisateur")</span><span class="sxs-lookup"><span data-stu-id="f1104-199">![New User](./media/active-directory-saas-greenhouse-tutorial/ic790792.png "New User")</span></span>

4. <span data-ttu-id="f1104-200">Dans la section **Add New User** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f1104-200">In the **Add New User** section, perform the following steps:</span></span>
   
   <span data-ttu-id="f1104-201">![Add New User](./media/active-directory-saas-greenhouse-tutorial/ic790793.png "Add New User")</span><span class="sxs-lookup"><span data-stu-id="f1104-201">![Add New User](./media/active-directory-saas-greenhouse-tutorial/ic790793.png "Add New User")</span></span>

   <span data-ttu-id="f1104-202">a.</span><span class="sxs-lookup"><span data-stu-id="f1104-202">a.</span></span> <span data-ttu-id="f1104-203">Dans la zone de texte **Enter user emails** , tapez l’adresse de messagerie d’un compte Azure Active Directory valide à approvisionner.</span><span class="sxs-lookup"><span data-stu-id="f1104-203">In the **Enter user emails** textbox, type the email address of a valid Azure Active Directory account you want to provision.</span></span>

   <span data-ttu-id="f1104-204">b.</span><span class="sxs-lookup"><span data-stu-id="f1104-204">b.</span></span> <span data-ttu-id="f1104-205">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="f1104-205">Click **Save**.</span></span>    
   
      >[!NOTE]
      ><span data-ttu-id="f1104-206">Le titulaire du compte Azure Active Directory recevra un message électronique contenant un lien pour confirmer le compte avant qu’il ne soit activé.</span><span class="sxs-lookup"><span data-stu-id="f1104-206">The Azure Active Directory account holders will receive an email including a link to confirm the account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="f1104-207">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1104-207">Assign the Azure AD test user</span></span>

<span data-ttu-id="f1104-208">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Greenhouse.</span><span class="sxs-lookup"><span data-stu-id="f1104-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Greenhouse.</span></span>

![Attribuer le rôle utilisateur][200] 

<span data-ttu-id="f1104-210">**Pour affecter Britta Simon à Greenhouse, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f1104-210">**To assign Britta Simon to Greenhouse, perform the following steps:**</span></span>

1. <span data-ttu-id="f1104-211">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="f1104-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="f1104-213">Dans la liste des applications, sélectionnez **Greenhouse**.</span><span class="sxs-lookup"><span data-stu-id="f1104-213">In the applications list, select **Greenhouse**.</span></span>

    ![Lien Greenhouse dans la liste des applications](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_app.png)  

3. <span data-ttu-id="f1104-215">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="f1104-215">In the menu on the left, click **Users and groups**.</span></span>

    ![Lien « Utilisateurs et groupes »][202]

4. <span data-ttu-id="f1104-217">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="f1104-217">Click **Add** button.</span></span> <span data-ttu-id="f1104-218">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="f1104-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Volet Ajouter une attribution][203]

5. <span data-ttu-id="f1104-220">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="f1104-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f1104-221">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="f1104-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f1104-222">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="f1104-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="f1104-223">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="f1104-223">Test single sign-on</span></span>

<span data-ttu-id="f1104-224">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="f1104-224">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f1104-225">Lorsque vous cliquez sur la vignette Greenhouse dans le volet d’accès, vous devez être connecté automatiquement à votre application Greenhouse.</span><span class="sxs-lookup"><span data-stu-id="f1104-225">When you click the Greenhouse tile in the Access Panel, you should get automatically signed-on to your Greenhouse application.</span></span>
<span data-ttu-id="f1104-226">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f1104-226">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f1104-227">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="f1104-227">Additional resources</span></span>

* [<span data-ttu-id="f1104-228">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f1104-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f1104-229">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="f1104-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_203.png

