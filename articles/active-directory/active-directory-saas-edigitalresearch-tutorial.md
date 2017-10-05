---
title: "Didacticiel : Intégration d’Azure Active Directory avec eDigitalResearch | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et eDigitalResearch."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: c6b66ea0-16ba-45b4-b550-e81c56262b1f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: f877a1dd844c40c913f3121e5288952653c312cd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-edigitalresearch"></a><span data-ttu-id="02b7e-103">Didacticiel : Intégration d’Azure Active Directory avec eDigitalResearch</span><span class="sxs-lookup"><span data-stu-id="02b7e-103">Tutorial: Azure Active Directory integration with eDigitalResearch</span></span>

<span data-ttu-id="02b7e-104">Dans ce didacticiel, vous allez apprendre à intégrer eDigitalResearch dans Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="02b7e-104">In this tutorial, you learn how to integrate eDigitalResearch with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="02b7e-105">L’intégration d’eDigitalResearch à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="02b7e-105">Integrating eDigitalResearch with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="02b7e-106">Dans Azure AD, vous pouvez contrôler qui a accès à eDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="02b7e-106">You can control in Azure AD who has access to eDigitalResearch.</span></span>
- <span data-ttu-id="02b7e-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à eDigitalResearch (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="02b7e-107">You can enable your users to automatically get signed-on to eDigitalResearch (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="02b7e-108">Vous pouvez gérer vos comptes dans un emplacement central : le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="02b7e-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="02b7e-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="02b7e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02b7e-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="02b7e-110">Prerequisites</span></span>

<span data-ttu-id="02b7e-111">Pour configurer l’intégration d’Azure AD avec eDigitalResearch, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="02b7e-111">To configure Azure AD integration with eDigitalResearch, you need the following items:</span></span>

- <span data-ttu-id="02b7e-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="02b7e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="02b7e-113">Un abonnement eDigitalResearch pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="02b7e-113">A eDigitalResearch single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="02b7e-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="02b7e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="02b7e-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="02b7e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="02b7e-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="02b7e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="02b7e-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="02b7e-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="02b7e-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="02b7e-118">Scenario description</span></span>
<span data-ttu-id="02b7e-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="02b7e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="02b7e-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="02b7e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="02b7e-121">Ajout d’eDigitalResearch à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="02b7e-121">Adding eDigitalResearch from the gallery</span></span>
2. <span data-ttu-id="02b7e-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="02b7e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-edigitalresearch-from-the-gallery"></a><span data-ttu-id="02b7e-123">Ajout d’eDigitalResearch à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="02b7e-123">Adding eDigitalResearch from the gallery</span></span>
<span data-ttu-id="02b7e-124">Pour configurer l’intégration d’eDigitalResearch avec Azure AD, vous devez ajouter eDigitalResearch, disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="02b7e-124">To configure the integration of eDigitalResearch into Azure AD, you need to add eDigitalResearch from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="02b7e-125">**Pour ajouter eDigitalResearch à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="02b7e-125">**To add eDigitalResearch from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="02b7e-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="02b7e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Bouton Azure Active Directory][1]

2. <span data-ttu-id="02b7e-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="02b7e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="02b7e-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="02b7e-129">Then go to **All applications**.</span></span>

    ![Panneau Applications d’entreprise][2]
    
3. <span data-ttu-id="02b7e-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="02b7e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Bouton Nouvelle application][3]

