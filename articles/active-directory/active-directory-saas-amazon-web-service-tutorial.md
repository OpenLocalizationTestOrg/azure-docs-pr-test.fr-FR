---
title: "Didacticiel : Intégration d’Azure Active Directory à Amazon Web Services (AWS) | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Amazon Web Services (AWS)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7561c20b-2325-4d97-887f-693aa383c7be
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 0fb9c8f428368271b548e3f174726fa01ea910c5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-amazon-web-services-aws"></a><span data-ttu-id="b8670-103">Didacticiel : Intégration d’Azure Active Directory à Amazon Web Services (AWS)</span><span class="sxs-lookup"><span data-stu-id="b8670-103">Tutorial: Azure Active Directory integration with Amazon Web Services (AWS)</span></span>

<span data-ttu-id="b8670-104">Dans ce tutoriel, vous allez apprendre à intégrer Amazon Web Services à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b8670-104">In this tutorial, you learn how to integrate Amazon Web Services (AWS) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b8670-105">L’intégration de Amazon Web Services (AWS) dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="b8670-105">Integrating Amazon Web Services (AWS) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b8670-106">Dans Azure AD, vous pouvez contrôler qui a accès à Amazon Web Services (AWS)</span><span class="sxs-lookup"><span data-stu-id="b8670-106">You can control in Azure AD who has access to Amazon Web Services (AWS)</span></span>
- <span data-ttu-id="b8670-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Amazon Web Services (AWS) (via l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="b8670-107">You can enable your users to automatically get signed-on to Amazon Web Services (AWS) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b8670-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="b8670-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b8670-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b8670-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with Amazon Web Services (AWS), it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in Amazon Web Services (AWS).

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="b8670-110">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="b8670-110">Prerequisites</span></span>

<span data-ttu-id="b8670-111">Pour configurer l’intégration d’Azure AD avec Amazon Web Services (AWS), vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="b8670-111">To configure Azure AD integration with Amazon Web Services (AWS), you need the following items:</span></span>

