---
title: "Didacticiel : Intégration d’Azure Active Directory à Showpad | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Showpad."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 48b6bee0-dbc5-4863-964d-75b25e517741
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: c8b39c9215675d8073f896f934339e7cd55334cc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-showpad"></a><span data-ttu-id="587c0-103">Didacticiel : intégration d’Azure Active Directory à Showpad</span><span class="sxs-lookup"><span data-stu-id="587c0-103">Tutorial: Azure Active Directory integration with Showpad</span></span>

<span data-ttu-id="587c0-104">Dans ce didacticiel, vous allez apprendre à intégrer Showpad avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="587c0-104">In this tutorial, you learn how to integrate Showpad with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="587c0-105">L’intégration de Showpad dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="587c0-105">Integrating Showpad with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="587c0-106">Dans Azure AD, vous pouvez contrôler qui a accès à Showpad.</span><span class="sxs-lookup"><span data-stu-id="587c0-106">You can control in Azure AD who has access to Showpad</span></span>
- <span data-ttu-id="587c0-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Showpad (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="587c0-107">You can enable your users to automatically get signed-on to Showpad (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="587c0-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="587c0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="587c0-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="587c0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="587c0-110">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="587c0-110">Prerequisites</span></span>

<span data-ttu-id="587c0-111">Pour configurer l’intégration d’Azure AD à Showpad, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="587c0-111">To configure Azure AD integration with Showpad, you need the following items:</span></span>

- <span data-ttu-id="587c0-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="587c0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="587c0-113">Abonnement Showpad pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="587c0-113">A Showpad single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="587c0-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="587c0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="587c0-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="587c0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="587c0-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="587c0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="587c0-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="587c0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="587c0-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="587c0-118">Scenario description</span></span>
<span data-ttu-id="587c0-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="587c0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="587c0-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="587c0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="587c0-121">Ajout de Showpad à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="587c0-121">Adding Showpad from the gallery</span></span>
2. <span data-ttu-id="587c0-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="587c0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-showpad-from-the-gallery"></a><span data-ttu-id="587c0-123">Ajout de Showpad à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="587c0-123">Adding Showpad from the gallery</span></span>

<span data-ttu-id="587c0-124">Pour configurer l’intégration de Showpad à Azure AD, vous devez ajouter Showpad à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="587c0-124">To configure the integration of Showpad into Azure AD, you need to add Showpad from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="587c0-125">**Pour ajouter Showpad à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="587c0-125">**To add Showpad from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="587c0-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="587c0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="587c0-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="587c0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="587c0-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="587c0-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="587c0-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="587c0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="587c0-133">Dans la zone de recherche, entrez **Showpad**.</span><span class="sxs-lookup"><span data-stu-id="587c0-133">In the search box, type **Showpad**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_search.png)

5. <span data-ttu-id="587c0-135">Dans le volet de résultats, sélectionnez **Showpad**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="587c0-135">In the results panel, select **Showpad**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="587c0-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="587c0-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="587c0-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Showpad sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="587c0-138">In this section, you configure and test Azure AD single sign-on with Showpad based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="587c0-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Showpad équivalent à l’utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="587c0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Showpad is to a user in Azure AD.</span></span> <span data-ttu-id="587c0-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Showpad associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="587c0-140">In other words, a link relationship between an Azure AD user and the related user in Showpad needs to be established.</span></span>

<span data-ttu-id="587c0-141">Dans Showpad, assignez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation de lien.</span><span class="sxs-lookup"><span data-stu-id="587c0-141">In Showpad, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="587c0-142">Pour configurer et tester l’authentification unique Azure AD avec Showpad, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="587c0-142">To configure and test Azure AD single sign-on with Showpad, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="587c0-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="587c0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="587c0-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="587c0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="587c0-145">**[Création d’un utilisateur de test Showpad](#creating-a-showpad-test-user)** - pour avoir un équivalent de Britta Simon dans Showpad lié à sa représentation dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="587c0-145">**[Creating a Showpad test user](#creating-a-showpad-test-user)** - to have a counterpart of Britta Simon in Showpad that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="587c0-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="587c0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="587c0-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="587c0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="587c0-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="587c0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="587c0-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Showpad.</span><span class="sxs-lookup"><span data-stu-id="587c0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Showpad application.</span></span>

<span data-ttu-id="587c0-150">**Pour configurer l’authentification unique Azure AD avec Showpad, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="587c0-150">**To configure Azure AD single sign-on with Showpad, perform the following steps:**</span></span>

1. <span data-ttu-id="587c0-151">Dans le portail Azure, sur la page d’intégration de l’application **Showpad**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="587c0-151">In the Azure portal, on the **Showpad** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="587c0-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="587c0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_samlbase.png)

