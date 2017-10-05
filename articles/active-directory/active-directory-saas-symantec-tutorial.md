---
title: "Didacticiel : Intégration d’Azure Active Directory à Symantec Web Security Service (WSS) | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Symantec Web Security Service (WSS)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d6e4d893-1f14-4522-ac20-0c73b18c72a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 61576d3a915d209e7355e04432e586dcf66e7c5a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-symantec-web-security-service-wss"></a><span data-ttu-id="eb36a-103">Didacticiel : Intégration d’Azure Active Directory à Symantec Web Security Service (WSS)</span><span class="sxs-lookup"><span data-stu-id="eb36a-103">Tutorial: Azure Active Directory integration with Symantec Web Security Service (WSS)</span></span>

<span data-ttu-id="eb36a-104">Dans ce didacticiel, vous allez apprendre à intégrer votre compte Symantec Web Security Service (WSS) à votre compte Azure Active Directory (Azure AD) afin que WSS puisse authentifier un utilisateur final approvisionné dans Azure AD à l’aide de l’authentification SAML et appliquer les règles de stratégie au niveau de l’utilisateur ou du groupe.</span><span class="sxs-lookup"><span data-stu-id="eb36a-104">In this tutorial, you will learn how to integrate your Symantec Web Security Service (WSS) account with your Azure Active Directory (Azure AD) account so that WSS can authenticate an end user provisioned in the Azure AD using SAML authentication and enforce user or group level policy rules.</span></span>

<span data-ttu-id="eb36a-105">L’intégration de Symantec Web Security Service (WSS) à Azure AD vous fait bénéficier des avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="eb36a-105">Integrating Symantec Web Security Service (WSS) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="eb36a-106">Gérer tous les groupes et utilisateurs finaux utilisés par votre compte WSS à partir de votre portail Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eb36a-106">Manage all of the end users and groups used by your WSS account from your Azure AD portal.</span></span> 

- <span data-ttu-id="eb36a-107">Autoriser les utilisateurs finaux à s’authentifier sur WSS à l’aide de leurs informations d’identification Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eb36a-107">Allow the end users to authenticate themselves in WSS using their Azure AD credentials.</span></span>

- <span data-ttu-id="eb36a-108">Activer l’application des règles de stratégie au niveau de l’utilisateur et du groupe définies dans votre compte WSS.</span><span class="sxs-lookup"><span data-stu-id="eb36a-108">Enable the enforcement of user and group level policy rules defined in your WSS account.</span></span>

<span data-ttu-id="eb36a-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="eb36a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eb36a-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="eb36a-110">Prerequisites</span></span>

<span data-ttu-id="eb36a-111">Pour configurer l’intégration d’Azure AD à Symantec Web Security Service (WSS), vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="eb36a-111">To configure Azure AD integration with Symantec Web Security Service (WSS), you need the following items:</span></span>

- <span data-ttu-id="eb36a-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb36a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="eb36a-113">Un compte Symantec Web Security Service (WSS)</span><span class="sxs-lookup"><span data-stu-id="eb36a-113">A Symantec Web Security Service (WSS) account</span></span>

> [!NOTE]
> <span data-ttu-id="eb36a-114">Pour tester les étapes de ce didacticiel, il est déconseillé d’utiliser un compte WSS qui est actuellement utilisé à des fins de production.</span><span class="sxs-lookup"><span data-stu-id="eb36a-114">To test the steps in this tutorial, we do not recommend using a WSS account that is currently being used for production purpose.</span></span>