- <span data-ttu-id="b8670-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="b8670-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b8670-113">Abonnement Amazon Web Services (AWS) avec authentification unique</span><span class="sxs-lookup"><span data-stu-id="b8670-113">Amazon Web Services (AWS) single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b8670-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="b8670-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b8670-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="b8670-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b8670-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="b8670-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="b8670-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b8670-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b8670-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="b8670-118">Scenario description</span></span>
<span data-ttu-id="b8670-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="b8670-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b8670-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="b8670-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b8670-121">Ajout d’Amazon Web Services (AWS) à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="b8670-121">Adding Amazon Web Services (AWS) from the gallery</span></span>
2. <span data-ttu-id="b8670-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b8670-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-amazon-web-services-aws-from-the-gallery"></a><span data-ttu-id="b8670-123">Ajout d’Amazon Web Services (AWS) à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="b8670-123">Adding Amazon Web Services (AWS) from the gallery</span></span>
<span data-ttu-id="b8670-124">Pour configurer l’intégration d’Amazon Web Services (AWS) avec Azure AD, vous devez ajouter Amazon Web Services (AWS), disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="b8670-124">To configure the integration of Amazon Web Services (AWS) into Azure AD, you need to add Amazon Web Services (AWS) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b8670-125">**Pour ajouter Amazon Web Services (AWS) à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b8670-125">**To add Amazon Web Services (AWS) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b8670-126">Dans le volet de navigation gauche du **[Portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b8670-126">In the **[Azure Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b8670-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="b8670-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b8670-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="b8670-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="b8670-131">Cliquez sur le bouton **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="b8670-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="b8670-133">Dans la zone de recherche, tapez **Amazon Web Services (AWS)**.</span><span class="sxs-lookup"><span data-stu-id="b8670-133">In the search box, type **Amazon Web Services (AWS)**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_search.png)

5. <span data-ttu-id="b8670-135">Dans le volet des résultats, sélectionnez **Amazon Web Services (AWS)**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="b8670-135">In the results panel, select **Amazon Web Services (AWS)**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b8670-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b8670-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b8670-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Amazon Web Services (AWS), en tirant parti d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="b8670-138">In this section, you configure and test Azure AD single sign-on with Amazon Web Services (AWS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b8670-139">Pour que l’authentification unique fonctionne, Azure AD a besoin de savoir quelle est l’équivalence de l’utilisateur Amazon Web Services (AWS) dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b8670-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Amazon Web Services (AWS) is to a user in Azure AD.</span></span> <span data-ttu-id="b8670-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Amazon Web Services (AWS) associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="b8670-140">In other words, a link relationship between an Azure AD user and the related user in Amazon Web Services (AWS) needs to be established.</span></span>

<span data-ttu-id="b8670-141">Pour cela, attribuez la valeur du **nom d’utilisateur** dans Azure AD au **nom d’utilisateur** dans Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="b8670-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Amazon Web Services (AWS).</span></span>

<span data-ttu-id="b8670-142">Pour configurer et tester l’authentification unique Azure AD avec Amazon Web Services (AWS), vous avez besoin de suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="b8670-142">To configure and test Azure AD single sign-on with Amazon Web Services (AWS), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b8670-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="b8670-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b8670-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b8670-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b8670-145">**[Création d’un utilisateur de test Amazon Web Services](#creating-an-amazon-web-services-test-user)** pour avoir un équivalent de Britta Simon dans Amazon Web Services (AWS) lié à sa représentation dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b8670-145">**[Creating an Amazon Web Services test user](#creating-an-amazon-web-services-test-user)** - to have a counterpart of Britta Simon in Amazon Web Services (AWS) that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="b8670-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b8670-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b8670-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="b8670-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b8670-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b8670-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b8670-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le nouveau portail Azure et configurer l’authentification unique dans votre application Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="b8670-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Amazon Web Services (AWS) application.</span></span>

<span data-ttu-id="b8670-150">**Pour configurer l’authentification unique Azure AD avec Amazon Web Services (AWS), procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b8670-150">**To configure Azure AD single sign-on with Amazon Web Services (AWS), perform the following steps:**</span></span>

1. <span data-ttu-id="b8670-151">Dans le portail Azure, sur la page d’intégration de l’application **Amazon Web Services (AWS)**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="b8670-151">In the Azure Portal, on the **Amazon Web Services (AWS)** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="b8670-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="b8670-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_samlbase.png)

3. <span data-ttu-id="b8670-155">Dans la section **Domaine et URL d’Amazon Web Services (AWS)**, l’utilisateur n’aura pas à effectuer les étapes que l’application a déjà intégrées préalablement avec Azure.</span><span class="sxs-lookup"><span data-stu-id="b8670-155">On the **Amazon Web Services (AWS) Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_url.png)

4. <span data-ttu-id="b8670-157">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier XML sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="b8670-157">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_certificate.png)

5. <span data-ttu-id="b8670-159">Votre application Amazon Web Services (AWS) attend les assertions SAML dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="b8670-159">The Amazon Web Services (AWS) Software application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="b8670-160">Configurez les revendications suivantes pour cette application.</span><span class="sxs-lookup"><span data-stu-id="b8670-160">Please configure the following claims for this application.</span></span> <span data-ttu-id="b8670-161">Vous pouvez gérer les valeurs de ces attributs à partir de la section « **Attributs utilisateur** » sur la page d’intégration des applications.</span><span class="sxs-lookup"><span data-stu-id="b8670-161">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="b8670-162">La capture d’écran suivante montre un exemple :</span><span class="sxs-lookup"><span data-stu-id="b8670-162">The following screenshot shows an example for this.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_attribute.png)

