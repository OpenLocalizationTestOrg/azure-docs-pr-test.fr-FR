---
title: "Didacticiel : intégration d’Azure Active Directory à Druva | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Druva."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ab92b600-1fea-4905-b1c7-ef8e4d8c495c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: b23e73c47b9a00893e036b67826e4b7ead819a1d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-druva"></a><span data-ttu-id="4d49d-103">Didacticiel : Intégration d’Azure Active Directory à Druva</span><span class="sxs-lookup"><span data-stu-id="4d49d-103">Tutorial: Azure Active Directory integration with Druva</span></span>

<span data-ttu-id="4d49d-104">Dans ce didacticiel, vous apprenez à intégrer Druva dans Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4d49d-104">In this tutorial, you learn how to integrate Druva with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4d49d-105">L’intégration de Druva dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="4d49d-105">Integrating Druva with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4d49d-106">Dans Azure AD, vous pouvez contrôler qui a accès à Druva.</span><span class="sxs-lookup"><span data-stu-id="4d49d-106">You can control in Azure AD who has access to Druva.</span></span>
- <span data-ttu-id="4d49d-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Druva (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d49d-107">You can enable your users to automatically get signed-on to Druva (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="4d49d-108">Vous pouvez gérer vos comptes dans un emplacement central : le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="4d49d-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="4d49d-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4d49d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4d49d-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="4d49d-110">Prerequisites</span></span>

<span data-ttu-id="4d49d-111">Pour configurer l’intégration d’Azure AD avec Druva, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="4d49d-111">To configure Azure AD integration with Druva, you need the following items:</span></span>

- <span data-ttu-id="4d49d-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d49d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4d49d-113">Un abonnement Druva pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="4d49d-113">A Druva single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4d49d-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="4d49d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4d49d-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="4d49d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4d49d-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="4d49d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4d49d-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4d49d-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4d49d-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="4d49d-118">Scenario description</span></span>
<span data-ttu-id="4d49d-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="4d49d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4d49d-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="4d49d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4d49d-121">Ajout de Druva depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="4d49d-121">Adding Druva from the gallery</span></span>
2. <span data-ttu-id="4d49d-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d49d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-druva-from-the-gallery"></a><span data-ttu-id="4d49d-123">Ajout de Druva depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="4d49d-123">Adding Druva from the gallery</span></span>
<span data-ttu-id="4d49d-124">Pour configurer l’intégration de Druva avec Azure AD, vous devez ajouter Druva disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="4d49d-124">To configure the integration of Druva into Azure AD, you need to add Druva from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4d49d-125">**Pour ajouter Druva à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4d49d-125">**To add Druva from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4d49d-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4d49d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Bouton Azure Active Directory][1]

2. <span data-ttu-id="4d49d-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="4d49d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4d49d-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="4d49d-129">Then go to **All applications**.</span></span>

    ![Panneau Applications d’entreprise][2]
    
3. <span data-ttu-id="4d49d-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="4d49d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Bouton Nouvelle application][3]

