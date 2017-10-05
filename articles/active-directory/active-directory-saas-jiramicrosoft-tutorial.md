---
title: "Didacticiel : Intégration d’Azure Active Directory à JIRA SAML SSO by Microsoft | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et JIRA SAML SSO by Microsoft."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0dc847b9-eec4-4c31-845e-0144ddedc4a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: b5f7813c8244d2964b6894ae49cd64e0ee71b704
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jira-saml-sso-by-microsoft"></a><span data-ttu-id="cda22-103">Didacticiel : Intégration d’Azure Active Directory à JIRA SAML SSO by Microsoft</span><span class="sxs-lookup"><span data-stu-id="cda22-103">Tutorial: Azure Active Directory integration with JIRA SAML SSO by Microsoft</span></span>

<span data-ttu-id="cda22-104">Dans ce didacticiel, vous allez apprendre à intégrer JIRA SAML SSO by Microsoft à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cda22-104">In this tutorial, you learn how to integrate JIRA SAML SSO by Microsoft with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cda22-105">L’intégration de JIRA SAML SSO by Microsoft à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="cda22-105">Integrating JIRA SAML SSO by Microsoft with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="cda22-106">Vous pouvez contrôler dans Azure AD qui a accès à JIRA SAML SSO by Microsoft</span><span class="sxs-lookup"><span data-stu-id="cda22-106">You can control in Azure AD who has access to JIRA SAML SSO by Microsoft</span></span>
- <span data-ttu-id="cda22-107">Vous pouvez permettre à vos utilisateurs d’être automatiquement authentifiés dans JIRA SAML SSO by Microsoft (authentification unique) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="cda22-107">You can enable your users to automatically get signed-on to JIRA SAML SSO by Microsoft (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cda22-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="cda22-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="cda22-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cda22-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cda22-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="cda22-110">Prerequisites</span></span>

<span data-ttu-id="cda22-111">Pour configurer l’intégration d’Azure AD à JIRA SAML SSO by Microsoft, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="cda22-111">To configure Azure AD integration with JIRA SAML SSO by Microsoft, you need the following items:</span></span>

- <span data-ttu-id="cda22-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="cda22-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cda22-113">Une application serveur JIRA installée sur un serveur Windows 64 bits (local ou dans l’infrastructure IaaS cloud)</span><span class="sxs-lookup"><span data-stu-id="cda22-113">JIRA server application installed on a Windows 64-bit server (on premise or on the cloud IaaS infrastructure)</span></span>
- <span data-ttu-id="cda22-114">L’activation du HTTPS dans le serveur JIRA</span><span class="sxs-lookup"><span data-stu-id="cda22-114">JIRA server is HTTPS enabled</span></span>
- <span data-ttu-id="cda22-115">Notez que les versions prises en charge par le plug-in JIRA sont mentionnées dans la section ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="cda22-115">Note the supported versions for JIRA Plugin are mentioned in below section.</span></span>
- <span data-ttu-id="cda22-116">L’accessibilité du serveur JIRA via Internet (particulièrement pour la page de connexion Azure AD pour l’authentification) et la capacité à recevoir le jeton d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="cda22-116">JIRA server is reachable on internet particularly to Azure AD Login page for authentication and should able to receive the token from Azure AD</span></span>
- <span data-ttu-id="cda22-117">La création d’informations d’identification administrateur dans JIRA</span><span class="sxs-lookup"><span data-stu-id="cda22-117">Admin credentials are set up in JIRA</span></span>
- <span data-ttu-id="cda22-118">La désactivation de WebSudo dans JIRA</span><span class="sxs-lookup"><span data-stu-id="cda22-118">WebSudo is disabled in JIRA</span></span>
- <span data-ttu-id="cda22-119">La création d’un utilisateur de test dans l’application serveur JIRA</span><span class="sxs-lookup"><span data-stu-id="cda22-119">Test user created in the JIRA server application</span></span>

> [!NOTE]
> <span data-ttu-id="cda22-120">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production de JIRA.</span><span class="sxs-lookup"><span data-stu-id="cda22-120">To test the steps in this tutorial, we do not recommend using a production environment of JIRA.</span></span> <span data-ttu-id="cda22-121">Testez d’abord l’intégration dans l’environnement de développement ou l’environnement intermédiaire de l’application, puis passez à l’environnement de production.</span><span class="sxs-lookup"><span data-stu-id="cda22-121">Test the integration first in development or staging environment of the application and then use the production environment.</span></span>

<span data-ttu-id="cda22-122">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="cda22-122">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cda22-123">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="cda22-123">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cda22-124">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez bénéficier de [l’offre d’essai](https://azure.microsoft.com/pricing/free-trial/) d’un mois.</span><span class="sxs-lookup"><span data-stu-id="cda22-124">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="supported-versions-of-jira"></a><span data-ttu-id="cda22-125">Versions de JIRA prises en charge</span><span class="sxs-lookup"><span data-stu-id="cda22-125">Supported versions of JIRA</span></span> 

<span data-ttu-id="cda22-126">Les versions suivantes de JIRA sont actuellement prises en charge :</span><span class="sxs-lookup"><span data-stu-id="cda22-126">As of now, following versions of JIRA are supported:</span></span>

- <span data-ttu-id="cda22-127">JIRA Core et logiciels : 6.0 à 7.2.0</span><span class="sxs-lookup"><span data-stu-id="cda22-127">JIRA Core and Software: 6.0 to 7.2.0</span></span>
- <span data-ttu-id="cda22-128">JIRA Service Desk : 3.0 à 3.2</span><span class="sxs-lookup"><span data-stu-id="cda22-128">JIRA Service Desk: 3.0 to 3.2</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cda22-129">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="cda22-129">Scenario description</span></span>
<span data-ttu-id="cda22-130">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="cda22-130">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cda22-131">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="cda22-131">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cda22-132">Ajout de JIRA SAML SSO by Microsoft à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="cda22-132">Adding JIRA SAML SSO by Microsoft from the gallery</span></span>
2. <span data-ttu-id="cda22-133">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="cda22-133">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jira-saml-sso-by-microsoft-from-the-gallery"></a><span data-ttu-id="cda22-134">Ajout de JIRA SAML SSO by Microsoft à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="cda22-134">Adding JIRA SAML SSO by Microsoft from the gallery</span></span>
<span data-ttu-id="cda22-135">Pour configurer l’intégration de JIRA SAML SSO by Microsoft à Azure AD, vous devez ajouter JIRA SAML SSO by Microsoft, disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="cda22-135">To configure the integration of JIRA SAML SSO by Microsoft into Azure AD, you need to add JIRA SAML SSO by Microsoft from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="cda22-136">**Pour ajouter JIRA SAML SSO by Microsoft à partir de la galerie, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="cda22-136">**To add JIRA SAML SSO by Microsoft from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="cda22-137">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cda22-137">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cda22-139">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="cda22-139">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="cda22-140">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="cda22-140">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="cda22-142">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="cda22-142">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="cda22-144">Dans la zone de recherche, tapez **JIRA SAML SSO by Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="cda22-144">In the search box, type **JIRA SAML SSO by Microsoft**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_search.png)

5. <span data-ttu-id="cda22-146">Dans le volet de résultats, sélectionnez **JIRA SAML SSO by Microsoft**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="cda22-146">In the results panel, select **JIRA SAML SSO by Microsoft**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cda22-148">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="cda22-148">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cda22-149">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec JIRA SAML SSO by Microsoft, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="cda22-149">In this section, you configure and test Azure AD single sign-on with JIRA SAML SSO by Microsoft based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="cda22-150">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur JIRA SAML SSO by Microsoft équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cda22-150">For single sign-on to work, Azure AD needs to know what the counterpart user in JIRA SAML SSO by Microsoft is to a user in Azure AD.</span></span> <span data-ttu-id="cda22-151">En d’autres termes, une relation doit être établie entre l’utilisateur Azure AD et l’utilisateur JIRA SAML SSO by Microsoft associé.</span><span class="sxs-lookup"><span data-stu-id="cda22-151">In other words, a link relationship between an Azure AD user and the related user in JIRA SAML SSO by Microsoft needs to be established.</span></span>

<span data-ttu-id="cda22-152">Dans JIRA SAML SSO by Microsoft, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="cda22-152">In JIRA SAML SSO by Microsoft, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="cda22-153">Pour configurer et tester l’authentification unique Azure AD avec JIRA SAML SSO by Microsoft, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="cda22-153">To configure and test Azure AD single sign-on with JIRA SAML SSO by Microsoft, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="cda22-154">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="cda22-154">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="cda22-155">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cda22-155">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cda22-156">**[Création d’un utilisateur de test JIRA SAML SSO by Microsoft](#creating-a-jira-saml-sso-by-microsoft-test-user)** pour avoir un équivalent de Britta Simon dans JIRA SAML SSO by Microsoft lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="cda22-156">**[Creating a JIRA SAML SSO by Microsoft test user](#creating-a-jira-saml-sso-by-microsoft-test-user)** - to have a counterpart of Britta Simon in JIRA SAML SSO by Microsoft that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="cda22-157">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cda22-157">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cda22-158">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="cda22-158">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cda22-159">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="cda22-159">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cda22-160">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application JIRA SAML SSO by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cda22-160">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your JIRA SAML SSO by Microsoft application.</span></span>

<span data-ttu-id="cda22-161">**Pour configurer l’authentification unique Azure AD avec JIRA SAML SSO by Microsoft, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="cda22-161">**To configure Azure AD single sign-on with JIRA SAML SSO by Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="cda22-162">Dans le portail Azure, dans la page d’intégration de l’application **JIRA SAML SSO by Microsoft**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="cda22-162">In the Azure portal, on the **JIRA SAML SSO by Microsoft** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="cda22-164">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="cda22-164">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_samlbase.png)

3. <span data-ttu-id="cda22-166">Dans la section **Domaine et URL JIRA SAML SSO by Microsoft**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="cda22-166">On the **JIRA SAML SSO by Microsoft Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_url.png)

    <span data-ttu-id="cda22-168">a.</span><span class="sxs-lookup"><span data-stu-id="cda22-168">a.</span></span> <span data-ttu-id="cda22-169">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="cda22-169">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    <span data-ttu-id="cda22-170">b.</span><span class="sxs-lookup"><span data-stu-id="cda22-170">b.</span></span> <span data-ttu-id="cda22-171">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<domain:port>/`</span><span class="sxs-lookup"><span data-stu-id="cda22-171">In the **Identifier** textbox, type a URL using the following pattern: `https://<domain:port>/`</span></span>

    <span data-ttu-id="cda22-172">c.</span><span class="sxs-lookup"><span data-stu-id="cda22-172">c.</span></span> <span data-ttu-id="cda22-173">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="cda22-173">In the **Reply URL** textbox, type a URL using the following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cda22-174">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="cda22-174">These values are not real.</span></span> <span data-ttu-id="cda22-175">Mettez à jour ces valeurs avec l’identificateur, l’URL de réponse et l’URL de connexion réels.</span><span class="sxs-lookup"><span data-stu-id="cda22-175">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="cda22-176">Le port est facultatif s’il s’agit d’une URL nommée.</span><span class="sxs-lookup"><span data-stu-id="cda22-176">Port is optional in case it’s a named URL.</span></span> <span data-ttu-id="cda22-177">Ces valeurs sont reçues durant la configuration du plug-in JIRA qui est décrite plus loin dans le didacticiel.</span><span class="sxs-lookup"><span data-stu-id="cda22-177">These values are received during the configuration of Jira plugin, which is explained later in the tutorial.</span></span>
 