6. <span data-ttu-id="b8670-164">Dans la section **Attributs utilisateur** de la boîte de dialogue **Authentification unique**, configurez le jeton SAML comme sur l’image ci-dessus et procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="b8670-164">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="b8670-165">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="b8670-165">Attribute Name</span></span>  | <span data-ttu-id="b8670-166">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="b8670-166">Attribute Value</span></span> | <span data-ttu-id="b8670-167">Espace de noms</span><span class="sxs-lookup"><span data-stu-id="b8670-167">Namespace</span></span> |
    | --------------- | --------------- | --------------- |
    | <span data-ttu-id="b8670-168">RoleSessionName</span><span class="sxs-lookup"><span data-stu-id="b8670-168">RoleSessionName</span></span> | <span data-ttu-id="b8670-169">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="b8670-169">user.userprincipalname</span></span> | <span data-ttu-id="b8670-170">https://aws.amazon.com/SAML/Attributes</span><span class="sxs-lookup"><span data-stu-id="b8670-170">https://aws.amazon.com/SAML/Attributes</span></span> |
    | <span data-ttu-id="b8670-171">Rôle</span><span class="sxs-lookup"><span data-stu-id="b8670-171">Role</span></span>            | <span data-ttu-id="b8670-172">user.assignedroles</span><span class="sxs-lookup"><span data-stu-id="b8670-172">user.assignedroles</span></span> |  <span data-ttu-id="b8670-173">https://aws.amazon.com/SAML/Attributes</span><span class="sxs-lookup"><span data-stu-id="b8670-173">https://aws.amazon.com/SAML/Attributes</span></span> |
    
    >[!TIP]
    ><span data-ttu-id="b8670-174">Vous devez configurer l’approvisionnement des utilisateurs dans Azure AD pour extraire tous les rôles de la console AWS.</span><span class="sxs-lookup"><span data-stu-id="b8670-174">You need to configure the user provisioning in Azure AD to fetch all the roles from AWS Console.</span></span> <span data-ttu-id="b8670-175">Consultez les étapes de l’approvisionnement ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="b8670-175">Please refer the provisioning steps below.</span></span>

    <span data-ttu-id="b8670-176">a.</span><span class="sxs-lookup"><span data-stu-id="b8670-176">a.</span></span> <span data-ttu-id="b8670-177">Cliquez sur **Ajouter un attribut** pour ouvrir la boîte de dialogue **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="b8670-177">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="b8670-179">b.</span><span class="sxs-lookup"><span data-stu-id="b8670-179">b.</span></span> <span data-ttu-id="b8670-180">Dans la zone de texte **Attribut**, indiquez le nom d’attribut pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="b8670-180">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="b8670-182">c.</span><span class="sxs-lookup"><span data-stu-id="b8670-182">c.</span></span> <span data-ttu-id="b8670-183">Dans la liste **Valeur** , saisissez la valeur d’attribut affichée pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="b8670-183">From the **Value** list, type the attribute value shown for that row.</span></span> <span data-ttu-id="b8670-184">Ajoutez la valeur d’espace de noms indiquée ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="b8670-184">Add the Namespace value as given above.</span></span>
    
    <span data-ttu-id="b8670-185">d.</span><span class="sxs-lookup"><span data-stu-id="b8670-185">d.</span></span> <span data-ttu-id="b8670-186">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b8670-186">Click **Ok**.</span></span>

7. <span data-ttu-id="b8670-187">Cliquez sur le bouton **Enregistrer** pour enregistrer les paramètres sur Azure.</span><span class="sxs-lookup"><span data-stu-id="b8670-187">Click **Save** button to save the settings on Azure.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="b8670-189">Dans une autre fenêtre de navigateur, connectez-vous au site de votre entreprise Amazon Web Services (AWS) en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="b8670-189">In a different browser window, sign-on to your Amazon Web Services (AWS) company site as administrator.</span></span>

9. <span data-ttu-id="b8670-190">Cliquez sur **Console Home**.</span><span class="sxs-lookup"><span data-stu-id="b8670-190">Click **Console Home**.</span></span>
   
    ![Configurer l’authentification unique][11]

10. <span data-ttu-id="b8670-192">Cliquez sur **IAM** à partir du service **Security, Identity & Compliance** (Sécurité, identité et conformité).</span><span class="sxs-lookup"><span data-stu-id="b8670-192">Click **IAM** from **Security, Identity & Compliance** service.</span></span>
   
    ![Configurer l’authentification unique][12]

11. <span data-ttu-id="b8670-194">Cliquez sur **Identity Providers**, puis sur **Create Provider**.</span><span class="sxs-lookup"><span data-stu-id="b8670-194">Click **Identity Providers**, and then click **Create Provider**.</span></span>
   
    ![Configurer l’authentification unique][13]