3. <span data-ttu-id="587c0-155">Dans la section **Domaine et URL Showpad**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="587c0-155">On the **Showpad Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_url.png)

    <span data-ttu-id="587c0-157">a.</span><span class="sxs-lookup"><span data-stu-id="587c0-157">a.</span></span> <span data-ttu-id="587c0-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<comapany-name>.showpad.biz/login`</span><span class="sxs-lookup"><span data-stu-id="587c0-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<comapany-name>.showpad.biz/login`</span></span>

    <span data-ttu-id="587c0-159">b.</span><span class="sxs-lookup"><span data-stu-id="587c0-159">b.</span></span> <span data-ttu-id="587c0-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<company-name>.showpad.biz`</span><span class="sxs-lookup"><span data-stu-id="587c0-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company-name>.showpad.biz`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="587c0-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="587c0-161">These values are not real.</span></span> <span data-ttu-id="587c0-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="587c0-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="587c0-163">Pour obtenir ces valeurs, contactez [l’équipe de support technique Showpad](https://help.showpad.com).</span><span class="sxs-lookup"><span data-stu-id="587c0-163">Contact [Showpad support team](https://help.showpad.com) to get these values.</span></span> 
 


4. <span data-ttu-id="587c0-164">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="587c0-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_certificate.png) 

5. <span data-ttu-id="587c0-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="587c0-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-showpad-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="587c0-168">Connectez-vous à votre client Showpad en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="587c0-168">Sign-on to your Showpad tenant as an administrator.</span></span>

7. <span data-ttu-id="587c0-169">Dans le menu situé en haut, cliquez sur **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="587c0-169">In the menu on the top, click the **Settings**.</span></span>
   
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_001.png) 

8. <span data-ttu-id="587c0-171">Accédez à **Authentification unique** et cliquez sur **Activer**.</span><span class="sxs-lookup"><span data-stu-id="587c0-171">Navigate to "**Single Sign-On**" and click "**Enable**."</span></span>
   
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_002.png)

9. <span data-ttu-id="587c0-173">Dans la boîte de dialogue **Add a SAML 2.0 Service** (Ajouter un service SAML 2.0), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="587c0-173">On the **Add a SAML 2.0 Service** dialog, perform the following steps:</span></span>
   
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_003.png) 
   
    <span data-ttu-id="587c0-175">a.</span><span class="sxs-lookup"><span data-stu-id="587c0-175">a.</span></span> <span data-ttu-id="587c0-176">Dans la zone de texte **Nom**, entrez le nom du fournisseur d’identificateurs (par exemple : le nom de votre entreprise).</span><span class="sxs-lookup"><span data-stu-id="587c0-176">In the **Name** textbox, type the name of Identifier Provider (for example: your company name).</span></span>
   
    <span data-ttu-id="587c0-177">b.</span><span class="sxs-lookup"><span data-stu-id="587c0-177">b.</span></span> <span data-ttu-id="587c0-178">Dans **Source des métadonnées**, sélectionnez **XML**.</span><span class="sxs-lookup"><span data-stu-id="587c0-178">As **Metadata Source**, select **XML**.</span></span>
   
    <span data-ttu-id="587c0-179">c.</span><span class="sxs-lookup"><span data-stu-id="587c0-179">c.</span></span> <span data-ttu-id="587c0-180">Copiez le contenu du fichier XML de métadonnées téléchargé à partir du portail Azure, puis collez-le dans la zone de texte **XML de métadonnées**.</span><span class="sxs-lookup"><span data-stu-id="587c0-180">Copy the content of metadata XML file, which you have downloaded from the Azure portal, and then paste it into the **Metadata XML** textbox.</span></span>
   
    <span data-ttu-id="587c0-181">d.</span><span class="sxs-lookup"><span data-stu-id="587c0-181">d.</span></span> <span data-ttu-id="587c0-182">Sélectionnez **Auto-provision accounts for new users when they log in**(Configurer automatiquement les comptes des nouveaux utilisateurs au moment de la connexion).</span><span class="sxs-lookup"><span data-stu-id="587c0-182">Select **Auto-provision accounts for new users when they log in**.</span></span>
   
    <span data-ttu-id="587c0-183">e.</span><span class="sxs-lookup"><span data-stu-id="587c0-183">e.</span></span> <span data-ttu-id="587c0-184">Cliquez sur **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="587c0-184">Click **Submit**.</span></span>

