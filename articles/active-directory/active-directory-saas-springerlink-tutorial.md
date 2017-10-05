---
title: "Didacticiel : Intégration d’Azure Active Directory avec Springer Link | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Springer Link."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 58cdf029-bdc0-43c4-a469-b921c2a669bd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: jeedes
ms.openlocfilehash: b9aec6f8f293cdd31456a7f50e3efe792804c7c8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-springer-link"></a><span data-ttu-id="d76f0-103">Didacticiel : Intégration d’Azure Active Directory avec Springer Link</span><span class="sxs-lookup"><span data-stu-id="d76f0-103">Tutorial: Azure Active Directory integration with Springer Link</span></span>

<span data-ttu-id="d76f0-104">Ce didacticiel explique comment intégrer Springer Link avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d76f0-104">In this tutorial, you learn how to integrate Springer Link with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d76f0-105">L’intégration de Springer Link avec Azure AD offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="d76f0-105">Integrating Springer Link with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d76f0-106">Dans Azure AD, vous pouvez contrôler qui a accès à Springer Link.</span><span class="sxs-lookup"><span data-stu-id="d76f0-106">You can control in Azure AD who has access to Springer Link.</span></span>
- <span data-ttu-id="d76f0-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Springer Link (via l’authentification unique) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d76f0-107">You can enable your users to automatically get signed-on to Springer Link (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="d76f0-108">Vous pouvez gérer vos comptes dans un emplacement central : le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d76f0-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="d76f0-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d76f0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d76f0-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d76f0-110">Prerequisites</span></span>

<span data-ttu-id="d76f0-111">Pour configurer l’intégration d’Azure AD avec Springer Link, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="d76f0-111">To configure Azure AD integration with Springer Link, you need the following items:</span></span>

- <span data-ttu-id="d76f0-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="d76f0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d76f0-113">Un abonnement Springer Link pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="d76f0-113">A Springer Link single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d76f0-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="d76f0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d76f0-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="d76f0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d76f0-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="d76f0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d76f0-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d76f0-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d76f0-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="d76f0-118">Scenario description</span></span>
<span data-ttu-id="d76f0-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="d76f0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d76f0-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="d76f0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d76f0-121">Ajout de Springer Link à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="d76f0-121">Adding Springer Link from the gallery</span></span>
2. <span data-ttu-id="d76f0-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d76f0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-springer-link-from-the-gallery"></a><span data-ttu-id="d76f0-123">Ajout de Springer Link à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="d76f0-123">Adding Springer Link from the gallery</span></span>
<span data-ttu-id="d76f0-124">Pour configurer l’intégration de Springer Link avec Azure AD, vous devez ajouter Springer Link à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="d76f0-124">To configure the integration of Springer Link into Azure AD, you need to add Springer Link from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d76f0-125">**Pour ajouter Springer Link à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d76f0-125">**To add Springer Link from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d76f0-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d76f0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Bouton Azure Active Directory][1]

2. <span data-ttu-id="d76f0-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="d76f0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d76f0-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="d76f0-129">Then go to **All applications**.</span></span>

    ![Panneau Applications d’entreprise][2]
    
3. <span data-ttu-id="d76f0-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="d76f0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Bouton Nouvelle application][3]