12. <span data-ttu-id="b8670-196">Dans la page **Configure Provider** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="b8670-196">On the **Configure Provider** dialog page, perform the following steps:</span></span>
   
    ![Configurer l’authentification unique][14]
 
    <span data-ttu-id="b8670-198">a.</span><span class="sxs-lookup"><span data-stu-id="b8670-198">a.</span></span> <span data-ttu-id="b8670-199">Pour **Provider Type**, sélectionnez **SAML**.</span><span class="sxs-lookup"><span data-stu-id="b8670-199">As **Provider Type**, select **SAML**.</span></span>

    <span data-ttu-id="b8670-200">b.</span><span class="sxs-lookup"><span data-stu-id="b8670-200">b.</span></span> <span data-ttu-id="b8670-201">Dans la zone de texte **Provider Name**, tapez le nom d’un fournisseur (par ex. : *WAAD*).</span><span class="sxs-lookup"><span data-stu-id="b8670-201">In the **Provider Name** textbox, type a provider name (e.g.: *WAAD*).</span></span>

    <span data-ttu-id="b8670-202">c.</span><span class="sxs-lookup"><span data-stu-id="b8670-202">c.</span></span> <span data-ttu-id="b8670-203">Pour télécharger votre fichier de métadonnées, cliquez sur **Choose File**.</span><span class="sxs-lookup"><span data-stu-id="b8670-203">To upload your downloaded metadata file, click **Choose File**.</span></span>

    <span data-ttu-id="b8670-204">d.</span><span class="sxs-lookup"><span data-stu-id="b8670-204">d.</span></span> <span data-ttu-id="b8670-205">Cliquez sur **Next Step**.</span><span class="sxs-lookup"><span data-stu-id="b8670-205">Click **Next Step**.</span></span>

13. <span data-ttu-id="b8670-206">Dans la page **Verify Provider Information**, cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="b8670-206">On the **Verify Provider Information** dialog page, click **Create**.</span></span> 
    
    ![Configurer l’authentification unique][15]

14. <span data-ttu-id="b8670-208">Cliquez sur **Roles**, puis sur **Create New Role**.</span><span class="sxs-lookup"><span data-stu-id="b8670-208">Click **Roles**, and then click **Create New Role**.</span></span> 
    
    ![Configurer l’authentification unique][16]

15. <span data-ttu-id="b8670-210">Dans la boîte de dialogue **Set Role Name** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="b8670-210">On the **Set Role Name** dialog, perform the following steps:</span></span> 
    
    ![Configurer l’authentification unique][17] 

    <span data-ttu-id="b8670-212">a.</span><span class="sxs-lookup"><span data-stu-id="b8670-212">a.</span></span> <span data-ttu-id="b8670-213">Dans la zone de texte **Role Name**, tapez un nom de rôle (par ex. : *Utilisateur_test*).</span><span class="sxs-lookup"><span data-stu-id="b8670-213">In the **Role Name** textbox, type a role name (e.g.: *TestUser*).</span></span> 

    <span data-ttu-id="b8670-214">b.</span><span class="sxs-lookup"><span data-stu-id="b8670-214">b.</span></span> <span data-ttu-id="b8670-215">Cliquez sur **Next Step**.</span><span class="sxs-lookup"><span data-stu-id="b8670-215">Click **Next Step**.</span></span>

16. <span data-ttu-id="b8670-216">Dans la boîte de dialogue **Select Role Type** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="b8670-216">On the **Select Role Type** dialog, perform the following steps:</span></span> 
    
    ![Configurer l’authentification unique][18] 

    <span data-ttu-id="b8670-218">a.</span><span class="sxs-lookup"><span data-stu-id="b8670-218">a.</span></span> <span data-ttu-id="b8670-219">Sélectionnez **Role For Identity Provider Access**.</span><span class="sxs-lookup"><span data-stu-id="b8670-219">Select **Role For Identity Provider Access**.</span></span> 

    <span data-ttu-id="b8670-220">b.</span><span class="sxs-lookup"><span data-stu-id="b8670-220">b.</span></span> <span data-ttu-id="b8670-221">Dans la section **Grant Web Single Sign-On (WebSSO) access to SAML providers**, cliquez sur **Select**.</span><span class="sxs-lookup"><span data-stu-id="b8670-221">In the **Grant Web Single Sign-On (WebSSO) access to SAML providers** section, click **Select**.</span></span>