4. <span data-ttu-id="02b7e-133">Dans la zone de recherche, tapez **eDigitalResearch**, sélectionnez **eDigitalResearch** dans le volet de résultats, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="02b7e-133">In the search box, type **eDigitalResearch**, select **eDigitalResearch** from result panel then click **Add** button to add the application.</span></span>

    ![eDigitalResearch dans la liste des résultats](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="02b7e-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="02b7e-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="02b7e-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec eDigitalResearch avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="02b7e-136">In this section, you configure and test Azure AD single sign-on with eDigitalResearch based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="02b7e-137">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur eDigitalResearch équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="02b7e-137">For single sign-on to work, Azure AD needs to know what the counterpart user in eDigitalResearch is to a user in Azure AD.</span></span> <span data-ttu-id="02b7e-138">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur eDigitalResearch associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="02b7e-138">In other words, a link relationship between an Azure AD user and the related user in eDigitalResearch needs to be established.</span></span>

<span data-ttu-id="02b7e-139">Dans eDigitalResearch, assignez la valeur du **nom d’utilisateur** d’Azure AD comme valeur de **Username** (Nom d’utilisateur) pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="02b7e-139">In eDigitalResearch, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="02b7e-140">Pour configurer et tester l’authentification unique Azure AD avec eDigitalResearch, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="02b7e-140">To configure and test Azure AD single sign-on with eDigitalResearch, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="02b7e-141">**[Configurer l’authentification unique Azure AD](#configure-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="02b7e-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="02b7e-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="02b7e-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="02b7e-143">**[Crééer un utilisateur de test eDigitalResearch](#create-a-edigitalresearch-test-user)** pour avoir dans eDigitalResearch un équivalent de Britta Simon lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="02b7e-143">**[Create a eDigitalResearch test user](#create-a-edigitalresearch-test-user)** - to have a counterpart of Britta Simon in eDigitalResearch that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="02b7e-144">**[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="02b7e-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="02b7e-145">**[Tester l’authentification unique](#test-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="02b7e-145">**[Test single sign-on](#test-single-sign-on)**  to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="02b7e-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="02b7e-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="02b7e-147">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application eDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="02b7e-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your eDigitalResearch application.</span></span>

<span data-ttu-id="02b7e-148">**Pour configurer l’authentification unique Azure AD avec eDigitalResearch, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="02b7e-148">**To configure Azure AD single sign-on with eDigitalResearch, perform the following steps:**</span></span>

1. <span data-ttu-id="02b7e-149">Dans le portail Azure, dans la page d’intégration de l’application **eDigitalResearch**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="02b7e-149">In the Azure portal, on the **eDigitalResearch** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="02b7e-151">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="02b7e-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_samlbase.png)

3. <span data-ttu-id="02b7e-153">Dans la section **eDigitalResearch Domain and URLs** (Domaine et URL eDigitalResearch), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="02b7e-153">On the **eDigitalResearch Domain and URLs** section, perform the following steps:</span></span>

    ![Informations d’authentification unique dans eDigitalResearch Domain and URLs (Domaine et URL eDigitalResearch)](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_url.png)

    <span data-ttu-id="02b7e-155">a.</span><span class="sxs-lookup"><span data-stu-id="02b7e-155">a.</span></span> <span data-ttu-id="02b7e-156">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<company-name>.edigitalresearch.com`</span><span class="sxs-lookup"><span data-stu-id="02b7e-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<company-name>.edigitalresearch.com`</span></span>

    <span data-ttu-id="02b7e-157">b.</span><span class="sxs-lookup"><span data-stu-id="02b7e-157">b.</span></span> <span data-ttu-id="02b7e-158">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://<company-name>.edigitalresearch.com/login/consume`</span><span class="sxs-lookup"><span data-stu-id="02b7e-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company-name>.edigitalresearch.com/login/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="02b7e-159">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="02b7e-159">These values are not real.</span></span> <span data-ttu-id="02b7e-160">Mettez à jour ces valeurs avec l’identificateur et l’URL de réponse réels.</span><span class="sxs-lookup"><span data-stu-id="02b7e-160">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="02b7e-161">Pour obtenir ces valeurs, contactez l’[équipe de support eDigitalResearch](http://www.maruedr.com/contact).</span><span class="sxs-lookup"><span data-stu-id="02b7e-161">Contact [eDigitalResearch support team](http://www.maruedr.com/contact) to get these values.</span></span>
 


4. <span data-ttu-id="02b7e-162">Dans la section **Certificat de signature SAML**, cliquez sur **Certificat (en base64)**, puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="02b7e-162">On the **SAML Signing Certificate** section, click **Certificate Base(64)** and then save the certificate file on your computer.</span></span>

    <span data-ttu-id="02b7e-163">!</span><span class="sxs-lookup"><span data-stu-id="02b7e-163">!</span></span>![Lien Téléchargement de certificat](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_certificate.png) 

5. <span data-ttu-id="02b7e-165">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="02b7e-165">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="02b7e-167">Dans la section **eDigitalResearch Configuration** (Configuration d’eDigitalResearch), cliquez sur **Configure eDigitalResearch** (Configurer eDigitalResearch) pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="02b7e-167">On the **eDigitalResearch Configuration** section, click **Configure eDigitalResearch** to open **Configure sign-on** window.</span></span> <span data-ttu-id="02b7e-168">Copiez **l’URL de déconnexion et l’ID d’entité SAML** à partir de la section **Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="02b7e-168">Copy the **Sign-Out URL, SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Configuration d’eDigitalResearch](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_configure.png) 

7. <span data-ttu-id="02b7e-170">Pour configurer l’authentification unique côté **eDigitalResearch**, vous devez envoyer le **fichier de certificat (en base64)** téléchargé, l’**ID d’entité SAML** et l’**URL de déconnexion** à l’[équipe de support eDigitalResearch](http://www.maruedr.com/contact).</span><span class="sxs-lookup"><span data-stu-id="02b7e-170">To configure single sign-on on **eDigitalResearch** side, you need to send the downloaded **Certificate (Base64) File**, **SAML Entity ID**, and **Sign-Out URL** to [eDigitalResearch support team](http://www.maruedr.com/contact).</span></span> <span data-ttu-id="02b7e-171">Celles-ci configurent ensuite ce paramètre pour que la connexion SSO SAML soit définie correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="02b7e-171">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="02b7e-172">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="02b7e-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="02b7e-173">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="02b7e-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="02b7e-174">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="02b7e-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="02b7e-175">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="02b7e-175">Create an Azure AD test user</span></span>

<span data-ttu-id="02b7e-176">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="02b7e-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="02b7e-178">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="02b7e-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="02b7e-179">Dans le volet gauche du Portail Azure, cliquez sur le bouton **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="02b7e-179">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Bouton Azure Active Directory](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="02b7e-181">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="02b7e-181">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Liens « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="02b7e-183">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="02b7e-183">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Bouton Ajouter](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="02b7e-185">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="02b7e-185">In the **User** dialog box, perform the following steps:</span></span>

    ![Boîte de dialogue Utilisateur](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_04.png)

    <span data-ttu-id="02b7e-187">a.</span><span class="sxs-lookup"><span data-stu-id="02b7e-187">a.</span></span> <span data-ttu-id="02b7e-188">Dans la zone **Nom**, tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="02b7e-188">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="02b7e-189">b.</span><span class="sxs-lookup"><span data-stu-id="02b7e-189">b.</span></span> <span data-ttu-id="02b7e-190">Dans la zone **Nom d’utilisateur** , tapez l’adresse e-mail de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="02b7e-190">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="02b7e-191">c.</span><span class="sxs-lookup"><span data-stu-id="02b7e-191">c.</span></span> <span data-ttu-id="02b7e-192">Cochez la case **Afficher le mot de passe**, puis notez la valeur affichée dans le champ **Mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="02b7e-192">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="02b7e-193">d.</span><span class="sxs-lookup"><span data-stu-id="02b7e-193">d.</span></span> <span data-ttu-id="02b7e-194">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="02b7e-194">Click **Create**.</span></span>
  
### <a name="create-a-edigitalresearch-test-user"></a><span data-ttu-id="02b7e-195">Créer un utilisateur de test eDigitalResearch</span><span class="sxs-lookup"><span data-stu-id="02b7e-195">Create a eDigitalResearch test user</span></span>

<span data-ttu-id="02b7e-196">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans eDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="02b7e-196">The objective of this section is to create a user called Britta Simon in eDigitalResearch.</span></span> 

<span data-ttu-id="02b7e-197">Pour créer des utilisateurs, contactez l’[équipe de support eDigitalResearch](http://www.maruedr.com/contact).</span><span class="sxs-lookup"><span data-stu-id="02b7e-197">Work with the [eDigitalResearch support team](http://www.maruedr.com/contact) to get users created.</span></span>     
    
 > [!NOTE]
 > <span data-ttu-id="02b7e-198">Le titulaire du compte Azure Active Directory reçoit un e-mail contenant un lien à suivre pour confirmer son compte et l’activer.</span><span class="sxs-lookup"><span data-stu-id="02b7e-198">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="02b7e-199">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="02b7e-199">Assign the Azure AD test user</span></span>

<span data-ttu-id="02b7e-200">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à eDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="02b7e-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to eDigitalResearch.</span></span>

![Attribuer le rôle d’utilisateur][200] 

<span data-ttu-id="02b7e-202">**Pour affecter Britta Simon à eDigitalResearch, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="02b7e-202">**To assign Britta Simon to eDigitalResearch, perform the following steps:**</span></span>

1. <span data-ttu-id="02b7e-203">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="02b7e-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="02b7e-205">Dans la liste des applications, sélectionnez **eDigitalResearch**.</span><span class="sxs-lookup"><span data-stu-id="02b7e-205">In the applications list, select **eDigitalResearch**.</span></span>

    ![Lien eDigitalResearch dans la liste des applications](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_app.png)  

3. <span data-ttu-id="02b7e-207">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="02b7e-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Lien « Utilisateurs et groupes »][202]

4. <span data-ttu-id="02b7e-209">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="02b7e-209">Click **Add** button.</span></span> <span data-ttu-id="02b7e-210">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="02b7e-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Volet Ajouter une attribution][203]

5. <span data-ttu-id="02b7e-212">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="02b7e-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="02b7e-213">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="02b7e-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="02b7e-214">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="02b7e-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="02b7e-215">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="02b7e-215">Test single sign-on</span></span>

<span data-ttu-id="02b7e-216">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="02b7e-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="02b7e-217">Lorsque vous cliquez sur la vignette eDigitalResearch dans le volet d’accès, vous devez être connecté automatiquement à votre application eDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="02b7e-217">When you click the eDigitalResearch tile in the Access Panel, you should get automatically signed-on to your eDigitalResearch application.</span></span>
<span data-ttu-id="02b7e-218">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="02b7e-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="02b7e-219">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="02b7e-219">Additional resources</span></span>

* [<span data-ttu-id="02b7e-220">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="02b7e-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="02b7e-221">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="02b7e-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_203.png

