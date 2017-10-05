---
title: "Didacticiel : Intégration d’Azure Active Directory à Origami | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Origami."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a28bb0ba-b564-46ba-accc-e587699295d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 3420409b72ff032e64ac59365083dd141dfc3c1b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-origami"></a><span data-ttu-id="c1284-103">Didacticiel : Intégration d’Azure Active Directory à Origami</span><span class="sxs-lookup"><span data-stu-id="c1284-103">Tutorial: Azure Active Directory integration with Origami</span></span>

<span data-ttu-id="c1284-104">Dans ce didacticiel, vous allez apprendre à intégrer Origami à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c1284-104">In this tutorial, you learn how to integrate Origami with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c1284-105">L’intégration d’Origami à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="c1284-105">Integrating Origami with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c1284-106">Dans Azure AD, vous pouvez contrôler qui a accès à Origami.</span><span class="sxs-lookup"><span data-stu-id="c1284-106">You can control in Azure AD who has access to Origami</span></span>
- <span data-ttu-id="c1284-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Origami (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c1284-107">You can enable your users to automatically get signed-on to Origami (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c1284-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="c1284-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c1284-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c1284-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c1284-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c1284-110">Prerequisites</span></span>

<span data-ttu-id="c1284-111">Pour configurer l’intégration d’Azure AD à Origami, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="c1284-111">To configure Azure AD integration with Origami, you need the following items:</span></span>

- <span data-ttu-id="c1284-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1284-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c1284-113">Un abonnement Origami pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="c1284-113">An Origami single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c1284-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="c1284-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c1284-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="c1284-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c1284-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="c1284-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c1284-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c1284-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c1284-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="c1284-118">Scenario description</span></span>
<span data-ttu-id="c1284-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="c1284-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c1284-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="c1284-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c1284-121">Ajout d’Origami à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="c1284-121">Adding Origami from the gallery</span></span>
2. <span data-ttu-id="c1284-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1284-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-origami-from-the-gallery"></a><span data-ttu-id="c1284-123">Ajout d’Origami à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="c1284-123">Adding Origami from the gallery</span></span>
<span data-ttu-id="c1284-124">Pour configurer l’intégration d’Origami à Azure AD, vous devez ajouter Origami à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="c1284-124">To configure the integration of Origami into Azure AD, you need to add Origami from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c1284-125">**Pour ajouter Origami à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c1284-125">**To add Origami from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c1284-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c1284-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c1284-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="c1284-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c1284-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="c1284-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="c1284-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="c1284-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="c1284-133">Dans la zone de recherche, entrez **Origami**.</span><span class="sxs-lookup"><span data-stu-id="c1284-133">In the search box, type **Origami**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-origami-tutorial/tutorial_origami_search.png)

5. <span data-ttu-id="c1284-135">Dans le panneau des résultats, sélectionnez **Origami**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="c1284-135">In the results panel, select **Origami**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-origami-tutorial/tutorial_origami_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c1284-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1284-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c1284-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Origami avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="c1284-138">In this section, you configure and test Azure AD single sign-on with Origami based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c1284-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Origami équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c1284-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Origami is to a user in Azure AD.</span></span> <span data-ttu-id="c1284-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Origami associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="c1284-140">In other words, a link relationship between an Azure AD user and the related user in Origami needs to be established.</span></span>

<span data-ttu-id="c1284-141">Dans Origami, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="c1284-141">In Origami, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c1284-142">Pour configurer et tester l’authentification unique Azure AD avec Origami, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="c1284-142">To configure and test Azure AD single sign-on with Origami, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c1284-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="c1284-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c1284-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c1284-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c1284-145">**[Création d’un utilisateur de test Origami](#creating-an-origami-test-user)** pour obtenir un équivalent de Britta Simon dans Origami lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="c1284-145">**[Creating an Origami test user](#creating-an-origami-test-user)** - to have a counterpart of Britta Simon in Origami that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c1284-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c1284-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c1284-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="c1284-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c1284-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1284-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c1284-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Origami.</span><span class="sxs-lookup"><span data-stu-id="c1284-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Origami application.</span></span>

<span data-ttu-id="c1284-150">**Pour configurer l’authentification unique Azure AD avec Origami, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c1284-150">**To configure Azure AD single sign-on with Origami, perform the following steps:**</span></span>

1. <span data-ttu-id="c1284-151">Dans le Portail Azure, sur la page d’intégration de l’application **Origami**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="c1284-151">In the Azure portal, on the **Origami** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="c1284-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c1284-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-origami-tutorial/tutorial_origami_samlbase.png)