17. <span data-ttu-id="b8670-222">Dans la boîte de dialogue **Establish Trust** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="b8670-222">On the **Establish Trust** dialog, perform the following steps:</span></span>  
    
    ![Configurer l’authentification unique][19] 

    <span data-ttu-id="b8670-224">a.</span><span class="sxs-lookup"><span data-stu-id="b8670-224">a.</span></span> <span data-ttu-id="b8670-225">Pour le fournisseur SAML, sélectionnez celui que vous avez déjà créé (par ex. : *WAAD*)</span><span class="sxs-lookup"><span data-stu-id="b8670-225">As SAML provider, select the SAML provider you have created previously (e.g.: *WAAD*)</span></span>
  
    <span data-ttu-id="b8670-226">b.</span><span class="sxs-lookup"><span data-stu-id="b8670-226">b.</span></span> <span data-ttu-id="b8670-227">Cliquez sur **Next Step**.</span><span class="sxs-lookup"><span data-stu-id="b8670-227">Click **Next Step**.</span></span>

18. <span data-ttu-id="b8670-228">Dans la boîte de dialogue **Verify Role Trust**, cliquez sur **Next Step**.</span><span class="sxs-lookup"><span data-stu-id="b8670-228">On the **Verify Role Trust** dialog, click **Next Step**.</span></span>
    
    ![Configurer l’authentification unique][32]

19. <span data-ttu-id="b8670-230">Dans la boîte de dialogue **Attach Policy**, cliquez sur **Next Step**.</span><span class="sxs-lookup"><span data-stu-id="b8670-230">On the **Attach Policy** dialog, click **Next Step**.</span></span>
    
    ![Configurer l’authentification unique][33]

20. <span data-ttu-id="b8670-232">Dans la boîte de dialogue **Review** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="b8670-232">On the **Review** dialog, perform the following steps:</span></span>
    
    ![Configurer l’authentification unique][34]
 
    <span data-ttu-id="b8670-234">a.</span><span class="sxs-lookup"><span data-stu-id="b8670-234">a.</span></span> <span data-ttu-id="b8670-235">Cliquez sur **Create Role**.</span><span class="sxs-lookup"><span data-stu-id="b8670-235">Click **Create Role**.</span></span>

    <span data-ttu-id="b8670-236">b.</span><span class="sxs-lookup"><span data-stu-id="b8670-236">b.</span></span> <span data-ttu-id="b8670-237">Créez autant de rôles que nécessaire et mappez-les vers le fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="b8670-237">Create as many roles as needed and map them to the Identity Provider.</span></span>

