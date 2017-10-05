---
title: "Didacticiel : Intégration d’Azure Active Directory à Confluence SAML SSO by Microsoft | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Confluence SAML SSO by Microsoft."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 1ad1cf90-52bc-4b71-ab2b-9a5a1280fb2d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 56de86df9c915fa7c41e3bf0a545cc528cdcf959
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-confluence-saml-sso-by-microsoft"></a><span data-ttu-id="1aa5f-103">Didacticiel : Intégration d’Azure Active Directory à Confluence SAML SSO by Microsoft</span><span class="sxs-lookup"><span data-stu-id="1aa5f-103">Tutorial: Azure Active Directory integration with Confluence SAML SSO by Microsoft</span></span>

<span data-ttu-id="1aa5f-104">Dans ce didacticiel, vous allez apprendre à intégrer Confluence SAML SSO by Microsoft à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1aa5f-104">In this tutorial, you learn how to integrate Confluence SAML SSO by Microsoft with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1aa5f-105">L’intégration de Confluence SAML SSO by Microsoft à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="1aa5f-105">Integrating Confluence SAML SSO by Microsoft with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1aa5f-106">Vous pouvez contrôler dans Azure AD qui a accès à Confluence SAML SSO by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-106">You can control in Azure AD who has access to Confluence SAML SSO by Microsoft</span></span>
- <span data-ttu-id="1aa5f-107">Vous pouvez permettre à vos utilisateurs d’être automatiquement authentifiés dans Confluence SAML SSO by Microsoft (authentification unique) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-107">You can enable your users to automatically get signed-on to Confluence SAML SSO by Microsoft (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1aa5f-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="1aa5f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1aa5f-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1aa5f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1aa5f-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1aa5f-110">Prerequisites</span></span>

<span data-ttu-id="1aa5f-111">Pour configurer l’intégration d’Azure AD à Confluence SAML SSO by Microsoft, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="1aa5f-111">To configure Azure AD integration with Confluence SAML SSO by Microsoft, you need the following items:</span></span>

- <span data-ttu-id="1aa5f-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="1aa5f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1aa5f-113">Une application serveur Confluence installée sur un serveur Windows 64 bits (local ou dans l’infrastructure IaaS cloud)</span><span class="sxs-lookup"><span data-stu-id="1aa5f-113">Confluence server application installed on a Windows 64-bit server (on premise or on the cloud IaaS infrastructure)</span></span>
- <span data-ttu-id="1aa5f-114">L’activation du HTTPS dans le serveur</span><span class="sxs-lookup"><span data-stu-id="1aa5f-114">Confluence server is HTTPS enabled</span></span>
- <span data-ttu-id="1aa5f-115">Notez que les versions prises en charge par le plug-in Confluence sont mentionnées dans la section ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-115">Note the supported versions for Confluence Plugin are mentioned in below section.</span></span>
- <span data-ttu-id="1aa5f-116">L’accessibilité du serveur Confluence via Internet (particulièrement pour la page de connexion Azure AD pour l’authentification) et la capacité à recevoir le jeton d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="1aa5f-116">Confluence server is reachable on internet particularly to Azure AD Login page for authentication and should able to receive the token from Azure AD</span></span>
- <span data-ttu-id="1aa5f-117">La création d’informations d’identification administrateur dans Confluence</span><span class="sxs-lookup"><span data-stu-id="1aa5f-117">Admin credentials are set up in Confluence</span></span>
- <span data-ttu-id="1aa5f-118">La désactivation de WebSudo dans Confluence</span><span class="sxs-lookup"><span data-stu-id="1aa5f-118">WebSudo is disabled in Confluence</span></span>
- <span data-ttu-id="1aa5f-119">La création d’un utilisateur de test dans l’application serveur Confluence</span><span class="sxs-lookup"><span data-stu-id="1aa5f-119">Test user created in the Confluence server application</span></span>

> [!NOTE]
> <span data-ttu-id="1aa5f-120">Il est déconseillé d’utiliser un environnement de production Confluence pour tester les étapes de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-120">To test the steps in this tutorial, we do not recommend using a production environment of Confluence.</span></span> <span data-ttu-id="1aa5f-121">Testez d’abord l’intégration dans l’environnement de développement ou l’environnement intermédiaire de l’application, puis passez à l’environnement de production.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-121">Test the integration first in development or staging environment of the application and then use the production environment.</span></span>