> [!TIP]
> <span data-ttu-id="587c0-185">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="587c0-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="587c0-186">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="587c0-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="587c0-187">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="587c0-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="587c0-188">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="587c0-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="587c0-189">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="587c0-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="587c0-191">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="587c0-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="587c0-192">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="587c0-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-showpad-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="587c0-194">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="587c0-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-showpad-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="587c0-196">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="587c0-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-showpad-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="587c0-198">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="587c0-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-showpad-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="587c0-200">a.</span><span class="sxs-lookup"><span data-stu-id="587c0-200">a.</span></span> <span data-ttu-id="587c0-201">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="587c0-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="587c0-202">b.</span><span class="sxs-lookup"><span data-stu-id="587c0-202">b.</span></span> <span data-ttu-id="587c0-203">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="587c0-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="587c0-204">c.</span><span class="sxs-lookup"><span data-stu-id="587c0-204">c.</span></span> <span data-ttu-id="587c0-205">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="587c0-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="587c0-206">d.</span><span class="sxs-lookup"><span data-stu-id="587c0-206">d.</span></span> <span data-ttu-id="587c0-207">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="587c0-207">Click **Create**.</span></span>
 
### <a name="creating-a-showpad-test-user"></a><span data-ttu-id="587c0-208">Création d’un utilisateur de test Showpad</span><span class="sxs-lookup"><span data-stu-id="587c0-208">Creating a Showpad test user</span></span>

<span data-ttu-id="587c0-209">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans Showpad.</span><span class="sxs-lookup"><span data-stu-id="587c0-209">The objective of this section is to create a user called Britta Simon in Showpad.</span></span> 

<span data-ttu-id="587c0-210">Showpad prend en charge l’approvisionnement juste-à-temps.</span><span class="sxs-lookup"><span data-stu-id="587c0-210">Showpad supports just-in-time provisioning.</span></span> <span data-ttu-id="587c0-211">Vous l’avez déjà activé dans **[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)**.</span><span class="sxs-lookup"><span data-stu-id="587c0-211">You have enabled provisioning in **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**.</span></span> 

<span data-ttu-id="587c0-212">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="587c0-212">There is no action item for you in this section.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="587c0-213">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="587c0-213">Assigning the Azure AD test user</span></span>

<span data-ttu-id="587c0-214">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Showpad.</span><span class="sxs-lookup"><span data-stu-id="587c0-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Showpad.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="587c0-216">**Pour affecter Britta Simon à Showpad, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="587c0-216">**To assign Britta Simon to Showpad, perform the following steps:**</span></span>

1. <span data-ttu-id="587c0-217">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="587c0-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="587c0-219">Dans la liste des applications, sélectionnez **Showpad**.</span><span class="sxs-lookup"><span data-stu-id="587c0-219">In the applications list, select **Showpad**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_app.png) 

3. <span data-ttu-id="587c0-221">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="587c0-221">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="587c0-223">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="587c0-223">Click **Add** button.</span></span> <span data-ttu-id="587c0-224">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="587c0-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="587c0-226">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="587c0-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="587c0-227">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="587c0-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="587c0-228">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="587c0-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="587c0-229">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="587c0-229">Testing single sign-on</span></span>

<span data-ttu-id="587c0-230">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="587c0-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="587c0-231">Lorsque vous cliquez sur la vignette Showpad dans le volet d’accès, vous devez être connecté automatiquement à l’application Showpad.</span><span class="sxs-lookup"><span data-stu-id="587c0-231">When you click the Showpad tile in the Access Panel, you should get automatically signed-on to Showpad application.</span></span>
<span data-ttu-id="587c0-232">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="587c0-232">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="587c0-233">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="587c0-233">Additional resources</span></span>

* [<span data-ttu-id="587c0-234">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="587c0-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="587c0-235">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="587c0-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_203.png

