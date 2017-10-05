---
title: "Didacticiel : Intégration d’Azure Active Directory avec Expensify | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Expensify."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1e761484-7a2f-4321-91f4-6d5d0b69344e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: jeedes
ms.openlocfilehash: e45576fd92706881121469ccd82150b3d48059cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-expensify"></a><span data-ttu-id="1b14b-103">Didacticiel : Intégration d’Azure Active Directory avec Expensify</span><span class="sxs-lookup"><span data-stu-id="1b14b-103">Tutorial: Azure Active Directory integration with Expensify</span></span>

<span data-ttu-id="1b14b-104">Dans ce didacticiel, vous allez apprendre à intégrer Expensify avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1b14b-104">In this tutorial, you learn how to integrate Expensify with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1b14b-105">L’intégration d’Expensify avec Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="1b14b-105">Integrating Expensify with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1b14b-106">Dans Azure AD, vous pouvez contrôler qui a accès à Expensify.</span><span class="sxs-lookup"><span data-stu-id="1b14b-106">You can control in Azure AD who has access to Expensify</span></span>
- <span data-ttu-id="1b14b-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Expensify (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1b14b-107">You can enable your users to automatically get signed-on to Expensify (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1b14b-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="1b14b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1b14b-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1b14b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b14b-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1b14b-110">Prerequisites</span></span>

<span data-ttu-id="1b14b-111">Pour configurer l’intégration d’Azure AD avec Expensify, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="1b14b-111">To configure Azure AD integration with Expensify, you need the following items:</span></span>

- <span data-ttu-id="1b14b-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="1b14b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1b14b-113">Un abonnement Expensify pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="1b14b-113">An Expensify single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1b14b-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="1b14b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1b14b-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1b14b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1b14b-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="1b14b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1b14b-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1b14b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1b14b-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="1b14b-118">Scenario description</span></span>
<span data-ttu-id="1b14b-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="1b14b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1b14b-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="1b14b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1b14b-121">Ajout d’Expensify à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="1b14b-121">Adding Expensify from the gallery</span></span>
2. <span data-ttu-id="1b14b-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1b14b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-expensify-from-the-gallery"></a><span data-ttu-id="1b14b-123">Ajout d’Expensify à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="1b14b-123">Adding Expensify from the gallery</span></span>
<span data-ttu-id="1b14b-124">Pour configurer l’intégration de Expensify à Azure AD, vous devez ajouter Expensify à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="1b14b-124">To configure the integration of Expensify into Azure AD, you need to add Expensify from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1b14b-125">**Pour ajouter Expensify à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1b14b-125">**To add Expensify from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1b14b-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1b14b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1b14b-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="1b14b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1b14b-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1b14b-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="1b14b-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1b14b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="1b14b-133">Dans la zone de recherche, tapez **Expensify**.</span><span class="sxs-lookup"><span data-stu-id="1b14b-133">In the search box, type **Expensify**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_search.png)

5. <span data-ttu-id="1b14b-135">Dans le panneau de résultats, sélectionnez **Expensify**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="1b14b-135">In the results panel, select **Expensify**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1b14b-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1b14b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1b14b-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Expensify avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="1b14b-138">In this section, you configure and test Azure AD single sign-on with Expensify based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1b14b-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Expensify équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1b14b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Expensify is to a user in Azure AD.</span></span> <span data-ttu-id="1b14b-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Expensify associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="1b14b-140">In other words, a link relationship between an Azure AD user and the related user in Expensify needs to be established.</span></span>

<span data-ttu-id="1b14b-141">Dans Expensify, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="1b14b-141">In Expensify, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1b14b-142">Pour configurer et tester l’authentification unique Azure AD avec Expensify, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="1b14b-142">To configure and test Azure AD single sign-on with Expensify, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1b14b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="1b14b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1b14b-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1b14b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1b14b-145">**[Création d’un utilisateur de test Expensify](#creating-an-expensify-test-user)** pour avoir un équivalent de Britta Simon dans Expensify lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1b14b-145">**[Creating an Expensify test user](#creating-an-expensify-test-user)** - to have a counterpart of Britta Simon in Expensify that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1b14b-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1b14b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1b14b-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="1b14b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1b14b-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1b14b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1b14b-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Expensify.</span><span class="sxs-lookup"><span data-stu-id="1b14b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Expensify application.</span></span>

<span data-ttu-id="1b14b-150">**Pour configurer l’authentification unique Azure AD avec Expensify, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1b14b-150">**To configure Azure AD single sign-on with Expensify, perform the following steps:**</span></span>

1. <span data-ttu-id="1b14b-151">Dans le portail Azure, sur la page d’intégration de l’application **Expensify**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="1b14b-151">In the Azure portal, on the **Expensify** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="1b14b-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="1b14b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_samlbase.png)

