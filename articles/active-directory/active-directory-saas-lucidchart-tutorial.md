---
title: "Didacticiel : Intégration d’Azure Active Directory avec Lucidchart | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Lucidchart."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1068d364-11f3-43b5-bd6d-26f00ecd5baa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 2dea669f03c893632c08d30feeb3173efc2d8243
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lucidchart"></a><span data-ttu-id="6c7c6-103">Didacticiel : Intégration d’Azure Active Directory à Lucidchart</span><span class="sxs-lookup"><span data-stu-id="6c7c6-103">Tutorial: Azure Active Directory integration with Lucidchart</span></span>

<span data-ttu-id="6c7c6-104">Dans ce didacticiel, vous allez apprendre à intégrer Lucidchart à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6c7c6-104">In this tutorial, you learn how to integrate Lucidchart with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6c7c6-105">L’intégration d’Azure AD à Lucidchart offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="6c7c6-105">Integrating Lucidchart with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6c7c6-106">Dans Azure AD, vous pouvez contrôler qui a accès à Lucidchart.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-106">You can control in Azure AD who has access to Lucidchart</span></span>
- <span data-ttu-id="6c7c6-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Lucidchart (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-107">You can enable your users to automatically get signed-on to Lucidchart (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6c7c6-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="6c7c6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6c7c6-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6c7c6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6c7c6-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="6c7c6-110">Prerequisites</span></span>

<span data-ttu-id="6c7c6-111">Pour configurer l’intégration d’Azure AD à Lucidchart, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="6c7c6-111">To configure Azure AD integration with Lucidchart, you need the following items:</span></span>

- <span data-ttu-id="6c7c6-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="6c7c6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6c7c6-113">Un abonnement Lucidchart pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="6c7c6-113">A Lucidchart single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6c7c6-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6c7c6-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="6c7c6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6c7c6-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6c7c6-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6c7c6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6c7c6-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="6c7c6-118">Scenario description</span></span>
<span data-ttu-id="6c7c6-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6c7c6-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="6c7c6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6c7c6-121">Ajout de Lucidchart à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="6c7c6-121">Adding Lucidchart from the gallery</span></span>
2. <span data-ttu-id="6c7c6-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="6c7c6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lucidchart-from-the-gallery"></a><span data-ttu-id="6c7c6-123">Ajout de Lucidchart à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="6c7c6-123">Adding Lucidchart from the gallery</span></span>
<span data-ttu-id="6c7c6-124">Pour configurer l’intégration de Lucidchart à Azure AD, vous devez ajouter Lucidchart à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-124">To configure the integration of Lucidchart into Azure AD, you need to add Lucidchart from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6c7c6-125">**Pour ajouter Lucidchart à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6c7c6-125">**To add Lucidchart from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6c7c6-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6c7c6-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6c7c6-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="6c7c6-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="6c7c6-133">Dans la zone de recherche, tapez **Lucidchart**.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-133">In the search box, type **Lucidchart**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_search.png)

5. <span data-ttu-id="6c7c6-135">Dans le panneau de résultats, sélectionnez **Lucidchart**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-135">In the results panel, select **Lucidchart**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6c7c6-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="6c7c6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6c7c6-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Lucidchart à l’aide d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="6c7c6-138">In this section, you configure and test Azure AD single sign-on with Lucidchart based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6c7c6-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Lucidchart équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Lucidchart is to a user in Azure AD.</span></span> <span data-ttu-id="6c7c6-140">En d’autres termes, une relation entre un utilisateur Azure AD et l’utilisateur Lucidchart associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-140">In other words, a link relationship between an Azure AD user and the related user in Lucidchart needs to be established.</span></span>

<span data-ttu-id="6c7c6-141">Dans Lucidchart, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-141">In Lucidchart, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6c7c6-142">Pour configurer et tester l’authentification unique Azure AD avec Lucidchart, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="6c7c6-142">To configure and test Azure AD single sign-on with Lucidchart, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6c7c6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6c7c6-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6c7c6-145">**[Création d’un utilisateur de test Lucidchart](#creating-a-lucidchart-test-user)** pour avoir un équivalent de Britta Simon dans Lucidchart lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-145">**[Creating a Lucidchart test user](#creating-a-lucidchart-test-user)** - to have a counterpart of Britta Simon in Lucidchart that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6c7c6-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6c7c6-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6c7c6-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="6c7c6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6c7c6-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Lucidchart.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Lucidchart application.</span></span>

<span data-ttu-id="6c7c6-150">**Pour configurer l’authentification unique Azure AD avec Lucidchart, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6c7c6-150">**To configure Azure AD single sign-on with Lucidchart, perform the following steps:**</span></span>

1. <span data-ttu-id="6c7c6-151">Dans le portail Azure, sur la page d’intégration de l’application **Lucidchart**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-151">In the Azure portal, on the **Lucidchart** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="6c7c6-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_samlbase.png)

3. <span data-ttu-id="6c7c6-155">Dans la section **Lucidchart Domain and URLs** (Domaine et URL Lucidchart), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="6c7c6-155">On the **Lucidchart Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_url.png)

    <span data-ttu-id="6c7c6-157">Dans la zone de texte **URL d’authentification**, tapez l’URL : `https://chart2.office.lucidchart.com/saml/sso/azure`</span><span class="sxs-lookup"><span data-stu-id="6c7c6-157">In the **Sign-on URL** textbox, type a URL as: `https://chart2.office.lucidchart.com/saml/sso/azure`</span></span>