<span data-ttu-id="1aa5f-122">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1aa5f-122">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1aa5f-123">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-123">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1aa5f-124">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez bénéficier de [l’offre d’essai](https://azure.microsoft.com/pricing/free-trial/) d’une durée d’un mois.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-124">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="supported-versions-of-confluence"></a><span data-ttu-id="1aa5f-125">Versions de Confluence prises en charge</span><span class="sxs-lookup"><span data-stu-id="1aa5f-125">Supported versions of Confluence</span></span> 

<span data-ttu-id="1aa5f-126">Les versions suivantes de Confluence sont actuellement prises en charge :</span><span class="sxs-lookup"><span data-stu-id="1aa5f-126">As of now, following versions of Confluence are supported:</span></span>

- <span data-ttu-id="1aa5f-127">Confluence : 5.0 à 5.10</span><span class="sxs-lookup"><span data-stu-id="1aa5f-127">Confluence: 5.0 to 5.10</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1aa5f-128">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="1aa5f-128">Scenario description</span></span>
<span data-ttu-id="1aa5f-129">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-129">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1aa5f-130">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="1aa5f-130">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1aa5f-131">Ajout de Confluence SAML SSO by Microsoft à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="1aa5f-131">Adding Confluence SAML SSO by Microsoft from the gallery</span></span>
2. <span data-ttu-id="1aa5f-132">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1aa5f-132">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-confluence-saml-sso-by-microsoft-from-the-gallery"></a><span data-ttu-id="1aa5f-133">Ajout de Confluence SAML SSO by Microsoft à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="1aa5f-133">Adding Confluence SAML SSO by Microsoft from the gallery</span></span>
<span data-ttu-id="1aa5f-134">Pour configurer l’intégration de Confluence SAML SSO by Microsoft à Azure AD, vous devez ajouter Confluence SAML SSO by Microsoft, disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-134">To configure the integration of Confluence SAML SSO by Microsoft into Azure AD, you need to add Confluence SAML SSO by Microsoft from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1aa5f-135">**Pour ajouter Confluence SAML SSO by Microsoft à partir de la galerie, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="1aa5f-135">**To add Confluence SAML SSO by Microsoft from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1aa5f-136">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-136">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1aa5f-138">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-138">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1aa5f-139">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-139">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="1aa5f-141">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-141">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="1aa5f-143">Dans la zone de recherche, tapez **Confluence SAML SSO by Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-143">In the search box, type **Confluence SAML SSO by Microsoft**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_search.png)

5. <span data-ttu-id="1aa5f-145">Dans le volet de résultats, sélectionnez **Confluence SAML SSO by Microsoft**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-145">In the results panel, select **Confluence SAML SSO by Microsoft**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1aa5f-147">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1aa5f-147">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1aa5f-148">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Confluence SAML SSO by Microsoft, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="1aa5f-148">In this section, you configure and test Azure AD single sign-on with Confluence SAML SSO by Microsoft based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1aa5f-149">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Confluence SAML SSO by Microsoft équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-149">For single sign-on to work, Azure AD needs to know what the counterpart user in Confluence SAML SSO by Microsoft is to a user in Azure AD.</span></span> <span data-ttu-id="1aa5f-150">En d’autres termes, une relation doit être établie entre l’utilisateur Azure AD et l’utilisateur Confluence SAML SSO by Microsoft associé.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-150">In other words, a link relationship between an Azure AD user and the related user in Confluence SAML SSO by Microsoft needs to be established.</span></span>