3. <span data-ttu-id="1b14b-155">Dans la section **Expensify Domain and URLs** (Domaine et URL Expensify), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1b14b-155">On the **Expensify Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_url.png)

    <span data-ttu-id="1b14b-157">a.</span><span class="sxs-lookup"><span data-stu-id="1b14b-157">a.</span></span> <span data-ttu-id="1b14b-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://www.expensify.com/authentication/saml/login`</span><span class="sxs-lookup"><span data-stu-id="1b14b-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.expensify.com/authentication/saml/login`</span></span>

    <span data-ttu-id="1b14b-159">b.</span><span class="sxs-lookup"><span data-stu-id="1b14b-159">b.</span></span> <span data-ttu-id="1b14b-160">Dans la zone de texte **Identifier URL** (URL d’identificateur), tapez une URL au format suivant : `https://www.<companyname>.expensify.com/`</span><span class="sxs-lookup"><span data-stu-id="1b14b-160">In the **Identifier URL** textbox, type a URL using the following pattern: `https://www.<companyname>.expensify.com/`</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="1b14b-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="1b14b-161">These values are not real.</span></span> <span data-ttu-id="1b14b-162">Mettez à jour ces valeurs avec l’URL de connexion et l’URL d’identificateur réelles.</span><span class="sxs-lookup"><span data-stu-id="1b14b-162">Update these values with the actual Sign-On URL and Identifier URL.</span></span> <span data-ttu-id="1b14b-163">Pour obtenir ces valeurs, contactez [l’équipe de support technique Expensify](mailto:help@expensify.com).</span><span class="sxs-lookup"><span data-stu-id="1b14b-163">Contact [Expensify Client support team](mailto:help@expensify.com) to get these values.</span></span> 
 
4. <span data-ttu-id="1b14b-164">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="1b14b-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_certificate.png) 

5. <span data-ttu-id="1b14b-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="1b14b-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-expensify-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1b14b-168">Pour activer l’authentification unique dans Expensify, vous devez d’abord activer le **contrôle de domaine** dans l’application.</span><span class="sxs-lookup"><span data-stu-id="1b14b-168">To enable SSO in Expensify, you first need to enable **Domain Control** in the application.</span></span> <span data-ttu-id="1b14b-169">Vous pouvez activer le contrôle de domaine dans l’application via la procédure répertoriée [ici](http://help.expensify.com/domain-control).</span><span class="sxs-lookup"><span data-stu-id="1b14b-169">You can enable Domain Control in the application through the steps listed [here](http://help.expensify.com/domain-control).</span></span> <span data-ttu-id="1b14b-170">Pour une assistance supplémentaire, travaillez avec [l’équipe de support technique Expensify](mailto:help@expensify.com).</span><span class="sxs-lookup"><span data-stu-id="1b14b-170">For additional support, work with [Expensify Client support team](mailto:help@expensify.com).</span></span> <span data-ttu-id="1b14b-171">Une fois que le contrôle de domaine est activé, suivez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1b14b-171">Once you have Domain Control enabled, follow these steps:</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_51.png)
    
    <span data-ttu-id="1b14b-173">a.</span><span class="sxs-lookup"><span data-stu-id="1b14b-173">a.</span></span> <span data-ttu-id="1b14b-174">Connectez-vous à votre application Expensify.</span><span class="sxs-lookup"><span data-stu-id="1b14b-174">Sign on to your Expensify application.</span></span>
    
    <span data-ttu-id="1b14b-175">b.</span><span class="sxs-lookup"><span data-stu-id="1b14b-175">b.</span></span> <span data-ttu-id="1b14b-176">Dans la barre d’outils située en haut, cliquez sur **Admin**.</span><span class="sxs-lookup"><span data-stu-id="1b14b-176">In the toolbar on the top, click **Admin**.</span></span>
    
    <span data-ttu-id="1b14b-177">c.</span><span class="sxs-lookup"><span data-stu-id="1b14b-177">c.</span></span> <span data-ttu-id="1b14b-178">Cliquez sur **Domaine**dans le panneau de gauche.</span><span class="sxs-lookup"><span data-stu-id="1b14b-178">In the left panel, click **Domain**.</span></span>
    
    <span data-ttu-id="1b14b-179">d.</span><span class="sxs-lookup"><span data-stu-id="1b14b-179">d.</span></span> <span data-ttu-id="1b14b-180">Cliquez sur le nom de votre domaine vérifié.</span><span class="sxs-lookup"><span data-stu-id="1b14b-180">Click your verified domain name.</span></span>
    
    <span data-ttu-id="1b14b-181">e.</span><span class="sxs-lookup"><span data-stu-id="1b14b-181">e.</span></span> <span data-ttu-id="1b14b-182">Dans le volet de gauche, cliquez sur **SAML**, puis sur **Activé**.</span><span class="sxs-lookup"><span data-stu-id="1b14b-182">In the left panel, click **SAML**, and then select **Enabled**.</span></span>
    
    <span data-ttu-id="1b14b-183">f.</span><span class="sxs-lookup"><span data-stu-id="1b14b-183">f.</span></span> <span data-ttu-id="1b14b-184">Dans le Bloc-notes, ouvrez les métadonnées de fédération téléchargées à partir d’Azure AD, copiez le contenu et collez-le dans la zone de texte **Identity Provider Metadata** (Métadonnées du fournisseur d’identité).</span><span class="sxs-lookup"><span data-stu-id="1b14b-184">Open the downloaded Federation Metadata from Azure AD in notepad, copy the content, and then paste it into the **Identity Provider Metadata** textbox.</span></span>