3. <span data-ttu-id="c1284-155">Dans la section **Domaine et URL Origami**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c1284-155">On the **Origami Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-origami-tutorial/tutorial_origami_url.png)

    <span data-ttu-id="c1284-157">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://live.origamirisk.com/origami/account/login?account=<companyname>`</span><span class="sxs-lookup"><span data-stu-id="c1284-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://live.origamirisk.com/origami/account/login?account=<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c1284-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="c1284-158">The value is not real.</span></span> <span data-ttu-id="c1284-159">Mettez à jour la valeur avec l’URL de connexion réelle.</span><span class="sxs-lookup"><span data-stu-id="c1284-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="c1284-160">Pour obtenir cette valeur, contactez l’[équipe du support technique d’Origami](https://wordpress.org/support/theme/origami).</span><span class="sxs-lookup"><span data-stu-id="c1284-160">Contact [Origami Client support team](https://wordpress.org/support/theme/origami) to get the value.</span></span> 
 
4. <span data-ttu-id="c1284-161">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="c1284-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-origami-tutorial/tutorial_origami_certificate.png) 

5. <span data-ttu-id="c1284-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="c1284-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-origami-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c1284-165">Dans la section **Configuration d’Origami**, cliquez sur **Configurer Origami** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="c1284-165">On the **Origami Configuration** section, click **Configure Origami** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c1284-166">Copiez **l’URL de déconnexion et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="c1284-166">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-origami-tutorial/tutorial_origami_configure.png) 

7. <span data-ttu-id="c1284-168">Connectez-vous au compte Origami avec les droits d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="c1284-168">Log in to the Origami account with Admin rights.</span></span>

8. <span data-ttu-id="c1284-169">Dans le menu situé en haut, cliquez sur **Admin**.</span><span class="sxs-lookup"><span data-stu-id="c1284-169">In the menu on the top, click **Admin**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)

9. <span data-ttu-id="c1284-171">Dans la page de boîte de dialogue de configuration de l’authentification unique, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c1284-171">On the Single Sign On Setup dialog page, perform the following steps:</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-origami-tutorial/tutorial_origami_531.png)

    <span data-ttu-id="c1284-173">a.</span><span class="sxs-lookup"><span data-stu-id="c1284-173">a.</span></span> <span data-ttu-id="c1284-174">Sélectionnez **Activer l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="c1284-174">Select **Enable Single Sign On**.</span></span>

    <span data-ttu-id="c1284-175">b.</span><span class="sxs-lookup"><span data-stu-id="c1284-175">b.</span></span> <span data-ttu-id="c1284-176">Dans la zone de texte **URL de la page de connexion du fournisseur d’identité**, collez la valeur **URL du service d’authentification unique SAML** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c1284-176">In the **Identity Provider's Sign-in Page URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="c1284-177">c.</span><span class="sxs-lookup"><span data-stu-id="c1284-177">c.</span></span> <span data-ttu-id="c1284-178">Dans la zone de texte **URL de la page de déconnexion du fournisseur d’identité**, collez la valeur **URL de déconnexion** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c1284-178">In the **Identity Provider's Sign-out Page URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="c1284-179">d.</span><span class="sxs-lookup"><span data-stu-id="c1284-179">d.</span></span> <span data-ttu-id="c1284-180">Cliquez sur **Parcourir** pour importer le certificat que vous avez téléchargé à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c1284-180">Click **Browse** to upload the certificate you have downloaded from the Azure portal.</span></span>

    <span data-ttu-id="c1284-181">e.</span><span class="sxs-lookup"><span data-stu-id="c1284-181">e.</span></span> <span data-ttu-id="c1284-182">Cliquez sur **Enregistrer les modifications**.</span><span class="sxs-lookup"><span data-stu-id="c1284-182">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="c1284-183">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="c1284-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c1284-184">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="c1284-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c1284-185">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c1284-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c1284-186">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1284-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="c1284-187">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c1284-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="c1284-189">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c1284-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c1284-190">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c1284-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-origami-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c1284-192">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="c1284-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-origami-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c1284-194">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="c1284-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-origami-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c1284-196">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c1284-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-origami-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c1284-198">a.</span><span class="sxs-lookup"><span data-stu-id="c1284-198">a.</span></span> <span data-ttu-id="c1284-199">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c1284-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c1284-200">b.</span><span class="sxs-lookup"><span data-stu-id="c1284-200">b.</span></span> <span data-ttu-id="c1284-201">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c1284-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c1284-202">c.</span><span class="sxs-lookup"><span data-stu-id="c1284-202">c.</span></span> <span data-ttu-id="c1284-203">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="c1284-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c1284-204">d.</span><span class="sxs-lookup"><span data-stu-id="c1284-204">d.</span></span> <span data-ttu-id="c1284-205">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="c1284-205">Click **Create**.</span></span>
 
### <a name="creating-an-origami-test-user"></a><span data-ttu-id="c1284-206">Création d’un utilisateur de test Origami</span><span class="sxs-lookup"><span data-stu-id="c1284-206">Creating an Origami test user</span></span>

<span data-ttu-id="c1284-207">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Origami.</span><span class="sxs-lookup"><span data-stu-id="c1284-207">In this section, you create a user called Britta Simon in Origami.</span></span> 

1. <span data-ttu-id="c1284-208">Connectez-vous au compte Origami avec les droits d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="c1284-208">Log in to the Origami account with Admin rights.</span></span>