<span data-ttu-id="eb36a-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="eb36a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="eb36a-116">N’utilisez pas le compte WSS qui est actuellement utilisé à des fins de production pour ce test, sauf si c’est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="eb36a-116">Do not use your WSS account that is currently being used for production purpose for this test unless it is necessary.</span></span>
- <span data-ttu-id="eb36a-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="eb36a-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="eb36a-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="eb36a-118">Scenario description</span></span>
<span data-ttu-id="eb36a-119">Dans ce didacticiel, vous allez configurer votre instance Azure AD pour activer l’authentification unique sur WWS à l’aide des informations d’identification de l’utilisateur final définies dans votre compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eb36a-119">In this tutorial, you will configure your Azure AD to enable single sign-on to WSS using the end user credentials defined in your Azure AD account.</span></span>
<span data-ttu-id="eb36a-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="eb36a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="eb36a-121">Ajout de l’application Symantec Web Security Service (WSS) à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="eb36a-121">Adding the Symantec Web Security Service (WSS) app from the gallery</span></span>
2. <span data-ttu-id="eb36a-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb36a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-symantec-web-security-service-wss-from-the-gallery"></a><span data-ttu-id="eb36a-123">Ajout de Symantec Web Security Service (WSS) à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="eb36a-123">Adding Symantec Web Security Service (WSS) from the gallery</span></span>
<span data-ttu-id="eb36a-124">Pour configurer l’intégration de Symantec Web Security Service (WSS) à Azure AD, vous devez ajouter Symantec Web Security Service (WSS) à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="eb36a-124">To configure the integration of Symantec Web Security Service (WSS) into Azure AD, you need to add Symantec Web Security Service (WSS) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="eb36a-125">**Pour ajouter Symantec Web Security Service (WSS) à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="eb36a-125">**To add Symantec Web Security Service (WSS) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="eb36a-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="eb36a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Bouton Azure Active Directory][1]

2. <span data-ttu-id="eb36a-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="eb36a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="eb36a-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="eb36a-129">Then go to **All applications**.</span></span>

    ![Panneau Applications d’entreprise][2]
    
3. <span data-ttu-id="eb36a-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="eb36a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Bouton Nouvelle application][3]