> [!TIP]
> <span data-ttu-id="1b14b-185">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="1b14b-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1b14b-186">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="1b14b-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1b14b-187">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1b14b-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1b14b-188">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="1b14b-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="1b14b-189">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1b14b-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="1b14b-191">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1b14b-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1b14b-192">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1b14b-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-expensify-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1b14b-194">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="1b14b-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-expensify-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1b14b-196">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1b14b-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-expensify-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1b14b-198">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1b14b-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-expensify-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1b14b-200">a.</span><span class="sxs-lookup"><span data-stu-id="1b14b-200">a.</span></span> <span data-ttu-id="1b14b-201">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1b14b-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1b14b-202">b.</span><span class="sxs-lookup"><span data-stu-id="1b14b-202">b.</span></span> <span data-ttu-id="1b14b-203">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1b14b-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1b14b-204">c.</span><span class="sxs-lookup"><span data-stu-id="1b14b-204">c.</span></span> <span data-ttu-id="1b14b-205">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="1b14b-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1b14b-206">d.</span><span class="sxs-lookup"><span data-stu-id="1b14b-206">d.</span></span> <span data-ttu-id="1b14b-207">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="1b14b-207">Click **Create**.</span></span>
 
### <a name="creating-an-expensify-test-user"></a><span data-ttu-id="1b14b-208">Création d’un utilisateur test Expensify</span><span class="sxs-lookup"><span data-stu-id="1b14b-208">Creating an Expensify test user</span></span>

<span data-ttu-id="1b14b-209">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Expensify.</span><span class="sxs-lookup"><span data-stu-id="1b14b-209">In this section, you create a user called Britta Simon in Expensify.</span></span> <span data-ttu-id="1b14b-210">Travaillez avec [l’équipe de support technique Expensify](mailto:help@expensify.com) pour ajouter les utilisateurs à la plateforme Expensify.</span><span class="sxs-lookup"><span data-stu-id="1b14b-210">Work with [Expensify Client support team](mailto:help@expensify.com) to add the users in the Expensify platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1b14b-211">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="1b14b-211">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1b14b-212">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Expensify.</span><span class="sxs-lookup"><span data-stu-id="1b14b-212">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Expensify.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="1b14b-214">**Pour affecter Britta Simon à Expensify, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1b14b-214">**To assign Britta Simon to Expensify, perform the following steps:**</span></span>

1. <span data-ttu-id="1b14b-215">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1b14b-215">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="1b14b-217">Dans la liste des applications, sélectionnez **Expensify**.</span><span class="sxs-lookup"><span data-stu-id="1b14b-217">In the applications list, select **Expensify**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_app.png) 

3. <span data-ttu-id="1b14b-219">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1b14b-219">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="1b14b-221">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="1b14b-221">Click **Add** button.</span></span> <span data-ttu-id="1b14b-222">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="1b14b-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="1b14b-224">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="1b14b-224">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1b14b-225">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1b14b-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1b14b-226">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="1b14b-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1b14b-227">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="1b14b-227">Testing single sign-on</span></span>

<span data-ttu-id="1b14b-228">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="1b14b-228">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>  

<span data-ttu-id="1b14b-229">Lorsque vous cliquez sur la mosaïque Expensify dans le volet d’accès, vous devriez être connecté automatiquement à votre application Expensify.</span><span class="sxs-lookup"><span data-stu-id="1b14b-229">When you click the Expensify tile in the Access Panel, you should get automatically signed-on to your Expensify application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1b14b-230">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="1b14b-230">Additional resources</span></span>

* [<span data-ttu-id="1b14b-231">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1b14b-231">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1b14b-232">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="1b14b-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_203.png

