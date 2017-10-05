---
title: "Didacticiel : Intégration d’Azure Active Directory dans &frankly | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et &frankly."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d702060-1b89-4e9d-9f01-ede4f1171c73
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: ea18a9f9bff258337a3de6d7703b4c548efa37df
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-frankly"></a><span data-ttu-id="52825-103">Didacticiel : Intégration d’Azure Active Directory dans &frankly</span><span class="sxs-lookup"><span data-stu-id="52825-103">Tutorial: Azure Active Directory integration with &frankly</span></span>

<span data-ttu-id="52825-104">Dans ce didacticiel, vous allez apprendre à intégrer &frankly à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="52825-104">In this tutorial, you learn how to integrate &frankly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="52825-105">L’intégration d’Azure AD dans &frankly offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="52825-105">Integrating &frankly with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="52825-106">Dans Azure AD, vous pouvez contrôler qui a accès à &frankly.</span><span class="sxs-lookup"><span data-stu-id="52825-106">You can control in Azure AD who has access to &frankly</span></span>
- <span data-ttu-id="52825-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à &frankly (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="52825-107">You can enable your users to automatically get signed-on to &frankly (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="52825-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="52825-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="52825-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="52825-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="52825-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="52825-110">Prerequisites</span></span>

<span data-ttu-id="52825-111">Pour configurer l’intégration d’Azure AD dans &frankly, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="52825-111">To configure Azure AD integration with &frankly, you need the following items:</span></span>

- <span data-ttu-id="52825-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="52825-112">An Azure AD subscription</span></span>
- <span data-ttu-id="52825-113">Un abonnement &frankly pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="52825-113">A &frankly single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="52825-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="52825-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="52825-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="52825-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="52825-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="52825-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="52825-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="52825-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="52825-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="52825-118">Scenario description</span></span>
<span data-ttu-id="52825-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="52825-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="52825-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="52825-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="52825-121">Ajout de &frankly à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="52825-121">Adding &frankly from the gallery</span></span>
2. <span data-ttu-id="52825-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="52825-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-frankly-from-the-gallery"></a><span data-ttu-id="52825-123">Ajout de &frankly à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="52825-123">Adding &frankly from the gallery</span></span>
<span data-ttu-id="52825-124">Pour configurer l’intégration de &frankly dans Azure AD, vous devez ajouter &frankly depuis la galerie dans votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="52825-124">To configure the integration of &frankly into Azure AD, you need to add &frankly from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="52825-125">**Pour ajouter &frankly à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="52825-125">**To add &frankly from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="52825-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="52825-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="52825-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="52825-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="52825-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="52825-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="52825-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="52825-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="52825-133">Dans la zone de recherche, tapez **&frankly**.</span><span class="sxs-lookup"><span data-stu-id="52825-133">In the search box, type **&frankly**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_search.png)

5. <span data-ttu-id="52825-135">Dans le volet de résultats, sélectionnez **&frankly**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="52825-135">In the results panel, select **&frankly**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="52825-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="52825-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="52825-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec &frankly, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="52825-138">In this section, you configure and test Azure AD single sign-on with &frankly based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="52825-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur &frankly correspondant dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="52825-139">For single sign-on to work, Azure AD needs to know what the counterpart user in &frankly is to a user in Azure AD.</span></span> <span data-ttu-id="52825-140">En d’autres termes, une relation entre un utilisateur Azure AD et l’utilisateur &frankly correspondant doit être établie.</span><span class="sxs-lookup"><span data-stu-id="52825-140">In other words, a link relationship between an Azure AD user and the related user in &frankly needs to be established.</span></span>

<span data-ttu-id="52825-141">Dans &frankly, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="52825-141">In &frankly, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="52825-142">Pour configurer et tester l’authentification unique Azure AD avec &frankly, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="52825-142">To configure and test Azure AD single sign-on with &frankly, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="52825-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="52825-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="52825-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="52825-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="52825-145">**[Création d’un utilisateur de test &frankly](#creating-a-frankly-test-user)** pour avoir un équivalent de Britta Simon dans &frankly lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="52825-145">**[Creating a &frankly test user](#creating-a-frankly-test-user)** - to have a counterpart of Britta Simon in &frankly that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="52825-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="52825-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="52825-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="52825-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="52825-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="52825-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="52825-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application &frankly.</span><span class="sxs-lookup"><span data-stu-id="52825-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your &frankly application.</span></span>

<span data-ttu-id="52825-150">**Pour configurer l’authentification unique Azure AD avec &frankly, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="52825-150">**To configure Azure AD single sign-on with &frankly, perform the following steps:**</span></span>

1. <span data-ttu-id="52825-151">Dans le portail Azure, dans la page d’intégration de l’application **&frankly**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="52825-151">In the Azure portal, on the **&frankly** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="52825-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="52825-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_samlbase.png)

3. <span data-ttu-id="52825-155">Dans la section **Domaine et URL &frankly**, si vous souhaitez configurer l’application en mode démarré par le **fournisseur d’identité**, suivez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="52825-155">On the **&frankly Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_url.png)

    <span data-ttu-id="52825-157">a.</span><span class="sxs-lookup"><span data-stu-id="52825-157">a.</span></span> <span data-ttu-id="52825-158">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/metadata.php/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="52825-158">In the **Identifier** textbox, type a URL using the following pattern: `https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/metadata.php/<tenant id>`</span></span>

    <span data-ttu-id="52825-159">b.</span><span class="sxs-lookup"><span data-stu-id="52825-159">b.</span></span> <span data-ttu-id="52825-160">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/saml2-acs.php/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="52825-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/saml2-acs.php/<tenant id>`</span></span>

