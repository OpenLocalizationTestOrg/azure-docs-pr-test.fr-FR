---
title: "Didacticiel : Intégration d’Azure Active Directory avec Envoy | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Envoy."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 71f7afcc-1033-4098-9b7e-4f9f2b26f734
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: 49211b35ab3e28e0df914061e7fa623907935638
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-envoy"></a><span data-ttu-id="87ab2-103">Didacticiel : Intégration d’Azure Active Directory avec Envoy</span><span class="sxs-lookup"><span data-stu-id="87ab2-103">Tutorial: Azure Active Directory integration with Envoy</span></span>

<span data-ttu-id="87ab2-104">Dans ce didacticiel, vous allez apprendre à intégrer Envoy à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="87ab2-104">In this tutorial, you learn how to integrate Envoy with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="87ab2-105">L’intégration d’Envoy à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="87ab2-105">Integrating Envoy with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="87ab2-106">Dans Azure AD, vous pouvez contrôler qui a accès à Envoy.</span><span class="sxs-lookup"><span data-stu-id="87ab2-106">You can control in Azure AD who has access to Envoy.</span></span>
- <span data-ttu-id="87ab2-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Envoy (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="87ab2-107">You can enable your users to automatically get signed-on to Envoy (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="87ab2-108">Vous pouvez gérer vos comptes dans un emplacement central : le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="87ab2-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="87ab2-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="87ab2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="87ab2-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="87ab2-110">Prerequisites</span></span>

<span data-ttu-id="87ab2-111">Pour configurer l’intégration d’Azure AD à Envoy, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="87ab2-111">To configure Azure AD integration with Envoy, you need the following items:</span></span>

- <span data-ttu-id="87ab2-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="87ab2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="87ab2-113">Un abonnement Envoy pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="87ab2-113">An Envoy single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="87ab2-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="87ab2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="87ab2-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="87ab2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="87ab2-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="87ab2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="87ab2-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="87ab2-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="87ab2-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="87ab2-118">Scenario description</span></span>
<span data-ttu-id="87ab2-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="87ab2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="87ab2-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="87ab2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="87ab2-121">Ajout d’Envoy à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="87ab2-121">Adding Envoy from the gallery</span></span>
2. <span data-ttu-id="87ab2-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="87ab2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-envoy-from-the-gallery"></a><span data-ttu-id="87ab2-123">Ajout d’Envoy à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="87ab2-123">Adding Envoy from the gallery</span></span>
<span data-ttu-id="87ab2-124">Pour configurer l’intégration d’Envoy à Azure AD, vous devez ajouter Envoy, disponible dans la galerie, à votre liste d’applications SaaS managées.</span><span class="sxs-lookup"><span data-stu-id="87ab2-124">To configure the integration of Envoy into Azure AD, you need to add Envoy from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="87ab2-125">**Pour ajouter Envoy à partir de la galerie, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="87ab2-125">**To add Envoy from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="87ab2-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="87ab2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Bouton Azure Active Directory][1]

2. <span data-ttu-id="87ab2-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="87ab2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="87ab2-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="87ab2-129">Then go to **All applications**.</span></span>

    ![Panneau Applications d’entreprise][2]
    
3. <span data-ttu-id="87ab2-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="87ab2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Bouton Nouvelle application][3]