4. <span data-ttu-id="cda22-178">Pour générer l’URL des **métadonnées**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="cda22-178">To generate the **Metadata** url, perform the following steps:</span></span>

    <span data-ttu-id="cda22-179">a.</span><span class="sxs-lookup"><span data-stu-id="cda22-179">a.</span></span> <span data-ttu-id="cda22-180">Cliquez sur **Inscriptions des applications**.</span><span class="sxs-lookup"><span data-stu-id="cda22-180">Click **App registrations**.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-jiramicrosoft-tutorial/appregistrations.png)
   
    <span data-ttu-id="cda22-182">b.</span><span class="sxs-lookup"><span data-stu-id="cda22-182">b.</span></span> <span data-ttu-id="cda22-183">Cliquez sur **Points de terminaison** pour ouvrir la boîte de dialogue **Points de terminaison**.</span><span class="sxs-lookup"><span data-stu-id="cda22-183">Click **Endpoints** to open **Endpoints** dialog box.</span></span>  
    
    ![Configurer l’authentification unique](./media/active-directory-saas-jiramicrosoft-tutorial/endpointicon.png)

    <span data-ttu-id="cda22-185">c.</span><span class="sxs-lookup"><span data-stu-id="cda22-185">c.</span></span> <span data-ttu-id="cda22-186">Cliquez sur le bouton Copier pour copier l’URL du document de métadonnées de fédération (**FEDERATION METADATA DOCUMENT**), puis collez-la dans le Bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="cda22-186">Click the copy button to copy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-jiramicrosoft-tutorial/endpoint.png)
     
    <span data-ttu-id="cda22-188">d.</span><span class="sxs-lookup"><span data-stu-id="cda22-188">d.</span></span> <span data-ttu-id="cda22-189">Accédez maintenant à la page de propriétés de **JIRA SAML SSO by Microsoft**, copiez **l’ID d’application** à l’aide du bouton **Copier**, puis collez-le dans le Bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="cda22-189">Now go to the property page of **JIRA SAML SSO by Microsoft** and copy the **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-jiramicrosoft-tutorial/appid.png)

    <span data-ttu-id="cda22-191">e.</span><span class="sxs-lookup"><span data-stu-id="cda22-191">e.</span></span> <span data-ttu-id="cda22-192">Générez **l’URL de métadonnées** en respectant le format suivant : `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` et copiez cette valeur dans le Bloc-notes, car vous en aurez besoin plus tard pour la configuration du plug-in.</span><span class="sxs-lookup"><span data-stu-id="cda22-192">Generate the **Metadata URL** using the following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` and copy this value in notepad as it is used later for the configuration of the plugin.</span></span>

5. <span data-ttu-id="cda22-193">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="cda22-193">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cda22-195">Contactez [Microsoft](mailto:waadpartners@microsoft.com) afin de leur communiquer les informations suivantes pour le plug-in JIRA.</span><span class="sxs-lookup"><span data-stu-id="cda22-195">Contact [Microsoft](mailto:waadpartners@microsoft.com) with the following information for the JIRA plugin.</span></span>
    
    *   <span data-ttu-id="cda22-196">Nom du client :</span><span class="sxs-lookup"><span data-stu-id="cda22-196">Customer Name:</span></span>
    *   <span data-ttu-id="cda22-197">Nom du domaine principal :</span><span class="sxs-lookup"><span data-stu-id="cda22-197">Primary domain name:</span></span>
    *   <span data-ttu-id="cda22-198">Azure AD Premium : Oui/Non (le plug-in est disponible pour tous les clients disposant d’un abonnement Gratuit, De base et Premium)</span><span class="sxs-lookup"><span data-stu-id="cda22-198">Azure AD Premium: Yes/No (Plugin will be available to all     the customer Free, Basic, and Premium SKU)</span></span>
    *   <span data-ttu-id="cda22-199">Nombre d’utilisateurs qui vont utiliser cette intégration :</span><span class="sxs-lookup"><span data-stu-id="cda22-199">Number of users who will be using this integration:</span></span>
    *   <span data-ttu-id="cda22-200">Version JIRA :</span><span class="sxs-lookup"><span data-stu-id="cda22-200">JIRA Version:</span></span>
    *   <span data-ttu-id="cda22-201">Commentaires :</span><span class="sxs-lookup"><span data-stu-id="cda22-201">Comments:</span></span>

7. <span data-ttu-id="cda22-202">Dans une autre fenêtre de navigateur web, connectez-vous à votre instance JIRA en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="cda22-202">In a different web browser window, log in to your JIRA instance as an administrator.</span></span>

8. <span data-ttu-id="cda22-203">Pointez sur le roue dentée, puis cliquez sur **Modules complémentaires**.</span><span class="sxs-lookup"><span data-stu-id="cda22-203">Hover on cog and click the **Add-ons**.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-jiramicrosoft-tutorial/addon1.png)

9. <span data-ttu-id="cda22-205">Sous l’onglet Add-ons (Modules complémentaires), cliquez sur **Manage add-ons** (Gérer les modules complémentaires).</span><span class="sxs-lookup"><span data-stu-id="cda22-205">Under Add-ons tab section, click **Manage add-ons**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-jiramicrosoft-tutorial/addon7.png)

10. <span data-ttu-id="cda22-207">Chargez manuellement le plug-in fourni par Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cda22-207">Manually upload the plugin provided by Microsoft.</span></span> <span data-ttu-id="cda22-208">Une fois que le plug-in est installé, il s’affiche sous **User Installed** (Installé par l’utilisateur), dans la section **Manage add-ons** (Gérer les modules complémentaires).</span><span class="sxs-lookup"><span data-stu-id="cda22-208">Once the plugin is installed, it appears in **User Installed** add-ons section of **Manage Add-on** section.</span></span>

11. <span data-ttu-id="cda22-209">Cliquez sur **Configurer** pour configurer le nouveau plug-in.</span><span class="sxs-lookup"><span data-stu-id="cda22-209">Click **Configure** to configure the new plugin.</span></span>

12. <span data-ttu-id="cda22-210">Effectuez les opérations suivantes dans la page de configuration :</span><span class="sxs-lookup"><span data-stu-id="cda22-210">Perform following steps on configuration page:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-jiramicrosoft-tutorial/addon5.png)
 
    <span data-ttu-id="cda22-212">a.</span><span class="sxs-lookup"><span data-stu-id="cda22-212">a.</span></span> <span data-ttu-id="cda22-213">Dans **Metadata URL** (URL des métadonnées), collez **l’URL de métadonnées** générée dans Azure AD, puis cliquez sur le bouton **Resolve** (Résoudre).</span><span class="sxs-lookup"><span data-stu-id="cda22-213">In **Metadata URL** paste the **Metadata URL** generated from Azure AD and click the **Resolve** button.</span></span> <span data-ttu-id="cda22-214">L’URL des métadonnées IdP est alors lue et tous les champs sont renseignés.</span><span class="sxs-lookup"><span data-stu-id="cda22-214">It reads the IdP metadata URL and populates all the fields information.</span></span>

    > [!Note]
    > <span data-ttu-id="cda22-215">Par défaut, l’emplacement de l’identificateur d’utilisateur SAML est défini sur l’élément NameIdentifier.</span><span class="sxs-lookup"><span data-stu-id="cda22-215">Default SAML User ID location is Name Identifier.</span></span> <span data-ttu-id="cda22-216">Vous pouvez remplacer cela par une option d’attribut et entrer le nom de l’attribut souhaité.</span><span class="sxs-lookup"><span data-stu-id="cda22-216">You can change this to an attribute option and enter the appropriate attribute name.</span></span>

    > [!TIP]
    > <span data-ttu-id="cda22-217">Vérifiez qu’un seul certificat est associé à l’application pour éviter toute erreur liée à la résolution des métadonnées.</span><span class="sxs-lookup"><span data-stu-id="cda22-217">Ensure that there is only one certificate mapped against the app so that there is no error in resolving the metadata.</span></span> <span data-ttu-id="cda22-218">Si plusieurs certificats sont associés, l’administrateur verra un message d’erreur s’afficher lors de la résolution des métadonnées.</span><span class="sxs-lookup"><span data-stu-id="cda22-218">If there are multiple certificates, upon resolving the metadata, admin gets an error.</span></span>
    
    <span data-ttu-id="cda22-219">b.</span><span class="sxs-lookup"><span data-stu-id="cda22-219">b.</span></span> <span data-ttu-id="cda22-220">Copiez les valeurs des champs **Identifier, Reply URL et Sign on URL**, puis collez-les dans les zones de texte **Identificateur, URL de réponse et URL de connexion** correspondantes dans la section **Domaine et URL JIRA SAML SSO by Microsoft** du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="cda22-220">Copy the **Identifier, Reply URL and Sign on URL** values and paste them in **Identifier, Reply URL and Sign on URL** textboxes respectively in **JIRA SAML SSO by Microsoft Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="cda22-221">c.</span><span class="sxs-lookup"><span data-stu-id="cda22-221">c.</span></span> <span data-ttu-id="cda22-222">Dans **Login Button Name** (Nom du bouton de connexion), tapez le nom du bouton que les utilisateurs doivent voir sur l’écran de connexion.</span><span class="sxs-lookup"><span data-stu-id="cda22-222">In **Login Button Name** type the name of button your organization wants the users to see on login screen.</span></span>

    <span data-ttu-id="cda22-223">d.</span><span class="sxs-lookup"><span data-stu-id="cda22-223">d.</span></span> <span data-ttu-id="cda22-224">Dans **SAML User ID Locations** (Emplacements de l’ID utilisateur SAML), sélectionnez **User ID is in the NameIdentifier element of the Subject statement** (L’ID utilisateur se trouve dans l’élément NameIdentifier de l’instruction Subject ) ou **User ID is in an Attribute element** (L’ID utilisateur se trouve dans l’élément Attribute).</span><span class="sxs-lookup"><span data-stu-id="cda22-224">In **SAML User ID Locations** select either **User ID is in the NameIdentifier element of the Subject statement** or **User ID is in an Attribute element**.</span></span>  <span data-ttu-id="cda22-225">Cet ID doit être l’ID utilisateur JIRA.</span><span class="sxs-lookup"><span data-stu-id="cda22-225">This ID has to be the JIRA user id.</span></span> <span data-ttu-id="cda22-226">Si aucun ID utilisateur correspondant n’est trouvé, le système n’autorise pas à l’utilisateur à se connecter.</span><span class="sxs-lookup"><span data-stu-id="cda22-226">If the user id is not matched, then system will not allow users to log in.</span></span> 
    
    <span data-ttu-id="cda22-227">e.</span><span class="sxs-lookup"><span data-stu-id="cda22-227">e.</span></span> <span data-ttu-id="cda22-228">Si vous sélectionnez l’option **User ID is in an Attribute element**, dans la zone de texte **Attribute name** (Nom de l’attribut), tapez le nom de l’attribut dans lequel l’identificateur d’utilisateur doit se trouver.</span><span class="sxs-lookup"><span data-stu-id="cda22-228">If you select **User ID is in an Attribute element** option, then in **Attribute name** textbox type the name of the attribute where User Id is expected.</span></span> 

    <span data-ttu-id="cda22-229">f.</span><span class="sxs-lookup"><span data-stu-id="cda22-229">f.</span></span> <span data-ttu-id="cda22-230">Si vous utilisez le domaine fédéré (AD FS, etc.) avec Azure AD, cochez l’option **Enable Home Realm Discovery** (Activer la détection de domaine d’accueil), puis entrez un nom de domaine sous **Domain Name**.</span><span class="sxs-lookup"><span data-stu-id="cda22-230">If you are using the federated domain (like ADFS etc.) with Azure AD, then click on the **Enable Home Realm Discovery** option and configure the **Domain Name**.</span></span>
    
    <span data-ttu-id="cda22-231">g.</span><span class="sxs-lookup"><span data-stu-id="cda22-231">g.</span></span> <span data-ttu-id="cda22-232">Si la connexion est basée sur AD FS, tapez le nom du domaine dans le champ **Domain Name**.</span><span class="sxs-lookup"><span data-stu-id="cda22-232">In **Domain Name** type the domain name here in case of the ADFS-based login.</span></span>

    <span data-ttu-id="cda22-233">h.</span><span class="sxs-lookup"><span data-stu-id="cda22-233">h.</span></span> <span data-ttu-id="cda22-234">Cochez l’option **Enable Single Sign out** (Activer la déconnexion unique) si vous souhaitez qu’un utilisateur soit déconnecté d’Azure AD lorsqu’il se déconnecte de JIRA.</span><span class="sxs-lookup"><span data-stu-id="cda22-234">Check **Enable Single Sign out** if you wish to log out from Azure AD when a user logs out from JIRA.</span></span> 

    <span data-ttu-id="cda22-235">i.</span><span class="sxs-lookup"><span data-stu-id="cda22-235">i.</span></span> <span data-ttu-id="cda22-236">Cliquez sur **Enregistrer** pour enregistrer les paramètres.</span><span class="sxs-lookup"><span data-stu-id="cda22-236">Click **Save** button to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="cda22-237">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="cda22-237">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="cda22-238">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="cda22-238">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="cda22-239">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cda22-239">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cda22-240">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="cda22-240">Creating an Azure AD test user</span></span>
<span data-ttu-id="cda22-241">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="cda22-241">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="cda22-243">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="cda22-243">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="cda22-244">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cda22-244">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cda22-246">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="cda22-246">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cda22-248">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="cda22-248">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cda22-250">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="cda22-250">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cda22-252">a.</span><span class="sxs-lookup"><span data-stu-id="cda22-252">a.</span></span> <span data-ttu-id="cda22-253">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cda22-253">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cda22-254">b.</span><span class="sxs-lookup"><span data-stu-id="cda22-254">b.</span></span> <span data-ttu-id="cda22-255">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cda22-255">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cda22-256">c.</span><span class="sxs-lookup"><span data-stu-id="cda22-256">c.</span></span> <span data-ttu-id="cda22-257">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="cda22-257">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="cda22-258">d.</span><span class="sxs-lookup"><span data-stu-id="cda22-258">d.</span></span> <span data-ttu-id="cda22-259">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="cda22-259">Click **Create**.</span></span>
 
### <a name="creating-a-jira-saml-sso-by-microsoft-test-user"></a><span data-ttu-id="cda22-260">Création d’un utilisateur de test JIRA SAML SSO by Microsoft</span><span class="sxs-lookup"><span data-stu-id="cda22-260">Creating a JIRA SAML SSO by Microsoft test user</span></span>

<span data-ttu-id="cda22-261">Pour permettre aux utilisateurs Azure AD de se connecter à un serveur local JIRA, vous devez les attribuer dans JIRA SAML SSO by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cda22-261">To enable Azure AD users to log in to JIRA on-premise server, they must be provisioned into JIRA SAML SSO by Microsoft.</span></span> <span data-ttu-id="cda22-262">Pour JIRA SAML SSO by Microsoft, l’attribution des utilisateurs se fait manuellement.</span><span class="sxs-lookup"><span data-stu-id="cda22-262">For JIRA SAML SSO by Microsoft, provisioning is a manual task.</span></span>

<span data-ttu-id="cda22-263">**Pour approvisionner un compte d’utilisateur, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="cda22-263">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="cda22-264">Connectez-vous à votre serveur local JIRA en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="cda22-264">Log in to your JIRA on-premise server as an administrator.</span></span>

2. <span data-ttu-id="cda22-265">Pointez sur la roue dentée, puis cliquez sur **Gestion des utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="cda22-265">Hover on cog and click the **User management**.</span></span>

    ![Ajouter un employé](./media/active-directory-saas-jiramicrosoft-tutorial/user1.png) 

3. <span data-ttu-id="cda22-267">Vous êtes redirigé vers la page d’accès administrateur dans laquelle vous entrez le **mot de passe**, puis cliquez sur le bouton **Confirmer**.</span><span class="sxs-lookup"><span data-stu-id="cda22-267">You are redirected to Administrator Access page to enter **Password** and click **Confirm** button.</span></span>

    ![Ajouter un employé](./media/active-directory-saas-jiramicrosoft-tutorial/user2.png) 

4. <span data-ttu-id="cda22-269">Sous l’onglet **User management** (Gestion des utilisateurs), cliquez sur **Create user** (Créer un utilisateur).</span><span class="sxs-lookup"><span data-stu-id="cda22-269">Under **User management** tab section, click **create user**.</span></span>

    ![Ajouter un employé](./media/active-directory-saas-jiramicrosoft-tutorial/user3.png) 

5. <span data-ttu-id="cda22-271">Dans la page de boîte de dialogue **Create New User** (Créer un utilisateur), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="cda22-271">On the **“Create new user”** dialog page, perform the following steps:</span></span>

    ![Ajouter un employé](./media/active-directory-saas-jiramicrosoft-tutorial/user4.png) 

    <span data-ttu-id="cda22-273">a.</span><span class="sxs-lookup"><span data-stu-id="cda22-273">a.</span></span> <span data-ttu-id="cda22-274">Dans la zone de texte **Email address** (Adresse e-mail), tapez l’adresse e-mail d’un utilisateur, par exemple, Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="cda22-274">In the **Email address** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="cda22-275">b.</span><span class="sxs-lookup"><span data-stu-id="cda22-275">b.</span></span> <span data-ttu-id="cda22-276">Dans la zone de texte **Full Name** (Nom complet), tapez le nom complet d’un utilisateur, par exemple, Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cda22-276">In the **Full Name** textbox, type full name of the user like Britta Simon.</span></span>

    <span data-ttu-id="cda22-277">c.</span><span class="sxs-lookup"><span data-stu-id="cda22-277">c.</span></span> <span data-ttu-id="cda22-278">Dans la zone de texte **Username** (Nom d’utilisateur), tapez l’e-mail d’un utilisateur, par exemple, Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="cda22-278">In the **Username** textbox, type the email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="cda22-279">d.</span><span class="sxs-lookup"><span data-stu-id="cda22-279">d.</span></span> <span data-ttu-id="cda22-280">Dans la zone de texte **Password** (Mot de passe), tapez le mot de passe de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="cda22-280">In the **Password** textbox, type the password of user.</span></span>

    <span data-ttu-id="cda22-281">e.</span><span class="sxs-lookup"><span data-stu-id="cda22-281">e.</span></span> <span data-ttu-id="cda22-282">Cliquez sur **Create User** (Créer un utilisateur).</span><span class="sxs-lookup"><span data-stu-id="cda22-282">Click **Create user**.</span></span>   

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="cda22-283">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="cda22-283">Assigning the Azure AD test user</span></span>

<span data-ttu-id="cda22-284">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à JIRA SAML SSO by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cda22-284">In this section, you enable Britta Simon to use Azure single sign-on by granting access to JIRA SAML SSO by Microsoft.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="cda22-286">**Pour attribuer Britta Simon à JIRA SAML SSO by Microsoft, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="cda22-286">**To assign Britta Simon to JIRA SAML SSO by Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="cda22-287">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="cda22-287">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="cda22-289">Dans la liste des applications, sélectionnez **JIRA SAML SSO by Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="cda22-289">In the applications list, select **JIRA SAML SSO by Microsoft**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_app.png) 

3. <span data-ttu-id="cda22-291">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="cda22-291">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="cda22-293">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="cda22-293">Click **Add** button.</span></span> <span data-ttu-id="cda22-294">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="cda22-294">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="cda22-296">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="cda22-296">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="cda22-297">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="cda22-297">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cda22-298">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="cda22-298">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cda22-299">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="cda22-299">Testing single sign-on</span></span>

<span data-ttu-id="cda22-300">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="cda22-300">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="cda22-301">Lorsque vous cliquez sur la vignette JIRA SAML SSO by Microsoft dans le volet d’accès, vous devez être connecté automatiquement à votre application JIRA SAML SSO by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cda22-301">When you click the JIRA SAML SSO by Microsoft tile in the Access Panel, you should get automatically signed-on to your JIRA SAML SSO by Microsoft application.</span></span>
<span data-ttu-id="cda22-302">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cda22-302">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cda22-303">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="cda22-303">Additional resources</span></span>

* [<span data-ttu-id="cda22-304">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cda22-304">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cda22-305">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="cda22-305">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_203.png