21. <span data-ttu-id="b8670-238">À présent, configurez l’approvisionnement d’utilisateur pour récupérer tous les rôles à partir d’AWS.</span><span class="sxs-lookup"><span data-stu-id="b8670-238">Now configure the user provisioning to fetch all the roles from AWS</span></span>

    <span data-ttu-id="b8670-239">a.</span><span class="sxs-lookup"><span data-stu-id="b8670-239">a.</span></span> <span data-ttu-id="b8670-240">Dans la console AWS, connectez-vous avec votre compte racine.</span><span class="sxs-lookup"><span data-stu-id="b8670-240">In the AWS Console login with your root account</span></span>

    <span data-ttu-id="b8670-241">b.</span><span class="sxs-lookup"><span data-stu-id="b8670-241">b.</span></span> <span data-ttu-id="b8670-242">Dans le coin supérieur droit, cliquez sur votre nom, puis sur l’option **My Security Credentials** (Mes informations d’identification).</span><span class="sxs-lookup"><span data-stu-id="b8670-242">In the top right corner click your name and then click the **My Security Credentials** option.</span></span> <span data-ttu-id="b8670-243">Un écran contenant un message d’avertissement s’affiche.</span><span class="sxs-lookup"><span data-stu-id="b8670-243">This will open up a screen as a warning message.</span></span> <span data-ttu-id="b8670-244">Cliquez sur le bouton **Informations d'identification de sécurité** pour passer l’écran.</span><span class="sxs-lookup"><span data-stu-id="b8670-244">Click the button **Security Credentials** button to pass the screen.</span></span>
        
       ![Configurer l’authentification unique][36]

       ![Configurer l’authentification unique][37]

    <span data-ttu-id="b8670-247">c.</span><span class="sxs-lookup"><span data-stu-id="b8670-247">c.</span></span> <span data-ttu-id="b8670-248">Dans la section Access Keys (Clés d’accès), cliquez sur le bouton **Create New Access Key (Créer un clé d’accès)**.</span><span class="sxs-lookup"><span data-stu-id="b8670-248">In the Access Keys section click the **Create New Access Key** button.</span></span> <span data-ttu-id="b8670-249">Cela génère l’ID de clé d’accès et une valeur de jeton.</span><span class="sxs-lookup"><span data-stu-id="b8670-249">This generates the Access Key ID and a token value.</span></span>
    
       ![Configurer l’authentification unique][38]

    <span data-ttu-id="b8670-251">d.</span><span class="sxs-lookup"><span data-stu-id="b8670-251">d.</span></span> <span data-ttu-id="b8670-252">Copiez ces deux valeurs et téléchargez-les, pour ne pas les perdre.</span><span class="sxs-lookup"><span data-stu-id="b8670-252">Copy both these values and also download it, so that you don't lose it.</span></span>

    <span data-ttu-id="b8670-253">e.</span><span class="sxs-lookup"><span data-stu-id="b8670-253">e.</span></span> <span data-ttu-id="b8670-254">Dans le portail Azure, sur la page d’intégration de l’application Amazon Web Services (AWS), cliquez sur **Provisioning** (Approvisionnement).</span><span class="sxs-lookup"><span data-stu-id="b8670-254">In the Azure Portal, on the Amazon Web Services (AWS) application integration page, click **Provisioning**.</span></span>
        
       ![Configurer l’authentification unique][35]

    <span data-ttu-id="b8670-256">f.</span><span class="sxs-lookup"><span data-stu-id="b8670-256">f.</span></span> <span data-ttu-id="b8670-257">Définissez le mode d’approvisionnement sur **Automatique**</span><span class="sxs-lookup"><span data-stu-id="b8670-257">Set the Provisioning mode to **Automatic**</span></span>
        
       ![Configurer l’authentification unique][39]

    <span data-ttu-id="b8670-259">g.</span><span class="sxs-lookup"><span data-stu-id="b8670-259">g.</span></span> <span data-ttu-id="b8670-260">À présent, dans les champs **clientsecret** et **Jeton secret**, collez les valeurs correspondantes, que vous avez copiées à partir de la console AWS.</span><span class="sxs-lookup"><span data-stu-id="b8670-260">Now in the **clientsecret** and **Secret Token** paste the corresponding values, which you have copied from AWS Console.</span></span>
    
    <span data-ttu-id="b8670-261">h.</span><span class="sxs-lookup"><span data-stu-id="b8670-261">h.</span></span> <span data-ttu-id="b8670-262">Vous pouvez cliquer sur le bouton **Tester la connexion** pour tester la connectivité.</span><span class="sxs-lookup"><span data-stu-id="b8670-262">You can click the **Test Connection** button to test the connectivity.</span></span> <span data-ttu-id="b8670-263">Une fois cette opération réussie, vous pouvez démarrer le connecteur d’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="b8670-263">Once that is successful then you can start the provisioning connector.</span></span>
       
       ![Configurer l’authentification unique][40]

    <span data-ttu-id="b8670-265">i.</span><span class="sxs-lookup"><span data-stu-id="b8670-265">i.</span></span> <span data-ttu-id="b8670-266">Définissez le paramètre État de l’approvisionnement sur **Activé**.</span><span class="sxs-lookup"><span data-stu-id="b8670-266">Now enable the Provisioning Status to **On**.</span></span> <span data-ttu-id="b8670-267">L’extraction des rôles de l’application commence.</span><span class="sxs-lookup"><span data-stu-id="b8670-267">This starts fetching the roles from the application.</span></span>

       ![Configurer l’authentification unique][41]

    > [!NOTE]
    > <span data-ttu-id="b8670-269">Le service d’approvisionnement Azure AD s’exécute après un certain temps pour synchroniser les rôles à partir d’AWS.</span><span class="sxs-lookup"><span data-stu-id="b8670-269">Azure AD Provisioning service runs every after some time to sync the roles from AWS.</span></span> <span data-ttu-id="b8670-270">Tous les rôles AWS associés au fournisseur d’identité doivent s’afficher dans Azure AD. Vous pouvez les utiliser pour attribuer l’application aux utilisateurs ou aux groupes.</span><span class="sxs-lookup"><span data-stu-id="b8670-270">You should see all the Identity Provider attached AWS roles into Azure AD and you can use them while assigning the application to users or groups.</span></span>