2. <span data-ttu-id="c1284-209">Dans le menu situé en haut, cliquez sur **Admin**.</span><span class="sxs-lookup"><span data-stu-id="c1284-209">In the menu on the top, click **Admin**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)

3. <span data-ttu-id="c1284-211">Dans la boîte de dialogue **Utilisateurs et sécurité**, cliquez sur **Utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="c1284-211">On the **Users and Security** dialog, click **Users**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-origami-tutorial/tutorial_origami_54.png)

4. <span data-ttu-id="c1284-213">Cliquez sur **Add New User**.</span><span class="sxs-lookup"><span data-stu-id="c1284-213">Click **Add New User**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-origami-tutorial/tutorial_origami_55.png)

5. <span data-ttu-id="c1284-215">Dans la boîte de dialogue Ajouter un nouvel utilisateur, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c1284-215">On the Add New User dialog, perform the following steps:</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-origami-tutorial/tutorial_origami_56.png)

    <span data-ttu-id="c1284-217">a.</span><span class="sxs-lookup"><span data-stu-id="c1284-217">a.</span></span> <span data-ttu-id="c1284-218">Dans la zone de texte **Nom d’utilisateur**, entrez l’adresse e-mail de l’utilisateur, par exemple **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="c1284-218">In the **User Name** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="c1284-219">b.</span><span class="sxs-lookup"><span data-stu-id="c1284-219">b.</span></span> <span data-ttu-id="c1284-220">Dans la zone de texte **Mot de passe** , entrez un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="c1284-220">In the **Password** textbox, type a password.</span></span>

    <span data-ttu-id="c1284-221">c.</span><span class="sxs-lookup"><span data-stu-id="c1284-221">c.</span></span> <span data-ttu-id="c1284-222">Dans la zone de texte **Confirmer le mot de passe** , entrez de nouveau le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="c1284-222">In the **Confirm Password** textbox, type the password again.</span></span>

    <span data-ttu-id="c1284-223">d.</span><span class="sxs-lookup"><span data-stu-id="c1284-223">d.</span></span> <span data-ttu-id="c1284-224">Dans la zone de texte **Prénom**, entrez le prénom de l’utilisateur, par exemple **Britta**.</span><span class="sxs-lookup"><span data-stu-id="c1284-224">In the **First Name** textbox, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="c1284-225">e.</span><span class="sxs-lookup"><span data-stu-id="c1284-225">e.</span></span> <span data-ttu-id="c1284-226">Dans la zone de texte **Nom**, tapez le nom de l’utilisateur, par exemple **Simon**.</span><span class="sxs-lookup"><span data-stu-id="c1284-226">In the **Last Name** textbox, enter the last name of user like **Simon**.</span></span>

    <span data-ttu-id="c1284-227">f.</span><span class="sxs-lookup"><span data-stu-id="c1284-227">f.</span></span> <span data-ttu-id="c1284-228">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="c1284-228">Click **Save**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-origami-tutorial/tutorial_origami_57.png)

6. <span data-ttu-id="c1284-230">Affectez des **Rôles d’utilisateur** et **l’Accès client** à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c1284-230">Assign **User Roles** and **Client Access** to the user.</span></span> 
   
    ![Configurer l’authentification unique](./media/active-directory-saas-origami-tutorial/tutorial_origami_58.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c1284-232">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1284-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c1284-233">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Origami.</span><span class="sxs-lookup"><span data-stu-id="c1284-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Origami.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="c1284-235">**Pour affecter Britta Simon à Origami, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c1284-235">**To assign Britta Simon to Origami, perform the following steps:**</span></span>

1. <span data-ttu-id="c1284-236">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="c1284-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="c1284-238">Dans la liste des applications, sélectionnez **Origami**.</span><span class="sxs-lookup"><span data-stu-id="c1284-238">In the applications list, select **Origami**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-origami-tutorial/tutorial_origami_app.png) 

3. <span data-ttu-id="c1284-240">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="c1284-240">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="c1284-242">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="c1284-242">Click **Add** button.</span></span> <span data-ttu-id="c1284-243">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="c1284-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="c1284-245">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="c1284-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c1284-246">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="c1284-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c1284-247">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="c1284-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c1284-248">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="c1284-248">Testing single sign-on</span></span>

<span data-ttu-id="c1284-249">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="c1284-249">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c1284-250">Quand vous cliquez sur la vignette Origami dans le volet d’accès, vous devez être connecté automatiquement à votre application Origami.</span><span class="sxs-lookup"><span data-stu-id="c1284-250">When you click the Origami tile in the Access Panel, you should get automatically signed-on to your Origami application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c1284-251">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="c1284-251">Additional resources</span></span>

* [<span data-ttu-id="c1284-252">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c1284-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c1284-253">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="c1284-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-origami-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-origami-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-origami-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-origami-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-origami-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-origami-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-origami-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-origami-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-origami-tutorial/tutorial_general_203.png