4. <span data-ttu-id="87ab2-133">Dans la zone de recherche, tapez **Envoy**, sélectionnez **Envoy** dans le panneau de résultats, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="87ab2-133">In the search box, type **Envoy**, select **Envoy** from result panel then click **Add** button to add the application.</span></span>

    ![Envoy dans la liste des résultats](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="87ab2-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="87ab2-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="87ab2-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Envoy, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="87ab2-136">In this section, you configure and test Azure AD single sign-on with Envoy based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="87ab2-137">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Envoy équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="87ab2-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Envoy is to a user in Azure AD.</span></span> <span data-ttu-id="87ab2-138">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Envoy associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="87ab2-138">In other words, a link relationship between an Azure AD user and the related user in Envoy needs to be established.</span></span>

<span data-ttu-id="87ab2-139">Dans Envoy, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="87ab2-139">In Envoy, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="87ab2-140">Pour configurer et tester l’authentification unique Azure AD avec Envoy, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="87ab2-140">To configure and test Azure AD single sign-on with Envoy, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="87ab2-141">**[Configurer l’authentification unique Azure AD](#configure-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="87ab2-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="87ab2-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="87ab2-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="87ab2-143">**[Créer un utilisateur de test Envoy](#create-an-envoy-test-user)** pour avoir un équivalent de Britta Simon dans Envoy, associé à sa représentation dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="87ab2-143">**[Create an Envoy test user](#create-an-envoy-test-user)** - to have a counterpart of Britta Simon in Envoy that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="87ab2-144">**[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="87ab2-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="87ab2-145">**[Tester l’authentification unique](#test-single-sign-on)** : pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="87ab2-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="87ab2-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="87ab2-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="87ab2-147">Dans cette section, vous activez l’authentification unique Azure AD dans le portail Azure et configurez l’authentification unique dans votre application Envoy.</span><span class="sxs-lookup"><span data-stu-id="87ab2-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Envoy application.</span></span>

<span data-ttu-id="87ab2-148">**Pour configurer l’authentification unique Azure AD avec Envoy, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="87ab2-148">**To configure Azure AD single sign-on with Envoy, perform the following steps:**</span></span>

1. <span data-ttu-id="87ab2-149">Dans le portail Azure, dans la page d’intégration de l’application **Envoy**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="87ab2-149">In the Azure portal, on the **Envoy** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="87ab2-151">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="87ab2-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_samlbase.png)

3. <span data-ttu-id="87ab2-153">Dans la section **Domaine et URL Envoy**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="87ab2-153">On the **Envoy Domain and URLs** section, perform the following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL Envoy](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_url.png)

    <span data-ttu-id="87ab2-155">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<tenant-name>.Envoy.com`</span><span class="sxs-lookup"><span data-stu-id="87ab2-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.Envoy.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="87ab2-156">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="87ab2-156">This value is not real.</span></span> <span data-ttu-id="87ab2-157">Mettez à jour cette valeur avec l’URL de connexion réelle.</span><span class="sxs-lookup"><span data-stu-id="87ab2-157">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="87ab2-158">Pour obtenir cette valeur, contactez [l’équipe du support Envoy](https://envoy.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="87ab2-158">Contact [Envoy Client support team](https://envoy.com/contact/) to get this value.</span></span>

4. <span data-ttu-id="87ab2-159">Dans la section **Certificat de signature SAML**, copiez la valeur **THUMBPRINT** du certificat.</span><span class="sxs-lookup"><span data-stu-id="87ab2-159">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate..</span></span>

    ![Lien Téléchargement de certificat](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_certificate.png) 

5. <span data-ttu-id="87ab2-161">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="87ab2-161">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-envoy-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="87ab2-163">Dans la section **Configuration de Envoy**, cliquez sur **Configurer Envoy** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="87ab2-163">On the **Envoy Configuration** section, click **Configure Envoy** to open **Configure sign-on** window.</span></span> <span data-ttu-id="87ab2-164">Copiez l**’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="87ab2-164">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuration d’Envoy](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_configure.png)

7. <span data-ttu-id="87ab2-166">Dans une autre fenêtre de navigateur web, connectez-vous au site de votre entreprise Envoy en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="87ab2-166">In a different web browser window, log into your Envoy company site as an administrator.</span></span>

8. <span data-ttu-id="87ab2-167">Dans la barre d’outils située en haut, cliquez sur **Settings**.</span><span class="sxs-lookup"><span data-stu-id="87ab2-167">In the toolbar on the top, click **Settings**.</span></span>

    <span data-ttu-id="87ab2-168">![Envoy](./media/active-directory-saas-envoy-tutorial/ic776782.png "Envoy")</span><span class="sxs-lookup"><span data-stu-id="87ab2-168">![Envoy](./media/active-directory-saas-envoy-tutorial/ic776782.png "Envoy")</span></span>

9. <span data-ttu-id="87ab2-169">Cliquez sur **Company**.</span><span class="sxs-lookup"><span data-stu-id="87ab2-169">Click **Company**.</span></span>

    <span data-ttu-id="87ab2-170">![Company](./media/active-directory-saas-envoy-tutorial/ic776783.png "Company")</span><span class="sxs-lookup"><span data-stu-id="87ab2-170">![Company](./media/active-directory-saas-envoy-tutorial/ic776783.png "Company")</span></span>

10. <span data-ttu-id="87ab2-171">Cliquez sur **SAML**.</span><span class="sxs-lookup"><span data-stu-id="87ab2-171">Click **SAML**.</span></span>

    <span data-ttu-id="87ab2-172">![SAML](./media/active-directory-saas-envoy-tutorial/ic776784.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="87ab2-172">![SAML](./media/active-directory-saas-envoy-tutorial/ic776784.png "SAML")</span></span>

11. <span data-ttu-id="87ab2-173">Dans la section de configuration **SAML Authentication** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="87ab2-173">In the **SAML Authentication** configuration section, perform the following steps:</span></span>

    <span data-ttu-id="87ab2-174">![SAML authentication](./media/active-directory-saas-envoy-tutorial/ic776785.png "SAML authentication")</span><span class="sxs-lookup"><span data-stu-id="87ab2-174">![SAML authentication](./media/active-directory-saas-envoy-tutorial/ic776785.png "SAML authentication")</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="87ab2-175">La valeur de l’ID d’emplacement du siège est générée automatiquement par l’application.</span><span class="sxs-lookup"><span data-stu-id="87ab2-175">The value for the HQ location ID is auto generated by the application.</span></span>
    
    <span data-ttu-id="87ab2-176">a.</span><span class="sxs-lookup"><span data-stu-id="87ab2-176">a.</span></span> <span data-ttu-id="87ab2-177">Dans la zone de texte **Fingerprint** (Empreinte digitale), collez la valeur du certificat **Empreinte** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="87ab2-177">In **Fingerprint** textbox, paste the **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="87ab2-178">b.</span><span class="sxs-lookup"><span data-stu-id="87ab2-178">b.</span></span> <span data-ttu-id="87ab2-179">Collez la valeur **URL du service d’authentification unique SAML** copiée dans le portail Azure dans la zone de texte **IDENTITY PROVIDER HTTP SAML URL** (URL HTTP SAML du fournisseur d’identité).</span><span class="sxs-lookup"><span data-stu-id="87ab2-179">Paste **SAML Single Sign-On Service URL** value, which you have copied form the Azure portal into the **IDENTITY PROVIDER HTTP SAML URL** textbox.</span></span>
    
    <span data-ttu-id="87ab2-180">c.</span><span class="sxs-lookup"><span data-stu-id="87ab2-180">c.</span></span> <span data-ttu-id="87ab2-181">Cliquez sur **Save changes**.</span><span class="sxs-lookup"><span data-stu-id="87ab2-181">Click **Save changes**.</span></span>

> [!TIP]
> <span data-ttu-id="87ab2-182">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="87ab2-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="87ab2-183">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="87ab2-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="87ab2-184">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="87ab2-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="87ab2-185">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="87ab2-185">Create an Azure AD test user</span></span>

<span data-ttu-id="87ab2-186">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="87ab2-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="87ab2-188">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="87ab2-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="87ab2-189">Dans le volet gauche du Portail Azure, cliquez sur le bouton **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="87ab2-189">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Bouton Azure Active Directory](./media/active-directory-saas-envoy-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="87ab2-191">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="87ab2-191">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Liens « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/active-directory-saas-envoy-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="87ab2-193">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="87ab2-193">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Bouton Ajouter](./media/active-directory-saas-envoy-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="87ab2-195">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="87ab2-195">In the **User** dialog box, perform the following steps:</span></span>

    ![Boîte de dialogue Utilisateur](./media/active-directory-saas-envoy-tutorial/create_aaduser_04.png)

    <span data-ttu-id="87ab2-197">a.</span><span class="sxs-lookup"><span data-stu-id="87ab2-197">a.</span></span> <span data-ttu-id="87ab2-198">Dans la zone **Nom**, tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="87ab2-198">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="87ab2-199">b.</span><span class="sxs-lookup"><span data-stu-id="87ab2-199">b.</span></span> <span data-ttu-id="87ab2-200">Dans la zone **Nom d’utilisateur** , tapez l’adresse e-mail de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="87ab2-200">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="87ab2-201">c.</span><span class="sxs-lookup"><span data-stu-id="87ab2-201">c.</span></span> <span data-ttu-id="87ab2-202">Cochez la case **Afficher le mot de passe**, puis notez la valeur affichée dans le champ **Mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="87ab2-202">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="87ab2-203">d.</span><span class="sxs-lookup"><span data-stu-id="87ab2-203">d.</span></span> <span data-ttu-id="87ab2-204">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="87ab2-204">Click **Create**.</span></span>
 
### <a name="create-an-envoy-test-user"></a><span data-ttu-id="87ab2-205">Créer un utilisateur de test Envoy</span><span class="sxs-lookup"><span data-stu-id="87ab2-205">Create an Envoy test user</span></span>

<span data-ttu-id="87ab2-206">Aucun élément d'action ne vous permet de configurer l’approvisionnement des utilisateurs dans Envoy.</span><span class="sxs-lookup"><span data-stu-id="87ab2-206">There is no action item for you to configure user provisioning to Envoy.</span></span> <span data-ttu-id="87ab2-207">Lorsqu’un utilisateur tente de se connecter à Envoy à l’aide du panneau d’accès, Envoy vérifie si cet utilisateur existe.</span><span class="sxs-lookup"><span data-stu-id="87ab2-207">When an assigned user tries to log into Envoy using the access panel, Envoy checks whether the user exists.</span></span> <span data-ttu-id="87ab2-208">Si aucun compte d'utilisateur n’est disponible, Envoy le crée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="87ab2-208">If there is no user account available yet, it is automatically created by Envoy.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="87ab2-209">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="87ab2-209">Assign the Azure AD test user</span></span>

<span data-ttu-id="87ab2-210">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Envoy.</span><span class="sxs-lookup"><span data-stu-id="87ab2-210">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Envoy.</span></span>

![Attribuer le rôle utilisateur][200] 

<span data-ttu-id="87ab2-212">**Pour attribuer Britta Simon à Envoy, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="87ab2-212">**To assign Britta Simon to Envoy, perform the following steps:**</span></span>

1. <span data-ttu-id="87ab2-213">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="87ab2-213">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="87ab2-215">Dans la liste des applications, sélectionnez **Envoy**.</span><span class="sxs-lookup"><span data-stu-id="87ab2-215">In the applications list, select **Envoy**.</span></span>

    ![Lien Envoy dans la liste des applications](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_app.png)  

3. <span data-ttu-id="87ab2-217">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="87ab2-217">In the menu on the left, click **Users and groups**.</span></span>

    ![Lien « Utilisateurs et groupes »][202]

4. <span data-ttu-id="87ab2-219">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="87ab2-219">Click **Add** button.</span></span> <span data-ttu-id="87ab2-220">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="87ab2-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Volet Ajouter une attribution][203]

5. <span data-ttu-id="87ab2-222">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="87ab2-222">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="87ab2-223">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="87ab2-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="87ab2-224">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="87ab2-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="87ab2-225">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="87ab2-225">Test single sign-on</span></span>

<span data-ttu-id="87ab2-226">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="87ab2-226">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="87ab2-227">Lorsque vous cliquez sur la vignette Envoy dans le volet d’accès, vous devez être connecté automatiquement à votre application Envoy.</span><span class="sxs-lookup"><span data-stu-id="87ab2-227">When you click the Envoy tile in the Access Panel, you should get automatically signed-on to your Envoy application.</span></span>
<span data-ttu-id="87ab2-228">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="87ab2-228">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="87ab2-229">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="87ab2-229">Additional resources</span></span>

* [<span data-ttu-id="87ab2-230">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="87ab2-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="87ab2-231">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="87ab2-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_203.png