4. <span data-ttu-id="d76f0-133">Dans la zone de recherche, tapez **Springer Link**, sélectionnez **Springer Link** dans le panneau de résultats, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="d76f0-133">In the search box, type **Springer Link**, select **Springer Link** from result panel then click **Add** button to add the application.</span></span>

    ![Springer Link dans la liste des résultats](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d76f0-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d76f0-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="d76f0-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Springer Link, sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="d76f0-136">In this section, you configure and test Azure AD single sign-on with Springer Link based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d76f0-137">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Springer Link équivalent à un utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d76f0-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Springer Link is to a user in Azure AD.</span></span> <span data-ttu-id="d76f0-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur Springer Link associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="d76f0-138">In other words, a link relationship between an Azure AD user and the related user in Springer Link needs to be established.</span></span>

<span data-ttu-id="d76f0-139">Dans Springer Link, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **Username** pour établir la relation de lien.</span><span class="sxs-lookup"><span data-stu-id="d76f0-139">In Springer Link, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d76f0-140">Pour configurer et tester l’authentification unique Azure AD avec Springer Link, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="d76f0-140">To configure and test Azure AD single sign-on with Springer Link, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d76f0-141">**[Configurer l’authentification unique Azure AD](#configure-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="d76f0-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d76f0-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d76f0-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d76f0-143">**[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d76f0-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
4. <span data-ttu-id="d76f0-144">**[Tester l’authentification unique](#test-single-sign-on)** : pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="d76f0-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="d76f0-145">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d76f0-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="d76f0-146">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Springer Link.</span><span class="sxs-lookup"><span data-stu-id="d76f0-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Springer Link application.</span></span>

<span data-ttu-id="d76f0-147">**Pour configurer l’authentification unique Azure AD avec Springer Link, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d76f0-147">**To configure Azure AD single sign-on with Springer Link, perform the following steps:**</span></span>

1. <span data-ttu-id="d76f0-148">Dans le portail Azure, sur la page d’intégration de l’application **Springer Link**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="d76f0-148">In the Azure portal, on the **Springer Link** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="d76f0-150">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="d76f0-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_samlbase.png)

3. <span data-ttu-id="d76f0-152">Dans la section **Domaine et URL Springer Link**, si vous souhaitez configurer l’application en mode initié par **IDP**, suivez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="d76f0-152">On the **Springer Link Domain and URLs** section,  If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Informations d’authentification unique dans Domaine et URL Springer Link](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_url1.png)

    <span data-ttu-id="d76f0-154">a.</span><span class="sxs-lookup"><span data-stu-id="d76f0-154">a.</span></span> <span data-ttu-id="d76f0-155">Dans la zone de texte **Identificateur**, saisissez l’URL : `https://fsso.springer.com`</span><span class="sxs-lookup"><span data-stu-id="d76f0-155">In the **Identifier** textbox, type the URL: `https://fsso.springer.com`</span></span>

    <span data-ttu-id="d76f0-156">b.</span><span class="sxs-lookup"><span data-stu-id="d76f0-156">b.</span></span> <span data-ttu-id="d76f0-157">Dans la zone de texte **URL de réponse**, tapez l’URL : `https://fsso-qa1.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span><span class="sxs-lookup"><span data-stu-id="d76f0-157">In the **Reply URL** textbox, type the URL: `https://fsso-qa1.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span></span>    

4. <span data-ttu-id="d76f0-158">Cliquez sur **Afficher les paramètres d’URL avancés**.</span><span class="sxs-lookup"><span data-stu-id="d76f0-158">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="d76f0-159">Si vous souhaitez configurer l’application en mode initié par le **fournisseur de service** :</span><span class="sxs-lookup"><span data-stu-id="d76f0-159">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Informations d’authentification unique dans Domaine et URL Springer Link](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_url.png)

    <span data-ttu-id="d76f0-161">Dans la zone de texte **URL de connexion**, entrez l’URL : `https://fsso.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span><span class="sxs-lookup"><span data-stu-id="d76f0-161">In the **Sign-on URL** textbox, type the URL : `https://fsso.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span></span>    

5. <span data-ttu-id="d76f0-162">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="d76f0-162">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-springerlink-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d76f0-164">Pour générer l’URL des **métadonnées**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="d76f0-164">To generate the **Metadata** url, perform the following steps:</span></span>

    <span data-ttu-id="d76f0-165">a.</span><span class="sxs-lookup"><span data-stu-id="d76f0-165">a.</span></span> <span data-ttu-id="d76f0-166">Cliquez sur **Inscriptions des applications**.</span><span class="sxs-lookup"><span data-stu-id="d76f0-166">Click **App registrations**.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_appregistrations.png)
   
    <span data-ttu-id="d76f0-168">b.</span><span class="sxs-lookup"><span data-stu-id="d76f0-168">b.</span></span> <span data-ttu-id="d76f0-169">Cliquez sur **Points de terminaison** pour ouvrir la boîte de dialogue **Points de terminaison**.</span><span class="sxs-lookup"><span data-stu-id="d76f0-169">Click **Endpoints** to open **Endpoints** dialog box.</span></span>  
    
    ![Configurer l’authentification unique](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_endpointicon.png)

    <span data-ttu-id="d76f0-171">c.</span><span class="sxs-lookup"><span data-stu-id="d76f0-171">c.</span></span> <span data-ttu-id="d76f0-172">Cliquez sur le bouton Copier pour copier l’URL du document de métadonnées de fédération (**FEDERATION METADATA DOCUMENT**), puis collez-la dans le Bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="d76f0-172">Click the copy button to copy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_endpoint.png)
     
    <span data-ttu-id="d76f0-174">d.</span><span class="sxs-lookup"><span data-stu-id="d76f0-174">d.</span></span> <span data-ttu-id="d76f0-175">Accédez maintenant à la page de propriétés de **Springer Link**, puis copiez l’**ID d’application** à l’aide du bouton **Copier** et collez-le dans le Bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="d76f0-175">Now go to the property page of **Springer Link** and copy the **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_appid.png)

    <span data-ttu-id="d76f0-177">e.</span><span class="sxs-lookup"><span data-stu-id="d76f0-177">e.</span></span> <span data-ttu-id="d76f0-178">Générez l’**URL des métadonnées** en utilisant le format suivant : `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="d76f0-178">Generate the **Metadata URL** using the following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

7. <span data-ttu-id="d76f0-179">Pour configurer l’authentification unique côté **Springer Link**, vous devez envoyer l’**URL de métadonnées** générée à l’[équipe de support Springer Link](mailto:identity@springernature.com).</span><span class="sxs-lookup"><span data-stu-id="d76f0-179">To configure single sign-on on **Springer Link** side, you need to send the generated **Metadata URL** to [Springer Link support team](mailto:identity@springernature.com).</span></span>

> [!TIP]
> <span data-ttu-id="d76f0-180">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="d76f0-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d76f0-181">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="d76f0-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d76f0-182">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d76f0-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d76f0-183">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="d76f0-183">Create an Azure AD test user</span></span>

<span data-ttu-id="d76f0-184">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d76f0-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="d76f0-186">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d76f0-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d76f0-187">Dans le volet gauche du Portail Azure, cliquez sur le bouton **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d76f0-187">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Bouton Azure Active Directory](./media/active-directory-saas-springerlink-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="d76f0-189">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="d76f0-189">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Liens « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/active-directory-saas-springerlink-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="d76f0-191">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="d76f0-191">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Bouton Ajouter](./media/active-directory-saas-springerlink-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="d76f0-193">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="d76f0-193">In the **User** dialog box, perform the following steps:</span></span>

    ![Boîte de dialogue Utilisateur](./media/active-directory-saas-springerlink-tutorial/create_aaduser_04.png)

    <span data-ttu-id="d76f0-195">a.</span><span class="sxs-lookup"><span data-stu-id="d76f0-195">a.</span></span> <span data-ttu-id="d76f0-196">Dans la zone **Nom**, tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d76f0-196">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d76f0-197">b.</span><span class="sxs-lookup"><span data-stu-id="d76f0-197">b.</span></span> <span data-ttu-id="d76f0-198">Dans la zone **Nom d’utilisateur** , tapez l’adresse e-mail de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d76f0-198">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="d76f0-199">c.</span><span class="sxs-lookup"><span data-stu-id="d76f0-199">c.</span></span> <span data-ttu-id="d76f0-200">Cochez la case **Afficher le mot de passe**, puis notez la valeur affichée dans le champ **Mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="d76f0-200">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="d76f0-201">d.</span><span class="sxs-lookup"><span data-stu-id="d76f0-201">d.</span></span> <span data-ttu-id="d76f0-202">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="d76f0-202">Click **Create**.</span></span>
 
### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="d76f0-203">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="d76f0-203">Assign the Azure AD test user</span></span>

<span data-ttu-id="d76f0-204">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Springer Link.</span><span class="sxs-lookup"><span data-stu-id="d76f0-204">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Springer Link.</span></span>

![Attribuer le rôle utilisateur][200] 

<span data-ttu-id="d76f0-206">**Pour affecter Britta Simon à Springer Link, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d76f0-206">**To assign Britta Simon to Springer Link, perform the following steps:**</span></span>

1. <span data-ttu-id="d76f0-207">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="d76f0-207">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="d76f0-209">Dans la liste des applications, sélectionnez **Springer Link**.</span><span class="sxs-lookup"><span data-stu-id="d76f0-209">In the applications list, select **Springer Link**.</span></span>

    ![Lien Springer Link dans la liste des applications](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_app.png)  

3. <span data-ttu-id="d76f0-211">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="d76f0-211">In the menu on the left, click **Users and groups**.</span></span>

    ![Lien « Utilisateurs et groupes »][202]

4. <span data-ttu-id="d76f0-213">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="d76f0-213">Click **Add** button.</span></span> <span data-ttu-id="d76f0-214">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="d76f0-214">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Volet Ajouter une attribution][203]

5. <span data-ttu-id="d76f0-216">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="d76f0-216">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d76f0-217">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="d76f0-217">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d76f0-218">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="d76f0-218">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="d76f0-219">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="d76f0-219">Test single sign-on</span></span>

<span data-ttu-id="d76f0-220">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="d76f0-220">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d76f0-221">Lorsque vous cliquez sur la vignette Springer Link dans le volet d’accès, vous devez être connecté automatiquement à votre application Springer Link.</span><span class="sxs-lookup"><span data-stu-id="d76f0-221">When you click the Springer Link tile in the Access Panel, you should get automatically signed-on to your Springer Link application.</span></span>
<span data-ttu-id="d76f0-222">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d76f0-222">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d76f0-223">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="d76f0-223">Additional resources</span></span>

* [<span data-ttu-id="d76f0-224">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d76f0-224">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d76f0-225">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="d76f0-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_203.png

