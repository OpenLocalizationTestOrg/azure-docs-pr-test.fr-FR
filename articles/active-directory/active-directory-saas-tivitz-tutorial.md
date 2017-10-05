---
title: "Didacticiel : Intégration d’Azure Active Directory à TiViTz | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et TiViTz."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b97ed88f-7888-4185-be22-41d1f62cbbf1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: b1b27918bb5fcff1d19f4711ea70fe46a5697933
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tivitz"></a><span data-ttu-id="9500b-103">Didacticiel : Intégration d’Azure AD avec TiViTz</span><span class="sxs-lookup"><span data-stu-id="9500b-103">Tutorial: Azure Active Directory integration with TiViTz</span></span>

<span data-ttu-id="9500b-104">Dans ce didacticiel, vous allez apprendre à intégrer TiViTz à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9500b-104">In this tutorial, you learn how to integrate TiViTz with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9500b-105">L’intégration de TiViTz dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="9500b-105">Integrating TiViTz with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9500b-106">Dans Azure AD, vous pouvez contrôler qui a accès à TiViTz</span><span class="sxs-lookup"><span data-stu-id="9500b-106">You can control in Azure AD who has access to TiViTz</span></span>
- <span data-ttu-id="9500b-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à TiViTz (via l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="9500b-107">You can enable your users to automatically get signed-on to TiViTz (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9500b-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="9500b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9500b-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9500b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9500b-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9500b-110">Prerequisites</span></span>

<span data-ttu-id="9500b-111">Pour configurer l’intégration d’Azure AD avec TiViTz, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="9500b-111">To configure Azure AD integration with TiViTz, you need the following items:</span></span>

- <span data-ttu-id="9500b-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="9500b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9500b-113">Un abonnement TiViTz pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="9500b-113">A TiViTz single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9500b-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="9500b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9500b-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="9500b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9500b-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="9500b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9500b-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9500b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9500b-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="9500b-118">Scenario description</span></span>
<span data-ttu-id="9500b-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="9500b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9500b-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="9500b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9500b-121">Ajout de TiViTz depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="9500b-121">Adding TiViTz from the gallery</span></span>
2. <span data-ttu-id="9500b-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9500b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tivitz-from-the-gallery"></a><span data-ttu-id="9500b-123">Ajout de TiViTz depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="9500b-123">Adding TiViTz from the gallery</span></span>
<span data-ttu-id="9500b-124">Pour configurer l’intégration de TiViTz avec Azure AD, vous devez ajouter TiViTz disponible à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="9500b-124">To configure the integration of TiViTz into Azure AD, you need to add TiViTz from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9500b-125">**Pour ajouter TiViTz à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9500b-125">**To add TiViTz from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9500b-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9500b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9500b-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="9500b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9500b-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="9500b-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="9500b-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="9500b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="9500b-133">Dans la zone de recherche, tapez **TiViTz**.</span><span class="sxs-lookup"><span data-stu-id="9500b-133">In the search box, type **TiViTz**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tivitz-tutorial/tutorial_tivitz_search.png)

5. <span data-ttu-id="9500b-135">Dans le volet de résultats, sélectionnez **TiViTz**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="9500b-135">In the results panel, select **TiViTz**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tivitz-tutorial/tutorial_tivitz_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9500b-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9500b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9500b-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec TiViTz avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="9500b-138">In this section, you configure and test Azure AD single sign-on with TiViTz based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9500b-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur TiViTz équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9500b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in TiViTz is to a user in Azure AD.</span></span> <span data-ttu-id="9500b-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur TiViTz associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="9500b-140">In other words, a link relationship between an Azure AD user and the related user in TiViTz needs to be established.</span></span>

<span data-ttu-id="9500b-141">Dans TiViTz, affectez la valeur du **nom d’utilisateur** indiquée dans Azure AD comme valeur de **Nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="9500b-141">In TiViTz, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9500b-142">Pour configurer et tester l’authentification unique Azure AD avec TiViTz, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="9500b-142">To configure and test Azure AD single sign-on with TiViTz, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9500b-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="9500b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9500b-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9500b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9500b-145">**[Création d’un utilisateur de test TiViTz](#creating-a-tivitz-test-user)** pour avoir un équivalent de Britta Simon dans TiViTz, lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="9500b-145">**[Creating a TiViTz test user](#creating-a-tivitz-test-user)** - to have a counterpart of Britta Simon in TiViTz that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9500b-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9500b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9500b-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="9500b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9500b-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9500b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9500b-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application TiViTz.</span><span class="sxs-lookup"><span data-stu-id="9500b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TiViTz application.</span></span>

<span data-ttu-id="9500b-150">**Pour configurer l’authentification unique Azure AD avec TiViTz, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9500b-150">**To configure Azure AD single sign-on with TiViTz, perform the following steps:**</span></span>

1. <span data-ttu-id="9500b-151">Dans le portail Azure, dans la page d’intégration de l’application **TiViTz**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="9500b-151">In the Azure portal, on the **TiViTz** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="9500b-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="9500b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-tivitz-tutorial/tutorial_tivitz_samlbase.png)