<!--### Next steps

To ensure users can sign-in to Amazon Web Services (AWS) after it has been configured to use Azure Active Directory, review the following tasks and topics:

- User accounts must be pre-provisioned into Amazon Web Services (AWS) prior to sign-in. To set this up, see Provisioning.
 
- Users must be assigned access to Amazon Web Services (AWS) in Azure AD to sign-in. To assign users, see Users.
 
- To configure access polices for Amazon Web Services (AWS) users, see Access Policies.
 
- For additional information on deploying single sign-on to users, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b8670-271">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="b8670-271">Creating an Azure AD test user</span></span>
<span data-ttu-id="b8670-272">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="b8670-272">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="b8670-274">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b8670-274">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b8670-275">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b8670-275">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b8670-277">Accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs** pour afficher la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="b8670-277">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b8670-279">En haut de la boîte de dialogue, cliquez sur **Ajouter** pour ouvrir la boîte de dialogue **Utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="b8670-279">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b8670-281">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="b8670-281">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b8670-283">a.</span><span class="sxs-lookup"><span data-stu-id="b8670-283">a.</span></span> <span data-ttu-id="b8670-284">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b8670-284">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b8670-285">b.</span><span class="sxs-lookup"><span data-stu-id="b8670-285">b.</span></span> <span data-ttu-id="b8670-286">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b8670-286">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b8670-287">c.</span><span class="sxs-lookup"><span data-stu-id="b8670-287">c.</span></span> <span data-ttu-id="b8670-288">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="b8670-288">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b8670-289">d.</span><span class="sxs-lookup"><span data-stu-id="b8670-289">d.</span></span> <span data-ttu-id="b8670-290">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="b8670-290">Click **Create**.</span></span>
 
### <a name="creating-an-amazon-web-services-test-user"></a><span data-ttu-id="b8670-291">Création d’un utilisateur de test pour Amazon Web Services</span><span class="sxs-lookup"><span data-stu-id="b8670-291">Creating an Amazon Web Services test user</span></span>

<span data-ttu-id="b8670-292">Pour que les utilisateurs d’Azure AD puissent se connecter à Amazon Web Services (AWS), ils doivent être configurés dans Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="b8670-292">In order to enable Azure AD users to log in to Amazon Web Services (AWS), they must be provisioned into Amazon Web Services (AWS).</span></span> <span data-ttu-id="b8670-293">L’approvisionnement d’Amazon Web Services (AWS) s’effectue manuellement.</span><span class="sxs-lookup"><span data-stu-id="b8670-293">In the case of Amazon Web Services (AWS), provisioning is a manual task.</span></span>

<span data-ttu-id="b8670-294">**Pour approvisionner un compte d’utilisateur, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b8670-294">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="b8670-295">Connectez-vous au site de votre entreprise **Amazon Web Services (AWS)** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="b8670-295">Log in to your **Amazon Web Services (AWS)** company site as administrator.</span></span>

2. <span data-ttu-id="b8670-296">Cliquez sur l’icône **Console Home** .</span><span class="sxs-lookup"><span data-stu-id="b8670-296">Click the **Console Home** icon.</span></span> 
   
    ![Configurer l’authentification unique][11]

3. <span data-ttu-id="b8670-298">Cliquez sur Identity and Access Management.</span><span class="sxs-lookup"><span data-stu-id="b8670-298">Click Identity and Access Management.</span></span> 
   
    ![Configurer l’authentification unique][28]