<span data-ttu-id="1aa5f-151">Dans Confluence SAML SSO by Microsoft, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-151">In Confluence SAML SSO by Microsoft, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1aa5f-152">Pour configurer et tester l’authentification unique Azure AD avec Confluence SAML SSO by Microsoft, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="1aa5f-152">To configure and test Azure AD single sign-on with Confluence SAML SSO by Microsoft, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1aa5f-153">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-153">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1aa5f-154">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-154">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1aa5f-155">**[Création d’un utilisateur de test Confluence SAML SSO by Microsoft](#creating-a-confluence-saml-sso-by-microsoft-test-user)** pour avoir un équivalent de Britta Simon dans Confluence SAML SSO by Microsoft lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-155">**[Creating a Confluence SAML SSO by Microsoft test user](#creating-a-confluence-saml-sso-by-microsoft-test-user)** - to have a counterpart of Britta Simon in Confluence SAML SSO by Microsoft that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1aa5f-156">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-156">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1aa5f-157">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-157">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1aa5f-158">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1aa5f-158">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1aa5f-159">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Confluence SAML SSO by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-159">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Confluence SAML SSO by Microsoft application.</span></span>

<span data-ttu-id="1aa5f-160">**Pour configurer l’authentification unique Azure AD avec Confluence SAML SSO by Microsoft, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="1aa5f-160">**To configure Azure AD single sign-on with Confluence SAML SSO by Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="1aa5f-161">Dans le portail Azure, dans la page d’intégration de l’application **Confluence SAML SSO by Microsoft**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-161">In the Azure portal, on the **Confluence SAML SSO by Microsoft** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="1aa5f-163">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-163">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_samlbase.png)

3. <span data-ttu-id="1aa5f-165">Dans la section **Domaine et URL Confluence SAML SSO by Microsoft**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="1aa5f-165">On the **Confluence SAML SSO by Microsoft Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_url.png)

    <span data-ttu-id="1aa5f-167">a.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-167">a.</span></span> <span data-ttu-id="1aa5f-168">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="1aa5f-168">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    <span data-ttu-id="1aa5f-169">b.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-169">b.</span></span> <span data-ttu-id="1aa5f-170">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<domain:port>/`</span><span class="sxs-lookup"><span data-stu-id="1aa5f-170">In the **Identifier** textbox, type a URL using the following pattern: `https://<domain:port>/`</span></span>

    <span data-ttu-id="1aa5f-171">c.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-171">c.</span></span> <span data-ttu-id="1aa5f-172">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="1aa5f-172">In the **Reply URL** textbox, type a URL using the following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1aa5f-173">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-173">These values are not real.</span></span> <span data-ttu-id="1aa5f-174">Mettez à jour ces valeurs avec l’identificateur, l’URL de réponse et l’URL de connexion réels.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-174">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="1aa5f-175">Le port est facultatif s’il s’agit d’une URL nommée.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-175">Port is optional in case it’s a named URL.</span></span> <span data-ttu-id="1aa5f-176">Ces valeurs sont reçues durant la configuration du plug-in Confluence qui est décrite plus loin dans le didacticiel.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-176">These values are received during the configuration of Confluence plugin, which is explained later in the tutorial.</span></span>
 