4. <span data-ttu-id="eb36a-133">Dans la zone de recherche, tapez **Symantec Web Security Service (WSS)**, sélectionnez **Symantec Web Security Service (WSS)** dans le volet des résultats, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="eb36a-133">In the search box, type **Symantec Web Security Service (WSS)**, select **Symantec Web Security Service (WSS)** from result panel then click **Add** button to add the application.</span></span>

    ![Symantec Web Security Service (WSS) dans la liste des résultats](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="eb36a-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb36a-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="eb36a-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD auprès de Symantec Web Security Service (WSS) avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="eb36a-136">In this section, you configure and test Azure AD single sign-on with Symantec Web Security Service (WSS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="eb36a-137">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Symantec Web Security Service (WSS) équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eb36a-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Symantec Web Security Service (WSS) is to a user in Azure AD.</span></span> <span data-ttu-id="eb36a-138">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Symantec Web Security Service (WSS) associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="eb36a-138">In other words, a link relationship between an Azure AD user and the related user in Symantec Web Security Service (WSS) needs to be established.</span></span>

<span data-ttu-id="eb36a-139">Dans Symantec Web Security Service (WSS), affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur de **Nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="eb36a-139">In Symantec Web Security Service (WSS), assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="eb36a-140">Pour configurer et tester l’authentification unique Azure AD auprès de Symantec Web Security Service (WSS), vous avez besoin de suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="eb36a-140">To configure and test Azure AD single sign-on with Symantec Web Security Service (WSS), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="eb36a-141">**[Configurer l’authentification unique Azure AD](#configure-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="eb36a-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="eb36a-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="eb36a-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="eb36a-143">**[Créer un utilisateur de test Symantec Web Security Service (WSS)](#create-a-symantec-web-security-service-wss-test-user)** pour avoir dans Symantec Web Security Service (WSS) un équivalent de Britta Simon lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="eb36a-143">**[Create a Symantec Web Security Service (WSS) test user](#create-a-symantec-web-security-service-wss-test-user)** - to have a counterpart of Britta Simon in Symantec Web Security Service (WSS) that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="eb36a-144">**[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eb36a-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="eb36a-145">**[Tester l’authentification unique](#test-single-sign-on)** : pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="eb36a-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="eb36a-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb36a-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="eb36a-147">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="eb36a-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Symantec Web Security Service (WSS) application.</span></span>

<span data-ttu-id="eb36a-148">**Pour configurer l’authentification unique Azure AD avec Symantec Web Security Service (WSS), procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="eb36a-148">**To configure Azure AD single sign-on with Symantec Web Security Service (WSS), perform the following steps:**</span></span>

1. <span data-ttu-id="eb36a-149">Dans le portail Azure, dans la page d’intégration de l’application **Symantec Web Security Service (WSS)**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="eb36a-149">In the Azure portal, on the **Symantec Web Security Service (WSS)** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="eb36a-151">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="eb36a-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_samlbase.png)

3. <span data-ttu-id="eb36a-153">Dans la section **Domaine et URL Symantec Web Security Service (WSS)** section, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="eb36a-153">On the **Symantec Web Security Service (WSS) Domain and URLs** section, perform the following steps:</span></span>

    ![Informations d’authentification unique Domaine et URL Symantec Web Security Service (WSS)](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_url.png)

    <span data-ttu-id="eb36a-155">a.</span><span class="sxs-lookup"><span data-stu-id="eb36a-155">a.</span></span> <span data-ttu-id="eb36a-156">Dans la zone de texte **Identificateur**, saisissez l’URL : `https://saml.threatpulse.net:8443/saml/saml_realm`</span><span class="sxs-lookup"><span data-stu-id="eb36a-156">In the **Identifier** textbox, type the URL: `https://saml.threatpulse.net:8443/saml/saml_realm`</span></span>

    <span data-ttu-id="eb36a-157">b.</span><span class="sxs-lookup"><span data-stu-id="eb36a-157">b.</span></span> <span data-ttu-id="eb36a-158">Dans la zone de texte **URL de réponse**, tapez l’URL : `https://saml.threatpulse.net:8443/saml/saml_realm/bcsamlpost`</span><span class="sxs-lookup"><span data-stu-id="eb36a-158">In the **Reply URL** textbox, type the URL: `https://saml.threatpulse.net:8443/saml/saml_realm/bcsamlpost`</span></span>

    > [!NOTE]
    > <span data-ttu-id="eb36a-159">Veuillez contacter l’[équipe de support technique de Symantec Web Security Service (WSS)](https://www.symantec.com/contact-us) si les valeurs **Identificateur** et **URL de réponse** ne fonctionnent pas pour une raison quelconque.</span><span class="sxs-lookup"><span data-stu-id="eb36a-159">Please contact the [Symantec Web Security Service (WSS) Client support team](https://www.symantec.com/contact-us) if the values for the **Identifier** and **Reply URL** are not working for some reason.</span></span>

4. <span data-ttu-id="eb36a-160">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="eb36a-160">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Lien Téléchargement de certificat](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_certificate.png) 

5. <span data-ttu-id="eb36a-162">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="eb36a-162">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-symantec-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="eb36a-164">Pour configurer l’authentification unique côté Symantec Web Security Service (WSS), consultez la documentation en ligne de WSS.</span><span class="sxs-lookup"><span data-stu-id="eb36a-164">To configure single sign-on on the Symantec Web Security Service (WSS) side, refer to the WSS online documentation.</span></span> <span data-ttu-id="eb36a-165">Le fichier **XML de métadonnées** devra être importé dans le portail WSS.</span><span class="sxs-lookup"><span data-stu-id="eb36a-165">The downloaded **Metadata XML** file will need to be imported into the WSS portal.</span></span> <span data-ttu-id="eb36a-166">Contactez l’[équipe de support Symantec Web Security Service (WSS)](https://www.symantec.com/contact-us) si vous avez besoin d’aide pour configurer le portail WSS.</span><span class="sxs-lookup"><span data-stu-id="eb36a-166">Contact the [Symantec Web Security Service (WSS) support team](https://www.symantec.com/contact-us) if you need assistance with the configuration on the WSS portal.</span></span>

> [!TIP]
> <span data-ttu-id="eb36a-167">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="eb36a-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="eb36a-168">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="eb36a-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="eb36a-169">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="eb36a-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="eb36a-170">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb36a-170">Create an Azure AD test user</span></span>

<span data-ttu-id="eb36a-171">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="eb36a-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="eb36a-173">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="eb36a-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="eb36a-174">Dans le volet gauche du Portail Azure, cliquez sur le bouton **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="eb36a-174">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Bouton Azure Active Directory](./media/active-directory-saas-symantec-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="eb36a-176">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="eb36a-176">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Liens « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/active-directory-saas-symantec-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="eb36a-178">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="eb36a-178">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Bouton Ajouter](./media/active-directory-saas-symantec-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="eb36a-180">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="eb36a-180">In the **User** dialog box, perform the following steps:</span></span>

    ![Boîte de dialogue Utilisateur](./media/active-directory-saas-symantec-tutorial/create_aaduser_04.png)

    <span data-ttu-id="eb36a-182">a.</span><span class="sxs-lookup"><span data-stu-id="eb36a-182">a.</span></span> <span data-ttu-id="eb36a-183">Dans la zone **Nom**, tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="eb36a-183">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="eb36a-184">b.</span><span class="sxs-lookup"><span data-stu-id="eb36a-184">b.</span></span> <span data-ttu-id="eb36a-185">Dans la zone **Nom d’utilisateur** , tapez l’adresse e-mail de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="eb36a-185">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="eb36a-186">c.</span><span class="sxs-lookup"><span data-stu-id="eb36a-186">c.</span></span> <span data-ttu-id="eb36a-187">Cochez la case **Afficher le mot de passe**, puis notez la valeur affichée dans le champ **Mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="eb36a-187">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="eb36a-188">d.</span><span class="sxs-lookup"><span data-stu-id="eb36a-188">d.</span></span> <span data-ttu-id="eb36a-189">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="eb36a-189">Click **Create**.</span></span>
 
### <a name="create-a-symantec-web-security-service-wss-test-user"></a><span data-ttu-id="eb36a-190">Créer un utilisateur de test Symantec Web Security Service (WSS)</span><span class="sxs-lookup"><span data-stu-id="eb36a-190">Create a Symantec Web Security Service (WSS) test user</span></span>

<span data-ttu-id="eb36a-191">Dans cette section, vous créez un utilisateur appelé Britta Simon dans Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="eb36a-191">In this section, you create a user called Britta Simon in Symantec Web Security Service (WSS).</span></span> <span data-ttu-id="eb36a-192">Le nom d’utilisateur final correspondante peut être créé manuellement dans le portail WSS ou vous pouvez attendre que les utilisateurs/groupes approvisionnés dans Azure AD se synchronisent dans le portail WSS après quelques minutes (environ 15 minutes).</span><span class="sxs-lookup"><span data-stu-id="eb36a-192">The corresponding end username can be manually created in the WSS portal or you can wait for the users/groups provisioned in the Azure AD to be synchronized to the WSS portal after a few minutes (~15 minutes).</span></span> <span data-ttu-id="eb36a-193">Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="eb36a-193">Users must be created and activated before you use single sign-on.</span></span> <span data-ttu-id="eb36a-194">L’adresse IP publique de l’ordinateur de l’utilisateur final, qui sera utilisée pour parcourir les sites web, doit également être configurée dans le portail Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="eb36a-194">The public IP address of the end user machine, which will be used to browse websites also need to be provisioned in the Symantec Web Security Service (WSS) portal.</span></span>

> [!NOTE]
> <span data-ttu-id="eb36a-195">[Cliquez ici](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) pour obtenir l’adresse IP publique de votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="eb36a-195">Please [click here](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) to get your machine's public IPaddress.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="eb36a-196">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb36a-196">Assign the Azure AD test user</span></span>

<span data-ttu-id="eb36a-197">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="eb36a-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Symantec Web Security Service (WSS).</span></span>

![Attribuer le rôle d’utilisateur][200] 

<span data-ttu-id="eb36a-199">**Pour affecter Britta Simon à Symantec Web Security Service (WSS), procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="eb36a-199">**To assign Britta Simon to Symantec Web Security Service (WSS), perform the following steps:**</span></span>

1. <span data-ttu-id="eb36a-200">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="eb36a-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="eb36a-202">Dans la liste des applications, sélectionnez **Symantec Web Security Service (WSS)**.</span><span class="sxs-lookup"><span data-stu-id="eb36a-202">In the applications list, select **Symantec Web Security Service (WSS)**.</span></span>

    ![Lien Symantec Web Security Service (WSS) dans la liste des applications](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_app.png)  

3. <span data-ttu-id="eb36a-204">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="eb36a-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Lien « Utilisateurs et groupes »][202]

4. <span data-ttu-id="eb36a-206">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="eb36a-206">Click **Add** button.</span></span> <span data-ttu-id="eb36a-207">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="eb36a-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Volet Ajouter une attribution][203]

5. <span data-ttu-id="eb36a-209">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="eb36a-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="eb36a-210">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="eb36a-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="eb36a-211">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="eb36a-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="eb36a-212">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="eb36a-212">Test single sign-on</span></span>

<span data-ttu-id="eb36a-213">Dans cette section, vous allez tester la fonctionnalité d’authentification unique maintenant que vous avez configuré votre compte WSS pour utiliser votre système Azure AD pour l’authentification SAML.</span><span class="sxs-lookup"><span data-stu-id="eb36a-213">In this section, you'll test the single sign-on functionality now that you've configured your WSS account to use your Azure AD for SAML authentication.</span></span>

<span data-ttu-id="eb36a-214">Une fois que vous avez configuré votre navigateur web pour le trafic de proxy WSS, lorsque vous ouvrez votre navigateur web et que vous essayez d’accéder à un site, vous serez redirigé vers la page d’ouverture de session Azure.</span><span class="sxs-lookup"><span data-stu-id="eb36a-214">After you have configured your web browser to proxy traffic to WSS, when you open your web browser and try to browse to a site then you'll be redirected to the Azure sign-on page.</span></span> <span data-ttu-id="eb36a-215">Entrez les informations d’identification de l’utilisateur final de test qui a été approvisionné dans Azure AD (autrement dit, BrittaSimon) et le mot de passe correspondant.</span><span class="sxs-lookup"><span data-stu-id="eb36a-215">Enter the credentials of the test end user that has been provisioned in the Azure AD (that is, BrittaSimon) and associated password.</span></span> <span data-ttu-id="eb36a-216">Une fois authentifié, vous pourrez accéder au site web que vous avez choisi.</span><span class="sxs-lookup"><span data-stu-id="eb36a-216">Once authenticated, you'll be able to browse to the website that you chose.</span></span> <span data-ttu-id="eb36a-217">Si vous devez créer une règle de stratégie côté WSS pour empêcher BrittaSimon d’accéder à un site spécifique, vous devriez voir la page de blocage WSS lorsque vous tentez d’accéder à ce site en tant que BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="eb36a-217">Should you create a policy rule on the WSS side to block BrittaSimon from browsing to a particular site then you should see the WSS block page when you attempt to browse to that site as user BrittaSimon.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="eb36a-218">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="eb36a-218">Additional resources</span></span>

* [<span data-ttu-id="eb36a-219">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eb36a-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="eb36a-220">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="eb36a-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_203.png