4. <span data-ttu-id="6c7c6-158">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-158">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_certificate.png) 

5. <span data-ttu-id="6c7c6-160">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="6c7c6-160">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lucidchart-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6c7c6-162">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Lucidchart en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-162">In a different web browser window, log into your Lucidchart company site as an administrator.</span></span>

7. <span data-ttu-id="6c7c6-163">Dans le menu situé en haut, cliquez sur **Team**.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-163">In the menu on the top, click **Team**.</span></span>
   
    <span data-ttu-id="6c7c6-164">![Équipe](./media/active-directory-saas-lucidchart-tutorial/ic791190.png "Équipe")</span><span class="sxs-lookup"><span data-stu-id="6c7c6-164">![Team](./media/active-directory-saas-lucidchart-tutorial/ic791190.png "Team")</span></span>

8. <span data-ttu-id="6c7c6-165">Cliquez sur **Applications \> Gérer SAML**.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-165">Click **Applications \> Manage SAML**.</span></span>
   
    <span data-ttu-id="6c7c6-166">![Gérer SAML](./media/active-directory-saas-lucidchart-tutorial/ic791191.png "Gérer SAML")</span><span class="sxs-lookup"><span data-stu-id="6c7c6-166">![Manage SAML](./media/active-directory-saas-lucidchart-tutorial/ic791191.png "Manage SAML")</span></span>

9. <span data-ttu-id="6c7c6-167">Dans la boîte de dialogue **SAML Authentication Settings** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="6c7c6-167">On the **SAML Authentication Settings** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="6c7c6-168">a.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-168">a.</span></span> <span data-ttu-id="6c7c6-169">Sélectionnez **Enable SAML Authentication**, puis cliquez sur **Optional**.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-169">Select **Enable SAML Authentication**, and then click **Optional**.</span></span>

    <span data-ttu-id="6c7c6-170">![Paramètres d’authentification SAML](./media/active-directory-saas-lucidchart-tutorial/ic791192.png "Paramètres d’authentification SAML")</span><span class="sxs-lookup"><span data-stu-id="6c7c6-170">![SAML Authentication Settings](./media/active-directory-saas-lucidchart-tutorial/ic791192.png "SAML Authentication Settings")</span></span>
 
    <span data-ttu-id="6c7c6-171">b.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-171">b.</span></span> <span data-ttu-id="6c7c6-172">Dans la zone de texte **Domain**, entrez votre domaine, puis cliquez sur **Change Certificate**.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-172">In the **Domain** textbox, type your domain, and then click **Change Certificate**.</span></span>

    <span data-ttu-id="6c7c6-173">![Modifier le certificat](./media/active-directory-saas-lucidchart-tutorial/ic791193.png "Modifier le certificat")</span><span class="sxs-lookup"><span data-stu-id="6c7c6-173">![Change Certificate](./media/active-directory-saas-lucidchart-tutorial/ic791193.png "Change Certificate")</span></span>
 
    <span data-ttu-id="6c7c6-174">c.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-174">c.</span></span> <span data-ttu-id="6c7c6-175">Ouvrez votre fichier de métadonnées téléchargé, copiez son contenu, puis collez-le dans la zone de texte **Upload Metadata** .</span><span class="sxs-lookup"><span data-stu-id="6c7c6-175">Open your downloaded metadata file, copy the content, and then paste it into the **Upload Metadata** textbox.</span></span>

    <span data-ttu-id="6c7c6-176">![Charger les métadonnées](./media/active-directory-saas-lucidchart-tutorial/ic791194.png "Charger les métadonnées")</span><span class="sxs-lookup"><span data-stu-id="6c7c6-176">![Upload Metadata](./media/active-directory-saas-lucidchart-tutorial/ic791194.png "Upload Metadata")</span></span>
 
    <span data-ttu-id="6c7c6-177">d.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-177">d.</span></span> <span data-ttu-id="6c7c6-178">Sélectionnez **Automatically Add new user to the team** (Ajouter automatiquement un utilisateur à l’équipe), puis cliquez sur **Enregistrer les modifications**.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-178">Select **Automatically Add new users to the team**, and then click **Save changes**.</span></span>

    <span data-ttu-id="6c7c6-179">![Enregistrer les modifications](./media/active-directory-saas-lucidchart-tutorial/ic791195.png "Enregistrer les modifications")</span><span class="sxs-lookup"><span data-stu-id="6c7c6-179">![Save Changes](./media/active-directory-saas-lucidchart-tutorial/ic791195.png "Save Changes")</span></span>