4. <span data-ttu-id="1aa5f-177">Pour générer l’URL des **métadonnées**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="1aa5f-177">To generate the **Metadata** url, perform the following steps:</span></span>

    <span data-ttu-id="1aa5f-178">a.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-178">a.</span></span> <span data-ttu-id="1aa5f-179">Cliquez sur **Inscriptions des applications**.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-179">Click **App registrations**.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-Confluencemicrosoft-tutorial/appregistrations.png)
   
    <span data-ttu-id="1aa5f-181">b.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-181">b.</span></span> <span data-ttu-id="1aa5f-182">Cliquez sur **Points de terminaison** pour ouvrir la boîte de dialogue **Points de terminaison**.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-182">Click **Endpoints** to open **Endpoints** dialog box.</span></span>  
    
    ![Configurer l’authentification unique](./media/active-directory-saas-Confluencemicrosoft-tutorial/endpointicon.png)

    <span data-ttu-id="1aa5f-184">c.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-184">c.</span></span> <span data-ttu-id="1aa5f-185">Cliquez sur le bouton Copier pour copier l’URL du document de métadonnées de fédération (**FEDERATION METADATA DOCUMENT**), puis collez-la dans le Bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-185">Click the copy button to copy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-Confluencemicrosoft-tutorial/endpoint.png)
     
    <span data-ttu-id="1aa5f-187">d.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-187">d.</span></span> <span data-ttu-id="1aa5f-188">Accédez maintenant à la page de propriétés de **Confluence SAML SSO by Microsoft**, copiez **l’ID d’application** à l’aide du bouton **Copier**, puis collez-le dans le Bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-188">Now go to the property page of **Confluence SAML SSO by Microsoft** and copy the **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-Confluencemicrosoft-tutorial/appid.png)

    <span data-ttu-id="1aa5f-190">e.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-190">e.</span></span> <span data-ttu-id="1aa5f-191">Générez **l’URL de métadonnées** en respectant le format suivant : `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` et copiez cette valeur dans le Bloc-notes, car vous en aurez besoin plus tard pour la configuration du plug-in.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-191">Generate the **Metadata URL** using the following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` and copy this value in notepad as it is used later for the configuration of the plugin.</span></span>

5. <span data-ttu-id="1aa5f-192">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="1aa5f-192">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-Confluencemicrosoft-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1aa5f-194">Communiquez à [Microsoft](mailto:waadpartners@microsoft.com) les informations suivantes pour le plug-in Confluence.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-194">Contact [Microsoft](mailto:waadpartners@microsoft.com) with the following information for the Confluence plugin.</span></span>
    
    *   <span data-ttu-id="1aa5f-195">Nom du client :</span><span class="sxs-lookup"><span data-stu-id="1aa5f-195">Customer Name:</span></span>
    *   <span data-ttu-id="1aa5f-196">Nom du domaine principal :</span><span class="sxs-lookup"><span data-stu-id="1aa5f-196">Primary domain name:</span></span>
    *   <span data-ttu-id="1aa5f-197">Azure AD Premium : Oui/Non (le plug-in est disponible pour tous les clients disposant d’un abonnement Gratuit, De base et Premium)</span><span class="sxs-lookup"><span data-stu-id="1aa5f-197">Azure AD Premium: Yes/No (Plugin will be available to all     the customer Free, Basic, and Premium SKU)</span></span>
    *   <span data-ttu-id="1aa5f-198">Nombre d’utilisateurs qui vont utiliser cette intégration :</span><span class="sxs-lookup"><span data-stu-id="1aa5f-198">Number of users who will be using this integration:</span></span>
    *   <span data-ttu-id="1aa5f-199">Version de Confluence :</span><span class="sxs-lookup"><span data-stu-id="1aa5f-199">Confluence Version:</span></span>
    *   <span data-ttu-id="1aa5f-200">Commentaires :</span><span class="sxs-lookup"><span data-stu-id="1aa5f-200">Comments:</span></span>

7. <span data-ttu-id="1aa5f-201">Dans une autre fenêtre de navigateur web, connectez-vous à votre instance de Confluence en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-201">In a different web browser window, log in to your Confluence instance as an administrator.</span></span>

8. <span data-ttu-id="1aa5f-202">Pointez sur le roue dentée, puis cliquez sur **Modules complémentaires**.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-202">Hover on cog and click the **Add-ons**.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-Confluencemicrosoft-tutorial/addon1.png)

9. <span data-ttu-id="1aa5f-204">Sous l’onglet Add-ons (Modules complémentaires), cliquez sur **Manage add-ons** (Gérer les modules complémentaires).</span><span class="sxs-lookup"><span data-stu-id="1aa5f-204">Under Add-ons tab section, click **Manage add-ons**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-Confluencemicrosoft-tutorial/addon72.png)

10. <span data-ttu-id="1aa5f-206">Chargez manuellement le plug-in fourni par Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-206">Manually upload the plugin provided by Microsoft.</span></span> <span data-ttu-id="1aa5f-207">Une fois que le plug-in est installé, il s’affiche sous **User Installed** (Installé par l’utilisateur), dans la section **Manage add-ons** (Gérer les modules complémentaires).</span><span class="sxs-lookup"><span data-stu-id="1aa5f-207">Once the plugin is installed, it appears in **User Installed** add-ons section of **Manage Add-on** section.</span></span>

11. <span data-ttu-id="1aa5f-208">Cliquez sur **Configurer** pour configurer le nouveau plug-in.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-208">Click **Configure** to configure the new plugin.</span></span>

12. <span data-ttu-id="1aa5f-209">Effectuez les opérations suivantes dans la page de configuration :</span><span class="sxs-lookup"><span data-stu-id="1aa5f-209">Perform following steps on configuration page:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-Confluencemicrosoft-tutorial/addon5.png)
 
    <span data-ttu-id="1aa5f-211">a.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-211">a.</span></span> <span data-ttu-id="1aa5f-212">Dans **Metadata URL** (URL des métadonnées), collez **l’URL de métadonnées** générée dans Azure AD, puis cliquez sur le bouton **Resolve** (Résoudre).</span><span class="sxs-lookup"><span data-stu-id="1aa5f-212">In **Metadata URL** paste the **Metadata URL** generated from Azure AD and click the **Resolve** button.</span></span> <span data-ttu-id="1aa5f-213">L’URL des métadonnées IdP est alors lue et tous les champs sont renseignés.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-213">It reads the IdP metadata URL and populates all the fields information.</span></span>

    > [!Note]
    > <span data-ttu-id="1aa5f-214">Par défaut, l’emplacement de l’identificateur d’utilisateur SAML est défini sur l’élément NameIdentifier.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-214">Default SAML User ID location is Name Identifier.</span></span> <span data-ttu-id="1aa5f-215">Vous pouvez remplacer cela par une option d’attribut et entrer le nom de l’attribut souhaité.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-215">You can change this to an attribute option and enter the appropriate attribute name.</span></span>

    > [!TIP]
    > <span data-ttu-id="1aa5f-216">Vérifiez qu’un seul certificat est associé à l’application pour éviter toute erreur liée à la résolution des métadonnées.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-216">Ensure that there is only one certificate mapped against the app so that there is no error in resolving the metadata.</span></span> <span data-ttu-id="1aa5f-217">Si plusieurs certificats sont associés, l’administrateur verra un message d’erreur s’afficher lors de la résolution des métadonnées.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-217">If there are multiple certificates, upon resolving the metadata, admin gets an error.</span></span>
    
    <span data-ttu-id="1aa5f-218">b.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-218">b.</span></span> <span data-ttu-id="1aa5f-219">Copiez les valeurs des champs **Identifier, Reply URL et Sign on URL**, puis collez-les dans les zones de texte **Identificateur, URL de réponse et URL de connexion** correspondantes dans la section **Domaine et URL Confluence SAML SSO by Microsoft** du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-219">Copy the **Identifier, Reply URL and Sign on URL** values and paste them in **Identifier, Reply URL and Sign on URL** textboxes respectively in **Confluence SAML SSO by Microsoft Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="1aa5f-220">c.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-220">c.</span></span> <span data-ttu-id="1aa5f-221">Dans **Login Button Name** (Nom du bouton de connexion), tapez le nom du bouton que les utilisateurs doivent voir sur l’écran de connexion.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-221">In **Login Button Name** type the name of button your organization wants the users to see on login screen.</span></span>

    <span data-ttu-id="1aa5f-222">d.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-222">d.</span></span> <span data-ttu-id="1aa5f-223">Dans **SAML User ID Locations** (Emplacements de l’identificateur d’utilisateur SAML), sélectionnez **User ID is in the NameIdentifier element of the Subject statement** (L’ID utilisateur se trouve dans l’élément NameIdentifier de l’instruction Subject ) ou **User ID is in an Attribute element** (L’identificateur d’utilisateur se trouve dans l’élément Attribute).</span><span class="sxs-lookup"><span data-stu-id="1aa5f-223">In **SAML User ID Locations** select either **User ID is in the NameIdentifier element of the Subject statement** or **User ID is in an Attribute element**.</span></span>  <span data-ttu-id="1aa5f-224">Cet ID doit être l’ID utilisateur Confluence.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-224">This ID has to be the Confluence user id.</span></span> <span data-ttu-id="1aa5f-225">Si aucun identificateur d’utilisateur correspondant n’est trouvé, le système n’autorise pas l’utilisateur à se connecter.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-225">If the user id is not matched, then system will not allow users to log in.</span></span> 
    
    <span data-ttu-id="1aa5f-226">e.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-226">e.</span></span> <span data-ttu-id="1aa5f-227">Si vous sélectionnez l’option **User ID is in an Attribute element**, dans la zone de texte **Attribute name** (Nom de l’attribut), tapez le nom de l’attribut dans lequel l’identificateur d’utilisateur doit se trouver.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-227">If you select **User ID is in an Attribute element** option, then in **Attribute name** textbox type the name of the attribute where User Id is expected.</span></span> 

    <span data-ttu-id="1aa5f-228">f.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-228">f.</span></span> <span data-ttu-id="1aa5f-229">Si vous utilisez le domaine fédéré (AD FS, etc.) avec Azure AD, cochez l’option **Enable Home Realm Discovery** (Activer la détection de domaine d’accueil), puis entrez un nom de domaine sous **Domain Name**.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-229">If you are using the federated domain (like ADFS etc.) with Azure AD, then click on the **Enable Home Realm Discovery** option and configure the **Domain Name**.</span></span>
    
    <span data-ttu-id="1aa5f-230">g.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-230">g.</span></span> <span data-ttu-id="1aa5f-231">Si la connexion est basée sur AD FS, tapez le nom du domaine dans le champ **Domain Name**.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-231">In **Domain Name** type the domain name here in case of the ADFS-based login.</span></span>

    <span data-ttu-id="1aa5f-232">h.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-232">h.</span></span> <span data-ttu-id="1aa5f-233">Cochez l’option **Enable Single Sign out** (Activer la déconnexion unique) si vous souhaitez qu’un utilisateur soit déconnecté d’Azure AD lorsqu’il se déconnecte de Confluence.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-233">Check **Enable Single Sign out** if you wish to log out from Azure AD when a user logs out from Confluence.</span></span> 

    <span data-ttu-id="1aa5f-234">i.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-234">i.</span></span> <span data-ttu-id="1aa5f-235">Cliquez sur **Enregistrer** pour enregistrer les paramètres.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-235">Click **Save** button to save the settings.</span></span>


> [!TIP]
> <span data-ttu-id="1aa5f-236">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-236">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1aa5f-237">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-237">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1aa5f-238">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1aa5f-238">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1aa5f-239">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="1aa5f-239">Creating an Azure AD test user</span></span>
<span data-ttu-id="1aa5f-240">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-240">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="1aa5f-242">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1aa5f-242">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1aa5f-243">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-243">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1aa5f-245">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-245">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1aa5f-247">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-247">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1aa5f-249">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1aa5f-249">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1aa5f-251">a.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-251">a.</span></span> <span data-ttu-id="1aa5f-252">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-252">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1aa5f-253">b.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-253">b.</span></span> <span data-ttu-id="1aa5f-254">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-254">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1aa5f-255">c.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-255">c.</span></span> <span data-ttu-id="1aa5f-256">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-256">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1aa5f-257">d.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-257">d.</span></span> <span data-ttu-id="1aa5f-258">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-258">Click **Create**.</span></span>
 
### <a name="creating-a-confluence-saml-sso-by-microsoft-test-user"></a><span data-ttu-id="1aa5f-259">Création d’un utilisateur de test Confluence SAML SSO by Microsoft</span><span class="sxs-lookup"><span data-stu-id="1aa5f-259">Creating a Confluence SAML SSO by Microsoft test user</span></span>

<span data-ttu-id="1aa5f-260">Pour permettre aux utilisateurs Azure AD de se connecter à un serveur local Confluence, vous devez les attribuer dans Confluence SAML SSO by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-260">To enable Azure AD users to log in to Confluence on premise server, they must be provisioned into Confluence SAML SSO by Microsoft.</span></span> <span data-ttu-id="1aa5f-261">Pour Confluence SAML SSO by Microsoft, l’attribution des utilisateurs se fait manuellement.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-261">For Confluence SAML SSO by Microsoft, provisioning is a manual task.</span></span>

<span data-ttu-id="1aa5f-262">**Pour approvisionner un compte d’utilisateur, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1aa5f-262">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="1aa5f-263">Connectez-vous à votre serveur local Confluence en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-263">Log in to your Confluence on premise server as an administrator.</span></span>

2. <span data-ttu-id="1aa5f-264">Pointez sur la roue dentée, puis cliquez sur **Gestion des utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-264">Hover on cog and click the **User management**.</span></span>

    ![Ajouter un employé](./media/active-directory-saas-confluencemicrosoft-tutorial/user1.png) 

3. <span data-ttu-id="1aa5f-266">Dans la section Utilisateurs, cliquez sur l’onglet **Add users** (Ajouter des utilisateurs).</span><span class="sxs-lookup"><span data-stu-id="1aa5f-266">Under Users section, click **Add users** tab.</span></span> <span data-ttu-id="1aa5f-267">Dans la page de boîte de dialogue **Add a User** (Ajouter un utilisateur), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1aa5f-267">On the **“Add a User”** dialog page, perform the following steps:</span></span>

    ![Ajouter un employé](./media/active-directory-saas-confluencemicrosoft-tutorial/user2.png) 

    <span data-ttu-id="1aa5f-269">a.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-269">a.</span></span> <span data-ttu-id="1aa5f-270">Dans la zone de texte **Username** (Nom d’utilisateur), tapez le nom d’un utilisateur, par exemple, Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-270">In the **Username** textbox, type the email of user like Britta Simon.</span></span>

    <span data-ttu-id="1aa5f-271">b.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-271">b.</span></span> <span data-ttu-id="1aa5f-272">Dans la zone de texte **Full Name** (Nom complet), tapez le nom complet d’un utilisateur, par exemple, Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-272">In the **Full Name** textbox, type the full name of user like Britta Simon.</span></span>

    <span data-ttu-id="1aa5f-273">c.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-273">c.</span></span> <span data-ttu-id="1aa5f-274">Dans la zone de texte **Email** (E-mail), tapez l’adresse e-mail d’un utilisateur, par exemple, Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-274">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="1aa5f-275">d.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-275">d.</span></span> <span data-ttu-id="1aa5f-276">Dans la zone de texte **Password** (Mot de passe), tapez le mot de passe de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-276">In the **Password** textbox, type the password for Britta Simon.</span></span>

    <span data-ttu-id="1aa5f-277">e.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-277">e.</span></span> <span data-ttu-id="1aa5f-278">Cliquez sur **Confirm Password** (Confirmer le mot de passe), puis entrez de nouveau le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-278">Click **Confirm Password** reenter the password.</span></span>
    
    <span data-ttu-id="1aa5f-279">f.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-279">f.</span></span> <span data-ttu-id="1aa5f-280">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-280">Click **Add** button.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1aa5f-281">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="1aa5f-281">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1aa5f-282">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Confluence SAML SSO by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-282">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Confluence SAML SSO by Microsoft.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="1aa5f-284">**Pour attribuer Britta Simon à Confluence SAML SSO by Microsoft, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="1aa5f-284">**To assign Britta Simon to Confluence SAML SSO by Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="1aa5f-285">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-285">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="1aa5f-287">Dans la liste des applications, sélectionnez **Confluence SAML SSO by Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-287">In the applications list, select **Confluence SAML SSO by Microsoft**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_app.png) 

3. <span data-ttu-id="1aa5f-289">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-289">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="1aa5f-291">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-291">Click **Add** button.</span></span> <span data-ttu-id="1aa5f-292">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-292">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="1aa5f-294">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-294">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1aa5f-295">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-295">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1aa5f-296">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-296">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1aa5f-297">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="1aa5f-297">Testing single sign-on</span></span>

<span data-ttu-id="1aa5f-298">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-298">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1aa5f-299">Lorsque vous cliquez sur la vignette Confluence SAML SSO by Microsoft dans le volet d’accès, vous devez être connecté automatiquement à votre application Confluence SAML SSO by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1aa5f-299">When you click the Confluence SAML SSO by Microsoft tile in the Access Panel, you should get automatically signed-on to your Confluence SAML SSO by Microsoft application.</span></span>
<span data-ttu-id="1aa5f-300">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1aa5f-300">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1aa5f-301">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="1aa5f-301">Additional resources</span></span>

* [<span data-ttu-id="1aa5f-302">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1aa5f-302">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1aa5f-303">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="1aa5f-303">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_203.png