3. <span data-ttu-id="9500b-155">Dans la section **Domaine et URL TiViTz**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="9500b-155">On the **TiViTz Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-tivitz-tutorial/tutorial_tivitz_url.png)

    <span data-ttu-id="9500b-157">a.</span><span class="sxs-lookup"><span data-stu-id="9500b-157">a.</span></span> <span data-ttu-id="9500b-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<companyname>.o365.tivitz.com/`</span><span class="sxs-lookup"><span data-stu-id="9500b-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.o365.tivitz.com/`</span></span>

    <span data-ttu-id="9500b-159">b.</span><span class="sxs-lookup"><span data-stu-id="9500b-159">b.</span></span> <span data-ttu-id="9500b-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<companyname>.o365.tivitz.com/`</span><span class="sxs-lookup"><span data-stu-id="9500b-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.o365.tivitz.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9500b-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="9500b-161">These values are not real.</span></span> <span data-ttu-id="9500b-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="9500b-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="9500b-163">Pour obtenir ces valeurs, contactez l’[équipe de support technique TiViTz](mailto:info@tivitz.com).</span><span class="sxs-lookup"><span data-stu-id="9500b-163">Contact [TiViTz Client support team](mailto:info@tivitz.com) to get these values.</span></span> 

4. <span data-ttu-id="9500b-164">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="9500b-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-tivitz-tutorial/tutorial_tivitz_certificate.png) 

5. <span data-ttu-id="9500b-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="9500b-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-tivitz-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9500b-168">Pour configurer l’authentification unique côté **TiViTz**, vous devez envoyer le **XML de métadonnées** téléchargé à [l’équipe de support technique TiViTz](mailto:info@tivitz.com).</span><span class="sxs-lookup"><span data-stu-id="9500b-168">To configure single sign-on on **TiViTz** side, you need to send the downloaded **Metadata XML** to [TiViTz support team](mailto:info@tivitz.com).</span></span>

> [!TIP]
> <span data-ttu-id="9500b-169">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="9500b-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9500b-170">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="9500b-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9500b-171">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9500b-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9500b-172">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="9500b-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="9500b-173">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="9500b-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="9500b-175">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9500b-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9500b-176">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9500b-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tivitz-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9500b-178">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="9500b-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tivitz-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9500b-180">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="9500b-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tivitz-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9500b-182">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="9500b-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tivitz-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9500b-184">a.</span><span class="sxs-lookup"><span data-stu-id="9500b-184">a.</span></span> <span data-ttu-id="9500b-185">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9500b-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9500b-186">b.</span><span class="sxs-lookup"><span data-stu-id="9500b-186">b.</span></span> <span data-ttu-id="9500b-187">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9500b-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9500b-188">c.</span><span class="sxs-lookup"><span data-stu-id="9500b-188">c.</span></span> <span data-ttu-id="9500b-189">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="9500b-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9500b-190">d.</span><span class="sxs-lookup"><span data-stu-id="9500b-190">d.</span></span> <span data-ttu-id="9500b-191">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="9500b-191">Click **Create**.</span></span>
 
### <a name="creating-a-tivitz-test-user"></a><span data-ttu-id="9500b-192">Création d’un utilisateur de test TiViTz</span><span class="sxs-lookup"><span data-stu-id="9500b-192">Creating a TiViTz test user</span></span>

<span data-ttu-id="9500b-193">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans TiViTz.</span><span class="sxs-lookup"><span data-stu-id="9500b-193">The objective of this section is to create a user called Britta Simon in TiViTz.</span></span> <span data-ttu-id="9500b-194">TiViTz prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="9500b-194">TiViTz supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="9500b-195">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="9500b-195">There is no action item for you in this section.</span></span> <span data-ttu-id="9500b-196">Un utilisateur est créé lors d’une tentative d’accès à TiViTz s’il n’existe pas déjà.</span><span class="sxs-lookup"><span data-stu-id="9500b-196">A new user is created during an attempt to access TiViTz if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="9500b-197">Si vous devez créer un utilisateur manuellement, contactez l’équipe du support technique [TiViTz](mailto:info@tivitz.com).</span><span class="sxs-lookup"><span data-stu-id="9500b-197">If you need to create an user manually, you need to contact [TiViTz support team](mailto:info@tivitz.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9500b-198">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="9500b-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9500b-199">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à TiViTz.</span><span class="sxs-lookup"><span data-stu-id="9500b-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TiViTz.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="9500b-201">**Pour affecter Britta Simon à TiViTz, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9500b-201">**To assign Britta Simon to TiViTz, perform the following steps:**</span></span>

1. <span data-ttu-id="9500b-202">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="9500b-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="9500b-204">Dans la liste des applications, sélectionnez **TiViTz**.</span><span class="sxs-lookup"><span data-stu-id="9500b-204">In the applications list, select **TiViTz**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-tivitz-tutorial/tutorial_tivitz_app.png) 

3. <span data-ttu-id="9500b-206">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="9500b-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="9500b-208">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="9500b-208">Click **Add** button.</span></span> <span data-ttu-id="9500b-209">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="9500b-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="9500b-211">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="9500b-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9500b-212">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="9500b-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9500b-213">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="9500b-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9500b-214">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="9500b-214">Testing single sign-on</span></span>

<span data-ttu-id="9500b-215">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="9500b-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9500b-216">Lorsque vous cliquez sur la vignette TiViTz dans le volet d’accès, vous devez être connecté automatiquement à votre application TiViTz.</span><span class="sxs-lookup"><span data-stu-id="9500b-216">When you click the TiViTz tile in the Access Panel, you should get automatically signed-on to your TiViTz application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9500b-217">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="9500b-217">Additional resources</span></span>

* [<span data-ttu-id="9500b-218">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9500b-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9500b-219">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="9500b-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_203.png