4. <span data-ttu-id="4d49d-133">Dans la zone de recherche, tapez **Druva**, sélectionnez **Druva** dans le volet de résultats, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="4d49d-133">In the search box, type **Druva**, select **Druva** from result panel then click **Add** button to add the application.</span></span>

    ![Druva dans la liste des résultats](./media/active-directory-saas-druva-tutorial/tutorial_druva_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="4d49d-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d49d-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="4d49d-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Druva, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="4d49d-136">In this section, you configure and test Azure AD single sign-on with Druva based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4d49d-137">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Druva correspondant dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d49d-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Druva is to a user in Azure AD.</span></span> <span data-ttu-id="4d49d-138">En d’autres termes, une relation entre un utilisateur Azure AD et l’utilisateur Druva associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="4d49d-138">In other words, a link relationship between an Azure AD user and the related user in Druva needs to be established.</span></span>

<span data-ttu-id="4d49d-139">Dans Druva, assignez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="4d49d-139">In Druva, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4d49d-140">Pour configurer et tester l’authentification unique Azure AD avec Druva, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="4d49d-140">To configure and test Azure AD single sign-on with Druva, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4d49d-141">**[Configurer l’authentification unique Azure AD](#configure-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="4d49d-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4d49d-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4d49d-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4d49d-143">**[Créer utilisateur de test Druva](#create-a-druva-test-user)** pour avoir un équivalent de Britta Simon dans Druva lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="4d49d-143">**[Create a Druva test user](#create-a-druva-test-user)** - to have a counterpart of Britta Simon in Druva that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4d49d-144">**[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d49d-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4d49d-145">**[Tester l’authentification unique](#test-single-sign-on)** : pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="4d49d-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="4d49d-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d49d-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="4d49d-147">Dans cette section, vous activez l’authentification unique Azure AD dans le portail Azure et configurez l’authentification unique dans votre application Druva.</span><span class="sxs-lookup"><span data-stu-id="4d49d-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Druva application.</span></span>

<span data-ttu-id="4d49d-148">**Pour configurer l’authentification unique Azure AD avec Druva, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4d49d-148">**To configure Azure AD single sign-on with Druva, perform the following steps:**</span></span>

1. <span data-ttu-id="4d49d-149">Dans le Portail Azure, sur la page d’intégration de l’application **Druva**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="4d49d-149">In the Azure portal, on the **Druva** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="4d49d-151">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="4d49d-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-druva-tutorial/tutorial_druva_samlbase.png)

3. <span data-ttu-id="4d49d-153">Dans la section **Domaine et URL Druva**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="4d49d-153">On the **Druva Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-druva-tutorial/tutorial_druva_url.png)

    <span data-ttu-id="4d49d-155">Dans la zone de texte **URL de connexion**, entrez l’URL : `https://cloud.druva.com/home`</span><span class="sxs-lookup"><span data-stu-id="4d49d-155">In the **Sign-on URL** textbox, type the URL: `https://cloud.druva.com/home`</span></span>

4. <span data-ttu-id="4d49d-156">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="4d49d-156">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Lien de téléchargement du certificat](./media/active-directory-saas-druva-tutorial/tutorial_druva_certificate.png) 

5. <span data-ttu-id="4d49d-158">Votre application Druva attend les assertions SAML dans un format spécifique, ce qui vous oblige à ajouter des mappages d’attributs personnalisés à votre configuration **Attributs du jeton SAML**.</span><span class="sxs-lookup"><span data-stu-id="4d49d-158">Your Druva application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **SAML Token Attributes** configuration.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-druva-tutorial/tutorial_druva_attribute.png)