> [!TIP]
> <span data-ttu-id="6c7c6-180">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6c7c6-181">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6c7c6-182">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6c7c6-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6c7c6-183">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="6c7c6-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="6c7c6-184">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="6c7c6-186">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6c7c6-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6c7c6-187">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-187">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6c7c6-189">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-189">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6c7c6-191">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-191">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6c7c6-193">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="6c7c6-193">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6c7c6-195">a.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-195">a.</span></span> <span data-ttu-id="6c7c6-196">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-196">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6c7c6-197">b.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-197">b.</span></span> <span data-ttu-id="6c7c6-198">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-198">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6c7c6-199">c.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-199">c.</span></span> <span data-ttu-id="6c7c6-200">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-200">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6c7c6-201">d.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-201">d.</span></span> <span data-ttu-id="6c7c6-202">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-202">Click **Create**.</span></span>
 
### <a name="creating-a-lucidchart-test-user"></a><span data-ttu-id="6c7c6-203">Création d’un utilisateur de test Lucidchart</span><span class="sxs-lookup"><span data-stu-id="6c7c6-203">Creating a Lucidchart test user</span></span>

<span data-ttu-id="6c7c6-204">Aucun élément d’action ne vous permet de configurer l’approvisionnement des utilisateurs dans Lucidchart.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-204">There is no action item for you to configure user provisioning to Lucidchart.</span></span>  <span data-ttu-id="6c7c6-205">Lorsqu’un utilisateur tente de se connecter à Lucidchart à l’aide du panneau d’accès, Lucidchart vérifie si cet utilisateur existe.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-205">When an assigned user tries to log into Lucidchart using the access panel, Lucidchart checks whether the user exists.</span></span>  

<span data-ttu-id="6c7c6-206">Si aucun compte d’utilisateur n’est disponible, Lucidchart le crée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-206">If there is no user account available yet, it is automatically created by Lucidchart.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6c7c6-207">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="6c7c6-207">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6c7c6-208">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Lucidchart.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Lucidchart.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="6c7c6-210">**Pour affecter Britta Simon à Lucidchart, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6c7c6-210">**To assign Britta Simon to Lucidchart, perform the following steps:**</span></span>

1. <span data-ttu-id="6c7c6-211">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="6c7c6-213">Dans la liste des applications, sélectionnez **Lucidchart**.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-213">In the applications list, select **Lucidchart**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_app.png) 

3. <span data-ttu-id="6c7c6-215">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-215">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="6c7c6-217">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-217">Click **Add** button.</span></span> <span data-ttu-id="6c7c6-218">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="6c7c6-220">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6c7c6-221">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6c7c6-222">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6c7c6-223">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="6c7c6-223">Testing single sign-on</span></span>

<span data-ttu-id="6c7c6-224">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-224">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6c7c6-225">Lorsque vous cliquez sur la vignette Lucidchart dans le panneau d’accès, vous devez être connecté automatiquement à votre application Lucidchart.</span><span class="sxs-lookup"><span data-stu-id="6c7c6-225">When you click the Lucidchart tile in the Access Panel, you should get automatically signed-on to your Lucidchart application.</span></span>
<span data-ttu-id="6c7c6-226">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6c7c6-226">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6c7c6-227">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="6c7c6-227">Additional resources</span></span>

* [<span data-ttu-id="6c7c6-228">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6c7c6-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6c7c6-229">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="6c7c6-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_203.png

