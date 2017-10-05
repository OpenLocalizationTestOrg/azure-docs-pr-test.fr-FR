---
title: "Didacticiel : Intégration d’Azure Active Directory à Ceridian Dayforce HCM | Microsoft docs"
description: "Découvrez comment configurer l'authentification unique entre Azure Active Directory et Ceridian Dayforce HCM."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 7adf1eb3-d063-45d6-96a8-fd53b329b3f3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: b2ea3d92f233dab5bd6814e4875f881117eac8e3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ceridian-dayforce-hcm"></a><span data-ttu-id="10187-103">Didacticiel : Intégration d’Azure Active Directory à Ceridian Dayforce HCM</span><span class="sxs-lookup"><span data-stu-id="10187-103">Tutorial: Azure Active Directory integration with Ceridian Dayforce HCM</span></span>

<span data-ttu-id="10187-104">Dans ce didacticiel, vous allez intégrer Ceridian Dayforce HCM à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="10187-104">In this tutorial, you learn how to integrate Ceridian Dayforce HCM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="10187-105">L’intégration de Ceridian Dayforce HCM à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="10187-105">Integrating Ceridian Dayforce HCM with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="10187-106">Dans Azure AD, vous pouvez contrôler qui a accès à Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="10187-106">You can control in Azure AD who has access to Ceridian Dayforce HCM.</span></span>
- <span data-ttu-id="10187-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Ceridian Dayforce HCM (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="10187-107">You can enable your users to automatically get signed-on to Ceridian Dayforce HCM (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="10187-108">Vous pouvez gérer vos comptes dans un emplacement central : le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="10187-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="10187-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="10187-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="10187-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="10187-110">Prerequisites</span></span>

<span data-ttu-id="10187-111">Pour configurer l’intégration d’Azure AD avec Ceridian Dayforce HCM, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="10187-111">To configure Azure AD integration with Ceridian Dayforce HCM, you need the following items:</span></span>

- <span data-ttu-id="10187-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="10187-112">An Azure AD subscription</span></span>
- <span data-ttu-id="10187-113">Un abonnement Ceridian Dayforce HCM pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="10187-113">A Ceridian Dayforce HCM single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="10187-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="10187-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="10187-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="10187-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="10187-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="10187-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="10187-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="10187-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="10187-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="10187-118">Scenario description</span></span>
<span data-ttu-id="10187-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="10187-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="10187-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="10187-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="10187-121">Ajout de Ceridian Dayforce HCM à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="10187-121">Adding Ceridian Dayforce HCM from the gallery</span></span>
2. <span data-ttu-id="10187-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="10187-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ceridian-dayforce-hcm-from-the-gallery"></a><span data-ttu-id="10187-123">Ajout de Ceridian Dayforce HCM à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="10187-123">Adding Ceridian Dayforce HCM from the gallery</span></span>
<span data-ttu-id="10187-124">Pour configurer l’intégration de Ceridian Dayforce HCM à Azure AD, vous devez ajouter Ceridian Dayforce HCM à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="10187-124">To configure the integration of Ceridian Dayforce HCM into Azure AD, you need to add Ceridian Dayforce HCM from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="10187-125">**Pour ajouter Ceridian Dayforce HCM à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="10187-125">**To add Ceridian Dayforce HCM from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="10187-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="10187-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Bouton Azure Active Directory][1]

2. <span data-ttu-id="10187-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="10187-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="10187-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="10187-129">Then go to **All applications**.</span></span>

    ![Panneau Applications d’entreprise][2]
    
3. <span data-ttu-id="10187-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="10187-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Bouton Nouvelle application][3]