6. <span data-ttu-id="4d49d-160">Dans la section **Attributs utilisateur** de la boîte de dialogue **Authentification unique**, configurez l’attribut du jeton SAML comme sur l’image précédente, puis procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="4d49d-160">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span></span>

    | <span data-ttu-id="4d49d-161">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="4d49d-161">Attribute Name</span></span>      | <span data-ttu-id="4d49d-162">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="4d49d-162">Attribute Value</span></span>      |
    | ------------------- | -------------------- |
    | <span data-ttu-id="4d49d-163">insync\_auth\_token</span><span class="sxs-lookup"><span data-stu-id="4d49d-163">insync\_auth\_token</span></span> |<span data-ttu-id="4d49d-164">Entrez la valeur du jeton générée</span><span class="sxs-lookup"><span data-stu-id="4d49d-164">Enter the token generated value</span></span> |
    
    <span data-ttu-id="4d49d-165">a.</span><span class="sxs-lookup"><span data-stu-id="4d49d-165">a.</span></span> <span data-ttu-id="4d49d-166">Cliquez sur **Ajouter un attribut** pour ouvrir la boîte de dialogue **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="4d49d-166">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-druva-tutorial/tutorial_attribute_04.png)
    
    ![Configurer l’authentification unique](./media/active-directory-saas-druva-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="4d49d-169">b.</span><span class="sxs-lookup"><span data-stu-id="4d49d-169">b.</span></span> <span data-ttu-id="4d49d-170">Dans la zone de texte **Attribut**, indiquez le nom d’attribut pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="4d49d-170">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="4d49d-171">c.</span><span class="sxs-lookup"><span data-stu-id="4d49d-171">c.</span></span> <span data-ttu-id="4d49d-172">Dans la liste **Valeur** , saisissez la valeur d’attribut affichée pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="4d49d-172">From the **Value** list, type the attribute value shown for that row.</span></span> <span data-ttu-id="4d49d-173">La valeur du jeton générée est expliquée plus loin dans le didacticiel.</span><span class="sxs-lookup"><span data-stu-id="4d49d-173">The token generated value is explained later in tutorial.</span></span>
    
    <span data-ttu-id="4d49d-174">d.</span><span class="sxs-lookup"><span data-stu-id="4d49d-174">d.</span></span> <span data-ttu-id="4d49d-175">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="4d49d-175">Click **Ok**.</span></span>    

7. <span data-ttu-id="4d49d-176">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="4d49d-176">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-druva-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="4d49d-178">Dans la section **Configuration de Druva** , cliquez sur **Configurer Druva** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="4d49d-178">On the **Druva Configuration** section, click **Configure Druva** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4d49d-179">Copiez **l’URL de déconnexion et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="4d49d-179">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-druva-tutorial/tutorial_druva_configure.png) 

9. <span data-ttu-id="4d49d-181">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Druva en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="4d49d-181">In a different web browser window, log in to your Druva company site as an administrator.</span></span>

10. <span data-ttu-id="4d49d-182">Accédez à **Manage \> Settings**.</span><span class="sxs-lookup"><span data-stu-id="4d49d-182">Go to **Manage \> Settings**.</span></span>

    <span data-ttu-id="4d49d-183">![Paramètres](./media/active-directory-saas-druva-tutorial/ic795091.png "Paramètres")</span><span class="sxs-lookup"><span data-stu-id="4d49d-183">![Settings](./media/active-directory-saas-druva-tutorial/ic795091.png "Settings")</span></span>

11. <span data-ttu-id="4d49d-184">Dans la boîte de dialogue Single Sign-On Settings, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="4d49d-184">On the Single Sign-On Settings dialog, perform the following steps:</span></span>

    <span data-ttu-id="4d49d-185">![Paramètres d’authentification unique](./media/active-directory-saas-druva-tutorial/ic795092.png "paramètres d’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="4d49d-185">![Single Sign-On Settings](./media/active-directory-saas-druva-tutorial/ic795092.png "Single Sign-On Settings")</span></span>
    
    <span data-ttu-id="4d49d-186">a.</span><span class="sxs-lookup"><span data-stu-id="4d49d-186">a.</span></span> <span data-ttu-id="4d49d-187">Collez la valeur **URL du service d’authentification unique SAML** copiée dans le portail Azure dans la zone de texte **Identity Provider Login URL (URL de connexion du fournisseur d’identité)**.</span><span class="sxs-lookup"><span data-stu-id="4d49d-187">Paste **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **ID Provider Login URL** textbox.</span></span>
    
    <span data-ttu-id="4d49d-188">b.</span><span class="sxs-lookup"><span data-stu-id="4d49d-188">b.</span></span> <span data-ttu-id="4d49d-189">Collez la valeur **URL d’authentification**  que vous avez copié à partir du portail Azure dans la zone de texte **Identity Provider Login URL (URL de connexion du fournisseur d’identité)**.</span><span class="sxs-lookup"><span data-stu-id="4d49d-189">Paste **Sign-Out URL** value, which you have copied from the Azure portal into the **ID Provider Logout URL** textbox.</span></span>
    
     <span data-ttu-id="4d49d-190">c.</span><span class="sxs-lookup"><span data-stu-id="4d49d-190">c.</span></span> <span data-ttu-id="4d49d-191">Ouvrez votre certificat codé en base 64 dans le bloc-notes, copiez son contenu dans le Presse-papiers, puis collez-le dans la zone de texte **ID Provider Certificate** .</span><span class="sxs-lookup"><span data-stu-id="4d49d-191">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **ID Provider Certificate** textbox</span></span>
     
     <span data-ttu-id="4d49d-192">d.</span><span class="sxs-lookup"><span data-stu-id="4d49d-192">d.</span></span> <span data-ttu-id="4d49d-193">Pour ouvrir la page **Settings**, cliquez sur**Save**.</span><span class="sxs-lookup"><span data-stu-id="4d49d-193">To open the **Settings** page, click **Save**.</span></span>

12. <span data-ttu-id="4d49d-194">Dans la page **Settings**, cliquez sur **Generate SSO Token**.</span><span class="sxs-lookup"><span data-stu-id="4d49d-194">On the **Settings** page, click **Generate SSO Token**.</span></span>

    <span data-ttu-id="4d49d-195">![Paramètres](./media/active-directory-saas-druva-tutorial/ic795093.png "Paramètres")</span><span class="sxs-lookup"><span data-stu-id="4d49d-195">![Settings](./media/active-directory-saas-druva-tutorial/ic795093.png "Settings")</span></span>

13. <span data-ttu-id="4d49d-196">Dans la boîte de dialogue **Single Sign-on Authentication Token**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="4d49d-196">On the **Single Sign-on Authentication Token** dialog, perform the following steps:</span></span>

    <span data-ttu-id="4d49d-197">![SSO Token](./media/active-directory-saas-druva-tutorial/ic795094.png "SSO Token")</span><span class="sxs-lookup"><span data-stu-id="4d49d-197">![SSO Token](./media/active-directory-saas-druva-tutorial/ic795094.png "SSO Token")</span></span>
    
    <span data-ttu-id="4d49d-198">a.</span><span class="sxs-lookup"><span data-stu-id="4d49d-198">a.</span></span> <span data-ttu-id="4d49d-199">Cliquez sur **Copier**, collez la valeur copiée dans la zone de texte **Valeur** de la section **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="4d49d-199">Click **Copy**, Paste copied value in the **Value** textbox in the **Add Attribute** section.</span></span>
    
    <span data-ttu-id="4d49d-200">b.</span><span class="sxs-lookup"><span data-stu-id="4d49d-200">b.</span></span> <span data-ttu-id="4d49d-201">Cliquez sur **Fermer**.</span><span class="sxs-lookup"><span data-stu-id="4d49d-201">Click **Close**.</span></span>

> [!TIP]
> <span data-ttu-id="4d49d-202">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="4d49d-202">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4d49d-203">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="4d49d-203">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4d49d-204">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4d49d-204">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4d49d-205">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d49d-205">Create an Azure AD test user</span></span>

<span data-ttu-id="4d49d-206">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="4d49d-206">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="4d49d-208">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4d49d-208">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4d49d-209">Dans le volet gauche du Portail Azure, cliquez sur le bouton **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4d49d-209">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Bouton Azure Active Directory](./media/active-directory-saas-druva-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="4d49d-211">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="4d49d-211">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Liens « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/active-directory-saas-druva-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="4d49d-213">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="4d49d-213">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Bouton Ajouter](./media/active-directory-saas-druva-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="4d49d-215">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="4d49d-215">In the **User** dialog box, perform the following steps:</span></span>

    ![Boîte de dialogue Utilisateur](./media/active-directory-saas-druva-tutorial/create_aaduser_04.png)

    <span data-ttu-id="4d49d-217">a.</span><span class="sxs-lookup"><span data-stu-id="4d49d-217">a.</span></span> <span data-ttu-id="4d49d-218">Dans la zone **Nom**, tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4d49d-218">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4d49d-219">b.</span><span class="sxs-lookup"><span data-stu-id="4d49d-219">b.</span></span> <span data-ttu-id="4d49d-220">Dans la zone **Nom d’utilisateur** , tapez l’adresse e-mail de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4d49d-220">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="4d49d-221">c.</span><span class="sxs-lookup"><span data-stu-id="4d49d-221">c.</span></span> <span data-ttu-id="4d49d-222">Cochez la case **Afficher le mot de passe**, puis notez la valeur affichée dans le champ **Mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="4d49d-222">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="4d49d-223">d.</span><span class="sxs-lookup"><span data-stu-id="4d49d-223">d.</span></span> <span data-ttu-id="4d49d-224">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="4d49d-224">Click **Create**.</span></span>
 
### <a name="create-a-druva-test-user"></a><span data-ttu-id="4d49d-225">Créer un utilisateur de test Druva</span><span class="sxs-lookup"><span data-stu-id="4d49d-225">Create a Druva test user</span></span>

<span data-ttu-id="4d49d-226">Pour se connecter à Druva, les utilisateurs d’Azure AD doivent être approvisionnés dans Druva.</span><span class="sxs-lookup"><span data-stu-id="4d49d-226">In order to enable Azure AD users to log in to Druva, they must be provisioned into Druva.</span></span> <span data-ttu-id="4d49d-227">Dans le cas de Druva, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="4d49d-227">In the case of Druva, provisioning is a manual task.</span></span>

<span data-ttu-id="4d49d-228">**Pour configurer l'approvisionnement des utilisateurs, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4d49d-228">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="4d49d-229">Connectez-vous à votre site d’entreprise **Druva** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="4d49d-229">Log in to your **Druva** company site as administrator.</span></span>

2. <span data-ttu-id="4d49d-230">Accédez à **Gérer \> Utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="4d49d-230">Go to **Manage \> Users**.</span></span>
   
   <span data-ttu-id="4d49d-231">![Gestion des utilisateurs](./media/active-directory-saas-druva-tutorial/ic795097.png "Gestion des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="4d49d-231">![Manage Users](./media/active-directory-saas-druva-tutorial/ic795097.png "Manage Users")</span></span>

3. <span data-ttu-id="4d49d-232">Cliquez sur **Create New**.</span><span class="sxs-lookup"><span data-stu-id="4d49d-232">Click **Create New**.</span></span>
   
   <span data-ttu-id="4d49d-233">![Gestion des utilisateurs](./media/active-directory-saas-druva-tutorial/ic795098.png "Gestion des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="4d49d-233">![Manage Users](./media/active-directory-saas-druva-tutorial/ic795098.png "Manage Users")</span></span>

4. <span data-ttu-id="4d49d-234">Dans la boîte de dialogue Create New User, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="4d49d-234">On the Create New User dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="4d49d-235">![Create NewUser](./media/active-directory-saas-druva-tutorial/ic795099.png "Create NewUser")</span><span class="sxs-lookup"><span data-stu-id="4d49d-235">![Create NewUser](./media/active-directory-saas-druva-tutorial/ic795099.png "Create NewUser")</span></span>
   
   <span data-ttu-id="4d49d-236">a.</span><span class="sxs-lookup"><span data-stu-id="4d49d-236">a.</span></span> <span data-ttu-id="4d49d-237">Dans la zone de texte **Email**, entrez l’adresse e-mail de l’utilisateur, par exemple **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="4d49d-237">In the **Email address** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>
   
   <span data-ttu-id="4d49d-238">b.</span><span class="sxs-lookup"><span data-stu-id="4d49d-238">b.</span></span> <span data-ttu-id="4d49d-239">Dans la zone de texte **Nom**, entrez le nom d’un utilisateur, par exemple **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="4d49d-239">In the **Name** textbox, enter the name of user like **BrittaSimon**.</span></span>
   
   <span data-ttu-id="4d49d-240">c.</span><span class="sxs-lookup"><span data-stu-id="4d49d-240">c.</span></span> <span data-ttu-id="4d49d-241">Cliquez sur **Create User**.</span><span class="sxs-lookup"><span data-stu-id="4d49d-241">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="4d49d-242">Vous pouvez utiliser n’importe quel autre outil ou API de création de compte d’utilisateur fourni par Druva pour approvisionner des comptes d’utilisateurs Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d49d-242">You can use any other Druva user account creation tools or APIs provided by Druva to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="4d49d-243">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d49d-243">Assign the Azure AD test user</span></span>

<span data-ttu-id="4d49d-244">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Druva.</span><span class="sxs-lookup"><span data-stu-id="4d49d-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Druva.</span></span>

![Attribuer le rôle d’utilisateur][200] 

<span data-ttu-id="4d49d-246">**Pour affecter Britta Simon à Druva, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4d49d-246">**To assign Britta Simon to Druva, perform the following steps:**</span></span>

1. <span data-ttu-id="4d49d-247">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="4d49d-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="4d49d-249">Dans la liste des applications, sélectionnez **Druva**.</span><span class="sxs-lookup"><span data-stu-id="4d49d-249">In the applications list, select **Druva**.</span></span>

    ![Lien Druva dans la liste des applications](./media/active-directory-saas-druva-tutorial/tutorial_druva_app.png)  

3. <span data-ttu-id="4d49d-251">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="4d49d-251">In the menu on the left, click **Users and groups**.</span></span>

    ![Lien « Utilisateurs et groupes »][202]

4. <span data-ttu-id="4d49d-253">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="4d49d-253">Click **Add** button.</span></span> <span data-ttu-id="4d49d-254">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="4d49d-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Volet Ajouter une attribution][203]

5. <span data-ttu-id="4d49d-256">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="4d49d-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4d49d-257">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="4d49d-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4d49d-258">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="4d49d-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="4d49d-259">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="4d49d-259">Test single sign-on</span></span>

<span data-ttu-id="4d49d-260">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="4d49d-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4d49d-261">Lorsque vous cliquez sur la vignette Druva dans le volet d’accès, vous devez être connecté automatiquement à votre application Druva.</span><span class="sxs-lookup"><span data-stu-id="4d49d-261">When you click the Druva tile in the Access Panel, you should get automatically signed-on to your Druva application.</span></span>
<span data-ttu-id="4d49d-262">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4d49d-262">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4d49d-263">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="4d49d-263">Additional resources</span></span>

* [<span data-ttu-id="4d49d-264">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4d49d-264">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4d49d-265">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="4d49d-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-druva-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-druva-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-druva-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-druva-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-druva-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-druva-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-druva-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-druva-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-druva-tutorial/tutorial_general_203.png

