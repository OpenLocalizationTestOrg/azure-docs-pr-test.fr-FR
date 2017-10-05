---
title: "Didacticiel : Intégration d’Azure Active Directory à New Relic | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et New Relic."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3186b9a8-f4d8-45e2-ad82-6275f95e7aa6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: 605e85c23a849f70fcc0237361d7a891f716ca3a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-new-relic"></a><span data-ttu-id="fd8ee-103">Didacticiel : Intégration d’Azure Active Directory à New Relic</span><span class="sxs-lookup"><span data-stu-id="fd8ee-103">Tutorial: Azure Active Directory integration with New Relic</span></span>

<span data-ttu-id="fd8ee-104">Dans ce didacticiel, vous allez apprendre à intégrer New Relic à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fd8ee-104">In this tutorial, you learn how to integrate New Relic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fd8ee-105">L’intégration de New Relic dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="fd8ee-105">Integrating New Relic with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="fd8ee-106">Dans Azure AD, vous pouvez contrôler qui a accès à New Relic.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-106">You can control in Azure AD who has access to New Relic</span></span>
- <span data-ttu-id="fd8ee-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à New Relic (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-107">You can enable your users to automatically get signed-on to New Relic (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fd8ee-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="fd8ee-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="fd8ee-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fd8ee-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fd8ee-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="fd8ee-110">Prerequisites</span></span>

<span data-ttu-id="fd8ee-111">Pour configurer l’intégration d’Azure AD à New Relic, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="fd8ee-111">To configure Azure AD integration with New Relic, you need the following items:</span></span>

- <span data-ttu-id="fd8ee-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd8ee-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fd8ee-113">Un abonnement New Relic pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="fd8ee-113">A New Relic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fd8ee-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fd8ee-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="fd8ee-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fd8ee-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fd8ee-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fd8ee-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fd8ee-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="fd8ee-118">Scenario description</span></span>
<span data-ttu-id="fd8ee-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fd8ee-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="fd8ee-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fd8ee-121">Ajout de New Relic depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="fd8ee-121">Adding New Relic from the gallery</span></span>
2. <span data-ttu-id="fd8ee-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd8ee-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-new-relic-from-the-gallery"></a><span data-ttu-id="fd8ee-123">Ajout de New Relic depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="fd8ee-123">Adding New Relic from the gallery</span></span>
<span data-ttu-id="fd8ee-124">Pour configurer l’intégration de New Relic à Azure AD, vous devez ajouter New Relic à votre liste d’applications SaaS gérées, à partir de la galerie.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-124">To configure the integration of New Relic into Azure AD, you need to add New Relic from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="fd8ee-125">**Pour ajouter New Relic à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="fd8ee-125">**To add New Relic from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="fd8ee-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fd8ee-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="fd8ee-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="fd8ee-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="fd8ee-133">Dans la zone de recherche, entrez **New Relic**.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-133">In the search box, type **New Relic**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_search.png)

5. <span data-ttu-id="fd8ee-135">Dans le panneau des résultats, sélectionnez **New Relic**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-135">In the results panel, select **New Relic**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fd8ee-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd8ee-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fd8ee-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec New Relic, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="fd8ee-138">In this section, you configure and test Azure AD single sign-on with New Relic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fd8ee-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur New Relic correspondant dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-139">For single sign-on to work, Azure AD needs to know what the counterpart user in New Relic is to a user in Azure AD.</span></span> <span data-ttu-id="fd8ee-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur New Relic associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-140">In other words, a link relationship between an Azure AD user and the related user in New Relic needs to be established.</span></span>

<span data-ttu-id="fd8ee-141">Dans New Relic, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-141">In New Relic, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="fd8ee-142">Pour configurer et tester l’authentification unique Azure AD avec New Relic, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="fd8ee-142">To configure and test Azure AD single sign-on with New Relic, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="fd8ee-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="fd8ee-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fd8ee-145">**[Création d’un utilisateur de test New Relic](#creating-a-new-relic-test-user)** pour obtenir un équivalent de Britta Simon dans New Relic lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-145">**[Creating a New Relic test user](#creating-a-new-relic-test-user)** - to have a counterpart of Britta Simon in New Relic that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="fd8ee-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fd8ee-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fd8ee-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd8ee-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fd8ee-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application New Relic.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your New Relic application.</span></span>

<span data-ttu-id="fd8ee-150">**Pour configurer l’authentification unique Azure AD avec New Relic, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="fd8ee-150">**To configure Azure AD single sign-on with New Relic, perform the following steps:**</span></span>

1. <span data-ttu-id="fd8ee-151">Dans le portail Azure, sur la page d’intégration de l’application **New Relic**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-151">In the Azure portal, on the **New Relic** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="fd8ee-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_samlbase.png)

3. <span data-ttu-id="fd8ee-155">Dans la section **Domaine et URL New Relic**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="fd8ee-155">On the **New Relic Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_url.png)

    <span data-ttu-id="fd8ee-157">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<subdomain>.newrelic.com`</span><span class="sxs-lookup"><span data-stu-id="fd8ee-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.newrelic.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fd8ee-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-158">The value is not real.</span></span> <span data-ttu-id="fd8ee-159">Mettez à jour la valeur avec l’URL de connexion réelle.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="fd8ee-160">Pour obtenir cette valeur, contactez l’[équipe du support technique de New Relic](https://support.newrelic.com/).</span><span class="sxs-lookup"><span data-stu-id="fd8ee-160">Contact [New Relic Client support team](https://support.newrelic.com/) to get the value.</span></span> 
 
4. <span data-ttu-id="fd8ee-161">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_certificate.png) 

5. <span data-ttu-id="fd8ee-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="fd8ee-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-new-relic-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fd8ee-165">Dans la section **Configuration de New Relic**, cliquez sur **Configurer New Relic** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-165">On the **New Relic Configuration** section, click **Configure New Relic** to open **Configure sign-on** window.</span></span> <span data-ttu-id="fd8ee-166">Copiez **l’URL de déconnexion et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-166">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_configure.png) 

7. <span data-ttu-id="fd8ee-168">Dans une autre fenêtre de navigateur web, connectez-vous au site de votre entreprise **New Relic** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-168">In a different web browser window, sign on to your **New Relic** company site as administrator.</span></span>

8. <span data-ttu-id="fd8ee-169">Dans le menu situé en haut, cliquez sur **Account Settings**.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-169">In the menu on the top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="fd8ee-170">![Paramètres de compte](./media/active-directory-saas-new-relic-tutorial/ic797036.png "Paramètres de compte")</span><span class="sxs-lookup"><span data-stu-id="fd8ee-170">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797036.png "Account Settings")</span></span>

9. <span data-ttu-id="fd8ee-171">Cliquez sur l’onglet **Security and authentication**, puis sur l’onglet **Single sign on**.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-171">Click the **Security and authentication** tab, and then click the **Single sign on** tab.</span></span>
   
    <span data-ttu-id="fd8ee-172">![Authentification unique](./media/active-directory-saas-new-relic-tutorial/ic797037.png "Authentification unique")</span><span class="sxs-lookup"><span data-stu-id="fd8ee-172">![Single Sign-On](./media/active-directory-saas-new-relic-tutorial/ic797037.png "Single Sign-On")</span></span>

10. <span data-ttu-id="fd8ee-173">Dans la page de boîte de dialogue SAML, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="fd8ee-173">On the SAML dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="fd8ee-174">![SAML](./media/active-directory-saas-new-relic-tutorial/ic797038.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="fd8ee-174">![SAML](./media/active-directory-saas-new-relic-tutorial/ic797038.png "SAML")</span></span>
   
   <span data-ttu-id="fd8ee-175">a.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-175">a.</span></span> <span data-ttu-id="fd8ee-176">Pour charger le certificat Azure Active Directory téléchargé, cliquez sur **Choose File** .</span><span class="sxs-lookup"><span data-stu-id="fd8ee-176">Click **Choose File** to upload your downloaded Azure Active Directory certificate.</span></span>

   <span data-ttu-id="fd8ee-177">b.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-177">b.</span></span> <span data-ttu-id="fd8ee-178">Dans la zone de texte **URL de connexion à distance**, collez la valeur de **URL du service d’authentification unique SAML** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-178">In the **Remote login URL** textbox,  paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="fd8ee-179">c.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-179">c.</span></span> <span data-ttu-id="fd8ee-180">Dans la zone de texte **URL de la page de déconnexion**, collez la valeur de **URL de déconnexion** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-180">In the **Logout landing URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

   <span data-ttu-id="fd8ee-181">d.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-181">d.</span></span> <span data-ttu-id="fd8ee-182">Cliquez sur **Save my changes**.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-182">Click **Save my changes**.</span></span>

> [!TIP]
> <span data-ttu-id="fd8ee-183">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="fd8ee-184">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="fd8ee-185">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fd8ee-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fd8ee-186">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd8ee-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="fd8ee-187">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="fd8ee-189">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="fd8ee-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="fd8ee-190">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-new-relic-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fd8ee-192">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-new-relic-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fd8ee-194">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-new-relic-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fd8ee-196">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="fd8ee-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-new-relic-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fd8ee-198">a.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-198">a.</span></span> <span data-ttu-id="fd8ee-199">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fd8ee-200">b.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-200">b.</span></span> <span data-ttu-id="fd8ee-201">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fd8ee-202">c.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-202">c.</span></span> <span data-ttu-id="fd8ee-203">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="fd8ee-204">d.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-204">d.</span></span> <span data-ttu-id="fd8ee-205">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-205">Click **Create**.</span></span>
 
### <a name="creating-a-new-relic-test-user"></a><span data-ttu-id="fd8ee-206">Création d’un utilisateur de test New Relic</span><span class="sxs-lookup"><span data-stu-id="fd8ee-206">Creating a New Relic test user</span></span>

<span data-ttu-id="fd8ee-207">Pour se connecter à New Relic, les utilisateurs d’Azure Active Directory doivent être configurés dans New Relic.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-207">In order to enable Azure Active Directory users to log in to New Relic, they must be provisioned into New Relic.</span></span> <span data-ttu-id="fd8ee-208">Dans le cas de New Relic, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-208">In the case of New Relic, provisioning is a manual task.</span></span>

<span data-ttu-id="fd8ee-209">**Pour approvisionner un compte d’utilisateur dans New Relic, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="fd8ee-209">**To provision a user account to New Relic, perform the following steps:**</span></span>

1. <span data-ttu-id="fd8ee-210">Connectez-vous à votre site d’entreprise **New Relic** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-210">Log in to your **New Relic** company site as administrator.</span></span>

2. <span data-ttu-id="fd8ee-211">Dans le menu situé en haut, cliquez sur **Account Settings**.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-211">In the menu on the top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="fd8ee-212">![Paramètres de compte](./media/active-directory-saas-new-relic-tutorial/ic797040.png "Paramètres de compte")</span><span class="sxs-lookup"><span data-stu-id="fd8ee-212">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797040.png "Account Settings")</span></span>

3. <span data-ttu-id="fd8ee-213">Dans le volet **Account** situé sur le côté gauche, cliquez sur **Summary**, puis sur **Add user**.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-213">In the **Account** pane on the left side, click **Summary**, and then click **Add user**.</span></span>
   
    <span data-ttu-id="fd8ee-214">![Paramètres de compte](./media/active-directory-saas-new-relic-tutorial/ic797041.png "Paramètres de compte")</span><span class="sxs-lookup"><span data-stu-id="fd8ee-214">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797041.png "Account Settings")</span></span>

4. <span data-ttu-id="fd8ee-215">Dans la boîte de dialogue **Active users** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="fd8ee-215">On the **Active users** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="fd8ee-216">![Utilisateurs actifs](./media/active-directory-saas-new-relic-tutorial/ic797042.png "Utilisateurs actifs")</span><span class="sxs-lookup"><span data-stu-id="fd8ee-216">![Active Users](./media/active-directory-saas-new-relic-tutorial/ic797042.png "Active Users")</span></span>
   
    <span data-ttu-id="fd8ee-217">a.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-217">a.</span></span> <span data-ttu-id="fd8ee-218">Dans la zone de texte **Email** , tapez l’adresse de messagerie d’un utilisateur Azure Active Directory valide à approvisionner.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-218">In the **Email** textbox, type the email address of a valid Azure Active Directory user you want to provision.</span></span>

    <span data-ttu-id="fd8ee-219">b.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-219">b.</span></span> <span data-ttu-id="fd8ee-220">Pour **Role**, sélectionnez **User**.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-220">As **Role** select **User**.</span></span>

    <span data-ttu-id="fd8ee-221">c.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-221">c.</span></span> <span data-ttu-id="fd8ee-222">Cliquez sur **Add this user**.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-222">Click **Add this user**.</span></span>

>[!NOTE]
><span data-ttu-id="fd8ee-223">Vous pouvez utiliser n’importe quel outil ou API de création de compte d’utilisateur, fourni par New Relic, pour approvisionner des comptes utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-223">You can use any other New Relic user account creation tools or APIs provided by New Relic to provision AAD user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="fd8ee-224">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd8ee-224">Assigning the Azure AD test user</span></span>

<span data-ttu-id="fd8ee-225">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à New Relic.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to New Relic.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="fd8ee-227">**Pour affecter Britta Simon à New Relic, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="fd8ee-227">**To assign Britta Simon to New Relic, perform the following steps:**</span></span>

1. <span data-ttu-id="fd8ee-228">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="fd8ee-230">Dans la liste des applications, sélectionnez **New Relic**.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-230">In the applications list, select **New Relic**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_app.png) 

3. <span data-ttu-id="fd8ee-232">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-232">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="fd8ee-234">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-234">Click **Add** button.</span></span> <span data-ttu-id="fd8ee-235">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="fd8ee-237">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="fd8ee-238">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fd8ee-239">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fd8ee-240">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="fd8ee-240">Testing single sign-on</span></span>

<span data-ttu-id="fd8ee-241">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-241">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="fd8ee-242">Lorsque vous cliquez sur la vignette New Relic dans le panneau d’accès, vous êtes automatiquement connecté à votre application New Relic.</span><span class="sxs-lookup"><span data-stu-id="fd8ee-242">When you click the New Relic tile in the Access Panel, you should get automatically signed-on to your New Relic application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fd8ee-243">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="fd8ee-243">Additional resources</span></span>

* [<span data-ttu-id="fd8ee-244">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fd8ee-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fd8ee-245">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="fd8ee-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_203.png