4. <span data-ttu-id="52825-161">Cliquez sur **Afficher les paramètres d’URL avancés**.</span><span class="sxs-lookup"><span data-stu-id="52825-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="52825-162">Si vous souhaitez configurer l’application en mode initié par le **fournisseur de service** :</span><span class="sxs-lookup"><span data-stu-id="52825-162">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_url1.png)

    <span data-ttu-id="52825-164">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://andfrankly.com/saml/okta/?saml_sso=<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="52825-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://andfrankly.com/saml/okta/?saml_sso=<tenant id>`</span></span>
    > [!NOTE] 
    > <span data-ttu-id="52825-165">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="52825-165">These values are not real.</span></span> <span data-ttu-id="52825-166">Mettez à jour ces valeurs avec l’identificateur, l’URL de connexion et l’URL de réponse réels.</span><span class="sxs-lookup"><span data-stu-id="52825-166">Update these values with the actual Identifier, Sign-on, and Reply URL.</span></span> <span data-ttu-id="52825-167">Pour obtenir ces valeurs, contactez [l’équipe du support &frankly](mailto:help@andfrankly.com).</span><span class="sxs-lookup"><span data-stu-id="52825-167">Contact [andfrankly support team](mailto:help@andfrankly.com) to get these values.</span></span>

5. <span data-ttu-id="52825-168">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="52825-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_certificate.png) 

6. <span data-ttu-id="52825-170">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="52825-170">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-andfrankly-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="52825-172">Pour configurer l’authentification unique du côté **&frankly**, vous devez envoyer le fichier **XML de métadonnées** téléchargé à [l’équipe du support &frankly](mailto:help@andfrankly.com).</span><span class="sxs-lookup"><span data-stu-id="52825-172">To configure single sign-on on **&frankly** side, you need to send the downloaded **Metadata XML** to [andfrankly support team](mailto:help@andfrankly.com).</span></span> 

> [!TIP]
> <span data-ttu-id="52825-173">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="52825-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="52825-174">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="52825-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="52825-175">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="52825-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="52825-176">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="52825-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="52825-177">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="52825-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="52825-179">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="52825-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="52825-180">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="52825-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="52825-182">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="52825-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="52825-184">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="52825-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="52825-186">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="52825-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="52825-188">a.</span><span class="sxs-lookup"><span data-stu-id="52825-188">a.</span></span> <span data-ttu-id="52825-189">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="52825-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="52825-190">b.</span><span class="sxs-lookup"><span data-stu-id="52825-190">b.</span></span> <span data-ttu-id="52825-191">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="52825-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="52825-192">c.</span><span class="sxs-lookup"><span data-stu-id="52825-192">c.</span></span> <span data-ttu-id="52825-193">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="52825-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="52825-194">d.</span><span class="sxs-lookup"><span data-stu-id="52825-194">d.</span></span> <span data-ttu-id="52825-195">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="52825-195">Click **Create**.</span></span>
 
### <a name="creating-a-frankly-test-user"></a><span data-ttu-id="52825-196">Création d’un utilisateur de test dans &frankly</span><span class="sxs-lookup"><span data-stu-id="52825-196">Creating a &frankly test user</span></span>

<span data-ttu-id="52825-197">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans &frankly.</span><span class="sxs-lookup"><span data-stu-id="52825-197">In this section, you create a user called Britta Simon in &frankly.</span></span> <span data-ttu-id="52825-198">Pour ajouter des utilisateurs dans la plateforme &frankly, contactez [l’équipe du support &frankly](mailto:help@andfrankly.com).</span><span class="sxs-lookup"><span data-stu-id="52825-198">Work with  [andfrankly support team](mailto:help@andfrankly.com) to add the users in the &frankly platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="52825-199">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="52825-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="52825-200">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à &frankly.</span><span class="sxs-lookup"><span data-stu-id="52825-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to &frankly.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="52825-202">**Pour affecter Britta Simon à &frankly, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="52825-202">**To assign Britta Simon to &frankly, perform the following steps:**</span></span>

1. <span data-ttu-id="52825-203">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="52825-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="52825-205">Dans la liste des applications, sélectionnez **&frankly**.</span><span class="sxs-lookup"><span data-stu-id="52825-205">In the applications list, select **&frankly**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_app.png) 

3. <span data-ttu-id="52825-207">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="52825-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="52825-209">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="52825-209">Click **Add** button.</span></span> <span data-ttu-id="52825-210">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="52825-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="52825-212">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="52825-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="52825-213">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="52825-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="52825-214">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="52825-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="52825-215">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="52825-215">Testing single sign-on</span></span>

<span data-ttu-id="52825-216">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="52825-216">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="52825-217">Le fait de cliquer sur la vignette &frankly dans le volet d’accès vous connecte automatiquement à votre application &frankly.</span><span class="sxs-lookup"><span data-stu-id="52825-217">When you click the &frankly tile in the Access Panel, you should get automatically signed-on to your &frankly application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="52825-218">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="52825-218">Additional resources</span></span>

* [<span data-ttu-id="52825-219">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="52825-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="52825-220">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="52825-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_203.png