4. <span data-ttu-id="b8670-300">Dans le tableau de bord, cliquez sur **Users** (Utilisateurs), puis sur **Create New Users** (Créer des utilisateurs).</span><span class="sxs-lookup"><span data-stu-id="b8670-300">In the Dashboard, click **Users**, and then click **Create New Users**.</span></span> 
   
    ![Configurer l’authentification unique][29]

5. <span data-ttu-id="b8670-302">Dans la boîte de dialogue Create User, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="b8670-302">On the Create User dialog, perform the following steps:</span></span> 
   
    ![Configurer l’authentification unique][30]   
    
    <span data-ttu-id="b8670-304">a.</span><span class="sxs-lookup"><span data-stu-id="b8670-304">a.</span></span> <span data-ttu-id="b8670-305">Dans les zones de texte **Entrer les noms d’utilisateur** , tapez le nom d’utilisateur de Brita Simon (userprincipalname) dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b8670-305">In the **Enter User Names** textboxes, type Brita Simon's user name (userprincipalname) in Azure AD.</span></span>

    <span data-ttu-id="b8670-306">b.</span><span class="sxs-lookup"><span data-stu-id="b8670-306">b.</span></span> <span data-ttu-id="b8670-307">Cliquez sur **Create** (Créer).</span><span class="sxs-lookup"><span data-stu-id="b8670-307">Click **Create.**</span></span>
        
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b8670-308">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="b8670-308">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b8670-309">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="b8670-309">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Amazon Web Services (AWS).</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="b8670-311">**Pour attribuer Britta Simon à Amazon Web Services (AWS), procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b8670-311">**To assign Britta Simon to Amazon Web Services (AWS), perform the following steps:**</span></span>

1. <span data-ttu-id="b8670-312">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="b8670-312">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="b8670-314">Dans la liste des applications, sélectionnez **Amazon Web Services (AWS)**.</span><span class="sxs-lookup"><span data-stu-id="b8670-314">In the applications list, select **Amazon Web Services (AWS)**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_app.png) 

3. <span data-ttu-id="b8670-316">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="b8670-316">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="b8670-318">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="b8670-318">Click **Add** button.</span></span> <span data-ttu-id="b8670-319">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="b8670-319">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="b8670-321">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="b8670-321">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b8670-322">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="b8670-322">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b8670-323">Sous l’onglet **Sélectionner un rôle**, sélectionnez le rôle souhaité pour l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b8670-323">On **Select Role** tab, select the appropriate role for the user.</span></span> <span data-ttu-id="b8670-324">Tous ces rôles comportent un nom de rôle et un nom de fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="b8670-324">All these roles are shown with the role name and identity provider name.</span></span> <span data-ttu-id="b8670-325">De cette façon, vous pouvez facilement identifier les rôles AWS.</span><span class="sxs-lookup"><span data-stu-id="b8670-325">This way you can easily identify the roles from AWS.</span></span>

8. <span data-ttu-id="b8670-326">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="b8670-326">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b8670-327">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="b8670-327">Testing single sign-on</span></span>

<span data-ttu-id="b8670-328">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="b8670-328">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b8670-329">Lorsque vous cliquez sur la vignette Amazon Web Services (AWS) dans le volet d’accès, vous devez être connecté automatiquement à votre application Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="b8670-329">When you click the Amazon Web Services (AWS) tile in the Access Panel, you should get automatically signed-on to your Amazon Web Services (AWS) application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b8670-330">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="b8670-330">Additional resources</span></span>

* [<span data-ttu-id="b8670-331">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b8670-331">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b8670-332">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="b8670-332">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_203.png
[11]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795031.png
[12]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795032.png
[13]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795033.png
[14]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795034.png
[15]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795035.png
[16]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795022.png
[17]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795023.png
[18]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795024.png
[19]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795025.png
[20]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950351.png
[21]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_80.png
[22]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950352.png
[23]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_81.png
[24]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950353.png
[25]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_15.png

[28]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950321.png
[29]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795037.png
[30]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795038.png
[32]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950251.png
[33]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950252.png
[34]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950253.png
[35]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning.png
[36]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials.png
[37]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials_continue.png
[38]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_createnewaccesskey.png
[39]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_automatic.png
[40]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_testconnection.png
[41]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_on.png