4. <span data-ttu-id="10187-133">Dans la zone de recherche, tapez **Ceridian Dayforce HCM**, sélectionnez **Ceridian Dayforce HCM** dans le volet de résultats, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="10187-133">In the search box, type **Ceridian Dayforce HCM**, select **Ceridian Dayforce HCM** from result panel then click **Add** button to add the application.</span></span>

    ![Ceridian Dayforce HCM figurant dans la liste des résultats](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="10187-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="10187-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="10187-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Ceridian Dayforce HCM, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="10187-136">In this section, you configure and test Azure AD single sign-on with Ceridian Dayforce HCM based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="10187-137">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Ceridian Dayforce HCM équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="10187-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Ceridian Dayforce HCM is to a user in Azure AD.</span></span> <span data-ttu-id="10187-138">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Ceridian Dayforce HCM associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="10187-138">In other words, a link relationship between an Azure AD user and the related user in Ceridian Dayforce HCM needs to be established.</span></span>

<span data-ttu-id="10187-139">Dans Ceridian Dayforce HCM, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="10187-139">In Ceridian Dayforce HCM, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="10187-140">Pour configurer et tester l’authentification unique Azure AD avec Ceridian Dayforce HCM, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="10187-140">To configure and test Azure AD single sign-on with Ceridian Dayforce HCM, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="10187-141">**[Configurer l’authentification unique Azure AD](#configure-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="10187-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="10187-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="10187-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="10187-143">**[Création d’un utilisateur de test Ceridian Dayforce HCM](#create-a-ceridian-dayforce-hcm-test-user)** pour avoir un équivalent de Britta Simon dans Ceridian Dayforce HCM lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="10187-143">**[Create a Ceridian Dayforce HCM test user](#create-a-ceridian-dayforce-hcm-test-user)** - to have a counterpart of Britta Simon in Ceridian Dayforce HCM that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="10187-144">**[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="10187-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="10187-145">**[Tester l’authentification unique](#test-single-sign-on)** : pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="10187-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="10187-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="10187-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="10187-147">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="10187-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Ceridian Dayforce HCM application.</span></span>

<span data-ttu-id="10187-148">**Pour configurer l'authentification unique Azure AD avec Ceridian Dayforce HCM, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="10187-148">**To configure Azure AD single sign-on with Ceridian Dayforce HCM, perform the following steps:**</span></span>

1. <span data-ttu-id="10187-149">Dans le portail Azure, dans la page d’intégration d’application **Ceridian Dayforce HCM**, cliquez sur **Configurer l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="10187-149">In the Azure portal, on the **Ceridian Dayforce HCM** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="10187-151">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="10187-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_samlbase.png)

3. <span data-ttu-id="10187-153">Dans la section **Domaine et URL Ceridian Dayforce HCM**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="10187-153">On the **Ceridian Dayforce HCM Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_url.png)
    
    <span data-ttu-id="10187-155">a.</span><span class="sxs-lookup"><span data-stu-id="10187-155">a.</span></span> <span data-ttu-id="10187-156">Dans la zone de texte **URL d’authentification** , tapez l’URL utilisée par vos utilisateurs pour se connecter à votre application Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="10187-156">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Ceridian Dayforce HCM application.</span></span>
    
    | <span data-ttu-id="10187-157">Environnement</span><span class="sxs-lookup"><span data-stu-id="10187-157">Environment</span></span> | <span data-ttu-id="10187-158">URL</span><span class="sxs-lookup"><span data-stu-id="10187-158">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="10187-159">Production</span><span class="sxs-lookup"><span data-stu-id="10187-159">For production</span></span> | `https://sso.dayforcehcm.com/<DayforcehcmNamespace>` |
    | <span data-ttu-id="10187-160">Test</span><span class="sxs-lookup"><span data-stu-id="10187-160">For test</span></span> | `https://ssotest.dayforcehcm.com/<DayforcehcmNamespace>` |
    
    <span data-ttu-id="10187-161">b.</span><span class="sxs-lookup"><span data-stu-id="10187-161">b.</span></span> <span data-ttu-id="10187-162">Dans la zone de texte **Identificateur**, entrez une URL au format suivant :</span><span class="sxs-lookup"><span data-stu-id="10187-162">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    
    | <span data-ttu-id="10187-163">Environnement</span><span class="sxs-lookup"><span data-stu-id="10187-163">Environment</span></span> | <span data-ttu-id="10187-164">URL</span><span class="sxs-lookup"><span data-stu-id="10187-164">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="10187-165">Production</span><span class="sxs-lookup"><span data-stu-id="10187-165">For production</span></span> | `https://ncpingfederate.dayforcehcm.com/sp` |
    | <span data-ttu-id="10187-166">Test</span><span class="sxs-lookup"><span data-stu-id="10187-166">For test</span></span> | `https://fs-test.dayforcehcm.com/sp` |
    
    <span data-ttu-id="10187-167">c.</span><span class="sxs-lookup"><span data-stu-id="10187-167">c.</span></span> <span data-ttu-id="10187-168">Dans la zone de texte **URL de réponse**, tapez l’URL utilisée par Azure AD pour publier la réponse.</span><span class="sxs-lookup"><span data-stu-id="10187-168">In the **Reply URL** textbox, type the URL used by Azure AD to post the response.</span></span>
    
    | <span data-ttu-id="10187-169">Environnement</span><span class="sxs-lookup"><span data-stu-id="10187-169">Environment</span></span> | <span data-ttu-id="10187-170">URL</span><span class="sxs-lookup"><span data-stu-id="10187-170">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="10187-171">Production</span><span class="sxs-lookup"><span data-stu-id="10187-171">For production</span></span> | `https://ncpingfederate.dayforcehcm.com/sp/ACS.saml2` |
    | <span data-ttu-id="10187-172">Test</span><span class="sxs-lookup"><span data-stu-id="10187-172">For test</span></span> | `https://fs-test.dayforcehcm.com/sp/ACS.saml2` |
    
    > [!NOTE] 
    > <span data-ttu-id="10187-173">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="10187-173">These values are not real.</span></span> <span data-ttu-id="10187-174">Mettez à jour ces valeurs avec l’identificateur, l’URL de réponse et l’URL de connexion réels.</span><span class="sxs-lookup"><span data-stu-id="10187-174">Update these values with the actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="10187-175">Pour obtenir ces valeurs, contactez [l’équipe du support Ceridian Dayforce HCM](https://www.ceridian.com/contact-us/index.html).</span><span class="sxs-lookup"><span data-stu-id="10187-175">Contact [Ceridian Dayforce HCM Client support team](https://www.ceridian.com/contact-us/index.html) to get these values.</span></span>

4. <span data-ttu-id="10187-176">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="10187-176">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Lien de téléchargement du certificat](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_certificate.png) 

5. <span data-ttu-id="10187-178">Votre application Ceridian Dayforce HCM attend les assertions SAML dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="10187-178">Your Ceridian Dayforce HCM application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="10187-179">Pour connaître l’identificateur d’utilisateur à utiliser, contactez [l’équipe du support Ceridian Dayforce HCM](https://www.ceridian.com/contact-us/index.html).</span><span class="sxs-lookup"><span data-stu-id="10187-179">Work with [Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html) first to identify the correct user identifier.</span></span> <span data-ttu-id="10187-180">Microsoft recommande d’utiliser l’attribut **« name »** sous la forme d’identificateur utilisateur.</span><span class="sxs-lookup"><span data-stu-id="10187-180">Microsoft recommends using the **"name"** attribute as user identifier.</span></span> <span data-ttu-id="10187-181">Vous pouvez gérer les valeurs de ces attributs à partir de la section **Attributs utilisateur** sur la page d’intégration des applications.</span><span class="sxs-lookup"><span data-stu-id="10187-181">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="10187-182">La capture d’écran suivante montre un exemple :</span><span class="sxs-lookup"><span data-stu-id="10187-182">The following screenshot shows an example for this.</span></span>  

    ![Configurer l’authentification unique](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_07.png)

6. <span data-ttu-id="10187-184">Dans la section **Attributs utilisateur** de la boîte de dialogue **Authentification unique**, configurez le jeton SAML comme sur l’image ci-dessus et procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="10187-184">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="10187-185">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="10187-185">Attribute Name</span></span>  | <span data-ttu-id="10187-186">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="10187-186">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    | <span data-ttu-id="10187-187">name</span><span class="sxs-lookup"><span data-stu-id="10187-187">name</span></span>  | <span data-ttu-id="10187-188">user.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="10187-188">user.extensionattribute2</span></span> |    

    <span data-ttu-id="10187-189">a.</span><span class="sxs-lookup"><span data-stu-id="10187-189">a.</span></span> <span data-ttu-id="10187-190">Cliquez sur **Ajouter un attribut** pour ouvrir la boîte de dialogue **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="10187-190">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_attribute_04.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="10187-193">b.</span><span class="sxs-lookup"><span data-stu-id="10187-193">b.</span></span> <span data-ttu-id="10187-194">Dans la zone de texte **Attribut**, indiquez le nom d’attribut pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="10187-194">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="10187-195">c.</span><span class="sxs-lookup"><span data-stu-id="10187-195">c.</span></span> <span data-ttu-id="10187-196">Dans la liste **Valeur**, sélectionnez l’attribut utilisateur que vous souhaitez utiliser pour votre implémentation.</span><span class="sxs-lookup"><span data-stu-id="10187-196">In the **Value** list, select the user attribute you want to use for your implementation.</span></span>
    <span data-ttu-id="10187-197">Par exemple, si vous souhaitez utiliser EmployeeID comme identificateur d’utilisateur unique et que vous avez stocké la valeur d’attribut dans ExtensionAttribute2, sélectionnez **user.extensionattribute2**.</span><span class="sxs-lookup"><span data-stu-id="10187-197">For example, if you want to use the EmployeeID as unique user identifier and you have stored the attribute value in the ExtensionAttribute2, then select **user.extensionattribute2**.</span></span>
    
    <span data-ttu-id="10187-198">d.</span><span class="sxs-lookup"><span data-stu-id="10187-198">d.</span></span> <span data-ttu-id="10187-199">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="10187-199">Click **Ok**.</span></span>

7. <span data-ttu-id="10187-200">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="10187-200">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="10187-202">Dans la section **Configuration de Ceridian Dayforce HCM**, cliquez sur **Configurer Ceridian Dayforce HCM** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="10187-202">On the **Ceridian Dayforce HCM Configuration** section, click **Configure Ceridian Dayforce HCM** to open **Configure sign-on** window.</span></span> <span data-ttu-id="10187-203">Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="10187-203">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuration de Ceridian Dayforce HCM](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_configure.png) 

9. <span data-ttu-id="10187-205">Pour configurer l’authentification unique côté **Ceridian Dayforce HCM**, vous devez envoyer le fichier **XML de métadonnées** téléchargé, **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à [l’équipe du support Ceridian Dayforce HCM](https://www.ceridian.com/contact-us/index.html).</span><span class="sxs-lookup"><span data-stu-id="10187-205">To configure single sign-on on **Ceridian Dayforce HCM** side, you need to send the downloaded **Metadata XML** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html).</span></span>

> [!TIP]
> <span data-ttu-id="10187-206">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="10187-206">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="10187-207">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="10187-207">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="10187-208">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="10187-208">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="10187-209">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="10187-209">Create an Azure AD test user</span></span>

<span data-ttu-id="10187-210">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="10187-210">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="10187-212">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="10187-212">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="10187-213">Dans le volet gauche du Portail Azure, cliquez sur le bouton **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="10187-213">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Bouton Azure Active Directory](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="10187-215">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="10187-215">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Liens « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="10187-217">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="10187-217">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Bouton Ajouter](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="10187-219">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="10187-219">In the **User** dialog box, perform the following steps:</span></span>

    ![Boîte de dialogue Utilisateur](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_04.png)

    <span data-ttu-id="10187-221">a.</span><span class="sxs-lookup"><span data-stu-id="10187-221">a.</span></span> <span data-ttu-id="10187-222">Dans la zone **Nom**, tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="10187-222">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="10187-223">b.</span><span class="sxs-lookup"><span data-stu-id="10187-223">b.</span></span> <span data-ttu-id="10187-224">Dans la zone **Nom d’utilisateur** , tapez l’adresse e-mail de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="10187-224">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="10187-225">c.</span><span class="sxs-lookup"><span data-stu-id="10187-225">c.</span></span> <span data-ttu-id="10187-226">Cochez la case **Afficher le mot de passe**, puis notez la valeur affichée dans le champ **Mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="10187-226">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="10187-227">d.</span><span class="sxs-lookup"><span data-stu-id="10187-227">d.</span></span> <span data-ttu-id="10187-228">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="10187-228">Click **Create**.</span></span>
 
### <a name="create-a-ceridian-dayforce-hcm-test-user"></a><span data-ttu-id="10187-229">Créer un utilisateur de test Ceridian Dayforce HCM</span><span class="sxs-lookup"><span data-stu-id="10187-229">Create a Ceridian Dayforce HCM test user</span></span>

<span data-ttu-id="10187-230">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="10187-230">The objective of this section is to create a user called Britta Simon in Ceridian Dayforce HCM.</span></span> <span data-ttu-id="10187-231">Pour ajouter des utilisateurs dans l’application Ceridian Dayforce HCM, contactez [l’équipe du support Ceridian Dayforce HCM](https://www.ceridian.com/contact-us/index.html).</span><span class="sxs-lookup"><span data-stu-id="10187-231">Work with the [Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html) to get users added in the Ceridian Dayforce HCM application.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="10187-232">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="10187-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="10187-233">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="10187-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Ceridian Dayforce HCM.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="10187-235">**Pour affecter Britta Simon à Ceridian Dayforce HCM, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="10187-235">**To assign Britta Simon to Ceridian Dayforce HCM, perform the following steps:**</span></span>

1. <span data-ttu-id="10187-236">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="10187-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="10187-238">Dans la liste des applications, sélectionnez **Ceridian Dayforce HCM**.</span><span class="sxs-lookup"><span data-stu-id="10187-238">In the applications list, select **Ceridian Dayforce HCM**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png) 

3. <span data-ttu-id="10187-240">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="10187-240">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="10187-242">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="10187-242">Click **Add** button.</span></span> <span data-ttu-id="10187-243">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="10187-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="10187-245">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="10187-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="10187-246">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="10187-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="10187-247">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="10187-247">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="10187-248">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="10187-248">Assign the Azure AD test user</span></span>

<span data-ttu-id="10187-249">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="10187-249">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Ceridian Dayforce HCM.</span></span>

![Attribuer le rôle d’utilisateur][200] 

<span data-ttu-id="10187-251">**Pour affecter Britta Simon à Ceridian Dayforce HCM, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="10187-251">**To assign Britta Simon to Ceridian Dayforce HCM, perform the following steps:**</span></span>

1. <span data-ttu-id="10187-252">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="10187-252">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="10187-254">Dans la liste des applications, sélectionnez **Ceridian Dayforce HCM**.</span><span class="sxs-lookup"><span data-stu-id="10187-254">In the applications list, select **Ceridian Dayforce HCM**.</span></span>

    ![Lien Ceridian Dayforce HCM dans la liste des applications](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png)  

3. <span data-ttu-id="10187-256">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="10187-256">In the menu on the left, click **Users and groups**.</span></span>

    ![Lien « Utilisateurs et groupes »][202]

4. <span data-ttu-id="10187-258">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="10187-258">Click **Add** button.</span></span> <span data-ttu-id="10187-259">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="10187-259">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Volet Ajouter une attribution][203]

5. <span data-ttu-id="10187-261">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="10187-261">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="10187-262">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="10187-262">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="10187-263">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="10187-263">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="10187-264">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="10187-264">Test single sign-on</span></span>

<span data-ttu-id="10187-265">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="10187-265">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="10187-266">Lorsque vous cliquez sur la mosaïque Ceridian Dayforce HCM dans le volet d’accès, vous devriez être connecté automatiquement à votre application Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="10187-266">When you click the Ceridian Dayforce HCM tile in the Access Panel, you should get automatically signed-on to your Ceridian Dayforce HCM application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="10187-267">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="10187-267">Additional resources</span></span>

* [<span data-ttu-id="10187-268">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="10187-268">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="10187-269">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="10187-269">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_203.png

